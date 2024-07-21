[[Resumo do que é Docker]]
[[comandos do docker]]
## Conhecendo o problema

Temos uma aplicação _**Nginx**_ que vai servir como um [[load balancer]] (balanceador de carga) do nosso sistema. Além disso, temos uma aplicação _**Java**_ e uma aplicação **C#** rodando com o _.NET_.

Nessa situação, queremos que todas essas aplicações estejam em execução para que o sistema como um todo esteja operacional. Para isso, precisamos de uma **máquina** para que essas aplicações rodem e o sistema funcione.

A nossa aplicação C# roda na **porta 80**, isto é, precisa da porta 80 para executar. Da mesma forma, a aplicação Java roda na porta 80, assim como a Nginx. Nesse caso, o C# que utilizamos está na **versão 9**, o Java na **versão 17**, e o Nginx na **versão 1.17.0**.

### Quais problemas podem ocorrer nessa situação?

Se observarmos cada uma dessas aplicações e ferramentas, podemos acabar tendo um **conflito de portas**, porque as 3 aplicações nesse cenário dependem da porta 80 para executar o fluxo necessário.

Além disso, como podemos **alterar as versões de maneira prática**? Se simplesmente fizéssemos o _downgrade_ ou o _upgrade_ da versão do C#, atualizando o .NET, quebraríamos algo? Precisamos desinstalar para instalar uma nova? O mesmo se aplica ao Java e ao Nginx: conseguiríamos atualizar de maneira prática?

Outra questão é a seguinte: como vamos ter um **controle de recursos de memória e de CPU** para essas aplicações? Por exemplo: a aplicação C# precisa de 100 _millicores_ de CPU e 200 _megabytes_ de memória para funcionar. Como podemos definir isso de maneira fácil?

O mesmo é válido para as outras aplicações: como podemos fazer essa definição de consumo de recursos do sistema de maneira prática? É uma questão que precisamos levantar.

Por fim, considerando todos esses problemas de uma vez só, como podemos fazer o **processo de manutenção** dessas aplicações? Como vamos conseguir mudar a versão? Como vamos ter esse controle sobre as portas das aplicações? Como vamos gerenciar os recursos e manter isso a longo prazo?

Uma solução que poderíamos pensar inicialmente que seria bem simples, mas ao mesmo tempo problemática, seria simplesmente comprar **uma máquina para cada aplicação**. Dessa forma, teríamos uma máquina para a aplicação .NET, outra máquina para a aplicação Java, e outra para a aplicação Nginx.

Assim, resolveríamos o problema de conflito de portas, já que cada máquina teria a sua respectiva porta 80; conseguiríamos controlar os recursos de maneira mais fácil, pois não teríamos essa dependência das aplicações entre si; e o controle de versionamento também ficaria mais fácil, pois não teríamos diversas aplicações no mesmo sistema.

Porém, qual o problema disso? O nosso dinheiro vai embora, porque se tivéssemos uma máquina para cada aplicação, pensando em sistemas que têm milhares ou milhões de aplicações em execução simultaneamente, precisaríamos de milhares ou milhões de máquinas para que o sistema esteja operante.

### Máquinas virtuais

Existe uma solução já bem difundida, que não é recente e ajuda a resolver esses problemas: as **máquinas virtuais**, onde teríamos o _hardware_ bem definido; o sistema operacional, seja ele Windows, Linux, _Mac_ ou outro; e uma camada de _hypervisor_, que fará um meio de campo para virtualizar um novo sistema operacional.

Esse sistema pode ser um Windows, um Linux, um Mac, rodando dentro de outro sistema, mas graças a essa camada de hypervisor, teríamos uma **camada de isolamento** desse sistema operacional original. Assim, conseguiríamos instalar as nossas dependências e aplicações de maneira isolada, porque cada uma delas tem o seu respectivo sistema operacional.

Essa solução resolve esses problemas iniciais, mas a pergunta que fica nesse momento é a seguinte: **é realmente necessário fazer isso**?

Queremos executar as nossas aplicações, como vimos, de maneira isolada, ter um controle de recursos, e ter um controle de versionamento bem definido. Então, essa camada de hypervisor é realmente necessária? Nessas situações, precisamos sempre virtualizar um sistema operacional? Pode ser que sim, pode ser que não, mas no caso que vamos abordar durante este curso, é a **utilização de [[Containers]]**.

No caso do uso de containers, não temos a camada de sistema operacional virtualizado, nem a de hypervisor, mas sim a camada diretamente do container rodando o sistema operacional, e mesmo assim, de forma isolada. Cada aplicação está isolada entre si e também isolada do sistema operacional original.

É isso que vamos entender a partir de agora: por que os containers são mais **leves**? Como eles vão **garantir esse isolamento**? E como eles vão funcionar **sem instalar um sistema operacional**?

No caso da máquina virtual, a aplicação C# terá um sistema operacional para ela, bem como a aplicação Java. Já no ambiente de containers, a aplicação C# está diretamente dentro do container. Nesse caso, qual sistema operacional ela vai usar? Windows? Linux? Precisamos instalar um sistema?

Precisamos responder essas perguntas. De onde vêm essas informações? Por último, temos a seguinte pergunta: como ficará a **divisão de recursos** entre as aplicações que estarão, a partir de agora, containerizadas?


## Docker Run

É importante compreender que, para o funcionamento do nosso `docker run`, é necessário localizar essa entidade denominada **`imagem`**, a fim de que o _container_ seja efetivo. Quando inserimos um nome sem sentido, o Docker não o localiza. No entanto, ao utilizar _`hello world`_, a localização é bem-sucedida.

Como o Docker identifica os locais para procurar e encontrar esses nomes, resolvendo e executando nosso _container_?

Um vasto repositório, conhecido como [[Docker Hub]] , abriga uma variedade dessas [[Imagens]], correspondendo aos parâmetros que estamos especificando. .

 [Docker Hub](https://hub.docker.com/)

docker

docker

Docker