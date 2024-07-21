[[Docker]]
## Criando a conta no [[Docker Hub]]

Primeiro, é necessário que você crie uma conta na parte direita da [home do Docker Hub](https://hub.docker.com/). Insira seu nome de usuário, e-mail, senha, aceite os termos e marque a opção recaptcha. Depois, clique em "_Sign up_" e confirme sua conta por e-mail.

Após a confirmação, no canto superior direito, clique em "_Sign in_". Insira seu nome de usuário e a senha que utilizou no momento do cadastro.

Quando entrar, o site carregará e na barra de navegação superior, você terá a opção "_Repositories_" (repositórios).

## Autenticando a conta do Docker Hub

Para isso, usamos o comando `docker login -u`. Em seguida, inserimos o nosso nome de usuário, `aluradocker`

```console
docker login -u aluradocker
```

Ao pressionar "Enter", será solicitada a senha (_password_) que usou durante o cadastro no Docker Hub. Por questões de segurança, o número de caracteres não aparecerá, mas estará sendo digitado.

Quando pressionar "Enter" e o login for bem-sucedido, receberá um aviso que sua senha foi armazenada de maneira não criptografada em um determinado caminho no arquivo `config.json`.

```console
Login Succeeded
```

## Subindo a imagem para Docker Hub

Agora, o que queremos fazer? Queremos enviar a imagem na versão `1.0` para o Docker Hub.

Para isso, usamos um comando específico. Ao invés do `docker pull`, utilizaremos o `docker push`seguido da imagem. Assim, esse comando enviará automaticamente a nossa imagem para o Docker Hub.

```console
docker push SeuNomeDeUsuario/app-node:1.0
```


Para não ter que buildar uma nova imagem basta seguir "clonar" a imagem que seja subir da seguinte forma:

```console
docker tag exemplo/app-node:1.2 SeuNomeDeUsuario/app-node:1.2
docker push SeuNomeDeUsuario/app-node:1.2
```
