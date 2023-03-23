---
title: "Deploy usando GIT-FTP"
datePublished: Tue Jun 26 2018 18:57:00 GMT+0000 (Coordinated Universal Time)
cuid: ckqsggljc0fl0jcs1d9f75ar7
slug: deploy-usando-git-ftp
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MAYEkmn7G6E/upload/d6bf961a729b1007baf04287606f07d0.jpeg
tags: ftp, git

---

Es muy común que cuando nos estamos iniciando en el mundo del desarrollo web y no tenemos dinero para costearnos un buen servicio, optemos por comprar espacio en un ‘Shared host’ o utilizar un hosting gratuito que básicamente funcional igual.

## **Introducción**

Cuando queremos desplegar nuestros proyectos webs en estos servicios de bajo costo o gratuitos, nos encontramos con una limitante de que no tenemos acceso por SSH, sino que nos colocan a disposición una cuenta FTP.

Para muchos que no han usado o trabajado con el control de versiones esto no es un problema, pero si queremos mantener un buen flujo de trabajo y llevar el seguimiento de nuestro proyecto usar git es tarea fundamental y a la hora del despliegue es una herramienta que nos facilita la vida, a diferencia de FTP que hace el proceso de despliegue muy tedioso y con mucha perdida de tiempo, ya que debemos saber que archivos fueron modificados para subir al servidor.

## **Git-FTP**

Esa herramienta nos viene a solucionar ese problema de no subir todos los archivos o seleccionar de forma manual los archivos que deseamos subir al servidor, sino que el se encarga de revisar que archivos fueron modificados desde la ultima actualización y solo sube estos archivos.

Que belleza y que hermosura fue lo que yo pensé cuando di con esta herramienta, ya que obviamente hace que nuestro flujo de trabajo sea mas optimo que usando solamente FTP, pero no todo es así de bello existe una limitación al usar este cliente FTP y es que las modificaciones hechas directamente sobre el servidor no serán vista desde nuestra área local, por lo que aconsejo mantener esto en cuenta.

## **Instalacion de Git-FTP**

La instalación es muy sencilla para los que usamos GNU/Linux yo en especial uso Debian es muy sencillo de instalar usando la terminal, para los que usen otro sistema operativo acá les dejo el [Manual de Instalación Oficial](https://github.com/git-ftp/git-ftp/blob/master/INSTALL.md) donde encontraran la instalación para los siguientes Sistemas operativos:

* Linux/Unix usando make
    
* Debian, Ubuntu y otros usando apt
    
* ArchLinux
    
* Mac OS X
    
* Windows
    

Para los que usamos Debian o Ubuntu solo debemos teclear esto en la terminal

```bash
sudo apt-get install git-ftp
```

Con esto ya tendríamos Git-FTP instalado

## **Configuración**

La configuración es muy sencilla desde nuestro terminal usamos los siguientes comandos:

```bash
git config git-ftp.url ftp.example.net
git config git-ftp.user ftp-user
git config git-ftp.password secr3t
```

Ya con esto tendríamos configurada la conexión a nuestro servidor por FTP, solo resta ubicarnos en la carpeta de nuestro proyecto y dependiendo las siguientes 2 opciones ejecutar el comando que sea conveniente:

* Subir todos los archivos (inicializacion)  
    `git ftp init`
    
* Indicar que los archivos ya se encuentran en el servidor.  
    `git ftp catchup`
    

## **Haciendo Deploy**

Para hacer deploy seguimos nuestro flujo de trabajo normal usando git, en el momento que necesitemos subir los archivos modificados al servidor solo debemos ejecutar este comando en la terminal:

```bash
git ftp push
```

Con esto ya tendremos nuestros archivos en el servidor.

## **Recomendación**

> Mantener siempre el mismo flujo de trabajo y no modificar archivos directamente al servidor.

> Leer la documentación Oficial de Git-FTP - [Pagina Oficial de Git-FTP](https://git-ftp.github.io/)