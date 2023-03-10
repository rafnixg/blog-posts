---
title: "Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 2"
datePublished: Wed Jul 29 2020 19:24:33 GMT+0000 (Coordinated Universal Time)
cuid: ckqsgfx1r0g33i2s11q4u5isq
slug: actualiza-tu-perfil-de-github-con-readme-y-github-actions-parte-2

---

![Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 2](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600285897/uuuLVxUOv.jpeg)

La idea principal es poder generar un archivo README.md con una lista de los últimos 5 post de este Blog, pero en esencia este código con muy poco o hasta nula modificacion en algunos casos puede servir para otros servicios como [dev.to](https://dev.to/), [Medium](https://medium.com/) o WordPress.

Ya teniendo nuestro archivo README.md creado en el post [Actualiza tu perfil de GitHub con README y Github Actions - Parte 1](http://rafnixg.dev/actualiza-tu-perfil-de-github-con-readme-y-github-actions-part-1/) , nos ubicamos en la carpeta de nuestro proyecto y empezaremos creamos una copia de nuestro archivo pero con extensión **.template**, quedándonos algo como esto: README.md.template, este sera el archivo que usaremos como base para generar nuestro README.md

Luego editamos la sección de "Latest post (Spanish)" sustituyendo nuestros post estáticos con este código en Jinja2, que nos ayuda a iterar sobre una lista de post.

    ## Latest Posts (Spanish)
    
    {% for post in latest_post %}
    - [{{post.title}}]({{post.link}})
    {%  endfor %}
    
    

En esta plantilla indico que le voy a pasar _latest\_post_ y que debo recorrer sus post e imprimirlos dentro de un link en markdown.

Ahora necesitamos el endpoint a el que consultaremos para obtener nuestras lista de posts, para esto haré uso de las [RSS](https://es.wikipedia.org/wiki/RSS) que tiene Ghost y con el siguiente servicio lo convertiré de XML a JSON

[

Rss to json online converter - rss2json.com

Free online API to convert RSS to JSON

![Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 2](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600287911/1jPcF_yql.x-icon)rss2json

![Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 2](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600290068/iOhUyOTphF.png)

](https://rss2json.com)

Acá pudimos haberlo hecho de muchas maneras distintas, se pudo haber usado la API ded Ghost y hacer la petición directa o se pudo haber hecho el cambio de XML a JSON usando Python, mi idea era hacerlo lo mas simple posible, si tienes una idea mejor la espero en los comentarios o un Pull Request, ya con esto aclarado podemos continuar xD.

Teniendo nuestro endpoint listo procederemos a crear nuestro script en Python, por lo que primero debemos preparar, es nuestro entorno virtual que nos ayude a aislar nuestras dependencias para este proyecto, podemos hacer uso de Pipenv del cual tengo un tutorial por acá ([Entornos virtuales en python usando Pipenv](http://rafnixg.dev/entornos-virtuales-en-python-usando-pipenv/)), pero en este caso lo haremos de la siguiente manera ya que es la mas comun.

    $ python3 -m venv env
    $ source env/bin/activate
    $ touch app.py
    

Lo que creara una carpeta _env_ en el _root_ de nuestro proyecto, activara nuestro entorno virtual y crea nuestro archivo **app.py**

Para poder usar nuestras librerías debemos instalarlas, en este caso haré uso de PIP que es nuestro gestor de paquetes en python y las librería a instalar son:

*   **urllib3**: Para realizar las consultas HTTP
*   **json**: para parsear la información recibida en la respuesta HTTP
*   **jinja2**: para renderizar nuestro archivo README con la potencia de esta librería de plantillas

    $ pip install urllib3 json jinja2
    $ pip freeze > requirements.txt
    

Ya tenemos nuestras dependencias instaladas nuestras dependencias, así que procederemos a crear nuestro script, quedándonos algo como esto:

    import json
    import urllib3
    from jinja2 import Environment, FileSystemLoader
    
    # Cantidad maxima de posts a mostrar
    MAX_POSTS = 5
    
    # Setup
    env = Environment(loader=FileSystemLoader('.'))
    http = urllib3.PoolManager()
    
    def get_latest_posts(max_posts=5):
        r = http.request('GET', 'https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Frafnixg.dev%2Frss%2F')
        data = json.loads(r.data.decode('utf-8'))['items']
        return data[0:max_posts]
    
    def render_readme(data):
        template = env.get_template('README.template')
        render = template.render(**data)
        with open("README.md", "w") as f:
            f.write(render)
    
    def main():
    
        latest_posts = get_latest_posts(MAX_POSTS)
        data = {
            'latest_post': latest_posts
        }
        render_readme(data)
    
    
    if __name__ == "__main__":
        main()
    

Las primeras 3 lineas de nuestro código son básicamente la importación de las librerías y utilidades que vamos a usar, luego definimos una constante para el numero máximo de post que vamos a escribir en nuestro archivo README.

El setup es donde indicamos a jinja en que fichero debe buscar los templates y creamos una instancia que llamaremos http para nuestras consultas HTTP

Como ven en la función _get\_latest\_posts()_ es un simple petición GET a el enpoint, como parámetro le podemos limitar el numero de items que retornara

En la función _render\_readme()_ indicamos el archivo a usar como template, cargamos la data obtenida de los últimos post y lo renderizamos en nuestro template para luego escribirlo en el archivo final README.md

Con esto ya podemos correr nuestro script y ver como nos genera de forma dinámica nuestro archivo README.md

    $ ptyhon3 app.py
    

Nuestro script ya genere de forma dinámica nuestro archivo README.md, con este mismo enfoque se pueden agregar muchísimas mas funciones consultando a diferentes servicios y editar desde el template como se va a renderizar esta información.

En la tercera y ultima parte veremos como automatizar la ejecución de nuestro script y actualizar README.md en nuestro repositorio de GitHub, gracias a las GitHub Actions.

Gracias por leerme, los espero por twitter [@rafnixg](https://twitter.com/rafnixg) y por mi GitHub [rafnixg](https://github.com/rafnixg/rafnixg)

Siguiente publicación de esta serie: [Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 3](http://rafnixg.dev/actualiza-tu-perfil-de-github-con-readme-y-github-actions-part-3/)