# CERTIFICADO SSL -- ACME - pfSense - Cloudflare

<p align="justify">
Gerando Certificados SSL no pfSense com Let's Encrypt
Quando um domínio (nomedodominio.com) é público ou possui suporte à validação DNS, a melhor opção para obter certificados SSL gratuitos e globalmente reconhecidos é o Let's Encrypt. Além de serem gratuitos, seus certificados podem ser renovados automaticamente.

Por padrão, a validação e emissão dos certificados pelo Let's Encrypt utilizam o HTTP-01 Challenge, que exige a exposição da porta 80 para que a autoridade certificadora valide a posse do domínio. No entanto, por razões de segurança, nem sempre é viável expor essa porta.

Para contornar essa limitação, podemos utilizar a validação via DNS-01, que elimina a necessidade de portas abertas.

## Pré-requisitos
Antes de iniciar o processo de emissão do certificado, certifique-se de que possui:

✅ Um domínio registrado e gerenciado em um provedor compatível (exemplo: Cloudflare).
✅ Acesso administrativo ao pfSense, com o pacote ACME instalado.
✅ Credenciais de API do provedor de DNS para automação da validação DNS-01.


## O que é DNS-01 e como funciona?
O DNS-01 Challenge é um método de validação usado pelo Let's Encrypt e outras Autoridades Certificadoras (CAs) para comprovar a posse de um domínio antes de emitir um certificado SSL.

## Fluxo da validação DNS-01:
O Let's Encrypt solicita a criação de um registro TXT no DNS do domínio, contendo um código de desafio único.
A CA consulta o DNS para verificar se o registro TXT foi criado corretamente.
Se a validação for bem-sucedida, o certificado é emitido.

Vantagens do DNS-01:
✅ Dispensa a abertura de portas (80 ou 443)
✅ Permite emitir certificados wildcard (exemplo: *.hirostack.com)
✅ Automatização possível com provedores de DNS compatíveis (Cloudflare, AWS Route 53, GoDaddy, etc.)

Essa abordagem será documentada nos próximos passos, detalhando a configuração do ACME (Let's Encrypt) no pfSense, integração com Cloudflare.
