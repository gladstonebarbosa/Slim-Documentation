---
title: Rescrevendo URL da Rota
status: live
---

Eu encorajo fortemente você a usar um servidor web que suporte reescrita de URL; isso fará você desfrutar de URLs
limpas e amigáveis com sua aplicação Slim. Para habilitar reescrita de URL, você deve usar as ferramentas apropriadas
providas pelo seu servidor web para encaminhar todas as requisições HTTP para o arquivo PHP em que você instancia e executa
a sua aplicação Slim.
A seguinte demonstração, minima necessária, configurações para o Apache com mod_php e nginx. Esses não são feitos
para ser configurações prontas para produção mas deve ser o suficiente para deixar as coisas funcionando.
Para ler mais sobre ser deployment em geral você pode continuar lendo em <http://www.phptherightway.com>.

### Apache e mod_rewrite

Aqui está um exemplo de estrutura de diretório:

    /path/www.mysite.com/
        public_html/ <-- Documento raiz!
            .htaccess
            index.php <-- Eu instancio o Slim aqui!
        lib/
            Slim/ <-- Eu armazeno as bibliotecas do Slim aqui!

O arquivo **.htaccess** na estrutura de diretório acima contém:

    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [QSA,L]

Você pode também precisar de uma diretriz de diretório para habilitar arquivos **.htaccess** e permitir que a diretriz
**RewriteEngine** seja usada.
Isto é as vezes feito globalmente no arquivo **httpd.conf**, mas é geralmente uma boa idéia limitar a diretriz para
apenas seu host virtual, cercando isso em seu bloco de configuração **VirualHost**. Isto é geralmente configurado em
sua configuração na forma de:

    <VirtualHost *:80>
        ServerAdmin me@mysite.com
        DocumentRoot "/path/www.mysite.com/public_html"
        ServerName mysite.com
        ServerAlias www.mysite.com

        #ErrorLog "logs/mysite.com-error.log"
        #CustomLog "logs/mysite.com-access.log" combined

        <Directory "/path/www.mysite.com/public_html">
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
    </VirtualHost>

Como resultado, o Apache enviará todas as requisições de arquivos não existentes para meu script **index.php** no qual
eu instancio e executo minha aplicação Slim. Com a reescrita de URL habilitada e presumindo que a seguinte aplicação
Slim está definida no **index.php**, você pode acessar a rota da aplicação abaixo em "/foo" ao invés de "index.php/foo".

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        echo "Foo!";
    });
    $app->run();

### nginx

Usaremos o mesmo exemplo de estrutura de diretório como antes, mas com nginx nossa configuração irá em **nginx.conf**.

    /path/www.mysite.com/
        public_html/ <-- Documento raiz!
            index.php <-- Eu instancio o Slim aqui!
        lib/
            Slim/ <-- Armazeno os arquivos da biblioteca do Slim aqui!

Aqui está um snippet de um **nginx.conf** em que usamos a diretriz **try_files** para servir o arquivo se ele existir,
bom para arquivos estaticos (imagens, css, js etc), e caso contrário, encaminha a requisição para o arquivo **index.php**.

    server {
        listen       80;
        server_name  www.mysite.com mysite.com;
        root         /path/www.mysite.com/public_html;

        try_files $uri /index.php;

        # this will only pass index.php to the fastcgi process which is generally safer but
        # assumes the whole site is run via Slim.
        location /index.php {
            fastcgi_connect_timeout 3s;     # default of 60s is just too long
            fastcgi_read_timeout 10s;       # default of 60s is just too long
            include fastcgi_params;
            fastcgi_pass 127.0.0.1:9000;    # assumes you are running php-fpm locally on port 9000
        }
    }

A maioria das instalações teram uma configuração de arquivo padrão **fastcgi_params** que você pode incluir como mostrado acima.
Algumas configurações não incluem o parâmetro **SCRIPT_FILENAME**. Você deve se certificar que você incluiu este parâmetro
caso contrário você poderá terminar com um erro de arquivo não especificado do rápido processo cgi.
Isso pode ser feito diretamente no bloco de localização ou simplesmente adicionado para o arquivo **fastcgi_params**.
De qualquer forma, se parece com isso:

    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;

### Sem reescrita de URL

Slim funcionará sem reescrita de URL. neste cenário, você deve incluir o nome do arquivo PHP em que você
instancia e executa a aplicação Slim na sua URI. Por exemplo, pressumir que a seguinte aplicação Slim é definida
em **index.php** na raiz do seu projeto:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        echo "Foo!";
    });
    $app->run();

Você pode acessar a rota definida em "/index.php/foo". Mas se ao invés, a mesma aplicação é definida em **index.php**
dentro do subdiretório físico blog/, você pode acessar a rota definida em /blog/index.php/foo.
