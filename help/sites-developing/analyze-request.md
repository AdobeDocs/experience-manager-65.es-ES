---
title: Secuencia de comandos de análisis de solicitud
seo-title: Request Analysis Script
description: La secuencia de comandos de análisis de solicitudes se realiza para facilitar el análisis de los archivos access.log que producen un informe legible para su procesamiento posterior
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Secuencia de comandos de análisis de solicitud{#request-analysis-script}

## Descargar {#download}

Esta secuencia de comandos se realiza para facilitar el análisis de la variable `access.log` archivos que generan un informe legible para su procesamiento posterior.

[Obtener archivo](assets/analyse-access.sh)

## Descripción {#description}

Esta secuencia de comandos se realiza para facilitar el análisis de la variable `access.log` archivos que generan un informe legible para su procesamiento posterior.

Genera el número total de solicitudes, GET frente a POST, y la distribución de solicitudes a lo largo del tiempo y más.

El resultado está en la sintaxis Markdown, por lo que será más fácil convertirla a PDF con herramientas como pandoc o mostrarla en un navegador con complementos como el visor Markdown.

Puede analizar una ruta personalizada que se proporciona en la línea de comandos.

Tomando del comentario dentro del archivo que le indica cómo ejecutarlo:

Analizar CQ `access.log` extrapolación de varias informaciones y producción de un resultado de Markdown en `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

puede proporcionar rutas personalizadas adicionales para analizar en la línea de comandos

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

puede guardar la salida utilizando una sencilla tubería

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
