## Hello world:
![[Pasted image 20240820105338.png]]

Para rodar o arquivo executável em go:
```
go run nomedoarquivo.go
```
## Pacotes em Go:

Vamos criar pacotes e ver como interagir entre eles:
 - Precisamos de um módulo que é um conjunto de pacotes que compõe o projeto.
 
 ```
 go mod init modulo
```

Este comando criará um go.mod dentro da estrutura de arquivos com o seguintes arquivos:
![[Pasted image 20240820110018.png]]
Nós podemos buildar o arquivo com o comando:
```
go build
```

Ao fim da execução deste código, nós podemos ver que é gerado um arquivo binário, cujo qual é um executável.

para rodar o executável basta executar no terminal:
```
 ./nomeDoArquivo
```

Ao executar o arquivo, você vera o resultado no terminal

Podemos também criar um arquivo auxiliar, para isso é necessário criar outro pacote em uma nova pasta:
![[Pasted image 20240820111000.png]]


Dentro da pasta auxiliar seguiremos o mesmo processo para criar o arquivo main.go, porém com o nome de auxiliar.go
![[Pasted image 20240820111106.png]]

Atente-se ao nome da função cujo qual deve ser nomeada com a primeira letra MAISCULA:

Para utilizarmos esta função no nosso arquivo main.go, nós devemos importá-la:
![[Pasted image 20240820111215.png]]
Pode rodar o comando:
```
	go run main.go
```

para ver o resultado no terminal:
![[Pasted image 20240820111303.png]]


Apesar de não podermos importar e utilizar uma função com letra minúscula no arquivo main.go, nós podemos instanciar outro arquivo por exemplo "auxiliar2" aonde dentro tem uma função com letra minúscula "auxiliar2" e importar dentro do mesmo pacote, a seguir:

![[Pasted image 20240820112200.png]]

![[Pasted image 20240820112145.png]]

> ⚠️ Temos também o comando `go install` aonde ao executá-lo ele builda o arquivo na raiz aonde você instalou o GO.



## Pacotes externos em Go:

Vamos aprender utilizar pacotes externos utilizando um pacote de validação de E-mail que se encontra no Git Hub `github.com/badoux/checkmail`.

Para isso nós vamos até raiz do projeto, na mesma pasta que esta o nosso modelo e executado o comando `go get LinkDoRepositório`
```
	go get github.com/badoux/checkmail
```


![[Pasted image 20240820113033.png]]

Repare que o pacote é adicionado na sua estrutura de arquivos junto com suas dependências:

![[Pasted image 20240820113102.png]]

Mudanças no arquivo go.mod

![[Pasted image 20240820113224.png]]
Agora nós podemos utilizar as funções dentro do nosso arquivo main.go

Primeiramente nós devemos fazer o import do pacote:
![[Pasted image 20240820113617.png]]

E para utilizar o as funções contidas no pacote importado na nossa função main, nós devemos nos referencia a ultima palavra no import que neste caso é o `checkmail`.

![[Pasted image 20240820113722.png]]

> ⚠️ Podemos utilizar o comando `go mod tidy` para remover todas as dependências que não estão sendo usadas


## Variáveis em Go:

Para declarar variáveis em Go nós podemos declarar seus tipos de forma explicita ou implícita, mas sempre devem ser declaradas já o que Go é fortemente tipado, exemplos: 

![[Pasted image 20240820120257.png]]

Também podes declarar mais de uma variável no mesmo escopo:
![[Pasted image 20240820120736.png]]

Podemos declarar constante e inverter valores das seguintes formas:
![[Pasted image 20240820121122.png]]

## Tipos de dados em Go
