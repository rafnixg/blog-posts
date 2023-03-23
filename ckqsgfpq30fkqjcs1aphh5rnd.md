---
title: "Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 3"
datePublished: Sun Aug 09 2020 00:59:16 GMT+0000 (Coordinated Universal Time)
cuid: ckqsgfpq30fkqjcs1aphh5rnd
slug: actualiza-tu-perfil-de-github-con-readme-y-github-actions-parte-3
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MAYEkmn7G6E/upload/d6bf961a729b1007baf04287606f07d0.jpeg
tags: python, readme, github-actions-1

---

Si aun no has leído las otras dos partes te invito a que las revises:

* [Crear nuestro README en GitHub](https://blog.rafnixg.dev/actualiza-tu-perfil-de-github-con-readme-y-github-actions-parte-1)
    
* [Escribir un script en python para crear nuestro README dinámico](https://blog.rafnixg.dev/actualiza-tu-perfil-de-github-con-readme-y-github-actions-parte-2)
    

En esta tercera entrega vamos a automatizar mediante GitHub Actions la generación de nuestro archivo README.md ejecutando de forma programada nuestro script de Python que creamos en la publicación anterior.

GitHub Actions es una funcionalidad de GitHub que nos permite automatizar flujos de desarrollo directamente en nuestro repositorio de código, lo que nos da la ventaja de poder crear nuestros propios flujos y trabajos a ejecutar.

Al estar integrado con nuestro repositorio de código, tenemos la ventaja de poder crear nuestros flujos de trabajo de CI/CD, en esta publicación no profundizaremos en este tipo de implementaciones, pero si haremos uso de GitGub Actions para ejecutar nuestro propio flujo que consiste en ejecutar un script de Python y realizar un **PUSH** a nuestro repositorio de datos cuando exista un cambio en el archivo README.md.

## Creando nuestro primer GitHub Actions

Para poder activar esta funcionalidad solo debemos crear un directorio en la raíz de nuestro proyecto llamado *.github* dentro de este directorio creamos otro directorio llamado ***workflows***\*.\*

```bash
mkdir .github 
cd .github 
mkdir workflows
```

Ya con esto podemos comenzara crear nuestro **workflow** usando un archivo YAML, para este caso mi archivo se va a llamar [*python-app.yml*](https://github.com/rafnixg/rafnixg/blob/master/.github/workflows/python-app.yml) pero puede tener el nombre que ustedes quieran.

Si hacemos un push al repositorio y revisamos el tab de "Actions" veremos nuestro **workflow** y estará en un estado de falla ya que aun no hemos agregado ningún trabajo ni los pasos a seguir.

```bash
# Raíz del proyecto 
git add .github/workflows/python-app.yml 
git commit -m "[ADD] new workflow for GitHub Actions" 
git push origin master
```

![GitHub Actions tab](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600269425/37-YsGPMGv.png align="left")

Para editar nuestro archivo lo haremos directamente desde GitHub para aprovechar el auto completado y otras herramientas que tiene GitHub para la creación de Actions, al abrir nuestro archivo escribimos lo siguiente:

![Actualiza tu perfil de GitHub con README y GitHub Actions - Parte 3](https://cdn.hashnode.com/res/hashnode/image/upload/v1625600271286/ryIhk_9kI.png align="left")

Acá podemos ver del lado derecho un panel que nos puede ayudar a buscar Actions creadas por la comunidad y también nos muestra la documentación de GitHub Actions.

```yaml
name: Python workflow # Nombre del workflow
on: # llave que indica que se realizara una acción sobre algun evento 
  schedule: # El evento que ejecutara la acción
    - cron: "0 */6 * * *" # configuración del intervalo de ejecución
```

Pudimos haber hecho que esta acción se ejecutara con otros eventos como un push o un pull request, pero de esto hablare en una siguiente publicación, para profundizar les recomiendo estas dos lecturas:

[https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#onschedule](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#onschedule)

[https://docs.github.com/en/actions/reference/events-that-trigger-workflows#scheduled-events](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#scheduled-events)

Hasta este momento solo hemos indicado, el nombre de nuestro **workflow** y que sera una acción que se ejecutara de forma programada cada 6 horas, pero aun no hemos definido el **job** y la secuencia de pasos que se van a ejecutar, para esto debemos editar nuestro archivo y nos debe quedar de la siguiente manera:

```yaml
name: Python workflow # Nombre del workflow
on: # llave que indica que se realizara una acción sobre algun evento 
  schedule: # El evento que ejecutara la acción
    - cron: "0 */6 * * *" # configuración del intervalo de ejecución

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up Python 3.8
        uses: actions/setup-python@v2
        with:
          python-version: 3.8
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Run script
        run: |
          python app.py
          git config user.name rafnixg
          git config user.email rafnixg@gmail.com
          git add README.md
          git diff --quiet && git diff --staged --quiet || git commit -m "[BOT] Update README with latest info"
          git push origin master
```

[https://github.com/rafnixg/rafnixg/blob/master/.github/workflows/python-app.yml](https://github.com/rafnixg/rafnixg/blob/master/.github/workflows/python-app.yml)

Al guardar los cambios en nuestro archivo tenemos ya definido un **job** de nombre ***build*** con el key ***run-on*** donde indicamos que el sistema operativo que va a correr es un ubuntu-latest, si han trabajado con este tipo de archivos YAML en docker, se les hará fácil comprender este archivo, sino no hay problema acá explico que hace nuestro archivo.

Después de la definición del jobs tenemos que definir los **steps,** que son esos pasos que va a seguir nuestro job, aqui usamos dos actions que están disponibles en el marketplace, esta creo es una de las cosas mas interesantes de GitHub Actions, ya que podemos crear actions y compartirlas con la comunidad para que otras personas las puedan implementar, yo estaré usando en esta oportunidad "action/checkout@v2" que nos ayuda a configurar git en nuestro **workspace** y poder tener acceso desde el **Workflow** que estamos definiendo hacia nuestro repositorio y "action/setup-python@v2" que nos ayuda a configurar python en el workspace para poder correr nuestro script.

Lo siguiente sera actualizar pip e instalar las dependencias de nuestro script y ejecutar nuestro script, ya en este punto tenemos nuestro archivo READM.md actualizado en nuestro **workspace**, solo nos resta crear un commit con este cambio y hacer push a nuestro repositorio.

Con este push ya tenemos nuestro README.md actualizado en nuestro repositorio, ahora cada 6 horas va a correr este Workflow en donde definimos un jobs que se encarga de correr nuestro script y hacer un commit cuando exista un cambio en el archivo README.md

En próximas publicaciones hablara un poco mas sobre las GitHubs Actions y de como crear nuestras propias actions y publicarlas para que puedan ser reutilizadas, si te gusto el contenido espero tu comentario.

Sígueme en twitter [@rafnixg](https://twitter.com/rafnixg)