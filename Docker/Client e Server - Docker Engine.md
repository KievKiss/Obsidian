1. **Client (Cliente)**:
    
    - O “Client” ou “Cliente” é a parte do Docker que você interage diretamente. É a interface de linha de comando (CLI) que você usa para executar comandos relacionados ao Docker no seu terminal.
    - Quando você digita comandos como `docker run`, `docker build` ou `docker pull`, está se comunicando com o cliente do Docker.
    - O cliente é responsável por enviar solicitações para o servidor (que veremos a seguir) e exibir as respostas no seu terminal.
2. **Server (Servidor)**:
    
    - O “Server” ou “Servidor” é a parte do Docker que gerencia os contêineres e imagens.
    - Ele executa os contêineres, gerencia o ciclo de vida deles (iniciar, parar, reiniciar) e lida com a criação e armazenamento de imagens.
    - O servidor também é responsável por expor a API do Docker, que o cliente usa para se comunicar com ele.
    - Em outras palavras, o servidor é o “motor” real do Docker que executa os contêineres.

Em resumo, o cliente é a interface que você usa para dar comandos ao Docker, enquanto o servidor é a parte que realmente executa os contêineres e gerencia as imagens. Eles trabalham juntos para tornar o Docker funcional e útil! 