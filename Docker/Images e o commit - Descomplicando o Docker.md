
#### Entendendo de camadas
![[Pasted image 20240720190301.png]]![[Pasted image 20240720190341.png]]


MULTI-LINE

RUN yum update -y && \\
yum install -y apache2\\
git\\
java\\
python

#### Boas práticas- 

 - Sempre dentro das imagens, apenas pacotes necessário
 - Sempre limpe a casa rm -rf / diretório
 - Reduza o numero de camadas // use o RUN com moderação
 - Use o .DOCKERIGNORE
 - Adicone um NON-ROOT user
 - CMD (Serve para que você posa executar um comando)
 - Entenda ~~UMA~~ duas coisas - Use o ENTRYPOINT
 - Entenda ~~UMA~~ ~~DUAS~~ TRÊS coisas - Use ENTRYPOINT e CMD no mesmo Dockerfile (MODO EXEC obrigatório)
 - USE ou NÃO o CACHE
 - CONTAINERS ARE BE IMMUTABLE & EPHEMERAL
 - USE um script de START ou NÃO
 - VARIAVEIS ENV KEVIN="LINDO"
 - USE VARIAVEIS no Dockerfile:
    ENV app_dir/opt/app
	WORKDIR ${app_dir}
	ADD .$app_dir
- SHELL ["powershell","-command"] // você pode trocar o shell
- LABELS
  LABEL "com.example.vendor"="LINUXtips"
  LABEL com.example.label-whit-value="VAIII"
  LABEL version="1.0"
  LABEL description ="Aqui você pode\\
  usar multi-line! :D"
- COPY
    COPY ./app
    COPY dir1 /app
    COPY file /app
- ARGS // São argumentos que posso mudar em momento de build
  ![[Pasted image 20240720192022.png]]
- HEALTHCHECK // ele faz um check a cada x periodo de tempo 
  HEALTHCHECK --invervall=5m --timeout=3s\\
  CMD curl -f http://localhos/ || exit 1
- MULTISTAGE // quase um pipeline dentro do seu container

