# Introdução ao Docker em 22 minutos

Projeto gerado na videoaula do canal no YouTube Programador a Bordo.

Link da aula:
https://www.youtube.com/watch?v=Kzcz-EVKBEQ

## Como rodar

### Construindo as imagens

Acesse a pasta raíz do projeto e construa cada imagem (MySQL, Node API e PHP):

```
docker build -t mysql-image -f api/db/Dockerfile .

docker build -t node-image -f api/Dockerfile .

docker build -t php-image -f website/Dockerfile .
```

### Rodando os containers

```
docker run -d -v $(pwd)/api/db/data:/var/lib/mysql --rm --name mysql-container mysql-image

docker run -d -v $(pwd)/api:/home/node/app -p 9001:9001 --link mysql-container --rm --name node-container node-image

docker run -d -v "$(pwd)/website":/var/www/html -p 8888:80 --link node-container --rm --name php-container php-image
```

### Agora faça o restore do banco:
```
docker exec mysql-container -uroot -pprogramadorabordo < api/db/script.sql
```


Para entender melhor sobre cada comando utilizado, assita a videoaula ;)