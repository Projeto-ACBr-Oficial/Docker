# Imagem base oficial do PHP com Apache.
# Para outras versões do PHP consultar as imagens disponiveis em https://hub.docker.com/_/php
FROM php:8.4-apache

# Projeto ACBr
LABEL maintainer="ti@projetoacbr.com.br" \
      version="1.0" \
      description="Imagem PHP Apache, com requisitos básicos para rodar os Demos da ACBrLib em PHP, usando a biblioteca FFI "

#Diretorio padrão Apache onde fica os fontes do projeto WEB.
WORKDIR /var/www/html/

# Instalação dos pacotes basicos essenciais para o funcionamento do projeto, e depois limpa arquivos temporários. 
# Para adicionar outros pacotes, veja o exemplo na linha comentada abaixo.
RUN set -eux && \
    apt-get update && \
    apt-get install -y \
        subversion \
        wget \
        openssl \
        libxml2 \
        libffi-dev \
        libonig-dev \
        libssl-dev \
        vim \
        #<nome_do_pacote_extra> \
    && \
    apt-get clean&& \
    rm -rf /var/lib/apt/lists/*   

# Criando Links simbolicos das bibliotecas ".SO" necessarias, e com os nomes conforme esperado pelos Fontes do ACBr
RUN ln -s /usr/lib/x86_64-linux-gnu/libxml2.so.2  /usr/lib/libxml2.so

# Instalação das extensões necessarias para PHP, se precisar instalar outras extensões 
# veja o exemplo na linha comentada abaixo.
RUN docker-php-ext-install \
    ffi \
    mbstring
    #<nome_da_extensão_extra> \

# Copiando um arquivo php.ini, já configurado para usar os módulos FFI e MBSTRING
# Para usar um php.ini proprio, substitua o arquivo, que está no mesmo diretorio do arquivo Dockerfile.
COPY php.ini /usr/local/etc/php/

# Editando Arquivo de Configuração do OpenSSL, para habilitar  modo Default e Legacy.
COPY openssl-legacy.cnf /etc/ssl/
ENV OPENSSL_CONF=/etc/ssl/openssl-legacy.cnf
RUN openssl list -providers


##################################################################################
###               Baixando ACBrLib DEMO para dentro do container               ###
### 1 - Para usar a versão PRO,                                                ### 
### 2 - Comente as linhas abaixo                                               ###
### 2 - Leia as intruções no próximo Bloco                                     ###  
##################################################################################
RUN wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrboleto64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrcep64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrconsultacnpj64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrgtin64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrmdfe64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrnfe64.so && \
    wget -P /usr/lib/ https://github.com/Projeto-ACBr-Oficial/Docker/raw/refs/heads/main/libs/libacbrnfse64.so

####################################################################################
###               Copiando ACBrLib PRO para dentro do container                  ###
###                                                                              ###
### 1 - Baixe as Bibliotecas PRO do Fórum do ACBr                                ###
###     https://www.projetoacbr.com.br/forum/files/category/36-acbrlib-pro/      ### 
### 2 - No Arquivo baixado, localize a Biblioteca na Pasta:                      ###
###     Linux, CONSOLE-MT                                                        ###          
### 3 - Copie as Biblioteca Pro, no diretorio 'libs/' e descomente o COPY        ###
### 4 - O comando abaixo, cuidará de copiar as novas Libs, no Conteiner          ###
####################################################################################

#COPY libs/*.so /usr/lib/

### Copiando os certificados, que foram informados na pasta cert/ ###
COPY cert /var/www/html/cert/

####################################
###  Instalando a aplicação PHP  ###
####################################
# Substitua as linhas abaixo, pelas instruções de carga da SUA APLICAÇÃO PHP

# Faz download dos fontes de demonstração PHP do ACBr para o diretorio do Apache, e remove pasta desnecessárias
RUN svn checkout "https://svn.code.sf.net/p/acbr/code/trunk2/Projetos/ACBrLib/Demos/PHP/" ./ && \
    rm -rf VersoesSemFFI && \
    rm -rf .svn && \
# Faz download dos Schemas para o diretorio do Apache, e remove pasta desnecessárias
    svn checkout "https://svn.code.sf.net/p/acbr/code/trunk2/Exemplos/ACBrDFe/Schemas/" && \
    rm -rf Schemas/.svn

### Copiando arquivos de Configuração, para facilitar a execução dos Demos ###
COPY conf/ACBrCEP.INI ConsultaCEP/MT
COPY conf/ACBrNFe.INI NFe/MT

# Criando Links Simbolicos nas pastas esperadas pelo Demo do ACBr em PHP 
#  NOTA: provavelmente você não precisa disso, no seu Docker
RUN ln -s /usr/lib/libacbrboleto64.so Boleto/MT/ACBrLib/x64/libacbrboleto64.so && \
    ln -s /usr/lib/libacbrcep64.so ConsultaCEP/MT/ACBrLib/x64/libacbrcep64.so && \
    ln -s /usr/lib/libacbrconsultacnpj64.so ConsultaCNPJ/MT/ACBrLib/x64/libacbrconsultacnpj64.so && \
    ln -s /usr/lib/libacbrgtin64.so GTIN/MT/ACBrLib/x64/libacbrgtin64.so && \
    ln -s /usr/lib/libacbrmdfe64.so MDFe/MT/ACBrLib/x64/libacbrmdfe64.so && \
    ln -s /usr/lib/libacbrnfe64.so NFe/MT/ACBrLib/x64/libacbrnfe64.so && \
    ln -s /usr/lib/libacbrnfse64.so NFSe/MT/ACBrLib/x64/libacbrnfse64.so

# Ajustando o Dono e Grupo dos arquivos em /var/www/html
RUN chown -R www-data:www-data ./*