---
title: "Los servicios que uso en mi HomeLab server: virtualización, contenedores y más."
datePublished: Mon Mar 20 2023 23:42:31 GMT+0000 (Coordinated Universal Time)
cuid: clfhh1yx8000509l0fqq77d7z
slug: los-servicios-que-uso-en-mi-homelab-server-virtualizacion-contenedores-y-mas
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/EJe6LqEjHpA/upload/769f355c1142c6c1634c19b941d72ddf.jpeg
tags: cloudflare, nginx, self-hosted, homelab, proxmox

---

¡Hola nuevamente! hoy quiero profundizar en cada uno de los servicios y aplicaciones que tengo en mi homelab server y compartirlas contigo.

## Introducción

En mi camino como desarrollador y entusiasta de la tecnología, he construido un homelab server en mi casa para experimentar con nuevas tecnologías y aprender de forma autodidacta. Mi homelab server es un servidor casero donde puedo ejecutar diferentes servicios y herramientas.

En este artículo, compartiré con ustedes los servicios que actualmente estoy corriendo en mi homelab server. Estos servicios incluyen virtualización con Proxmox, contenedores con LXC y Docker, una plataforma como servicio (PaaS) llamada Coolify, un backend as a service (BaaS) llamado Appwrite, Pi-hole para bloquear anuncios y rastreadores, Plausible para analizar las métricas de mi sitio, y mucho más. Si estás interesado en crear tu propio homelab server o simplemente deseas conocer qué servicios estoy usando, sigue leyendo para conocer más.

## **Proxmox VE**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679354595439/a606ff2f-6af1-497c-9a35-71f59a74bc02.png align="center")

[Proxmox VE](https://www.proxmox.com/) es una plataforma de virtualización de código abierto que utilizo para virtualizar y administrar mis servidores. Proxmox me permite crear y gestionar contenedores Linux (LXC) y máquinas virtuales (VM), lo que me brinda una gran flexibilidad y ahorro de recursos en mi homelab server.

Los contenedores LXC son una forma ligera y eficiente de virtualización que me permiten ejecutar múltiples servicios en mi homelab server de manera aislada y segura. Por otro lado, las máquinas virtuales son una forma más tradicional de virtualización que me permiten ejecutar sistemas operativos completos en mi homelab server, lo que es útil para probar diferentes configuraciones y experimentar con nuevas tecnologías.

Proxmox tiene una interfaz web fácil de usar que me permite crear y gestionar mis contenedores LXC y máquinas virtuales de manera sencilla. También cuenta con una comunidad activa y una amplia documentación que me ha sido de gran ayuda a lo largo del tiempo.

## **Coolify**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679354733424/3149397a-9f00-444b-844d-2d918f1d7a94.png align="center")

[Coolify](https://coolify.io/) es una plataforma como servicio (PaaS) que utilizo para alojar mi sitio web. Es una alternativa a Heroku, pero self-hosted, lo que me brinda más control y flexibilidad. Dentro de Coolify, tengo desplegado mi sitio [web](https://rafnixg.dev). Además, utilizo Appwrite, un Backend as a Service (BaaS) del que hablare mas adelante y algunas aplicaciones desplegadas usando docker.

## **Appwrite**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679354761054/c8fd9ad7-b7a9-44e1-8a5a-0cb47d698f52.png align="center")

[Appwrite](https://appwrite.io/) es un Backend as a Service (BaaS) que utilizo para gestionar mi sitio web. Me ayuda a manejar fácilmente usuarios, bases de datos y autenticación en mi sitio web, lo que me ahorra mucho tiempo y esfuerzo. Appwrite es muy fácil de integrar con Coolify, y tiene una interfaz de usuario web muy intuitiva.

## **Plausible**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679354407326/3617b113-832c-4f33-bd2f-ba2709e781c8.png align="center")

[Plausible](https://plausible.io/) es una herramienta de análisis web de código abierto que utilizo para analizar las métricas de mi sitio web. Es una alternativa a Google Analytics, pero más centrada en la privacidad. Plausible utiliza una arquitectura simple y ligera que no rastrea a los usuarios y no recopila información personal. Plausible me brinda información detallada sobre el tráfico de mi sitio web, como la cantidad de visitas, la ubicación geográfica de los visitantes y el tiempo promedio en el sitio.

## **Portainer**

![Portainer User Interface - Multiple endpoints](https://www.portainer.io/hubfs/Edge%20Aug22/edge-mockup.png align="left")

[Portainer](https://www.portainer.io/) es una herramienta de gestión de contenedores de Docker que utilizo para administrar y supervisar mis contenedores. Portainer tiene una interfaz de usuario web que me permite ver fácilmente el estado de mis contenedores, administrar imágenes y supervisar logs. Utilizo Portainer para gestionar Pi-Hole y otros servicios como el speedtracker en mi homelab server.

## **Pi-Hole**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679354884844/267bfbbc-b436-43b2-8fbf-6e749f0df02b.png align="center")

[Pi-hole](https://pi-hole.net/) es una aplicación de bloqueo de anuncios y rastreadores en Internet que utilizo para proteger mi navegación web y reducir la cantidad de anuncios. Pi-Hole utiliza una lista de bloqueo de anuncios actualizada regularmente para bloquear anuncios en todos mis dispositivos de red. Pi-hole funciona bloqueando las solicitudes de DNS de anuncios y rastreadores, lo que significa que la mayoría de los anuncios y rastreadores simplemente no se cargan.

En mi homelab server, utilizo Pi-hole como mi servidor de DNS local y bloqueador de anuncios y rastreadores. Pi-hole es fácil de configurar y puedo personalizar las listas de bloqueo de anuncios y rastreadores según mis necesidades. También puedo ver estadísticas detalladas sobre los dominios bloqueados y la cantidad de solicitudes de DNS procesadas por Pi-hole. Es una herramienta útil para mantener la privacidad y seguridad en mi red doméstica.

## **Speedtest Tracker**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679354922703/afb58053-71c3-4ce7-801d-6c62a6ad0355.png align="center")

[Speedtest Tracker](https://docs.speedtest-tracker.dev/) es una herramienta de monitoreo de velocidad de internet que utilizo para supervisar la velocidad de mi conexión a internet. Speedtest Tracker se ejecuta en un contenedor de Docker y utiliza Speedtest CLI para realizar pruebas de velocidad en intervalos regulares. Speedtest Tracker me brinda información detallada sobre la velocidad de mi conexión a internet, como la velocidad de descarga, la velocidad de carga y la latencia. También puedo ver gráficas de tendencias y estadísticas de velocidad a lo largo del tiempo.

## **Cloudflare Tunnels**

Cloudflare Tunnels es un servicio que utilizo para conectar mis contenedores y mi dominio. Con Cloudflare Tunnels, puedo acceder a mis servicios de forma segura desde cualquier lugar, sin tener que preocuparme por abrir puertos en mi firewall. Cloudflare Tunnels también me ayuda a ocultar la dirección IP de mi servidor, lo que aumenta mi privacidad y seguridad. Si quieres conocer más acerca de Cloudflare Tunnels, puedes visitar [**su sitio web**](https://developers.cloudflare.com/cloudflare-one/tutorials/share-localhost-on-the-internet).

## **Nginx Proxy Manager**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679355046298/fb56717b-721d-422f-bf9c-6c140bfbe487.png align="center")

Nginx Proxy Manager es una herramienta de gestión de proxies que utilizo para gestionar la redirección en dominios locales junto con Pi-Hole. Nginx Proxy Manager tiene una interfaz de usuario web sencilla que me permite configurar fácilmente proxies y redirecciones para mis servicios en contenedores. Además, Nginx Proxy Manager me ayuda a asegurar mis servicios al permitirme configurar SSL/TLS para mis dominios. Si estás interesado en conocer más sobre Nginx Proxy Manager, puedes visitar [**su sitio web**](https://nginxproxymanager.com/).

## Resumen

En mi homelab server, tengo configurados varios servicios para llevar a cabo diversas tareas. Proxmox me permite virtualizar y administrar mis servidores, y utilizo tanto contenedores LXC como máquinas virtuales para ejecutar diferentes servicios y experimentar con nuevas tecnologías.

Coolify es una plataforma como servicio que utilizo para alojar mi sitio web, con un backend as a service llamado Appwrite para manejar usuarios y bases de datos. Para analizar las métricas de mi sitio, utilizo Plausible, y para bloquear anuncios y rastreadores en mi red, utilizo Pi-hole.

Además, utilizo Cloudflare Tunnels para conectar mis contenedores dentro de mi servidor y mi dominio de forma segura, y Nginx Proxy Manager para gestionar la redirección en dominios locales junto con Pi-hole.

En resumen, estos son los servicios que tengo en mi homelab server y que me permiten experimentar con diferentes tecnologías y aplicaciones en un entorno seguro y controlado. Si estás interesado en crear tu propio homelab server, te recomiendo comenzar con algunos de estos servicios y experimentar para encontrar lo que mejor se adapte a tus necesidades. ¡Que disfrutes la creación de tu homelab server!