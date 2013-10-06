---
title: Método de Requisição
status: live
---

Toda requisição HTTP tem um método (ex: GET ou POST). Você pode obter o método de requisição HTTP atual através do objeto
de requisição:

    /**
     * Qual é o método de requisição?
     * @return string (e.g. GET, POST, PUT, DELETE)
     */
    $app->request()->getMethod();

    /**
     * É uma requisição GET?
     * @return bool
     */
    $app->request()->isGet();

    /**
     * É uma requisição POST?
     * @return bool
     */
    $app->request()->isPost();

    /**
     * É uma requisição PUT?
     * @return bool
     */
    $app->request()->isPut();

    /**
     * É uma requisição DELETE?
     * @return bool
     */
    $app->request()->isDelete();

    /**
     * É uma requisição HEAD?
     * @return bool
     */
    $app->request()->isHead();

    /**
     * É uma requisição OPTIONS?
     * @return bool
     */
    $app->request()->isOptions();

    /**
     * É uma requisição XHR/AJAX?
     * @return bool
     */
    $app->request()->isAjax();
