---
title: Armazenamento de sessão de Cookie
status: live
---

Você pode também usar o middleware `\Slim\Middleware\SessionCookie` para persistir dados de sessão em cookies HTTP
criptografados e hashed. Para habilitar o middleware de cookie de sessão, adicione o middleware `\Slim\Middleware\SessionCookie`
para sua aplicação Slim:

    <?php
    $app = new Slim();
    $app->add(new \Slim\Middleware\SessionCookie(array(
        'expires' => '20 minutes',
        'path' => '/',
        'domain' => null,
        'secure' => false,
        'httponly' => false,
        'name' => 'slim_session',
        'secret' => 'CHANGE_ME',
        'cipher' => MCRYPT_RIJNDAEL_256,
        'cipher_mode' => MCRYPT_MODE_CBC
    )));

O segundo parâmetro é opcional; é mostrado aqui assim você pode ver as configurações padrões do middleware. O middleware de
de cookie de sessão funcionará sem problemas com a superglobal `$_SESSION` assim você pode facilmente migrar para esse middleware
de armazenamento de sessão com zero de mudanças para o código da sua aplicação.

Se você usa o middleware de cookie de sessão, você NÃO precisa iniciar uma sessão nativa do PHP. A superglobal `$_SESSION`
estará ainda disponível e será persistido em um cookie HTTP através da camada do middleware ao invés do gerencimento de sessão
nativo do PHP.

Lembre-se, cookies HTTP são limitados para apenas 4 KB de dados. Se os dados da sua sessão execeder 
esse tamanho, você deve depender então de sessões nativas do PHP ou um armazenamento de sessão alternativo.

<div class="alert">
    <strong>AVISO:</strong> 
    Armazenamento de dados de sessão no lado do cliente não é recomendado se você está
    lhe dando com informações sigilosas, mesmo quando usando o middleware de cookie de sessão 
    criptografado do Slim. Se você precisa armazenar informações sigilosas, você deve criptografar 
    e armazenar a informação da sessão no seu servidor.
</div>
