---
title: Solicitar script de análisis
seo-title: Solicitar script de análisis
description: La secuencia de comandos de análisis de solicitudes se realiza para facilitar el análisis de los archivos access.log y generar un informe legible para su posterior procesamiento
seo-description: La secuencia de comandos de análisis de solicitudes se realiza para facilitar el análisis de los archivos access.log y generar un informe legible para su posterior procesamiento
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Solicitar script de análisis{#request-analysis-script}

## Descargar {#download}

Esta secuencia de comandos se realiza para facilitar el análisis de los `access.log` archivos que producen un informe legible para su posterior procesamiento.

[Obtener archivo](assets/analyse-access.sh)

## Descripción {#description}

Esta secuencia de comandos se realiza para facilitar el análisis de los `access.log` archivos que producen un informe legible para su posterior procesamiento.

Genera el número total de solicitudes, GET vs. POST, la distribución de solicitudes a lo largo del tiempo y más.

El resultado está en la sintaxis Markdown, por lo tanto será más fácil convertirlo a archivos PDF con herramientas como pandoc o mostrarlo en un navegador con complementos como el visor Markdown.

Puede analizar una ruta personalizada proporcionada en la línea de comandos.

Tomando del comentario dentro del archivo que le dice cómo ejecutarlo:

Analizar CQ `access.log` extrapolando varias informaciones y produciendo una salida de Markdown en `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

puede proporcionar rutas personalizadas adicionales para analizarlas en la línea de comandos

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

la salida se puede guardar mediante una simple tubería

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
