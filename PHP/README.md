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

Acesse em seu navegador de preferência http://localhost:8080<br/>
Será carregada a página inicial com os Links dos exemplos em PHP

# Transformar o Docker em **ACBr PRO** 
1. Link com informações da ACBr PRO [../libs/README.md](../libs/README.md#versão-pro)
2. Copie as bibliotecas para [../PHP/libs](../PHP/libs)
3. Comente as linhas   [Dockerfile](../PHP/Dockerfile)

```dockerfile
RUN wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrboleto64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrcep64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrconsultacnpj64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrgtin64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrmdfe64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrnfe64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrnfse64.so

```
para

```dockerfile
#RUN wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrboleto64.so && \
#    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrcep64.so && \
#    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrconsultacnpj64.so && \
#    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrgtin64.so && \
#    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrmdfe64.so && \
#    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrnfe64.so && \
#    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrnfse64.so

```

4. Descomente as linhas
```dockerfile
#COPY libs/*.so /usr/lib/
```

```dockerfile
COPY libs/*.so /usr/lib/
```


# Customizando o Docker para rodar a sua aplicação
- Explicação sobre quais linhas editar no `DockerFile`
- Explicação de como recompilar o Docker
- Explicação de como usar outro `php.ini`