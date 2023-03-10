---
title: "Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 1"
datePublished: Tue Jul 28 2020 21:35:14 GMT+0000 (Coordinated Universal Time)
cuid: ckqsgg5vq0fktjcs11taghdxb
slug: actualiza-tu-perfil-de-github-con-readme-y-github-actions-parte-1
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MAYEkmn7G6E/upload/d6bf961a729b1007baf04287606f07d0.jpeg

---

Esta sera una serie de 3 Post:

* [Crear nuestro README en GitHub](http://rafnixg.dev/actualiza-tu-perfil-de-github-con-readme-y-github-actions-part-1/)
    
* [Escribir un script en python para crear nuestro README dinámico](http://rafnixg.dev/actualiza-tu-perfil-de-github-con-readme-y-github-actions-part-2/)
    
* [Implementar GitHub Actions para automatizar nuestro README](http://rafnixg.dev/actualiza-tu-perfil-de-github-con-readme-y-github-actions-part-3/)
    

Acá te dejo una mirada de como quedo [mi perfil](https://github.com/rafnixg), espero me dejes una estrella :D

![Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 1](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600297367/qIgriV0bP.png align="left")

## Preparando nuestro repositorio

Para iniciar, debemos crear un repositorio en GitHub con nuestro nombre de usuario, en mi caso "rafnixg", tiene que ser publico y estar inicializado con un archivo README.

Ingresando a [https://github.com/new](https://github.com/new) podemos crear nuestro repositorio

![Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 1](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600299615/ZGBEIU-y7.png align="left")

En mi caso ya me indica que tengo este repositorio creado, pero ademas se ve un mensaje que nos indica que activamos esta funcionalidad "secreta"

![Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 1](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600301793/LW4AZUI3I.png align="left")

## Creando nuestro README

En esta parte del proceso tendremos que empezar clonando nuestro repositorio y editar nuestro archivo README con la información que quisiéramos mostrar, para esto usaremos el siguiente comando de Git:

$ git clone https://github.com/tu\_username/tu\_username.git

Luego de clonar nuestro repositorio procedemos a crear nuestro archivo README usando Markdown, yo en esta parte del proceso use varias referencias para tomar ideas y armar algo que me gustara, les dejo por acá los enlaces para que las visiten y tomen ideas.

* [https://github.com/kautukkundan/Awesome-Profile-README-templates](https://github.com/kautukkundan/Awesome-Profile-README-templates)
    
* [https://github.com/abhisheknaiidu/awesome-github-profile-readme](https://github.com/abhisheknaiidu/awesome-github-profile-readme)
    

Ya con una idea de lo que queremos hacer, escribimos nuestro archivo y subimos estos cambios a GitHub

$ git add README.md $ git commit -m "\[IMP\] Mejora de nuestro README" $ git push -u origin master

Con esto ya tendremos nuestro archivo README desplegado en nuestro perfil de GitHub.

En la segunda entrega veremos como poder obtener datos de una API como la Ghost o Dev.to y actualizar nuestro archivo README usando Python.

Siguiente de esta serie: [Escribir un script en python para crear nuestro README dinámico](http://rafnixg.dev/actualiza-tu-perfil-de-github-con-readme-y-github-actions-part-2/)

Gracias por leerme! los espero por mi twitter [@rafnixg](https://rafnixg@gmail.com)