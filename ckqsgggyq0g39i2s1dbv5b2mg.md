---
title: "🐍 Entornos virtuales en Python usando Pipenv"
datePublished: Sun May 12 2019 00:39:00 GMT+0000 (Coordinated Universal Time)
cuid: ckqsgggyq0g39i2s1dbv5b2mg
slug: entornos-virtuales-en-python-usando-pipenv

---

![🐍 Entornos virtuales en Python usando Pipenv](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600315359/rhbETuQqI.jpeg)

Cuando iniciamos en el desarrollo con Python muchas veces no nos damos cuenta del dolor de cabeza que es mantener varios proyectos con diferentes versiones de dependencias en nuestra entorno de desarrollo local, a medida que vamos evolucionando vamos adquiriendo nuevas herramientas que mejoren nuestro flujo de trabajo, como el uso de entornos virtuales o manejadores de paquetes, entre otras, Pipenv es una de estas herramientas que nos ayudan mucho a integrar y mejorar nuestros flujos en Python, tanto es así que su eslogan por así decirlo es _"Python Development Workflow for Humans"_.

Esta herramienta básicamente nos ayuda a optimizar nuestro flujo de desarrollo unificando _pip_ y _virtualenv_ en una sola herramienta que funciona por linea de comandos _(Terminal)_, lo que nos daria un entorno aislado en el cual instalar nuestras dependencia y luego replicar este mismo entorno en otra maquina gracias a el archivo que se genera **[Pipfile](https://github.com/pypa/pipfile)**, que viene a ser el sustituto del archivo que genera pip **requirements.txt**

Instalando Pipenv
-----------------

El proceso de instalación de Pipenv es muy sencillo, en esta ocasión voy a detallar 2 formas de instalar usando lo indicado en la [documentación oficial](https://pipenv-es.readthedocs.io/es/latest/).

Si estas usando Ubuntu 16.04:

    $ sudo apt install software-properties-common python-software-properties
    $ sudo add-apt-repository ppa:pypa/ppa
    $ sudo apt update
    $ sudo apt install pipenv
    

Esta otra opción es por si ya tienes instalado pip:

    $ pip install pipenv
    

Como acabamos de ver la instalación es muy sencilla, de igual manera si tienen algún problema con la instalación me pueden escribir.

Usando Pipenv
-------------

Para efectos de este ejemplo vamos a generar una aplicación sencilla usando `Flask` y haremos el típico _Hola Mundo_, ya que este post no se trata de desarrollo de apps usando `Flask`

Primero creamos nuestro entorno virtual para aislar nuestra aplicación:

    $ pipenv shell
    
    Creating a virtualenv for this project…
    Pipfile: /home/usuario/nombre_del_proyecto/Pipfile
    Using /usr/bin/python3 (3.6.7) to create virtualenv…
    

Con la ejecución de este comando se crea un entorno virtual si no existe, ademas de crear 2 archivos: `Pipfile` y `Pipfile.lock`.

Si se instala en un proyecto preexistente Pipenv convierte tu archivo _requirements.txt_ en _Pipfile_.

Para este proyecto se ha creado un entorno con una versión de python 3, si necesitas instalar una versión de python 2 solo debes agregar el argumento --two, también funciona para python 3 el argumento --three.

    $ pipenv shell --two    #Genera entorno en Python2
    $ pipenv shell --three  #Genera entorno en Python3
    

Ahora procedemos a instalar los paquetes que necesitamos, en nuestro caso Flask, pero supondremos que necesitamos una versión especifica para este ejemplo usaremos la versión 1.0, para el momento de escribir este post la versión latest de Flask es la 1.0.2

    $ pipenv install flask==1.0
    
    Installing flask==1.0…
    Adding flask to Pipfile's [packages]…
    ✔ Installation Succeeded 
    Pipfile.lock not found, creating…
    Locking [dev-packages] dependencies…
    Locking [packages] dependencies…
    ✔ Success! 
    Updated Pipfile.lock (db0e09)!
    Installing dependencies from Pipfile.lock (db0e09)…
      🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 6/6 —
    

Con esto ya tendremos Flask instalado en nuestro entorno virtual, y procedemos a realizar nuestro desarrollo.

Crean un archivo llamado `apps.py` con este contenido dentro:

    from flask import Flask
    app = Flask(__name__)
    
    @app.route("/")
    def hello():
        return "Hello World!"
    

Por ultimo iniciamos nuestro servidor Flask

    $ FLASK_APP=apps.py flask run
    
     * Serving Flask app "apps.py"
     * Environment: production
       WARNING: Do not use the development server in a production environment.
       Use a production WSGI server instead.
     * Debug mode: off
     * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
    

Con esto tendremos nuestro server Flask corriendo nuestro archivo `apps.py`.

Consideraciones finales
-----------------------

A lo largo de este post hemos visto como el flujo de trabajo se puede optimizar con el uso de esta herramienta, ya que no debemos generar los entornos virtuales por separado usando algo como `virtualenv` con el que como yo muchas personas no han estado conformes, también hemos visto como instalar paquetes usando pipenv tan fácil como si usáramos `pip`, queda de parte de cada quien darle una probada a esta herramienta y ver si le ayuda a optimizar su flujo de desarrollo y mantener un poco más homogéneo los ambientes de desarrollo.

Si deseas que siga publicando contenido sobre entornos virtuales, pip, o explique más a fondo los ficheros `Pipfile`o `Pipfile.lock`, que otros comandos puede ejecutar Pipenv, solo házmelo saber en un comentario o a través de mi cuenta twitter [@rafnixg](https://twitter.com/rafnixg)

**Referencias**  
[Documentación Pipenv](https://pipenv-es.readthedocs.io/es/latest/)