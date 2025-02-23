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

## ** Criando um Token de API no Cloudflare**

O pfSense precisa de permissões para modificar os registros DNS automaticamente, por este motivo deve ser gerado um Token de API com as devidas permissões.

**1.** Acesse o Cloudflare Dashboard.

**2.** Vá para: 
  - My Profile > API Tokens (para tokens de usuário) 
  - Manage Account > API Tokens (para tokens de conta)
    
**3.** Clique em "Criar Token".

**4.** Escolha "Criar Token Personalizado".
   
**6.** Defina as permissões: 
  - Zona → DNS → Editar (permite criar e excluir registros TXT para validação).
    
**7.** Selecione os recursos: 
  - Inclua apenas as zonas específicas que o Let's Encrypt usará.
    
**8.** (Opcional) Restrinja por IP para maior segurança.
   
**9.** Clique em "Continuar", revise e "Criar Token".
    
**10.** Copie o segredo para um local seguro e configure o Certbot para usá-lo. 

>
>⚠️**Aviso!**⚠️
>
>  O segredo do token é mostrado apenas uma vez. Não armazene o segredo em texto simples onde outros possam acessá-lo. \
>Recomendo utlizar cofres de senha, como por exemplo KeePassXC Password Manager para uso local ou em integrações de CI\CD utilizar ferramentas como AWS Secrets Manager, HashiCorp Vault entre outras. \
>Pois qualquer pessoa com esse token pode executar as ações autorizadas contra os recursos aos quais o token tem acesso.
>

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
