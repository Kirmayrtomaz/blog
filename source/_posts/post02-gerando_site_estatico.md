title: Criando sites performáticos com HEXO (Parte 2 - 2)
tags:
  - javascript
  - node
categories:
  - ferramentas
author: Kirmayr
date: 2016-08-31 00:38:00
---
Nesse post mostrarei o template que estou utilizando no meu blog e os plugins adicionais que estou utilizando.


A primeira coisa que fiz depois de baixar o hexo foi buscar um template legal, ele tem uma lista bem nesse [link](https://hexo.io/themes/).

O tema que escolhi foi o [Again](https://github.com/DrakeLeung/hexo-theme-again).

Para coloca-lo no meu template vc pode simplismente baixa-lo e inserir na pasta `themes/`

``` bash
git clone https://github.com/DrakeLeung/hexo-theme-again.git again
```

Depois disso, precisei baixar uma nova dependência pois o template precisa utiliza o pre-processador   Sass


``` bash
npm install --save hexo-renderer-sass

```

E por último vc precisa alterar o arquivo de configuração `_config.yml` do tema e trocar-lo para again que é o nome do template


## Estrutura do template

A estrutura do template é composto das seguintes pastas

``` plain
.
├── _config.yml
├── layout
├── source
````

* **_config.yml ** -  Estarão as configurações do template
* **layout  ** - Está todo o template no formato EJS template
* **source  **  - Está os assets, (js, css e imagens)

### Configurando tema no _config.yml

A configuração básica do tema é identica ao `_config.yml` da raiz.

``` yml
title: Kirmayr Tomaz
description : Blog sobre assuntos de desenvolvimento web voltando para o frontend e vida saudável.
subtitle: Desenvolvedor web pseudo corredor
language: pt_br
timezone: America/Manaus
```

Nele vc já tem suporte pra inserir imagens e inserir também o [disqus](https://disqus.com/)

``` yml
avatar: /images/avatar_2.JPG
banner_small: /images/title.png
banner_large: /images/title.png

```

```yml
# disqus
disqus_shortname: kirmayr-blog

# social
social:
  github: https://github.com/kirmayrtomaz
 # twitter: https://twitter.com/DrakeLeung

```


No nav, será inserido o menu de navegação. Cada link será um item do menu

nav:
  home: .
  archive: archives
  about: about
  rss: sitemap.xml

```




## Plugins adicionais

Abaixo segue um lista dos plugins que achei essencial de utilizar no blog

#### [hexo-admin](https://github.com/jaredly/hexo-admin)

Para vc que sente saudade dá interface web do wordpress, joomla ou qualquer outro CMS. Esse plugin pode ajudar um pouquinho criando uma interface web para visualizar e editar seus posts. 

Abaixo temos um exemplo da interface web dele:

![teste](/blog/images/02/hexoadmin.png)

Vc consegue também editar o post pelo próprio Hexo-admin

![teste](/blog/images/02/hexoadmin_02.png)

Com esse plugin vc tem as seguintes funcionalidades 


* Edição de texto Markdown lado-a-lado
* Os posts são salvos automaticamente 
* Copiar a imagem e colar. (Issa coisa do capeta funciona sabe deus como)
* Publicar/despublicar imagem
* Adicionar categorias, tags, nome do Autor e horário da publicação(exemplo abaixo)


![pasted image](/blog/images/pasted-2.png)


Segundo o criando desse plugin [Jared Forsyth](https://github.com/jaredly)


para instar basta digitar na linha de comando

``` bash
$ npm install --save hexo-admin

```

Daí basta digitar 

``` bash
$ npm install server -d

```
Adicione também algumas propriedades para acesso dos usuários no arquivo de configuração `_config.yml`

``` yml
admin:
    name: admin ##nome do usuário
    password: admin ##senha
    secret: hey hexo ##segredo
    expire: 60*1 ##segredo

```

Após isso basta acessar seu ambiente de desenvolvimento /admin/


``` bash
$ http://localhost:4000/admin

```


#### [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)

Um dos plugins mais legais que encontrei foi o deploy direto no git, configurei super rápido sua estrutura para funcionar no `gh-pages` no `github`

Quem não sabe o que é gh-pages acesso o posto do [Segredos do Github do da2k](http://blog.da2k.com.br/2015/02/05/segredos-do-github-hospedando-seu-site-no-github/)



``` bash
$ npm install hexo-deployer-git --save

```



``` yml
deploy:
  type: git #o hexo tem suporte para outros deploys, no caso  desde será o git
  repo: https://github.com/Kirmayrtomaz/blog.git #url do repositório
  branch: ["gh-pages"] #branch que deseja enviar
```

Após realizar essas configurações, basta utilizar sempre esses dois comandos para fazer deploy. Primeiro precisamos gerar os arquivos estáticos e depois a função deploy pega os arquivos da pasta que foi gerando e envia direto para o git no branch gh-pages

> Plugin maravilhoso demais 


``` bash
$ hexo generate
$ hexo deploy

```

#### hexo-filter-cleanup

Esse com certeza é um dos principais plugins que não deve faltar no seu projeto. É ultra mega power mother fucker tera tander foda.
Ele vem com um conjuntos de plugins para otimização do seu site

1. **hexo-html-minifier** todas suas páginas html serão minificadas
1. **hexo-clean-css** minifica seu css baseado no [clean-css](https://github.com/jakubpawlowicz/clean-css)
1. **hexo-uglify** minifica seu js 
1. **hexo-imagemin** compacta suas imagens mantendo a qualidade real
1. **useref** transforma blocos de js em um só o mesmo para css
1. **favicons** gerador automático de favicons



``` bash
$ npm install hexo-generator-sitemap --save

```

ele executa automáticamente após a instalação, caso queira algo mais avançado basta [acessar seu projeto](https://github.com/mamboer/hexo-filter-cleanup)

#### hexo-generator-sitemap

Gerador de site map

``` bash
$ npm install hexo-generator-sitemap --save

```


#### hexo-generator-json-content

Gera um json do seu conteúdo. No meu caso ele gerou o `content.json`. De forma que vc pode acessar por outras aplicações via ajax.

``` json

{
    "meta": {
        "title": "Kirmayr",
        "subtitle": "Blog de tecnologia e saúde",
        "description": "Blog sobre assuntos ...",
        "author": "Kirmayr Tomaz",
        "url": "http://kirmayrtomaz.github.io"
    },
    "pages": [..],
    "posts": [{
        "title": "Criando sites perfo...",
        "slug": "post02-gerando_site_estatico",
        "date": "2016-08-31T04:38:00.000Z",
        "updated": "2016-09-01T16:49:49.249Z",
        "comments": true,
        "path": "2016/08/31/post02-gerando_site_estatico/",
        "link": "",
        "permalink": "...",
        "excerpt": "",
        "text": "Nesse post mostrarei ...",
        "categories": [{
            "name": "ferramentas",
            "slug": "ferramentas",
            "permalink": "..."
        }],
        "tags": [{
            "name": "javascript",
            "slug": "javascript",
            "permalink": "http://kirmayrtomaz.github.io/tags/javascript/"
        }],
        "keywords": [{..}]
    }
```





``` bash
$ npm install hexo-generator-sitemap --save

```

# Conclusão
O artigo foi curtinho, mas a ideia é mostrar que o **hexo** é uma ferramente muito poderosa e as facilidades de criar um blog ou site são muitas. Tanto que em poucos minutos vc consegue fazer seu site rodar rapidamente

