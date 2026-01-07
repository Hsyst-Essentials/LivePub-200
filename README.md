# Tutorial de Uso
Caso apenas queira realizar o download e execução do LivePub, [clique aqui!](https://github.com/Hsyst-Essentials/LivePub-200/blob/main/use-tutorial.md)
# LivePub - Documentação Técnica
## Índice:
- Sobre o LivePub
- Requisitos
- Funcionamento
  - Explicação do HLS (Nginx)
  - Explicação das APIs (NodeJS - Feito por nós)
- Configuração do Nginx
- Configuração do LivePub
  - Versão SSL
  - Versão Comum
- Endpoints
- Fluxos
- Créditos
- Finalização
- Licença

---
---

## Sobre o LivePub
O LivePub, é uma plataforma de Transmissão Ao-Vivo gratuita, utilizando as tecnologias RTMP e HLS para realizar a transmissão, NodeJS (JavaScript), JavaScript (puro), HTML, e Bootstrap para o site e API e dentre outras tecnologias. O objetivo e democratizar e facilitar a criação de um ambiente de streaming para sua empresa ou para uso pessoal!

---

O LivePub pode ser utilizado por exemplo, em sua empresa para transmitir eventos privados e restritos. E para uso pessoal, criar uma Twitch opensource, porquê não?


## Requisitos
O LivePub ele utiliza do NodeJS para sua API de funcionamento, portanto, é necessário que você tenha o NPM, NodeJS e as depedências do projeto (package.json) instalados em seu sistema. Além disso, usamos do Nginx e o Nginx rtmp-module para receber as transmissões RTMP e converte-las em HLS. Além disso, apenas garantimos o funcionamento pleno dele no Ubuntu 20.04 em diante.


# Funcionamento
Aqui, falaremos sobre como o LivePub funciona na prática.

## Explicação do HLS (Nginx)
O Nginx, ele deve estar configurado para receber as conexões RTMP, converter para o HLS e colocar em /var/www/html (pasta padrão do servidor web nginx). Com isso, ele ao receber a transmissão, ele automaticamente começa a sua conversão para o HLS (que é mais amigavel com navegadores). As configurações pré-definidas que funcionam com o LivePub estão disponíveis em: [clique aqui!](https://github.com/Hsyst-Essentials/LivePub-200/tree/main/nginx-config-files)

## Explicação das APIs (NodeJS - Feito por nós)
Esse script, é responsável por administrar as lives que entram para a plataforma (apenas que é dono do canal consegue liberar a transmisão), como todos podem transmitir com o nome do canal, a api ela libera para a homepage apenas caso o nome-do-canal.m3u8 esteja disponivel no Servidor HTTP (HLS), e caso a chave do canal esteja correto, e portanto, transmitir no nome do outro canal se torna algo inutil 👍. Além disso, ele administra a criação e a remoção de lives, e de canais!

# Configuração do Nginx
A configuração do Nginx está disponível em: [clique aqui!](https://github.com/Hsyst-Essentials/LivePub-200/tree/main/nginx-config-files). Mas atenção, você deve ter o Nginx e o **módulo RTMP** instalado.

# Configuração do LivePub
## Versão SSL e MAIN

### create-a-channel.html
```
deve ser alterado nas versões MAIN e SSL
```
Segundo, você deve alterar o [create-a-channel.html](https://github.com/Hsyst-Essentials/LivePub-200/blob/main/create-a-channel.html) a linha 647 pelo servidor RTMP (NGINX).

### index-ssl.js
```
deve ser alterado apenas na versão SSL
```
Altere o [index-ssl.js](https://github.com/Hsyst-Essentials/LivePub-200/blob/main/back/index-ssl.js) nas linhas 14 - Config de porta, 21/22 - Config de SSL, 143 (IP da `HLS (HTTP) Server`, aprenda a executar no *Tutorial de Uso*)

### index.js
```
deve ser alterado apenas na versão Comum (MAIN)
```
Altere o [index.js](https://github.com/Hsyst-Essentials/LivePub-200/blob/main/back/index.js) nas linhas 12 - Config de porta, 140 (IP da `HLS (HTTP) Server`, aprenda a executar no *Tutorial de Uso*)



# Endpoints

## /add-channel
O add-channel, é um endpoint GET, que cria um canal e adiciona ao banco de dados. Um exemplo de uso seria: `/add-channel?name=open&desc=Meu top channel!` e a resposta seria: `message: 'Canal criado com sucesso', key`

## /release-live
Ele serve para verificar se a live já está com o arquivo .m3u8 disponivel no `Servidor HLS (HTTP) do nginx`, e ao estar disponivel ele adiciona a live ao Banco de Dados, o que faz ser liberado na página principal. Um exemplo de uso seria: `/release-live?channel=open&key=chave-do-canal-aqui`

## /rem-live
Ele remove a transmissão ao vivo do banco de dados, o que faz com que ele saia da página principal. Um exemplo de uso seria: `/rem-live?channel=open&key=chave-do-canal-aqui` e a resposta: `message: Transmissão ao vivo do canal ${channel} foi encerrada com sucesso.`

## /get-live-streams
Ele mostra todas as transmissões ao vivo que estão disponiveis.

## /query-live-streams?query=pesquise-aqui
Ele mostra todas as transmissões que se conformam no parâmetro "query". Porém, ainda não foi implementado pois não temos tráfego o suficiente pra isso.

## /get-channels
Ele mostra todos os canais cadastrados.


# Fluxos
Esta aplicação não contém fluxos, pois cada endpoint é individual e não depende do outro diretamente.

# Créditos
Este projeto foi criado por op3n [(Discord Nick: op3n / Github: op3ny)](https://github.com/op3ny) e é um prazer ver você interessado nele!

# Finalização
Esta foi a documentação técnica do LivePub. Caso queira testar o projeto, acesse: [clique aqui!](https://hsyst.xyz/html/livepub)

# Licença
Este projeto está licenciado pela licença [MIT](https://github.com/Hsyst-Essentials/LivePub-200/blob/main/LICENSE), e portanto, o uso dela está condicionado a esta licença.
