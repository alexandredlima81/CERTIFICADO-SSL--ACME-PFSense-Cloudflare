# CERTIFICADO SSL -- ACME - pfSense - Cloudflare

<p align="justify">
Gerando Certificados SSL no pfSense com Let's Encrypt
Quando um domínio (nomedodominio.com) é público ou possui suporte à validação DNS, a melhor opção para obter certificados SSL gratuitos e globalmente reconhecidos é o Let's Encrypt. Além de serem gratuitos, seus certificados podem ser renovados automaticamente.

Por padrão, a validação e emissão dos certificados pelo Let's Encrypt utilizam o HTTP-01 Challenge, que exige a exposição da porta 80 para que a autoridade certificadora valide a posse do domínio. No entanto, por razões de segurança, nem sempre é viável expor essa porta.

Para contornar essa limitação, podemos utilizar a validação via DNS-01 Challenge, que elimina a necessidade de portas abertas.

## Pré-requisitos
Antes de iniciar o processo de emissão do certificado, certifique-se de que possui:

✅ Um domínio registrado e gerenciado em um provedor compatível (exemplo: Cloudflare).\
✅ Acesso administrativo ao pfSense, com o pacote ACME instalado.\
✅ Credenciais de API do provedor de DNS para automação da validação DNS-01.


## O que é DNS-01 Challenge e como funciona?
O DNS-01 Challenge é um método de validação usado pelo Let's Encrypt e outras Autoridades Certificadoras (CAs) para comprovar a posse de um domínio antes de emitir um certificado SSL.

## Fluxo da validação DNS-01 Challenge:
O Let's Encrypt solicita a criação de um registro TXT no DNS do domínio, contendo um código de desafio único.
A CA consulta o DNS para verificar se o registro TXT foi criado corretamente.
Se a validação for bem-sucedida, o certificado é emitido.

**Vantagens do DNS-01 Challenge:**

✅ Dispensa a abertura de portas (80 ou 443)\
✅ Permite emitir certificados wildcard (exemplo: *.nomedodominio.com)\
✅ Automatização possível com provedores de DNS compatíveis (Cloudflare, AWS Route 53, GoDaddy, etc.)

Essa abordagem será documentada nos próximos passos, detalhando a configuração do ACME (Let's Encrypt) no pfSense, integração com Cloudflare.

## PROXIMOS PASSOS (EM ANDAMENTO)

# Ambiente Cloudflare

## Criar os registro DNS do tipo TXT (Manualmente)

**1.	Acesse o painel da Cloudflare:**

  o	Vá para Cloudflare Dashboard \
  o	Selecione seu domínio hirostack.com \

**2.	Criar os registros TXT:**

  o	Vá para DNS → Adicionar Registro \
  o	Escolha o tipo TXT \
  o	Em Nome, coloque:

>
>_acme-challenge.nomedodominio.com
>

o	Em Conteúdo, adicione o código fornecido pelo Let's Encrypt:

>
>abc123xyz
>
o	Clique em Salvar

**3.	Criar o segundo registro TXT:**

o	Adicione um novo registro TXT com o mesmo nome:
>
>_acme-challenge.hirostack.com
>
o	No conteúdo, coloque o segundo código gerado:

>
>def456uvw
>

o	Salve novamente.

**4.	Esperar a propagação (pode levar alguns minutos).**


## Criando um API Token no Cloudflare

# Ambiente pfSense

##

## Considerações Finais
(EM ANDAMENTO)
## Links de referência

https://letsencrypt.org/docs/challenge-types/?utm_source=chatgpt.com \
https://letsencrypt.org/docs/client-options/ \
https://docs.netgate.com/pfsense/en/latest/packages/acme/index.html \
https://docs.netgate.com/pfsense/en/latest/certificates/index.html \
https://developers.cloudflare.com/fundamentals/api/get-started/create-token/ \
https://community.cloudflare.com/t/cloudflare-lets-encrypt-pfsense/118198/5?utm_source=chatgpt.com \
https://wolffhaven.gitlab.io/wolffhaven_icarus_test/2017/11/07/intranet-ssl-certificate-for-pfsense-using-lets-encrypt--cloudflare/?utm_source=chatgpt.com
