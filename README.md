# Aceleração DIO Ruby

Evento realizado entre os dias 01/02/2021 e 05/02/2021

## Integração de Aplicação Ruby on Rails com RabbitMQ usando Bunny
### Visão Geral
Este projeto demonstra a integração de uma aplicação Ruby on Rails com o RabbitMQ, utilizando a gem bunny para gerenciamento e comunicação de mensagens. O objetivo é consumir mensagens de uma fila RabbitMQ e criar ou atualizar registros de clientes na base de dados Rails conforme as mensagens são processadas.

### Estrutura do Projeto
- Modelo Customer:

  - Representa um cliente na aplicação.
  - Valida a presença de name e email.
  - Garante a unicidade do email.
  - Método create_or_update_from_bunny para criar ou atualizar um cliente a partir de uma mensagem.
- Modelo ServiceOrder:

  - Representa uma ordem de serviço que pertence a um cliente.
  - Método generate para criar uma nova ordem de serviço associada a um cliente existente.
- Classe BunnyConsumer:

  - Processa mensagens recebidas do RabbitMQ.
  - Verifica se o tipo de mensagem é válido.
  - Cria ou atualiza registros de clientes conforme necessário.
- Inicializador do Bunny:

  - Configura a conexão Bunny com o RabbitMQ.
  - Garante que a conexão seja fechada graciosamente ao encerrar a aplicação.
- Script Bunny Consumer:

  - Executa a lógica de consumir mensagens da fila RabbitMQ.
  - Usa a classe BunnyConsumer para processar as mensagens.
- Docker Compose:

  - Configura um contêiner RabbitMQ com a interface de gerenciamento habilitada para facilitar a administração.
### Fluxo de Trabalho
- Inicialização do Ambiente:
  - O RabbitMQ é inicializado usando Docker Compose.
  - A aplicação Rails é configurada para se conectar ao RabbitMQ via Bunny.

- Publicação de Mensagens:
  - Mensagens são publicadas na fila RabbitMQ através de outras partes da aplicação ou sistemas externos.

- Consumo de Mensagens:
  - O script bunny_consumer.rb é executado para consumir mensagens da fila.
  - As mensagens são processadas pela classe BunnyConsumer.
  - Dependendo do tipo da mensagem, um cliente é criado ou atualizado no banco de dados Rails.

- Administração do RabbitMQ:
  - A interface de gerenciamento do RabbitMQ pode ser acessada para monitorar filas e mensagens.

 
[Slide](https://drive.google.com/file/d/1SqsToLomUNzotukQRO7SqiehbwgfFYq4/view?usp=sharing)

Implemente um microsserviço assíncrono trabalhando com rabbitMQ, um dos principais serviços de mensageria utilizado no mercado.

## Docker rabbitmq
```sh
docker-compose up
```
### Config .env
- update .env_sample to .env
- update add with amqp://guest:guest@localhost:5672

## Microsserviço Users

### Setup do projeto

```sh
bundle install
```

```sh
rails db:setup
```

### Executando o projeto

```sh
rails server -p 3001
```

### Criando um User

POST:
http://localhost:3001/users

## Microsserviço ServiceOrders

```sh
bundle install
```

```sh
rails db:setup
```

### Executando o projeto

```sh
rails server -p 3002
```

### Criando uma ServiceOrder

POST:
http://localhost:3002/service_orders

## Referências

- [Microsoft estilo de arquitetura de microsserviços](https://docs.microsoft.com/pt-br/azure/architecture/guide/architecture-styles/microservices)
- [RedHat - O que é arquitetura de microsserviços?](https://www.redhat.com/pt-br/topics/microservices)
- [Mastering Chaos - A Netflix Guide to Microservices](https://www.youtube.com/watch?v=CZ3wIuvmHeM&ab_channel=InfoQ)
- [Introdução teórica aos Microservices](https://www.anchietajunior.com/posts/microservices-introduction/)
- [RabbitMQ](https://www.rabbitmq.com/)
- [CloudAMQP](https://www.cloudamqp.com/)
- [RabbitMQ Hello World](https://www.rabbitmq.com/tutorials/tutorial-one-ruby.html)
