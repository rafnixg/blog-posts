---
title: "Crea tu blog con python usando GitHub Pages y Pelican"
datePublished: Sat May 18 2019 19:06:00 GMT+0000 (Coordinated Universal Time)
cuid: ckqsggcm30fkxjcs19b51d10m
slug: crea-tu-blog-con-python-usando-github-pages-y-pelican

---

![Crea tu blog con python usando GitHub Pages y Pelican](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600307224/KegES0MXo.jpeg)

Cuando comencé a darle vuelta a la idea de empezar un blog de nuevo me vinieron muchas ideas de como hacerlo a la mente, como el de usar el famoso [Wordpress](https://wordpress.org), teniendo en cuenta que el blog lo quería hacer para hablar un poco de python y las tecnologías que iba a ir conociendo y aprendiendo decidí mejor usar Pelican ya que esta desarrollado en Python.

¿Qué es Pelican?
----------------

[Pelican](https://blog.getpelican.com/) es un generador de sitios estáticos desarrollado en python que nos permite escribir los post en archivos escritos en reStructuredText, Markdown, o AsciiDoc, y estos serán luego procesados para generar un sitio web estático como este blog, por lo que no necesitaremos una base de datos ni un servidor web que soporte un lenguaje de Backend como lo es GitHub Pages.

¿Qué es GitHub Pages?
---------------------

[GitHub Pages](https://pages.github.com/) es un hosting de sitios estáticos y como su pagina web lo indica, esta diseñado para hostear directamente en un repositorio de GitHub la pagina web de nuestros proyecto, paginas personales o de organizaciones, ademas de ser un servicio gratuito.

Gracias a estas características, podemos fácilmente crear nuestros sitios estáticos y subirlos a un repositorio de GitHub que debe tener la siguiente estructura `username.github.io` mas adelante indicare como crear y configurar el repositorio para que pueda servir nuestro sitio web.

GitHub recomienda el uso de [Jekyll](https://jekyllrb.com/) para generar nuestros sitios estáticos, pero este esta hecho en Ruby, lo que no es un problema si usas Ruby pero yo al ser un #PythonLover decidí usar Pelican que esta desarrollado en Python.

Creando nuestro repositorio en GitHub
-------------------------------------

Esta parte es la mas sencilla de post, ya que solo debemos entrar a nuestra cuenta de GitHub y crear un nuevo repositorio publico, que tenga el siguiente nombre.

`tu_username.github.io`, en mi caso el repositorio donde se aloja este blog se llama [rafnixg.github.io](https://rafnixg.github.io)

Solo con esto ya tendremos nuestro Github Pages listo para comenzar a subir nuestro contenido estático.

Instalando y configurando Pelican
---------------------------------

Instalar y tener Pelican funcionando es super sencillo. Pero si les quiero recomendar que toda la instalación se haga en un entorno virtual usando Pipenv, para mantener separado esta instalación de los demás paquetes de Python que tengan instalados en sus sistema, si no saben como usar Pipenv acá les dejo un post que tengo sobre este tema, Entornos virtuales en Python usando Pipenv.

Antes de iniciar con la instalación de pelican, debemos clonar nuestro repositorio donde esta hosteada nuestro blog, para esto solo debemos ubicarnos sonde queramos tener nuestro proyecto, en este caso yo lo haré en la raíz de mi sistema.

    $ cd ~
    $ git clone https://github.com/tu_username/tu_username.github.io.git
    $ cd tu_username.github.io
    

Luego de esto, procedemos a instalar nuestro Pelican, lo primero que debemos hacer es crear un nuevo branch llamado `source` donde ira todo nuestro código fuente y librerías, ya que para GitHub todo lo que este en la rama `master` es lo que sera servido, para nuestro interés solo debemos subir a `master` lo que pelican genera en su carpeta output, pero mas adelante nos preocuparemos de esto.

    $ git checkout -b source
    $ pipenv shell
    

Con esto ya tendremos nuestro entorno virtual para nuestra instalación de pelican, ahora procedemos a instalar `pelican` que es nuestro generador de sitios estáticos, `markdown` que nos ayudara para escribir nuestros post usando este lenguaje y `ghp-import` que nos ayuda a publicar nuestro sitio a GitHub.

    $ pipenv install pelican markdown ghp-import
    
    Installing pelican…
    Adding pelican to Pipfile's [packages]…
    ✔ Installation Succeeded 
    Installing markdown…
    Adding markdown to Pipfile's [packages]…
    ✔ Installation Succeeded 
    Installing ghp-import…
    Adding ghp-import to Pipfile's [packages]…
    ✔ Installation Succeeded 
    Pipfile.lock not found, creating…
    Locking [dev-packages] dependencies…
    Locking [packages] dependencies…
    ✔ Success! 
    Updated Pipfile.lock (b0c318)!
    Installing dependencies from Pipfile.lock (b0c318)…
      🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 13/13 — 
    

Ya con esto tenemos todo listo para empezar a usar Pelican así que creemos nuestro primer blog usándolo.

    $ pelican-quickstart
    
    Welcome to pelican-quickstart v4.0.1.
    
    This script will help you create a new Pelican-based website.
    
    Please answer the following questions so this script can generate the files
    needed by Pelican.
        
    Using project associated with current virtual environment.Will save to:
    /home/username/blog/pelican
    
    > What will be the title of this web site? prueba pelican
    > Who will be the author of this web site? rafnix guzman
    > What will be the default language of this web site? [es] es
    > Do you want to specify a URL prefix? e.g., https://example.com   (Y/n) n
    > Do you want to enable article pagination? (Y/n) y
    > How many articles per page do you want? [10] 
    > What is your time zone? [Europe/Paris] America/Lima
    > Do you want to generate a tasks.py/Makefile to automate generation and publishing? (Y/n) Y **# Responder Y, esto nos ayuda mucho!**
    > Do you want to upload your website using FTP? (y/N) n
    > Do you want to upload your website using SSH? (y/N) n
    > Do you want to upload your website using Dropbox? (y/N) n
    > Do you want to upload your website using S3? (y/N) n
    > Do you want to upload your website using Rackspace Cloud Files? (y/N) n
    > Do you want to upload your website using GitHub Pages? (y/N) y
    > Is this your personal page (username.github.io)? (y/N) y
    Done. Your new project is available at /home/username/blog/pelican
    

Si tienen alguna duda respecto a la zona horaria acá les dejo una lista con todas las [zonas horarias](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)

    > Do you want to generate a tasks.py/Makefile to automate generation and publishing? (Y/n)
    

A esta pregunta deben responder (Y), ya que este Makefile nos ayudara a generar nuestro sitio de forma mas fácil, como podemos ver ya con esto se nos ha generado nuestro proyecto de pelican con el que podemos empezar a trabajar.

Escribiendo nuestro primer post
-------------------------------

Vamos a crear nuestro primer post, para esto nos debemos ubicar en la carpeta `content` y con nuestro editor de texto favorito procedemos a crear un archivo llamado hola-mundo.md (si, lo se, la imaginación esta a la orden del día), este archivo luego puede ser borrado es solo para pruebas.

    Title: Hola Mundo
    Date: 2019-05-18 10:30
    Modified: 2019-05-18 11:30
    Category: blog
    Tags: principal, otros
    Slug: hola-mundo
    Authors: Rafnix Guzmán
    Summary: Mi primer post usando Pelican y GitHub Pages
    
    Aca pueden empezar a escribir todo lo que quieran pueden agregar todas las sintaxis de *Markdown* que deseen.
    
    ## Título
    ### Subtítulo
    Este es un ejemplo de texto que da entrada a una lista genérica de elementos:
    
    - Elemento 1
    - Elemento 2
    - Elemento 3
    
    Este es un ejemplo de texto que da entrada a una lista numerada:
    
    1. Elemento 1
    2. Elemento 2
    3. Elemento 3
    
    Al texto en Markdown puedes añadirle formato como **negrita** o *cursiva* de una manera muy sencilla.
    
    Todo esto fue extraído de este [Post sobre markdown](https://markdown.es/sintaxis-markdown/)
    

Probando nuestro blog en local
------------------------------

Luego de escribir y guardar su primer post, procedemos a generar un servidor de pruebas para ver nuestro resultado antes de subir nuestra web a GitHub, estando en la raíz de nuestro proyecto ejecutamos el siguiente comando.

    $ make devserver
    
    pelican -lr /home/username/blog/pelican/content -o /home/username/blog/pelican/output -s /home/username/blog/pelican/pelicanconf.py 
    
    -> Modified: content, theme, settings. re-generating...
    Done: Processed 1 article, 0 drafts, 0 pages, 0 hidden pages and 0 draft pages in 0.15 seconds.
    

Para entrar a nuestro servidor local de pruebas debemos ingresar a la siguiente URL [http://localhost:8000](http://localhost:8000) con nuestro explorador favorito(espero no se IE, xD)

![Crea tu blog con python usando GitHub Pages y Pelican](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600309775/aOk6bSn3b.jpeg)

Hola mundo pelican

Subir nuestro blog a GitHub Pages
---------------------------------

Ya con esto procederemos a preparar todo para subir lo a github, este primer comando sube nuestro código fuente.

    $ git add -A && git commit -a -m 'post hola-mundo.md' && git push --all
    

Ahora subimos todo a la rama `master`, recuerdan que les dije que no se preocuparan por esto, es debido a que este comando hace toda esta preparación de subir todo lo que se encuentra en la carpeta `output` a nuestra rama `master`

    $ make github
    

Acá se les preguntaran sus credenciales de github, para poder subir a su repositorio todo el sitio estático ya generado, con esto su blog estará funcionando en https://su\_username.github.io/

Para el próximo post veremos como configurar un `Thema` y algunos `Plugins` para potenciar el funcionamiento de Pelican, ademas de unas configuraciones extra que nos ayudaran a tener mejor SEO.

Nos vemos en el proximo post, muchas gracias por leerme y cualquier duda, comentario, o lo que sea, lo pueden dejar por aca o por mi cuenta de Twitter [@rafnixg](https://twitter.com/rafnixg).