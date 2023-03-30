---
title: "Explorando Odoo a fondo: Cómo trabajar con la shell de la CLI y configurar IPython como REPL"
seoDescription: "Aprende a utilizar y configurar la shell de la CLI de Odoo con IPython, una herramienta esencial para desarrolladores que desean profundizar en Odoo"
datePublished: Thu Mar 30 2023 12:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clfv2dvp4014vmvnvgeie8rtc
slug: explorando-odoo-a-fondo-como-trabajar-con-la-shell-de-la-cli-y-configurar-ipython-como-repl
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/a4X1cdC1QAc/upload/0907fbada7fd37c284884a528569e522.jpeg
tags: python, cli, odoo, shell-odoo

---

¡Hola a todos! Hoy vamos a explorar un tema esencial para todos los programadores de Odoo que deseen profundizar en el desarrollo y uso del ORM de Odoo: la shell de la CLI de Odoo. La CLI (Command Line Interface) de Odoo es la forma en que se ejecuta Odoo en la mayoría de los casos, ya sea en modo de desarrollo o en producción. Conocer cómo funciona la CLI y cómo usarla de manera efectiva nos permitirá aprovechar al máximo las herramientas y funciones de Odoo y mejorar la eficiencia de nuestro trabajo.

En este post, te guiaré a través de cómo acceder a la shell de Odoo y cómo configurarla para trabajar con IPython.

## **Cómo ejecutar una shell usando la CLI de Odoo**

Para acceder a la shell de Odoo, primero debemos asegurarnos de que Odoo esté instalado en nuestro sistema. Si aún no lo has hecho, te recomiendo seguir los pasos de instalación de Odoo para tu sistema operativo o [Creando un entorno de desarrollo para Odoo 14.0 con VSCode](https://blog.rafnixg.dev/creando-un-entorno-de-desarrollo-para-odoo-140-con-vscode-en-ubuntu-2204). Una vez instalado, sigue estos pasos para acceder a la shell de Odoo:

1. Abre la línea de comandos o terminal.
    
2. Navega hasta el directorio de instalación de Odoo. Normalmente, esto se encuentra en "/usr/lib/odoo" o "/opt/odoo".
    
3. Ejecuta el siguiente comando si tienes una instalacion desde codigo fuente:
    

```bash
./odoo-bin shell -c /path/to/odoo.conf --xmlrpc-port 8888 --longpolling-port 8899
```

Si es desde una instalcion usando los paquetes del sistema operativo

```bash
odoo shell -c /path/to/odoo.conf --xmlrpc-port 8888 --longpolling-port 8899
```

* `-c /path/to/odoo.conf`: especifica la ruta al archivo de configuración de Odoo que deseas utilizar.
    
* `--xmlrpc-port 8888`: establece el puerto XML-RPC que utiliza Odoo para comunicarse con otras aplicaciones.
    
* `--longpolling-port 8899`: establece el puerto de long polling que utiliza Odoo para notificaciones en tiempo real.
    

Cambiamos los puertos para que no choque con los puertos de nuestra instancia de Odoo que se esta ejecutando.

Si todo funciona correctamente, deberías ver la siguiente línea en la terminal:

```bash
env: <odoo.api.Environment object at 0x7efc89670ef0>
odoo: <module 'odoo' from '/usr/lib/python3/dist-packages/odoo/__init__.py'>
openerp: <module 'odoo' from '/usr/lib/python3/dist-packages/odoo/__init__.py'>
self: res.users(1,)
Python 3.x.x (default, MMM DD YYYY, HH:MM:SS)
```

Ahora estás en la shell de Odoo. Puedes empezar a ejecutar comandos de Odoo y explorar la plataforma ERP. Por ejemplo, puedes ejecutar el siguiente comando para el usuario que se ejecuta en esta shell Odoo:

```python
print(self.name)
```

También puedes interactuar con la base de datos de Odoo utilizando la sintaxis de ORM de Odoo. Por ejemplo, el siguiente comando cuenta todos los modelos de datos que tiene esta instancia de Odoo:

```javascript
print(env['ir.model'].search_count([]))
```

## **Cómo configurar la interfaz de la shell para usar IPython como REPL**

IPython es un shell interactivo de Python que proporciona funciones avanzadas como autocompletado, resaltado de sintaxis, historial de comandos y más. Utilizar IPython como REPL (Read-Eval-Print Loop) en lugar del shell estándar de Python puede mejorar nuestra experiencia de programación en Odoo.

Para configurar la shell de Odoo para usar IPython como REPL, sigue estos pasos:

1. Instala IPython en tu sistema. En la mayoría de los sistemas operativos, puedes instalarlo ejecutando el siguiente comando:
    

```bash
pip install ipython
```

1. Ahora que IPython está instalado, debes modificar el comando que usamos anteriormente para acceder a la shell de Odoo, incluyendo la opción `--shell-interface ipython`. El comando modificado se verá así:
    

```bash
# Desde codigo fuente
./odoo-bin shell -c /path/to/odoo.conf --xmlrpc-port 8888 --longpolling-port 8899 --shell-interface ipython
```

```bash
# Binario instalado
odoo shell -c /path/to/odoo.conf --xmlrpc-port 8888 --longpolling-port 8899 --shell-interface ipython
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680142682619/4e5967a9-664c-4b2e-a86c-d2d044b443f4.png align="center")

Al ejecutar este comando, accederás a la shell de Odoo con IPython como REPL,como vemos en la imagen, lo que te permitirá aprovechar sus funciones avanzadas mientras trabajas con Odoo, para salir del modo shell con IPython debes usar `ctrl+D`

## **Recomendaciones para el uso de la shell de Odoo**

### **Configuración separada para la shell de Odoo**

Es altamente recomendable tener un archivo de configuración separado para la shell de Odoo. Esto nos permite ajustar los parámetros específicos para la shell sin afectar la configuración de nuestra instancia de Odoo en producción o desarrollo. Algunos de los parámetros que podrías considerar ajustar en este archivo de configuración separado incluyen:

* `--xmlrpc-port 8888`: Establecer un puerto XML-RPC diferente para evitar conflictos con la instancia principal de Odoo.
    
* `--longpolling-port 8899`: Establecer un puerto de Long Polling diferente para evitar conflictos con la instancia principal de Odoo.
    
* Cambiar los valores de límite de memoria (soft y hard memory limit) para asignar más o menos recursos a la shell.
    
* Ajustar el número de workers para adaptarlo a tus necesidades específicas.
    

Para crear un archivo de configuración separado, simplemente copia tu archivo de configuración principal y modifica los parámetros mencionados anteriormente. Luego, al ejecutar la shell de Odoo, usa la opción `-c` para especificar la ruta a este nuevo archivo de configuración. Por ejemplo:

```bash
./odoo-bin shell -c /path/to/shell-odoo.conf --shell-interface ipython
```

```bash
odoo- shell -c /path/to/shell-odoo.conf --shell-interface ipython
```

### **Uso de librerías externas**

Al trabajar con la shell de Odoo, no estás limitado a utilizar solo las funcionalidades integradas en Odoo. Puedes aprovechar también las ventajas de librerías externas de Python para mejorar tu productividad y facilitar el análisis y procesamiento de datos. Una de estas librerías es Pandas, una herramienta popular y potente para el análisis y manipulación de datos en Python.

Puedes importar Pandas en la shell de Odoo e interactuar con los datos utilizando sus estructuras de datos como DataFrames y Series. Por ejemplo, puedes convertir los registros de un modelo de Odoo en un DataFrame de Pandas y luego realizar análisis y manipulación de datos avanzados. Esto puede ser especialmente útil cuando necesitas generar informes o analizar datos de forma rápida y eficiente.

Recuerda que al usar librerías externas como Pandas, es importante garantizar que estén correctamente instaladas y configuradas en tu entorno de desarrollo y, si es necesario, en el entorno de producción.

## **Conclusión**

En resumen, la shell de la CLI de Odoo es una herramienta muy útil para los desarrolladores de Odoo que desean profundizar en la programación del ERP. A través de la CLI, podemos interactuar con Odoo de una manera más avanzada y personalizada. Además, al configurar la interfaz de la shell para usar IPython como REPL, podemos aprovechar las funciones avanzadas de IPython y mejorar nuestra experiencia de programación en Odoo.

Espero que este post te haya sido útil y te haya brindado una mejor comprensión de cómo trabajar con la shell de Odoo y configurarla con IPython. Si te ha gustado este post y crees que puede ser útil para otros desarrolladores de Odoo, no dudes en compartirlo en tus redes sociales. Nos vemos en un proximo post donde profundizaremos en el uso de la shell de Odoo.

Si quieren saber mas sobre IPython y la CLI de Odoo, aca les dejo los enlaces a su documentación.

* [Documentación Oficial de IPython](https://ipython.readthedocs.io/en/stable/)
    
* [Documentación Oficial de Odoo CLI](https://www.odoo.com/documentation/master/developer/reference/cli.html)