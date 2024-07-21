
- Por que os _containers_ são mais **leves** em relação a uma máquina virtual?
- Como eles garantem o **isolamento**?
- Como funcionam sem instalar um **sistema operacional**?
- Como fica a **divisão de recursos** do sistema?

## Como _containers_ funcionam?

O container funciona da seguinte maneira: dentro de um sistema operacional, temos vários containers, isto é, diversas aplicações sendo executadas. No entanto, eles funcionarão diretamente como **processos** dentro do nosso sistema.

Enquanto uma máquina virtual terá toda aquela etapa de **virtualização** dos sistemas operacionais dentro do sistema original, os containers funcionarão diretamente como processos dentro do sistema.

Portanto, no que diz respeito ao **consumo**, podemos visualizar que ele será um pouco menor. O consumo de recursos, a carga para que ele possa ser executado, é um pouco menor, porque eles serão processos, e não uma virtualização completa.

- Como um processo garantirá o **isolamento**?
- Como ele funcionará sem instalar um sistema operacional?
- Como vamos conseguir resolver e responder essas perguntas?

A questão é que, quando containers estiverem em execução no nosso sistema operacional, para garantir o isolamento entre cada um deles e o sistema operacional original, existe um conceito chamado _**[[Namespaces]]**_, que garantirá que cada um desses containers tenha capacidade de se isolar em determinados **níveis**.

O UTS, ajuda a responder à próxima pergunta:

- Como o container dentro do sistema operacional funcionará sem um sistema operacional?

Na verdade, graças ao namespace UTS, se executarmos nossos containers em uma máquina com kernel _Linux_, cada um dos containers, a princípio, também terá um pedaço desse kernel, mas devidamente isolado.

Assim, conseguimos responder à pergunta: não precisamos necessariamente instalar um sistema operacional dentro de um container, porque ele já terá, graças ao namespace UTS, acesso ao kernel do sistema original, mas isoladamente.

### _Cgroups_

Por fim, na parte de **gerenciamento de recursos**, suponha que queiramos definir, conforme levantado em um problema anteriormente, o consumo máximo de memória, de CPU e afins para cada um dos containers.

Existe outro conceito chamado _**Cgroups**_, que garantirá que podemos definir, tanto de maneira automática, quanto de maneira manual, como os consumos serão feitos para cada um desses processos, isto é, para cada um desses containers dentro do sistema operacional.

De volta às perguntas originais, graças aos namespaces e aos Cgroups, conseguimos garantir o isolamento, garantir que o nosso container funciona sem instalar um sistema operacional dentro dele, e também conseguir ter um controle de gerenciamento de recursos como **memória** e **CPU**.

Quanto à questão de por que eles são mais leves, entendemos que eles funcionarão como processos diretamente do sistema operacional, mas ao longo deste curso, entenderemos ainda mais por que eles conseguem ser tão mais práticos em relação a uma máquina virtual em termos de consumo de recursos e de tamanho de armazenamento também no nosso sistema operacional.

containers