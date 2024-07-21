Resumo de como criar uma imagem no docker

```
"Uma imagem é como se fosse um container parado" 

"As imagens no docker hub são feitas como base para sua própria imagem em um projeto pessoal ou da sua empresa" 

~Jefferon LinuxTips
```


Inicialmente, crie um diretório com um nome à escolha. Dentro dele, crie um arquivo chamado `Dockerfile` e extraia o conteúdo da pasta do [zip](https://github.com/danielartine/alura-docker/blob/aula-3/app-exemplo.zip?raw=true) neste mesmo diretório. Este será o arquivo usado para o Docker interpretar as instruções e construir a imagem final.

Com seu editor de texto favorito, edite o arquivo e adicione o seguinte conteúdo:

```sql
FROM node:14
WORKDIR /app-node
COPY . .
RUN npm install
ENTRYPOINT npm start
```

Com estas instruções acima, estamos informando ao Docker que queremos usar a imagem do `node` na versão 14 como base para nossa imagem. Definimos que nosso diretório padrão para executar os comandos dentro do container será o `/app-node` e em seguida copiamos todo o conteúdo do diretório atual Dockerfile para o diretório `/app-node` dentro do container.

Por fim, em tempo de construção da imagem, executamos o comando `npm install` e definimos que, ao executar o container gerado por esta imagem, o comando executado será o `npm start`.

Ainda dentro do diretório do Dockerfile, através do terminal, execute o comando `docker build -t <seu-nome-de-usuario-do-docker-hub>/app-node:1.0 .`. Dessa forma, sua primeira imagem será criada. Confira através do comando `docker images` se sua imagem está sendo listada.

Saber como criar e definir imagens é de suma importância, pois elas são a base para o funcionamento de um futuro container.

Para isso, precisamos seguir um fluxo. Primeiro, definimos um arquivo Dockerfile e a partir dele criamos nossa imagem. Uma vez em posse da imagem, basta executar o comando `run` para gerar um container a partir da imagem.