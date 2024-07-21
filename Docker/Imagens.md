imagens
## O que são imagens?

Até agora, temos aceitado que as imagens são uma receita para criar um container, mas efetivamente como elas funcionam?

Uma imagem nada mais é que um conjunto de camadas, que ao serem unidas formam imagens. E essas camadas são independentes, cada uma tem o seu respectivo ID (identificador).

Após executar um `docker pull` de uma `imagem no docker hub` e um `docker run` na nossa imagem, podemos visualizar as imagens que temos baixadas no nosso sistema, através do comando `docker images` ou `docker image ls`

```console
docker images
```

Exemplo do `dockersamples`
![[Pasted image 20240423212103.png]]

Temos baixada a nossa imagem, que é o `dockersamples/static-site`, com essa tag `latest`, com seu respectivo ID. E ela foi criada há cinco anos pelo grupo do `dockersamples` e o tamanho dela é 191 megabytes.

Podemos ir um pouco mais além, podemos dar o comando `docker inspect` em uma imagem passando o identificador do que queremos inspecionar.

```console
docker inspect f589ccde7957
```

Dessa maneira, teremos diversas informações.

Temos um conjunto muito grande de informação que podemos ter detalhadamente sobre determinado recurso dentro do nosso Docker.

Por exemplo, o ID, a tag do repositório, o _digest_ que foi utilizado para validação da imagem, se tem alguma imagem que é um _parent_, uma imagem pai ou mãe, a data de criação, o container e sua configuração. Inclusive, no final, temos mais informações sobre a parte de _layers_, ou seja, das camadas.

Existe um comando específico para verificar quais são as camadas de uma imagem. Basta usar o comando `docker history`, passando o ID da imagem.

```console
docker history f589ccde7957
```

![[Pasted image 20240423212310.png]]

Repare que temos a nossa imagem `f589ccde7957` na primeira linha. Ela tem 13 camadas, as quais quando são aglutinadas, ou seja, quando são empilhadas umas nas outras formam essa imagem final do `dockersamples/static-site`. E caso alguma outra imagem venha a depender dessas camadas, conseguimos reutilizá-las.

Ele mostra detalhadamente qual é o tamanho de cada uma dessas camadas, a data de criação e a ordem de cada uma delas, como CMD, WORKDIR, COPY. Assim, conseguimos verificar todas essas informações e entender o que está acontecendo.

`Em resumo, uma imagem é um conjunto de camadas empilhadas para formar determinada regra de execução de um container.

## Como imagens viram containers?

Quando fizemos o comando `docker run` pela primeira vez, ou simplesmente um `docker pull`, não para executar o container, mas só baixar a imagem, o que pode acontecer? Vamos fazer o download das nossas imagens, das nossas camadas.

Mas é possível que, por exemplo, já tenhamos algumas das camadas que queremos no nosso host. Por isso, no momento em que fazemos um `pull` ou um `run`, que vai fazer um `pull` consequentemente, faremos os downloads simplesmente das camadas que necessitamos.

O Docker é inteligente o suficiente para **reutilizar** essas camadas para compor novas imagens, conseguindo assim uma performance muito boa, já que não precisaremos ter informação duplicada ou triplicada, porque conseguimos reutilizar as camadas em outras imagens.

O que mais podemos explorar na parte de criação de imagens? No fim das contas, quando temos a nossa imagem, ela é _**read-only**_ (somente leitura), isso significa que não conseguimos modificar as camadas dessa imagem, depois que ela foi criada.

Voltando ao exemplo no terminal, no momento em que temos a imagem do `dockersamples/static-site`, ela é imutável - assim como a imagem que temos do Ubuntu.

Mais uma vez, se fazemos `docker run -it ubuntu bash` para executar o _bash_ em modo iterativo, vamos baixar a camada necessária para ter a nossa imagem de execução para que consigamos executar nosso container do Ubuntu.

```console
docker run -it ubuntu bash
```

Como o instrutor já apagado a imagem, ela será baixada, extraída e o terminal será aberto.

Contudo, havíamos criado na _home_ um arquivo qualquer de exemplo com o comando `touch um-arquivo-qualquer.txt`. Isso significa que estaríamos escrevendo dentro do container. Mas como estamos conseguindo fazer isso se a imagem que gera o nosso container é apenas para leitura (_read only_)?

Se ela é bloqueada para escrita, como é que o container consegue escrever informação dentro dela? Porque um container nada mais é do que uma imagem com uma camada adicional de _**read-write**_ (leitura e escrita).

`Quando criamos um container, criamos uma camada temporária em cima da imagem, onde conseguimos escrever informações. E, no momento em que esse container é deletado, essa camada extra também é deletada.

Por isso que quando fizemos aquele experimento anteriormente, a nossa informação dentro do container era perdida quando nosso container era apagado. Porque essa camada é temporária, bem fina e leve para que o container tenha um ambiente de execução muito leve e fácil de ser executado.

## Por que os containers são tão leves?

Agora voltamos àquela primeira pergunta, onde questionávamos por que os containers são tão leves.

Além de serem simplesmente processos dentro do nosso sistema, podemos dizer que, quando um container entra em execução, estamos sempre reaproveitando a mesma imagem.

Como a imagem é apenas de leitura, podemos ter vários containers baseados na mesma imagem. A diferença é que cada um desses containers terá apenas uma camada diferente de _read-write_, e como essa camada é extremamente leve, a fim de manter essa performance, temos uma **reutilização da imagem para múltiplos containers**.

No fim das contas, o que acontece é que quando definimos um container ou outro container baseado na mesma imagem, o tamanho desse container será apenas o tamanho da camada de escrita que estamos gerando para ele, porque a imagem será reutilizada para cada um deles.

Em breve, faremos um experimento prático, conforme formos avançando na criação e no fluxo das nossas imagens.

`O container é leve e otimizado, porque consegue reaproveitar as camadas das imagens prévias que já temos. E, quando criamos novos containers, ele simplesmente reutiliza as mesmas imagens e, consequentemente, as camadas.

Além disso, utiliza a camada de _read-write_ para utilizar de maneira mais performática o que ele já tem no ecossistema do Docker.

Agora, precisamos entender como[[Criando uma imagem no docker]] efetivamente para não depender totalmente de imagens de outras pessoas.

