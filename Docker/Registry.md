```
docker container run -d -p 5000:5000 --restart=always --name registry registry:2
```

O Docker Registry **é uma forma padrão de armazenar e distribuir imagens do Docker**. O Registry é um repositório baseado em código aberto sob a licença Apache permissiva.

```
docker image tag <id> localhost:5000/<name:version>
```