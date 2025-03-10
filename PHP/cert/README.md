# Pasta `cert`

Nessa pasta, estamos salvando um arquivo `PFX`, para ser facilmete utilizado no Docker.

O Arquivo `A1.PFX`, presente nesse diretório, é inválido  e não será funcional nos exemplos.

Nesse repositório, ele serve apenas para ilustrar que você poderia copiar os seus próprios certificados nessa pasta, e eles seriam copiados pelo Script, para dentro do Docker na pasta: `/var/www/html/cert/`

Você não precisa seguir essa prática, provavelmente em sua API final, os Certificados serão parte integrante das configurações do Sistema, e podem ser informados por Stream

O Certificado `A1.pfx` desse diretório, é um Certificado auto-assinado. Gerado usando os comandos abaixo:

```
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 3650 -nodes -subj "/C=BR/ST=São Paulo/L=Tatuí/O=ProjetoACBr/OU=Dev/CN=projetoacbr.com.br"
```
```
openssl pkcs12 -export -out cert.pfx -inkey key.pem -in cert.pem
```

