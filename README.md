# Utilizando Docker

![GitHub repo size](https://img.shields.io/github/repo-size/dauid64/utilizando_docker?style=for-the-badge)
![GitHub language count](https://img.shields.io/github/languages/count/dauid64/utilizando_docker?style=for-the-badge)
![GitHub forks](https://img.shields.io/github/forks/dauid64/utilizando_docker?style=for-the-badge)
![Bitbucket open issues](https://img.shields.io/bitbucket/issues/dauid64/utilizando_docker?style=for-the-badge)
![Bitbucket open pull requests](https://img.shields.io/bitbucket/pr-raw/dauid64/utilizando_docker?style=for-the-badge)

<p align="center">
    <img src="https://github.com/dauid64/utilizando_docker/assets/94979678/48993813-33a6-4e06-bdde-1906db49930e" alt="Logo do Docker">
</p>

> Segundo projeto da matéria de Rede de Computadores na UnB. Objetivo desse projeto é desenvolver um docker compose que define múltiplos serviços complementares ou interdependentes entre si, como fariamos em uma aplicação comercial.

### Serviços utilizados

- Banco de dados (PostgreSQL, Redis)
- Hospedagem de site (NGINX)
- Fila de tarefas (CELERY)
- Aplicação web (Django)

## 💻 Pré-requisitos

Antes de começar, verifique se você atendeu aos seguintes requisitos:

- Você instalou a versão mais recente do `< Docker >`
- Você tem uma máquina `< Windows / Linux / Mac >`

## 📍 Motivações


O objetivo deste projeto foi realizar uma simulação de uma aplicação web utilizando o framework Django, executando-a por meio do Docker. Nesse contexto, configurei os bancos de dados utilizados e implementei o Celery para possibilitar a programação de tarefas assíncronas no projeto, o que é frequentemente utilizado no cotidiano de um grande sistema.

Na raiz do projeto, encontra-se o arquivo `Dockerfile`, no qual configuro minha própria imagem para o projeto. Essa imagem será utilizada para criar o contêiner do Django. Utilizo a imagem do Python como base, configurando diversas variáveis de ambiente para escrever arquivos de bytecode (.pyc) e otimizar a execução do código. Além disso, desabilito o buffer da saída padrão para tornar a saída mais imediata. Também copiamos a pasta do projeto e instalamos as bibliotecas necessárias para a execução do projeto.

No arquivo docker-compose.yml, localizado no mesmo ramo do projeto, configurei os contêineres da seguinte maneira: estabeleci a configuração do Redis, que será utilizado para executar as tarefas assíncronas por meio do Celery; configurei o PostgreSQL, onde os dados da aplicação web serão armazenados; configurei o Django, que funcionará como a aplicação principal gerenciadora dos dados; configurei o Celery, que será inicializado e estará pronto para possibilitar a criação da fila de tarefas em conjunto com o Redis; e, por fim, configurei o Nginx para atuar como nosso servidor web.

Em relação aos volumes, realizei a configuração para que eles espelhem entre si. Isso permite que qualquer modificação ocorrida em ambos os lados seja atualizada tanto no contêiner quanto na minha máquina. Esses volumes estão centralizados na pasta `data` localizada na raiz do projeto.

Na pasta `nginx`, estou apenas configurando uma imagem para excluir o arquivo de configuração padrão do Nginx e substituí-lo por um criado por mim.

## ☕ Usando o Docker

Para usar o Docker, siga estas etapas:

* Primeiro você terá que entrar na pastar "dotenv_files" copiar o arquvio ".env-examples" para a mesma pasta com o nome ".env" e configurar como o exemplo suas variáveis de ambiente.

* depois basta ir até a raiz do projeto com o Docker rodando em sua máquina e executar o comando `docker-compose up --build` para iniciar a criação dos contêineres.

* Depois que todos os contêineres estiverem instanciados. Basta entrar no link http://localhost/ e verá uma mensagem na tela dizendo "Olá Mundo"