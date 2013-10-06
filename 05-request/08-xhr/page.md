---
title: XMLHttpRequest
status: live
---

Quando usando um framework Javascript tipo Mootools ou jQuery para executar um XMLHttpRequest, o XMLHttpRequest 
geralmente será enviado com o cabeçalho HTTP **X-Requested-With**. A aplicação Slim irá detectar o cabeçalho 
**X-Requested-With** e marcar a requisição como tal. Se por alguma requisição um XMLHttpRequest não pode ser enviado
com o cabeçalho **X-Requested-With**, you can force the Slim application to assume an HTTP request
is an XMLHttpRequest by setting a GET, POST, or PUT parameter in the HTTP request named “isajax” with a truthy value.

Use os métodos `isAjax()` ou `isXhr()` para dizer que a requisição é uma requisição XHR/Ajax:

    <?php
    $isXHR = $app->request()->isAjax();
    $isXHR = $app->request()->isXhr();
