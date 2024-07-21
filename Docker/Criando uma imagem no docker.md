 criaremos nossa imagem
### [[Resumo Criando Imagem no Docker]]

## Definindo arquivo Dockerfile

Para esse projeto, vamos usar uma [aplicação Node](https://github.com/danielartine/alura-docker/blob/aula-3/app-exemplo.zip?raw=true). Ressaltamos que não vamos entrar em nenhum detalhe específico de Node ou qualquer linguagem de programação, apenas usamos como exemplo para ter uma aplicação efetiva para empacotar, transformar em uma imagem e depois em um container.

O que queremos é que, ao executar nosso container e acessá-lo via nosso host, por exemplo, mapeando as portas, tenhamos a visualização, da aplicação em execução. Nesse caso, será uma tela azul com a frase "Eu amo Docker!".

Mas não queremos simplesmente clicar duas vezes no arquivo `index.html` para abri-lo, queremos um servidor que nos disponibilize essa aplicação.

Portanto, de alguma maneira, precisamos colocar todo o conteúdo da aplicação dentro de uma imagem, instalar o Node, que será responsável por executar o servidor e, finalmente, quando nosso container executar, queremos que ele execute algum comando que mantenha esse servidor em execução.

Neste caso, vamos utilizar o Visual Studio Code para fazer a edição de texto, mas você pode usar o IDE de sua preferência.

De ínicio, vamos criar um novo arquivo clicando em "File > New File" (ou "Ctrl + N") e apertar "Ctrl+S" para salvá-lo dentro da nossa pasta de "exemplo-node", que também estará disponível para download.

Dentro desta pasta, vamos criar um **arquivo chamado `Dockerfile`**, que é basicamente o arquivo que vamos criar. Repare que o VS Code consegue reconhecer que é um arquivo Dockerfile.

Dentro deste arquivo, vamos definir como será a criação da nossa imagem. O que queremos fazer? Nós queremos que dentro do nosso projeto como um todo nós tenhamos o Node para que consigamos rodar um servidor.

Então, se queremos usar o Node como base para nossa aplicação, podemos pegar emprestado o que já desenvolveram. Assim, poderíamos fazer o `pull` dessa imagem já existente para poder usar em nosso projeto, e a partir daí, fazer modificações para customizar o projeto da nossa maneira.

Podemos simplesmente usar uma imagem que já disponibilize o Node para nós, como a própria [imagem do Node no Docker Hub](https://hub.docker.com/_/node), que é uma imagem oficial.

A descrição contém todas as versões que podemos definir. Então, o que podemos fazer neste cenário? Podemos simplesmente dizer que queremos pegar uma dessas versões do Node para executar nosso projeto e usar essa imagem como base para a nossa. A partir da imagem que vamos definir, começamos a usar a nossa.

Como pegamos uma imagem emprestada? Por exemplo, se queremos usar o Node na versão 20, devemos definir isso dentro do arquivo `Dockerfile`.

Para definir que queremos pegar a partir do Node, digitamos `FROM node`. Mas como **explicitar a versão**? Utilizando dois pontos e a versão que queremos:

```dockerfile
FROM node:20
```

Como sabemos que é preciso escrever `20`? Porque na documentação da imagem do Node, ele mostra quais são as tags suportadas, inclusive a 20.

A partir do Node na versão 20, o que queremos fazer? 

Queremos colocar todo o nosso projeto, que são esses arquivos do diretório `exemplo-node`, exceto o próprio Dockerfile, dentro dessa imagem.

Portanto, queremos **copiar o conteúdo do nosso host para nossa imagem**. Mas como fazemos isso? 

Podemos simplesmente digitar `COPY` e copiar todo o conteúdo do nosso diretório atual. Em que diretório está o nosso Dockerfile.

Então, todo o conteúdo do nosso diretório atual será copiado para algum diretório dentro do nosso container, por exemplo, para uma pasta chamada `/app-node`.

```dockerfile
COPY . /app-node
```

A partir deste momento, estamos copiando esse conteúdo do diretório do nosso host para o diretório dentro da nossa imagem chamado `/app-node`.

E o que precisamos fazer? Queremos executar o comando `npm install`, mas esse comando deve ser executado dentro do nosso diretório `/app-node`, para que possamos **instalar as dependências** da nossa aplicação.

```dockerfile
RUN npm install
```

Caso você não conheça Node, esse comando basicamente é responsável apenas por instalar as dependências que nosso projeto precisa em um projeto Node. Basicamente, estamos instalando as dependências e o Node está resolvendo isso automaticamente.

Por fim, queremos que o **ponto de entrada** (`ENTRYPOINT`) do nosso container ao executar essa imagem e começar a ter seu container devidamente em execução, seja iniciar a aplicação. Para isso, usamos `npm start`.

```dockerfile
ENTRYPOINT npm start
```

Esse comando também tem que ser executado dentro desse diretório `/app-node`. Mas teríamos que colocar `/app-node` em todos os lugares. 

Nós podemos resolver isso de uma maneira mais simples, podemos decidir um diretório como padrão de trabalho.

Para isso, existe a instrução `WORKDIR`, e com ela podemos definir o nosso diretório padrão `/app-node`.

Com isso, podemos modificar o `COPY` inclusive. Podemos fazer um `COPY` de ponto, ou seja, esse ponto é o diretório atual dentro do nosso host, para ponto também, que será o nosso diretório atual dentro da nossa imagem.

Qual será o nosso diretório atual? Nosso `/app-node`, que foi definido através do nosso `WORKDIR`.

```dockerfile
FROM node:20
WORKDIR /app-node
COPY . .
RUN npm install
ENTRYPOINT npm start
```

 Estamos definindo que vamos utilizar a imagem do `node` na versão 14 como base para a nossa imagem. Também vamos definir o nosso diretório de trabalho padrão como o `/app-node`.

Depois, vamos copiar do diretório atual, onde está o Dockerfile do nosso host, que é esta pasta "exemplo-node", para a pasta atual dentro da nossa imagem, que é o `/app-node`, que foi definida dentro do nosso `WORKDIR`.

Finalmente, vamos executar esse comando `npm install`, enquanto a imagem estiver sendo criada. Este comando `npm install` será executado na etapa de criação da imagem. E quando o container for executado a partir dessa imagem, o comando executado será o `npm start`.

## Criando a imagem

Após salvar o arquivo, vamos ao terminal e acessar o diretório `exemplo-node` que está na área de trabalho.

```console
cd Desktop/exemplo-node/
```

Como podemos gerar uma imagem a partir do arquivo `Dockerfile`? Através do comando `docker build`, passamos o `-t`, para criar um nome, ou seja, etiquetar a nossa imagem. Nesse caso, vamos colocar `euamodocker/app-node`, por exemplo, na versão `1`. Com os dois pontos (`:`), podemos explicitar qual é a versão que estamos criando.

Devemos também adicionar em qual contexto tudo isso será executado. No contexto do diretório atual, ou seja, ponto (`.`) que é a referência ao diretório atual.

```console
docker build -t danielartine/app-node:1 .
```

Ao executar esse comando, o Docker vai ao Docker Hub buscar a imagem do node, na versão 14, para baixá-la. Em outras palavras, ele pega todo esse conteúdo para a nossa máquina e vai construir uma nova imagem, utilizando essa como base.

No momento em que todos os 5 passos terminarem, vamos executar o comando `docker history` para verificar o que ele vai fazer e entender como essa imagem vai se comportar dentro do nosso sistema.

`É importante mencionar que todas as instruções podem ser deduzidas a partir da própria [documentação do Docker](https://docs.docker.com/engine/reference/builder/). É uma documentação muito completa, na qual podemos e devemos nos basear para seguir nossos projetos de criação de imagens.

Voltando para o terminal, ele estará terminando de extrair nesse momento as últimas camadas dos downloads que ele fez da imagem do Node.

`Status: Downloaded newer image for node:20

Feito isso, passamos para a etapa de `WORKDIR`, depois de cópia de arquivos e execução do `npm install`. E por fim, ele definiu o `npm start` no `ENTRYPOINT`.

## Iniciando um container

Agora, vamos limpar o terminal e dar um `docker images` na máquina para analisar o que temos.

```console
docker images
```


![[Pasted image 20240424132748.png]]


Temos o `euamodocker/app-node` na versão 1.0 com o ID `4cb1da959a47`.

E se agora fizemos um `docker run` nessa imagem `euamodocker/app-node` para fazer um mapeamento? Lembra que definimos a nossa aplicação dentro do container, mas ela é isolada? Como podemos saber em qual porta essa aplicação está rodando dentro do container?

Vamos usar a criatividade, conferindo o arquivo `index.js` e descobrindo que ela está sendo executada a princípio na porta `3000`.

index.js
```javascript
app.listen("3000", ()=>{
    console.log("Server is listening on port 3000")
})
```


Há um pequeno problema que precisaremos resolver, mas primeiro vamos colocar isso no terminal.

Após `docker run`, vamos acrescentar `-p`. Com a porta `8080`.(não esqueça de verificar se a porta já esta em uso) Além disso, queremos que a porta `8080` reflita na porta `3000`, que é onde a nossa aplicação vai ficar em execução dentro do nosso container.

Também vamos acrescentar um `-d` para ficar em modo _detached_. Também faltou especificar a versão da imagem, nesse caso, será `1.0`.

```console
docker run -d –p 8080:3000 danielartine/app-node:1.0
```

Após executar, vamos ao navegador para tentar acessar o localhost na porta 8080.

```plaintext
localhost:8080
```

Conseguimos acessar a nossa aplicação agora de maneira containerizada! Então, criamos a nossa própria imagem e executamos um container a partir dela

