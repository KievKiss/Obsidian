
## Volumes e bind mounts
A persistência de dados no [[Docker]] é realizada principalmente através de **volumes** e **bind mounts**. Aqui estão alguns comandos básicos:

1. **Criar um volume**:

```bash
docker volume create meu_volume
```

2. **Listar volumes**:

```bash
docker volume ls
```

3. **Remover um volume**:

```bash
docker volume rm meu_volume
```

4. **Usar um volume com um contêiner**:

```bash
docker run -d --name meu_container -v meu_volume:/caminho/no/container minha_imagem
```

Para **bind mounts**, que mapeiam um local no sistema de arquivos do host para um local no contêiner, você pode usar a opção `-v` com o comando `docker run` da seguinte maneira:

```bash
docker run -d --name meu_container -v /caminho/no/host:/caminho/no/container minha_imagem
```

Neste exemplo, `/caminho/no/host` é o caminho para o diretório no seu sistema de arquivos e `/caminho/no/container` é o caminho no sistema de arquivos do contêiner.

Lembre-se, a persistência de dados é uma parte importante do trabalho com contêineres Docker, pois permite que os dados sobrevivam além do ciclo de vida do contêiner. No entanto, é importante gerenciar seus volumes e bind mounts com cuidado para evitar o uso desnecessário de espaço em disco.

## TMPFS

`tmpfs` é um sistema de arquivos temporário que reside na memória e/ou no espaço de troca do seu sistema. No Docker, você pode usar `tmpfs` para criar um sistema de arquivos temporário dentro do seu contêiner que não é gravado no disco, o que pode ser útil para armazenar informações sensíveis ou para melhorar o desempenho para cargas de trabalho que exigem muitas operações de E/S.

Aqui está como você pode usar `tmpfs` com o Docker:

```bash
docker run -d --tmpfs /tmp meu_container
```

Neste exemplo, um sistema de arquivos `tmpfs` é criado no diretório `/tmp` do contêiner. Qualquer coisa escrita neste diretório será armazenada na memória do host e será perdida quando o contêiner for parado.

Você também pode especificar opções para o `tmpfs` usando a sintaxe `--tmpfs /caminho:noexec,nosuid,size=1g`. Isso criará um `tmpfs` no caminho especificado com as opções `noexec` e `nosuid` e um tamanho máximo de 1 GB.

Por favor, note que o uso de `tmpfs` pode consumir uma quantidade significativa de memória do host, então use com cuidado. Além disso, qualquer dado escrito em um `tmpfs` será perdido quando o contêiner for parado, então não é adequado para dados que precisam ser persistentes. Para a persistência de dados, considere usar volumes Docker ou bind mounts.