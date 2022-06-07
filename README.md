## **Tutorial docker compose:**

**obs**.: não esqueça de verificar se tem o docker e o docker compose instalado

```shell
docker --version
```
```shell
docker-compose --version
```
**Baixando a aplicação:**
```shell
git clone https://github.com/lima-anderson/tutorial.git
```
**Entre na pasta tutorial**
```shell
cd tutorial/
```
**Criando a receita de bolo!**
Exemplo de arquivo docker-compose.yml:

```yaml
version: '3'
services:  # Declarando serviços
  db: # Serviço db declarado
    image: mongo:3.4 # Execute a imagem do mongo
  backend:
    image: node:8.1
    volumes:
      - ./backend:/backend
    ports: # Execute o container nas portas
      - 3000:3000 # 3000 do meu PC e a porta 3000 do container
    command: bash -c "cd /backend && npm i && node app"
  frontend:
    image: nginx:1.13
    volumes:
      - ./frontend:/usr/share/nginx/html/
    ports:
      - 80:80
```
- **version** serve para dizermos qual a versão do Docker Compose estamos utilizando.
- **services** são os nossos containers, 
	- **backend** é nossa api em NodeJS, 
	- **frontend** é  interface gráfica do usuário para nossa api, temos também mais um chamado
	- **db** que é o nosso banco de dados.
- **image** podemos definir qual imagem vamos utilizar no serviço, para o nosso serviço backend vamos utilizar a imagem com um **node** na versão 8.1; para o nosso serviço frontend  vamos utilizar a imagem com o **nginx** na versão 1.13 e no serviço db  vamos utilizar a imagem com o **mongo** na versão 3.4
- **command** dizemos qual comando vamos executar ao subir aquele serviço.
- usamos o campo **volumes** para dizer onde o nosso source se encontra no HOST, funciona assim primeiro o caminho do HOST, no caso *./backend* e *./frontend* e depois o caminho no contêiner que está depois dos “:” (dois pontos)
- **ports**: diz em qual porta o container vai executar. Antes dos “:” (dois pontos)
é a porta no meu PC, depois é a porta do container.

Na pasta onde o docker-compose.yml se encontra, execute o comando:

```shell
docker-compose up -d
```

Para verificar os containers que estão rodando

```shell
docker ps
```

Parando os containers com um único comando!

```shell
docker-compose down
```

Para ver todas as imagens

```shell
docker images
```

Para excluir todas as imagens docker no computador

```shell
docker image prune -a
```

[Link](https://docs.google.com/presentation/d/1liSzQPGCLVrNZM1rNN1rPtn_rXOhoahM3uaa6bxMgNA/edit?usp=sharing)
