---
title: "Creando un entorno de desarrollo para Odoo 14.0 con VSCode en Ubuntu 22.04"
datePublished: Tue Mar 14 2023 13:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clf89het403bcxnnv71zqaebj
slug: creando-un-entorno-de-desarrollo-para-odoo-140-con-vscode-en-ubuntu-2204
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/f77Bh3inUpE/upload/bf647ff9837c4d4b1c50314394b07e63.jpeg
tags: python, odoo, vscode-cjevho8kk00bo1ss2lmqqjr51, spanish, odoo-developer

---

En este artículo aprenderás a configurar un entorno de desarrollo para Odoo 14.0 en Ubuntu 22.04. Si estás leyendo esto, probablemente ya sabes que Odoo es un ERP basado en Python, PostgreSQL y XML que permite a las empresas gestionar sus procesos empresariales de manera integrada.

Antes de empezar con la configuración del entorno de desarrollo, asegúrate de tener instalado los siguientes requisitos previos: Python 3, Git, PostgreSQL y VSCode. Si aún no los tienes, puedes seguir los siguientes enlaces para instalarlos:

* Python 3: [**https://www.python.org/downloads/**](https://www.python.org/downloads/)
    
* Git: [**https://git-scm.com/downloads**](https://git-scm.com/downloads)
    
* PostgreSQL: [**https://www.postgresql.org/download/**](https://www.postgresql.org/download/)
    
* VSCode: [**https://code.visualstudio.com/download**](https://code.visualstudio.com/download)
    

Una vez que tengas estos requisitos previos instalados, estás listo para empezar a configurar tu entorno de desarrollo de Odoo. En este post, te enseñare cómo crear una estructura de carpetas adecuada para trabajar con Odoo y cómo configurar VSCode para poder debuggear el código.

## Instalación de PostgreSQL

Para trabajar con Odoo, necesitarás tener instalado PostgreSQL. PostgreSQL es un sistema de gestión de bases de datos relacional de código abierto. Para instalar PostgreSQL en Ubuntu/Debian, puede seguir los siguientes pasos en la terminal:

```bash
sudo apt update
sudo apt upgrade
sudo apt install postgresql postgresql-client
sudo -u postgres createuser -s $USER
createdb odoo-dev-14.0
```

* `sudo apt update`: Este comando se utiliza para actualizar la lista de paquetes disponibles en los repositorios de Ubuntu/Debian. Es importante ejecutar este comando antes de instalar cualquier software nuevo en Ubuntu para asegurarse de que se están utilizando las versiones más recientes de los paquetes disponibles.
    
* `sudo apt upgrade`: Este comando se utiliza para actualizar los paquetes existentes en el sistema operativo. Al ejecutar este comando, se descargarán e instalarán las actualizaciones disponibles para todos los paquetes instalados en el sistema.
    
* `sudo apt install postgresql postgresql-client`: Estos comandos se utilizan para instalar PostgreSQL y su cliente en el sistema operativo. PostgreSQL es un sistema de gestión de bases de datos relacionales que se utiliza comúnmente como base de datos para Odoo.
    
* `sudo -u postgres createuser -s $USER`: Este comando se utiliza para crear un usuario en PostgreSQL con todos los privilegios necesarios para trabajar con Odoo. El comando se ejecuta como el usuario "postgres", que es el usuario por defecto de PostgreSQL. `$USER` es una variable de entorno que contiene el nombre de usuario actual.
    
* `createdb odoo-dev-14.0`: Este comando se utiliza para crear una nueva base de datos en PostgreSQL llamada "odoo-dev-14.0". Esta será la base de datos que se utilizará para desarrollar y probar Odoo en este entorno de desarrollo.
    

Es importante destacar que después de la instalación, es necesario realizar algunas configuraciones de seguridad adicionales para garantizar la protección de los datos de la empresa. Sin embargo, para fines de este tutorial y dado que nos encontramos en un ambiente de desarrollo, no profundizaremos en este aspecto

## Instalación de dependencias

Antes de empezar a trabajar con Odoo, necesitamos instalar algunas dependencias en nuestro sistema operativo. Para hacerlo, podemos seguir las instrucciones [oficiales](https://www.odoo.com/documentation/14.0/es/administration/install/install.html#id14) que recomiendan utilizar los siguientes comandos en la terminal:

```bash
sudo apt update
sudo apt upgrade
sudo apt install python3-dev python3-pip python3-venv libxml2-dev \
libxslt1-dev libldap2-dev libsasl2-dev libtiff5-dev \
libjpeg8-dev libopenjp2-7-dev zlib1g-dev libfreetype6-dev \
liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev libxcb1-dev libpq-dev
```

Estos comandos nos permitirán instalar todas las dependencias necesarias para trabajar con Odoo en nuestro sistema Ubuntu 22.04. Es importante asegurarse de que todas las dependencias se instalen correctamente antes de continuar con la configuración de nuestro entorno de desarrollo.

## Creación de la estructura de carpetas

Una vez instalado PostgreSQL y las dependencias necesarias, es hora de crear una estructura de carpetas para trabajar con Odoo. Para ello, ejecuta en la terminal el siguiente comando:

```bash
mkdir -p ~/Odoo/{src,workspaces,instances,instances/odoo-dev-14.0}
```

Esta una forma abreviada de crear varias carpetas a la vez utilizando llaves y una lista de nombres de carpeta separados por comas.

En este caso, el comando crea una estructura de carpetas dentro de la carpeta principal del usuario (representado por el símbolo "~" que se refiere al directorio de inicio del usuario) con los siguientes nombres de carpeta:

* src
    
* workspaces
    
* instances
    
* instances/odoo-dev-14.0
    

La opción "-p" indica que se crearán todas las carpetas necesarias en la ruta, incluso si algunas de ellas ya existen. De esta manera, se crea una estructura de carpetas adecuada para trabajar con Odoo y se asegura de que todas las carpetas necesarias estén disponibles en el directorio de inicio del usuario.

## Instalación de Odoo 14.0

Ahora que hemos instalado PostgreSQL, Python y las dependencias necesarias, podemos proceder a instalar Odoo.

### Descargar el código fuente de Odoo 14.0

Para descargar el código fuente de Odoo 14.0, ejecuta en la terminal el siguiente comando:

```bash
git clone https://github.com/odoo/odoo.git --single-branch --depth 1 --branch 14.0 ~/Odoo/src/14.0
```

Este comando descargará el código fuente de Odoo 14.0 en la carpeta `~/Odoo/src/14.0`.

El parámetro --single-branch indica que solo se clonará la rama especificada en lugar de todas las ramas del repositorio. El parámetro --depth 1 indica que solo se clonará el historial más reciente del repositorio, lo que reduce el tiempo y espacio necesarios para la descarga.

### Crear un entorno virtual

Para crear un entorno virtual de Python para Odoo, ejecute el siguiente comando:

```bash
python3 -m venv ~/Odoo/instances/odoo-dev-14.0/venv
```

Este comando creará un entorno virtual para Odoo en la carpeta `~/Odoo/instances/odoo-dev-14.0/venv`.

### Instalar las dependencias de Odoo

Para instalar las dependencias de python para Odoo, ejecute los siguientes comandos:

```bash
source ~/Odoo/instances/odoo-dev-14.0/venv/bin/activate
pip3 install setuptools wheel inotify psycopg2-binary
pip3 install -r ~/Odoo/src/14.0/requirements.txt
deactivate
```

Estos comandos activarán el entorno virtual de Odoo, instalarán las dependencias necesarias y desactivarán el entorno virtual.

1. `source ~/Odoo/instances/odoo-dev-14.0/venv/bin/activate`: este comando activa el entorno virtual de Odoo para que puedas instalar las dependencias necesarias sin afectar al sistema operativo.
    
2. `pip3 install setuptools wheel inotify psycopg2-binary`: estos son paquetes de Python necesarios para ejecutar Odoo. `setuptools` y `wheel` son herramientas de construcción de paquetes, `inotify` es una biblioteca para monitorear cambios en archivos y directorios, y `psycopg2-binary` es un controlador de base de datos PostgreSQL para Python.
    
3. `pip3 install -r ~/Odoo/src/14.0/requirements.txt`: este comando instala todas las dependencias adicionales requeridas por Odoo, que están enumeradas en el archivo `requirements.txt`. El prefijo `-r` significa "de un archivo de requisitos".
    
4. `deactivate`: este comando desactiva el entorno virtual de Odoo, lo que significa que ya no se están utilizando las dependencias instaladas en dicho entorno.
    

Con estos pasos, hemos instalado Odoo 14.0 en nuestro entorno de desarrollo de Ubuntu 22.04. Ahora podemos empezar a trabajar con Odoo y personalizarlo según nuestras necesidades.

### Crear el archivo de configuración de Odoo

Después de haber creado el entorno virtual de Python y haber instalado las dependencias necesarias, el siguiente paso es configurar Odoo para que se ejecute correctamente en el entorno virtual. Para esto, es necesario crear un archivo de configuración específico para su instancia de Odoo.

Para crear el archivo de configuración, ejecute los siguientes comandos:

```bash
cp ~/Odoo/src/14.0/debian/odoo.conf ~/Odoo/instances/odoo-dev-14.0 
sed -i 's/db_user = odoo/db_user = '$USER'/' ~/Odoo/instances/odoo-dev-14.0/odoo.conf
```

El primer comando copia el archivo de configuración predeterminado de Odoo a la carpeta de su instancia de Odoo. El segundo comando utiliza el comando "sed" para reemplazar el usuario de la base de datos predeterminado de "odoo" por el usuario actual. Esto es necesario para que Odoo pueda acceder a la base de datos en el entorno virtual.

Una vez que haya creado el archivo de configuración de Odoo, podrá personalizarlo para adaptarlo a sus necesidades específicas. Puede configurar la dirección IP, el puerto, la base de datos y otras opciones para su instancia de Odoo si ya tenia una instalación de PostgreSQL.

## **Inicializar la base de datos de Odoo**

Una vez que se han instalado las dependencias de Odoo y se ha creado el archivo de configuración, el siguiente paso es inicializar la base de datos de Odoo. Para hacer esto, se utilizará el comando:

```bash
~/Odoo/instances/odoo-dev-14.0/venv/bin/python3 ~/Odoo/src/14.0/odoo-bin -c ~/Odoo/instances/odoo-dev-14.0/odoo.conf -d odoo-dev-14.0 -i base --stop-after-init
```

Este comando ejecuta el archivo `odoo-bin` que se encuentra en la carpeta `src/14.0` del directorio raíz de Odoo. El parámetro `-c` especifica la ruta del archivo de configuración de Odoo que se creó anteriormente. El parámetro `-d` especifica el nombre de la base de datos que se creará e inicializará. En este caso, se está utilizando `odoo-dev-14.0`.

El parámetro `-i` indica los módulos de Odoo que se instalarán. En este caso, solo se está instalando el módulo base de Odoo. Sin embargo, es posible agregar más módulos separándolos por comas.

Finalmente, el parámetro `--stop-after-init` detiene el servidor de Odoo después de inicializar la base de datos. Esto es útil si solo se desea inicializar la base de datos y no ejecutar el servidor completo de Odoo.

Una vez que se ejecuta este comando, se creará y se inicializará la base de datos de Odoo. Este proceso puede tardar unos minutos, dependiendo de la velocidad de su computadora.

## Configuración del debugger de VSCode para Odoo 14.0

Una herramienta útil para desarrollar en Odoo es el debugger de Visual Studio Code (VSCode), que permite depurar código en tiempo real. A continuación, se muestra cómo configurar el debugger de VSCode para trabajar con Odoo 14.0.

1. Abre Visual Studio Code en la carpta de la instancia `~/Odoo/instances/odoo-dev-14.0/` y haz clic en la pestaña "Debug" en la barra lateral izquierda.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678753259740/c30934dc-32b9-44ee-8952-84074af4430d.png align="center")
    
2. Haz clic en el botón "cree un archivo `launch.json`" en la parte inferior de la pestaña "Debug".
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678753416525/8f98379f-5b41-45e3-aec4-ca3634d20082.png align="center")
    
3. Copia y pega el siguiente código en el archivo "launch.json" que se ha creado:
    

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "odoo-dev-14.0",
            "type": "python",
            "request": "launch",
            "program": "~/Odoo/src/14.0/odoo-bin",
            "console": "integratedTerminal",
            "args": [
                "-c","~/Odoo/instances/odoo-dev-14.0/odoo.conf",
                "--limit-time-real", "99999",
                "-d", "odoo-dev-14.0"
            ]
        },
        {
            "name": "odoo-dev-14.0-install-addons",
            "type": "python",
            "request": "launch",
            "program": "~/Odoo/src/14.0/odoo-bin",
            "console": "integratedTerminal",
            "args": [
                "-c","~/Odoo/instances/odoo-dev-14.0/odoo.conf",
                "--limit-time-real", "99999",
                "-d", "odoo-dev-14.0",
                "-i","",
                "--stop-after-init"
            ]
        },
        {
            "name": "odoo-dev-14.0-update-addons",
            "type": "python",
            "request": "launch",
            "program": "~/Odoo/src/14.0/odoo-bin",
            "console": "integratedTerminal",
            "args": [
                "-c","~/Odoo/instances/odoo-dev-14.0/odoo.conf",
                "--limit-time-real", "99999",
                "-d", "odoo-dev-14.0",
                "-u","",
                "--stop-after-init"
            ]
        },
        {
            "name": "odoo-dev-14.0-repl",
            "type": "python",
            "request": "launch",
            "program": "~/Odoo/src/14.0/odoo-bin",
            "console": "integratedTerminal",
            "args": [
                "shell",
                "-c","~/Odoo/instances/odoo-dev-14.0/odoo.conf",
                "--limit-time-real", "99999",
                "--xmlrpc-port","8888",
                "--longpolling-port","8899",
                "-d", "odoo-dev-14.0",
                "--shell-interface", "ipython"
            ]
        }
    ]
}
```

1. Ahora, puedes elegir una de las siguientes opciones de configuración del debugger:
    

* odoo-dev-14.0: esta opción inicia Odoo en modo de desarrollo con la base de datos "odoo-dev-14.0".
    
* odoo-dev-14.0-install-addons: esta opción instala los módulos de Odoo que agregemos al parametro "-i", en la base de datos "odoo-dev-14.0".
    
* odoo-dev-14.0-update-addons: esta opción actualiza los módulos de Odoo que agregemos al parametro "-u", en la base de datos "odoo-dev-14.0".
    
* odoo-dev-14.0-repl: esta opcion inicia Odoo en modo de consola interactiva (REPL) donde puedes ejecutar comandos del ORM
    

El parametro "--limit-time-real" establece el tiempo máximo permitido para la ejecución de una solicitud de servidor en Odoo, con un valor de "99999" establece este límite en un tiempo muy alto, prácticamente ilimitado. Esto es útil durante el desarrollo, ya que nos permite depurar el código sin interrupciones debido a la expiración del tiempo límite de Odoo

Con la configuración adecuada, podemos utilizar el debugger de VSCode para solucionar problemas en el código de Odoo y mejorar la calidad del software. Además, al tener un debugger integrado en su entorno de desarrollo, pueden ahorrar tiempo y mejorar la eficiencia de su trabajo.

Espero que este tutorial haya sido útil para aquellos que buscan configurar el debugger de VSCode para trabajar con Odoo 14.0. Si tienes alguna pregunta o comentario, no dudes en escribirme.