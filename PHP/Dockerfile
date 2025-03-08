# Imagem base oficial do PHP com Apache.
# Para outras versões do PHP consultar as imagens disponiveis em https://hub.docker.com/_/php
FROM php:8.4-apache

# Projeto ACBr
LABEL maintainer="ti@projetoacbr.com.br" \
      version="1.0" \
      description="Imagem PHP Apache, com requisitos básicos para rodar os Demos da ACBrLib em PHP"

#Diretorio padrão Apache onde fica os fontes do projeto WEB.
WORKDIR /var/www/html/

# Instalação dos pacotes basicos essenciais para o funcionamento do projeto, e depois limpa arquivos temporários. 
# Para adicionar outros pacotes, veja o exemplo na linha comentada abaixo.
RUN set -eux; \
    apt-get update; \
    apt-get install -y \
        subversion \
        openssl \
        libxml2 \
        libffi-dev \
        libonig-dev \
        libssl-dev \
        vim \
        #<nome_do_pacote_extra> \
    ; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*   

# Criando Links simbolicos das bibliotecas ".SO" necessarias, e com os nomes conforme esperado pelos Fontes do ACBr
RUN ln -s /usr/lib/x86_64-linux-gnu/libxml2.so.2  /usr/lib/x86_64-linux-gnu/libxml2.so

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

####################################
###  Executando a aplicação PHP  ###
####################################
# Substitua as linhas abaixo, pelas instruções de carga da SUA APLICAÇÃO PHP

# Faz download dos fontes de demonstração PHP do ACBr para o diretorio do Apache e ajusta as permissões dos arquivos.
RUN svn checkout "https://svn.code.sf.net/p/acbr/code/trunk2/Projetos/ACBrLib/Demos/PHP/" ./; \
    rm -rf VersoesSemFFI 

# Faz download dos fontes de demonstração PHP do ACBr para o diretorio do Apache e ajusta as permissões dos arquivos.
RUN svn checkout "https://svn.code.sf.net/p/acbr/code/trunk2/Projetos/ACBrLib/Demos/PHP/" ./; \
    rm -rf VersoesSemFFI 

# --- Copiando as Bibliotecas do ACBrLib, para dentro da Imagem ---
# Para utilizar as versões PRO das Bibliotcas (.so), 
# 1 - Baixe as Bibliotcas Pro do Fórum do ACBr
#     https://www.projetoacbr.com.br/forum/files/category/36-acbrlib-pro/
# 2 - No Arquivo baixado, localize a Bibliotca na Pasta:  Linux, Console, MT          
# 2 - Substitua as Biblioteca Pro, no mesmo diretorio 'libs/'
COPY ../libs/libacbrcep64.so ConsultaCEP/MT/ACBrLib/x64/
COPY ../libs/libacbrconsultacnpj64.so ConsultaCNPJ/MT/ACBrLib/x64/
COPY ../libs/libacbrnfe64.so NFe/MT/ACBrLib/x64/
COPY ../libs/libacbrboleto64.so Boleto/MT/ACBrLib/x64/
COPY ../libs/libacbrgtin64.so GTIN/MT/ACBrLib/x64/

# Ajustando o Dono e Grupo dos arquivos
RUN chown -R www-data:www-data ./*