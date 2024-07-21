
Executaremos um exemplo prático de uma aplicação _web_ que permitirá visualizar sua saída através do navegador.

Neste caso específico, optamos por utilizar essa imagem para ilustrar e visualizar o Docker em funcionamento com um _container_.

Como funcionará? Iremos copiar mais uma vez o nome da imagem (`dockersamples/static-site`) e realizar um `docker run`, passando o dockersamples/static-site.

```bash
docker run dockersamples/static-site
```

Este processo envolverá o _download_ de todas as camadas necessárias para a execução do _container_, o qual é baseado na imagem `dockersamples/static-site`.

Porém se utilizarmos o -d:

```bash
docker run -d dockersamples/static-site 
```

Isso fará com que o _container_ baseado nesta imagem seja executado sem impactar nosso terminal. Observemos o que ocorrerá. O processo envolverá o _download_ de todas as camadas necessárias para a execução do _container_, o qual é baseado na imagem `dockersamples/static-site`.

Esse fluxo que já observamos está validando todas as camadas necessárias no docker hub para a execução do _container_. O _container_ é o que encontramos, e a verificação ocorre após o _download_ e extração das camadas em nossa máquina. Concluída a extração e o _download_, o terminal não trava devido à flag `-d`. No entanto, ao executar um `docker ps`, podemos verificar o estado atual.

```undefined
docker ps
```

Como retorno, temos:

![[Pasted image 20240423151026.png]]

O comando revela que o _container_ está em execução, foi baseado na imagem, foi criado há poucos segundos e permanece em execução.

Este comando, `/bin.sh -c`, não exibe o comando completo, mas mantém um processo ativo dentro do terminal do nosso _container_. Como resultado, o próprio _container_ continua em execução. O `docker ps` é utilizado várias vezes, indicando que a aplicação está em execução graças ao comando padrão executado durante a inicialização do _container_.

A coluna de portas mostra que a aplicação está operando nas portas `80` e `443`, e o nome registrado é "_frangley lamar_". Se a aplicação está na porta `80`, vamos abrir o **navegador** e acessar _localhost_ nessa porta.

```makefile
localhost:80
```

O comando a seguir esta redirecionando qual a porta deve ser referenciada na porta 8080 que no caso essa é a 80.
```bash
docker run -d -p 8080:80 dockersamples/static-site 
```
Executamos o comando. Agora, ao acessar _localhost_ na porta `8080`, conseguimos realizar esse mapeamento de uma porta específica do nosso _host_ para o _container_.
```makefile
localhost:8080
```
Temos como retorno no navegador:

`Hello Docker!`

Temos o isolamento de rede, mas conseguimos realizar um mapeamento para acessar o conteúdo do _container_, validando o que está acontecendo, evitando não sabermos o que ocorre dentro do _container_. No final, conseguimos expor nossa aplicação para que as pessoas usuárias possam acessar.

### Resumo
Inicialmente, execute o comando `docker run -d dockersamples/static-site` para que o seu host baixe a imagem e execute o container em seguida.

A seguir, verifique se o seu container está em execução sem problemas através do comando `docker ps` ou `docker container ls`. Repare na coluna `PORTS` e veja que seu container está informando que possui uma aplicação que pode ser exposta tanto na porta 80 quanto na 443.

Obtendo esta informação, remova o container recém-criado com o comando `docker container rm <id-do-container> --force`.

Seu objetivo agora será criar um novo container fazendo o devido mapeamento de portas. Para isso, execute o comando `docker run -d -p 8080:80 dockersamples/static-site`. Repare que através da flag `-p`, estamos informando que a porta 8080 de nosso host irá refletir na porta 80 do container.

Por fim, acesse em seu navegador `localhost:8080` e veja a aplicação sendo carregada dentro de seu container.

Com a utilização da flag `-p`, é possível fazer uma ponte entre a aplicação dentro do container e o nosso host. Este cenário é muito interessante quando queremos testar o funcionamento e como uma aplicação está interagindo com outras.