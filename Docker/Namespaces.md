namespaces

### O que são _namespaces_?

Teremos os principais namespaces: primeiramente, o **PID**, que garante o isolamento a nível de processo dentro de cada um dos containers. Portanto, um processo dentro de um container, que, consequentemente, é um processo dentro do sistema operacional, estará isolado de todos os outros do nosso _host_, isto é, da nossa máquina original.

Teremos também o **NET**, o namespace de **rede**, que garantirá o isolamento entre uma interface de rede de cada um dos containers e também do nosso sistema operacional original.

O namespace **IPC** será de intercomunicação entre cada um dos processos da nossa máquina.

O **MNT**, que é a parte de _file system_ (sistema de arquivos), montagem, volumes e afins, também estará devidamente isolado.

**UTS** faz um compartilhamento e um isolamento ao mesmo tempo do host, isto é, do _kernel_, da máquina que executa o container.

![[Pasted image 20240423131152.png]]

