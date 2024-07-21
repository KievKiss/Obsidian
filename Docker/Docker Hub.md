Docker Hub

Um vasto repositório, conhecido como [Docker Hub](https://hub.docker.com/) , abriga uma variedade dessas imagens, correspondendo aos parâmetros que estamos especificando. Voltamos ao terminal. Se executarmos `docker run --help`, notamos as informações apresentadas.

```bash
docker run --help
```

Além das diversas _flags_ retornadas, o comando `docker run` segue a seguinte estrutura:

```
Usage: docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

O `docker run`, algumas opções (a serem compreendidas em breve), e o nome da imagem que pretendemos executar. Portanto, _hello world_ é o nome de uma imagem.

Isso significa que, se formos ao [Docker Hub](https://hub.docker.com/) e pesquisarmos na parte superior, por exemplo, por _hello world_, ele vai encontrar essa imagem.

A imagem oficial significa que ela foi criada e é mantida por um grupo confiável de pessoas desenvolvedoras e tem reconhecimento da comunidade. Ela recebe esse selo de oficial. Na parte inferior da busca, ele mostra as instruções, o que é essa imagem efetivamente, conta uma breve história sobre ela e pronto.



Docker Hub