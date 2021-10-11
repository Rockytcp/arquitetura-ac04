# arquitetura-ac04

Aluno: Gustavo Braganti Pessoa
RA: 1902194

Comandos para Execução:

- O Primeiro passo será inicializar uma imagem docker que contém o RabbitMQ:

  - docker-compose up

- O segundo passo será instalar a biblioteca pika que será responsável por fazer a conexão com o rabbitMQ que está funcionando dentro da nossa imagem Docker:

  - pip install pika

- O terceiro passo será inicilizar os programas escritos em python para poder enviar e receber mensagens, Primeiramente vamos inicializar o receive-log.py que será responsável por ficar "escutando" a exchange que, por ora, chamamos de "logs" do rabbitMQ em busca de novas mensagens:

  - python3 python3 receive-log.py
  - Importante lembrar que esse programa ficará rodando eternamente. Para encerrar seu funcionamento pressione CTRL+C.

- O quarto passo será inicializar o programa emit-log.py. Esse programa é responsável por enviar uma mensagem direcionada a exchange "logs" que foi criada dentro do RabbitMQ. Esse programa rodará apenas uma vez e se encerrará. Caso queira enviar mais mensagens, é só rodar o programa novamente:

  - python3 emit-log.py

Descrição:

O programa emit-log.py tem as seguintes funções:

    - A variável connection é responsável por guardar as informações de conexão com o RabbitMQ. Ela estabelece que a conexão está estabelecida no localhost, já que estamos rodando a aplicação localmente.

    - A linha 9 é responsável por declarar uma exchange chamada "logs" dentro do RabbitMQ, já que não conseguimos enviar uma mensagem ao RabbitMQ sem que seja criado uma exchange.

    - A linha 11 contém a variável message que contém a mensagem, de fato, que será enviada a exchange "logs". Caso o contéudo dessa varável seja aditado, o conteúdo da mensagem também sofrerá alteração

    - A linha 12 contém o comando basic_publish. Esse comando é reponsável por direcionar o contéudo da váriavel message (linha 11) para a exchange "logs".

    - A linha 14 encerra a conexão com o RabittMQ

O programa receive-log.py tem as seguintes funções:

    - Ele possui basicamente as mesmas funcionalidades do programa emit-log.
    A diferença primordial está na linha 17 em diante.

    - Na linha 17 delcaramos uma função chamada callback que será executada toda vez que uma mensagem for publicada na exchange "logs".

    - O comando da linha 20 define que o programa está consumindo uma determinada fila dentro do RabbitMQ e que, ao receber uma mensagem, será executada a função callback.
