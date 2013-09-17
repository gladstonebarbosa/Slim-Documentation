---
title: Armazenamento Nativo de Sessão
status: live
---

Uma aplicação Slim não presume qualquer coisa sobre sessões. Se você prefere usar uma sessão PHP, você deve configurar
e iniciar uma sessão PHP nativa com `session_start()` antes de você instanciar a aplicação Slim.

Você deve também desabilitar o limitador de cache da sessão do PHP para que o PHP não envie cabeçalhos conflitantes de 
expiração de cache com a resposta HTTP. Você pode desabilitar o limitador de cache da sessão do PHP com:

    <?php
    session_cache_limiter(false);
    session_start();
