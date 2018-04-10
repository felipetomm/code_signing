# Assinatura de executável com certificado próprio
Processo de criação do certificado digital e assinatura do Executável da empresa

1.  Criação do certificado Digital

`openssl req -x509 -days 365 -newkey rsa:2048 -keyout my-key.pem -out my-cert.pem`

2.  Informações do certificado

> Country Name (2 letter code) [AU]:**BR**
>
> State or Province Name (full name) [Some-State]:**Rio Grande do Sul**
>
> Locality Name (eg, city) []:**My City**
>
> Organization Name (eg, company) [Internet Widgits Pty Ltd]:**My Company**
>
> Organizational Unit Name (eg, section) []:**I.T.**
>
> Common Name (e.g. server FQDN or YOUR name) []:**mydomain.com**
>
> Email Address []:**user@home.com**

3.  Criando o arquivo PFX

`openssl pkcs12 -export -in my-cert.pem -inkey my-key.pem -out my-pfx.pfx`

4.  Arquivo Public

`openssl pkcs12 -in my-pfx.pfx -clcerts -nokeys -out my-public.pem`

5.  Por fim, assinal o executável

`.\signtool\signtool.exe sign /t http://timestamp.comodoca.com /f my-pfx.pfx /p aquivaiasenha Application.exe`
