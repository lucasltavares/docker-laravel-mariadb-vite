# Laravel + MariaDB Docker Setup

Este repositório contém um setup para rodar uma aplicação Laravel utilizando o MariaDB, tudo gerenciado pelo Docker. Seguindo as instruções abaixo, você conseguirá configurar e iniciar rapidamente o ambiente de desenvolvimento.

## Pré-requisitos

- [Docker](https://docs.docker.com/get-docker/) instalado.
- [Docker Compose](https://docs.docker.com/compose/install/) instalado.

## Passo a Passo de Execução

### 1. Criar a Rede Docker

Antes de iniciar os containers, precisamos garantir que eles estarão na mesma rede Docker para que possam se comunicar entre si.

Execute o comando abaixo para criar a rede chamada `laravel-network`:

```bash
sudo docker network create laravel-network
```

### 2. Criar o Volume Docker para o MariaDB
Crie um volume Docker chamado mariadb_data para garantir que os dados do banco de dados sejam persistidos:

```bash
sudo docker volume create --name mariadb_data
```

### 3. Configurar e Iniciar o Docker ComposeAgora que a rede e o volume foram criados, vamos utilizar o arquivo docker-compose.yml para subir os containers do MariaDB e Laravel.

Com o arquivo docker-compose.yml disponível no seu diretório de trabalho, execute o seguinte comando para iniciar os serviços:

```bash
sudo docker-compose up -d
```
Isso irá:

- Criar e iniciar o container MariaDB.
- Criar e iniciar o container Laravel.
- Expor a aplicação Laravel nas portas 8000 e 5173.

### 4. Configuração do Laravel
Após os containers estarem em execução, precisamos gerar a chave de criptografia da aplicação Laravel e rodar alguns comandos essenciais.

#### 4.1 Gerar a app key laravel
```bash
sudo docker exec laravel php artisan key:generate
```
#### 4.2 Instalar dependencias
```bash
sudo docker exec laravel composer install
```

#### 4.3 Buildar dependências do front-end com VITE
```bash
sudo docker exec laravel npm install
sudo docker exec laravel npm run build
sudo docker exec laravel npm run dev
```