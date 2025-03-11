# Sobre o Docker **ACBr PHP**
Docker ACBr PHP contém o contêiner com exemplos de aplicações PHP que usam a ACBrLib
[Links para Imagens do Docker em execução](https://hub.docker.com/r/projetoacbr/acbrlib_php)

Baixando a imagem do docker hub

```sh
docker pull projetoacbr/acbrlib_php
```


# Rodando o Docker **ACBr PHP**
Executando o projeto
Obs.: a opção **-p** redireciona conexão do servidor (contêiner) para a porta 8080

**-it** modo interativo 

```sh
docker run -p 8080:80 -it projetoacbr/acbrlib_php:latest
```

Acesse em seu navegador de preferência http://localhost:8080

# Transformar o Docker em **ACBr PRO** 
- Onde baixar as bibliotecas **Versão Pro**
- Onde copiar as bibliotecas **Versão Pro**

# Customizando o Docker para rodar a sua aplicação
- Explicação sobre quais linhas editar no `DockerFile`
- Explicação de como recompilar o Docker
- Explicação de como usar outro `php.ini`