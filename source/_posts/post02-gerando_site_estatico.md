title: Criando sites performáticos com HEXO (Parte 2 - 2)[construção]
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

Depois disso precisa baixar uma nova dependência pois o template precisa do preprocessador Sass

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



``` yml
# nav #
nav:
  home: .
  archive: archives
  about: about
  rss: sitemap.xml

```
