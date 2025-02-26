# Docker

- link: https://docs.docker.com/desktop/



### Informações iniciais:

### Comandos Principais

- Saber quantos e quais containers estão sendo executados em nossa máquina.

```shell
docker ps
```



- Usando uma imagem de teste do próprio docker
  
  Ele pega esta imagem e roda na nossa maquina a título de teste. Caso tenha sucesso ele mostra um "hello world".
  
  Caso esta imagem do docker não exista, ele vai lá e busca aimagem. Caso exista, ele só executa.
  
  ```docker
  docker run hello-world
  ```

Ao rodar este container ele mostra as informações e para porque não há processos rodando dentro deste container. Caso tenha, ele é mostrado no "docker ps".



- Para visualizar todod os conatiners mesmo os que já pararam de executar.
  
  ```docker
  docker ps -a
  ```

- Iniciando uma aplicação que aguarda informações. A titulo de exemplo, iniciando o Ubunto e executando __bash__ que fica rondado e processo fica aberto.
  
  o **-it** é de interagir, interação
  
  ```docker 
  docker run -it ubunto bash
  ```

- Parando um container e todos os processos:
  
  1. Precisa saber o **container id** do container que deseja parar.
     
     ```docker 
     docker stop <número container id>
     ```

- Iniciando um container 
  
  ```docker
  docker start <número container id> 
  ```

- Retornando ao uso de um container já executado

``` docker
docker exec -iti <número container id> bash
```

# Criando uma aplicação no docker

### Criando uma nova imagem para dentro do Docker:

1. Criando o ambiente para criação da imagem:
   
   1.1. Criar uma pasta para conter o script e todo processo de criação
   
   ```bash
   mkdir projetoImagemDocker
   ```
   
   1.2. Dentro da pasta criada, que esta vazia, vamos inciar criando o arquivo _dockerfile_
   
   ```bash
   nano Dockerfile
   ```

    1.3. Dentro do arquivo _Dockerfile_ vamos especifciar o que o container vai conter.

- _FROM_: Importa uma imagem já existe.

- _16.10_: versão do ubunto que queremos usar.

- __RUN_: Roda comandos pós baixar do _FROM_

exemplo:

```vim
FROM ubuntu:22.04
RUN apt -y update
```

2. Nomeando a **build**:
   
   - Não tenho certeza se o nome precisa da "/", mas acredito que seja para criar um caminho dentro do projeto.
   
   - O "." no final é para ele procurar o arquivo **Dockerfile** criado anteriormente.
   
   ```shell
   docker build -t <nomeando/novo_projeto> .
   ```

    2.1 Verificar se a imagem foi criada com sucesso

```shell
docker images
```

3. Criando o conteiner novo:
   
   - /bin/bash: Usado para já passar alguns comandos para o container
   
   ```bash
   docker run -it <nome da imagem> /bin/bash
   ```

 Com isso deve entrar na imagem ubuntu e poder manipular via bash.

**OBS**: Como a imagem do ubunto é bem básica, algumas funções e recursos podem  não vir por padrão com ping, ipconfig, por exemplo. Mas nada impede de instalar através do 'RUN apt  -y install  net-tools' (por exemplo).

```vim
RUN apt -y install net-tools
RUN apt -y install iputils-ping
```





### Criando aplicação usando uma imagem (layers) existente:

1. Importar o Maven:
   
   Para poder fazer o build da nossa aplicação.
   
   - __From_: Importa uma imagem já existe.
   
   - __3.8.4_: versão da imagem do maven, e não a versão maven em si.
   
   - _8_: Esta sim é a versão do maven.
   
   - as build: Como apelidamos
   
   ```docker
   from maven:3.8.4-jdk-8 as build
   ```

2. Trazer todos os arquivo da imagem para dentro da aplicação:
   
   Passar o comando _copy_ e o local onde ficará a cópia, que no caso é o path; /app/src

        

```Docker
COPY src /app/src
```


