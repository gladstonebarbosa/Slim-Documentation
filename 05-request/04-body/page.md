---
title: Corpo da requisição
status: live
---

Use o método `getBody()` do objeto de requisição para obter o corpo da requisição HTTP enviado pelo cliente HTTP.
Isso é particularmente útil para uma aplicação Slim que consume requisições JSON ou XML.

    <?php
    $request = $app->request();
    $body = $request->getBody();
