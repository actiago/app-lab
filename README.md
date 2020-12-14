# App stack

Stack para estudos - Aplicação com docker-compose, MongoDB, Flask e Nginx

Baseado no tutorial [**How To Set Up Flask with MongoDB and Docker**](https://www.digitalocean.com/community/tutorials/how-to-set-up-flask-with-mongodb-and-docker) da Digital Ocean.

Recomendo que leia todo o tutorial para compreensão de todo o ambiente.

## Execução

```bash
docker-compose up -d
```

## Ajustes

Antes de validar a aplicação, será necessário criar o usuário do banco, vá até o item 6 do tutorial e siga as instruções.

1. Login no container mongodb

```bash
$ docker exec -it mongodb bash
```

2. Login no mongo, use a senha criada para o ```MONGO_INITDB_ROOT_PASSWORD```

```bash
# mongo -u mongodbuser -p
```

3. Crie o banco flaskdb

```bash
mongodb > use flaskdb
```

4. Crie o usuário do flask com permissões de leitura e escrita no banco _flaskdb_

```
mongodb > db.createUser({user: 'flaskuser', pwd: 'your password', roles: [{role: 'readWrite', db: 'flaskdb'}]})
exit
```

## Testes

```
curl -i http://localhost
```

Criando uma entrada

```bash
curl -i -H "Content-Type: application/json" -X POST -d '{"todo": "Dockerize Flask application with MongoDB backend"}' http://localhost/todo
```

Validando a entrada

```bash
curl -i http://your_server_ip/todo
```
