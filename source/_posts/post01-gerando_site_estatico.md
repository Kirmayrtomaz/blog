title: Criando sites performáticos com HEXO (Parte 1 - 2)
tags:
  - javascript
  - node
categories:
  - ferramentas
author: Kirmayr
date: 2016-08-29 00:38:00
---
A ideia desse artigo é mostrar as vantagens de sites estáticos  com a utilização HEXO (framework feito NODEJS). Esse artigo vai ser composto por duas partes, nessa primeira  mostrarei somente os conceitos básicos do HEXO e na segunda parte a instalção dos principais plugins e customização de um tema.



## **Por que utilizar sites estáticos?**

Imagine uma situação em que  toda vez que precisamos criar um site novo, pensamos logo em inserir um CMS monstro para que o cliente veja o que foi feito. Ou  quando o site passa muitos meses sem nenhuma mudança, sem contar do custo pra deixar um site desse rodando. Situações comuns que ocorrem no nosso dia a dia de desenvolvedor web. 

Vamos pensar de maneira diferente, por que vale a pena fazer um site estático falando das vantagens do CDN(Content delivery Network) como parte do nosso projeto.

*	**Custo** – Reduzem o custo da infraestrutura, soluções como CDN são mais baratas. 
o	Gastar 10 reais na [cdn77](https://www.cdn77.com) seria necessário 63 GB  já tendo suporte a http2. Imagine seu site abrindo nesa velocidade como nesse [link](https://www.alura.com.br/)
o	Dúvidas sobre preço basta acessar esse [link](http://www.cdncalc.com/) 
*	**Escalabilidade** – Esse serviço é altamente escalavel, e não precisamos  nos preocupar com a infra. De forma que ele responderia da mesma forma tanto para 1 quanto para 100000 usuários acessando ao mesmo tempo o conteúdo
*	**Confiabilidade** – Seus arquivos serão acessados 24/7 por semana. Na outra situação um ataque de DDoS poderia derrubar seu servidor
* **Integridade** - Garatia de  que os arquivos não são perdidos. O que já tem chance de acontecer com um servidor comum se fosse hackedo



## Principais geradores

Uma vez que  definido as vantagens para sites estáticos vamos analisar os principais  geradores do mercado.

No site [StaticGen](https://www.staticgen.com/) podemos encontar  a lista dos principais frameworks open-sources que tem no mercado 

De todos, peguei somente os principais para analisar, já que nesse site possuem muitos

 
 
   
*	### [Jekyll](https://jekyllrb.com/) 
	*	Stars -26630
	*	Forks – 5858
	*	Issues - 101
	*	Language – Ruby
	*	Templates - Liquid
    

*	### [GitBook](https://www.gitbook.com/)
  *		Stars -12834
  *		Forks – 1529
  *		Issues - 528
  *		Language – Javascript
  *		Templates – Jinja2
  
*	### [Hexo](https://hexo.io/)
	*	Stars -11685
	*	Forks – 1902
	*	Issues - 278
	*	Language – Javascript
	*	Templates – EJS, JADE
    

*	### [Hugo](http://gohugo.io/)
	*	Stars -11287
	*	Forks – 1830
	*	Issues - 312
	*	Language – Go
	*	Templates – Go templates


Os critérios para definir qual framewok foram os  números de estrelas no github, linguagem em javascript(Stack de desenvolvimento que trabalho) e customização

**Jekyll** e **Hugo**  foram logo descartados por serem de outras linguagens  e restou   ** Gitbook**  e ** Hexo**.
 Analizando o  ** Gitbook**   percebemos que este é mais voltado pra documentação e não possui tanto suporte para customização. Já o ** HEXO**  possui características parecidas com o ** Jekyll**  (principal gerador de sites estáticos) e possui um grande leque de customização, por isso foi o escolhido dentro todos.


## Hexo

### Instalação

Para que seja instalado o **hexo**, primeiramente é necessário ter o NODEJS instalado, caso não tenha,  basta acessar esse [link](https://nodejs.org/)

a versão que tenho instaldo na minha máquina é a ** 6.2.1 **


Após instalar o node, vamos instalar o HEXO globalmente com o seguinte comando abaixo:


``` bash
npm install –g hexo-cli 

```


De forma que será instalado o hexo-cli globalmente no sistema



### Configuração

 Vamos iniciar um novo projeto com esse comando abaixo

``` bash
Hexo init <nome do projeto>
```


Ele criará essa estrutura abaixo


``` plain
.
├── _config.yml 
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
````

Explicarei agora o que cada arquivo criado significa 


* **_config.yml** -  O hexo utilizará esse arquivo de configuração como base. Como por exemplo nome do site, endereço do tema, plugins e customizações 

* ** package.json ** - Nesse arquivo constam as dependência em node para executar o gerador, sem esses pacotes  algumas funções inseridas do _config.yml não serão executadas.


``` javascript

package.json
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": ""
  },
  "dependencies": {
    "hexo": "^3.0.0",
    "hexo-generator-archive": "^0.1.0",
    "hexo-generator-category": "^0.1.0",
    "hexo-generator-index": "^0.1.0",
    "hexo-generator-tag": "^0.1.0",
    "hexo-renderer-ejs": "^0.1.0",
    "hexo-renderer-stylus": "^0.2.0",
    "hexo-renderer-marked": "^0.2.4",
    "hexo-server": "^0.1.2"
  }
}
````

* Pacotes
	* ** hexo-generator-archive ** – gera automaticamente um diretório para acessar os posts por arquivo
	* **hexo-generator-category** – pacote para dar suporte para as categorias do site. Para que isso funcione é nessário os posts terem categorias e o template ter gerado uma parte somente para isso 
	* ** hexo-generator-index ** – gera a index do site 
    * ** hexo-generator-tag **  – suporte para gerar link para posts com tags
    * ** hexo-renderer-stylus** - Suporte para o preprocessador [stylus](http://stylus-lang.com/)
	* ** hexo-renderer-ejs ** – Suporte para  template  [ejs](http://www.embeddedjs.com/) (Effective JavaScript templating.)que transforma javascript em HTML
	* ** hexo-renderer-marked **  – Suporte para [markdown](https://daringfireball.net/projects/markdown/), os posts são escritos nesse formato de texto e convertidos em html


* **Scaffolds** – quando for necessário criar um post ou uma página nova, o esqueleto dele será copiado dessa pasta, como no exemplo abaixo 

* **source** – Local onde serão criados os posts e páginas do blog
	* **_drafts** – Post que foram criados mas ficam ocultos
	* **_post** – post que foram criados e devem ser postados 

* **themes** – local onde deve ser criado o template do sistema ou inserir template que achar melhor. Caso queira algum tema legal basta acessar 
por padrão é baixado o template hexo-theme-landscape
https://hexo.io/themes/ 


Uma vez que o esqueleto do blog foi gerado, 
Será necessário instalar as dependências do sistema.
Basta utilizar o comando abaixo para instalar as dependências 

``` bash
$ npm install 
```

### Comandos Básicos

para criar um novo post basta digitar

``` bash
$ hexo new [layout] <title>

```

uma vez  que o site foi instalado basta digitar

``` bash
$ hexo server 
```
para acessar no ambiente local do sistema o site

``` bash
$ hexo generate 
```




### Configurações básicas


#### Customizando _config.yml

Uma vez que já temos nosso site inicial configurado, a primeira coisa que começamos a fazer é customizar o arquivo `_config.yml`



#### site

Configurações gerais do site

tipo | descricao
--- | ---
`title`| Nome padrao que aparecerá no título do site
`subtitle`| Subtítulo 
`description`| descrição do que o site aparesentará
`author`| nome do autor
`language`| lingua padrão do site, por defaut fica em "en", recomendavel trocar para "pt". 
`timezone`| Timezone que deve ser utilziado ex:America/Manaus


#### url


tipo | descricao
--- | ---
`url`| Url do seu site, no meu caso é http://kirmayrtomaz.github.io/
`root`| raiz que deve ser acessado, no meu caso é /blog/
`permalink`| permalink dos posts, :year/:month/:day/:title/ , vc pode customizar da forma que achar necessário



#### Directory

tipo | descricao
--- | ---
source_dir| `source` -  Diretório onde estão os posts e páginas 
public_dir| `public` Diretório onde será gerado os arquivos estáticos
tag_dir| `tags` - Dentro da pasta `public_dir` será gerado a pasta `tag_dir`
archive_dir| `archives` - Dentro da pasta `public_dir` será gerado a pasta `archive_dir`
category_dir| `categories` - Dentro da pasta `public_dir` será gerado a pasta `category_dir`
code_dir| downloads/code


Outras funções básicas basta acessar a [documentação do HEXO](https://hexo.io/docs/configuration.html)



No próximo post, explicarei como funciona o template e os principais plugin do HEXO.