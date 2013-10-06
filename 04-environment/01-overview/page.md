---
title: Environment Overview
status: live
---

O Slim Framework implementa uma derivação do [protocolo Rack](http://rack.rubyforge.org/doc/files/SPEC.html). Quando
você instancia uma aplicação Slim, ela imediatamente inspeciona a superglobal `$_SERVER` e deriva um conjunto de
variáveis de ambiente what prescreve o comportamento da aplicação.

### O que é o Ambiente?

Um "ambiente" de uma aplicação Slim é um array associativo de configurações que são validados uma vez e feitos acessiveis
para a aplicação Slim e sua middleware. Você é livre para modificar as variáveis de ambiente durante o tempo de execução;
mudanças irão propagar imediatamente em torno da aplicação.

Quando você instancia uma aplicação Alim, as variáveis de ambiente são derivadas da superglobal `$_SERVER`; você
não precisa setá-las por si mesmo; No entanto, vocÊ é livre para modificar ou suplementar essas variáveis no middleware do
Slim.

Essas variáveis são fundamentais para determinar como sua aplicação Slim executa: Os recursos URI, o método HTTP,
o corpo da requisição HTTP, os parâmmetros das URL querys, saídas de erro, entre outros. Middleware, descrito depois,
dá a você o poder para - entre outras coisas - manipular variáveis de ambiente antes e/ou depois da aplicação Slim
está rodando.

### Variáveis de Ambiente

O texto a seguir respeitosamente pede emprestado a mesma informação inicialmente disponível em:
<http://rack.rubyforge.org/doc/files/SPEC.html>. O array de ambiente deve incluir estas variáveis:

REQUEST_METHOD
: O método de requisição HTTP. Este é obrigatório e pode nunca ser uma string vazia.

SCRIPT_NAME
: A parte inicial do "path" da URI que corresponde ao diretório físico no qual a aplicação Slim está instalada
- assim a aplicação conhece sua "localização" virtual. Isso pode ser uma string vazia se a aplicação está instalada 
no nível mais alto do diretório raiz do documento público. Isso nunca terá uma barra final.

PATH_INFO
: A parte restante do "path" da URI que determina a localização "virtual" do recurso alvo da requisição HTTP dentro do contexto da aplicação Slim.
Isso sempre terá uma barra principal; Pode ou não pode ter uma barra final.

QUERY_STRING
: A parte da URI após, mas não incluindo o "?". Isso é obrigatório mas pode ser uma string vazia.

SERVER_NAME
: Quando combinado com `SCRIPT_NAME` e `PATH_INFO`, isso pode ser usado para criar uma URL totalmente qualificada para um recurso de aplicação.
No entanto, se `HTTP_HOST` está presente, deverá ser usado. Isso é obrigatório e pode nunca ser uma string vazia.

SERVER_PORT
: Quando combinado com `SCRIPT_NAME` e `PATH_INFO`, isso pode ser usado para criar uma URL totalmente qualificada para qualquer recurso da aplicação.
Isso é obrigatório e pode nunca ser uma string vazia.

HTTP_*
: Variáveis combinando os cabeçalhos de requisições HTTP enviadas para o cliente. A existencia dessas variáveis correspondem com aquelas enviadas para a requisição HTTP atual.

slim.url_scheme
: Será “http” ou “https” dependendo da URL de requisição HTTP.

slim.input
: Será uma string representando o corpo da requisição HTTP. Se o corpo da requisição HTTP é vazio (ex: com a requisição GET), isso será uma string vazia.

slim.errors
: Deve sempre ser um recurso com permisão de escrita; por padrão, isso é um manipulador de recurso apenas de escrita para `php://stderr`.

A aplicação Slim pode armazenar seus próprios dados no ambiente também. As chaves dos arrays de ambiente devem conter
pelo menos um ponto, e deve ser prefixado unicamente (ex: "prefix.foo"). O prefixo **slim.** é reservado para uso do próprio Slim
e não deve ser usado. O ambiente não deve conter as chaves `HTTP_CONTENT_TYPE` ou `HTTP_CONTENT_LENGTH` (use as versões sem HTTP_).
As chaves CGI, (nomeado sem um ponto) devem ser valores do tipo String. Existem as seguintes restrições:


* slim.url_scheme deve ser ou “http” ou “https”.
* `slim.input` deve ser uma string.
* Deve haver um recurso válido e com permisão de escrita em `slim.errors`.
* O `REQUEST_METHOD` deve ser um token válido.
* O `SCRIPT_NAME`, se não vazio, deve começar com "/"
* O `PATH_INFO`, se não vazio, deve começar com "/"
* O `CONTENT_LENGTH`, se passado, deve consistir apenas de dígitos
* `SCRIPT_NAME` ou `PATH_INFO` deve ser definido. `PATH_INFO` deve ser "/" se `SCRIPT_NAME` for vazio. `SCRIPT_NAME`
  nunca deve ser "/", mas em vez disso ser uma string vazia.
