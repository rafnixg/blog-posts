---
title: "Ejecutar Código JavaScript en Sublime Text"
datePublished: Wed Jun 28 2017 18:48:00 GMT+0000 (Coordinated Universal Time)
cuid: ckqsggpy10fl3jcs19yfx61de
slug: ejecutar-codigo-javascript-en-sublime-text

---

![Ejecutar Código JavaScript en Sublime Text](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600327139/rywzHY5gy.jpeg)

Cuando estamos iniciando en el desarrollo con JavaScript uno de los flujos de trabajos menos óptimos para no decir los mas fastidiosos, son tener que escribir el código en nuestro editor de código favorito y tener que ir a la consola del explorador a probarlo.

Para resolver este problema existen muchos camino, el que yo propongo aquí es el que mas se adapto a mis necesidades y espero que pueda ayudar en las suyas, para todos esos que usan _Sublime Text_ y mantiene este flujo de trabajo de crear código en sublime y luego pasarlo a un explorador y depurar en la consola del explorador doy este pequeño pero para mi poderoso tip.

Inicialmente debemos tener instalado _Sublime Text_, es muy sencillo de instalar y en su sitio web existe mucha documentación al respecto, y lo segundo que tendremos que tener instalado es _Node.js_,

Si aun no tienes instalado _Node.js_ acá te dejo la documentación oficial donde encontrás la guiá de como instalarlo en cualquier sistema operativo que uses, [Manual de Instalación](https://nodejs.org/es/download/package-manager/)

#### Configurando Sublime

Luego de tener Sublime Text y Node.js instalados y funcionando, vamos a proceder a hacer una pequeña configuración en sublime Text, para esto debemos ingresar en **“Tools > Build System > New Build System”**, se abrirá un documento nuevo con el siguiente contenido:

> {  
> “cmd”: \[“make”\]  
> }

Este contenido debe ser sustituido por el siguiente:

> {  
> “cmd”: \[“node”, “$file”\],  
> “selector”: “source.js”  
> }

Hecho esto procedemos a guardar el archivo en la ruta sugerida por Sublime Text, para poder probar que esta funcionando solo debemos crear un nuevo archivo JS con el código JavaScript que deseen, recomiendo solo a modo de prueba el siguiente:

> console.log(“JavaScript funcionando desde Sublime Text”)

Guardan el archivo nuevo con el nombre que deseen en mi caso **“prueba.js”** y para poder ejecutarlo deben ir a **“Tools > Build”** o ejecutando la siguiente combinación de teclas **“Control + B”**.

#### Recomendaciones

Para los que se están iniciando en el mundo de JavaScript los recomiendo leer un poco sobre Node.js y lo potente que puede llegar a ser, ya que en este post no se aprecia la potencia de este.

Instalar Snippets y verificadores de código para Sublime Text, para aumentar su productividad y saber donde puedan tener posibles errores.