# Assinatura de executável com certificado próprio
Processo de criação do certificado digital e assinatura do Executável da empresa

# Criação do certificado Digital
`openssl req -x509 -days 365 -newkey rsa:2048 -keyout my-key.pem -out my-cert.pem`

##
`Generating a 2048 bit RSA private key
.....................+++
.............................................+++
writing new private key to 'magestal-key.pem'
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:**BR**
State or Province Name (full name) [Some-State]:**Rio Grande do Sul**
Locality Name (eg, city) []:**My City**
Organization Name (eg, company) [Internet Widgits Pty Ltd]:**My Company**
Organizational Unit Name (eg, section) []:**I.T.**
Common Name (e.g. server FQDN or YOUR name) []:**mydomain.com**
Email Address []:**user@home.com**`

## Criando o arquivo PFX
`openssl pkcs12 -export -in my-cert.pem -inkey my-key.pem -out my-pfx.pfx`

## Arquivo Public
openssl pkcs12 -in my-pfx.pfx -clcerts -nokeys -out my-public.pem

## Por fim, assinal o executável
.\signtool\signtool.exe sign /t http://timestamp.comodoca.com /f my-pfx.pfx /p aquivaiasenha Application.exe
