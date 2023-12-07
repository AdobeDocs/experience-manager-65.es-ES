---
title: Script de análisis de solicitud
description: El script de análisis de solicitud se realiza para facilitar el análisis de los archivos access.log y producir un informe legible para un procesamiento posterior
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Script de análisis de solicitud{#request-analysis-script}

## Descargar {#download}

Este script se crea para facilitar el análisis de la `access.log` archivos que producen un informe legible para un procesamiento posterior.

[Obtener archivo](assets/analyse-access.sh)

## Descripción {#description}

Este script se crea para facilitar el análisis de la `access.log` archivos que producen un informe legible para un procesamiento posterior.

Genera el número de solicitudes generales, GET frente a POST, distribución de solicitudes a lo largo del tiempo y más.

La salida está en sintaxis Markdown por lo tanto será más fácil convertirla en PDF con herramientas como pandoc o mostrarla en un navegador con complementos como Markdown viewer.

Puede analizar una ruta personalizada proporcionada en la línea de comandos.

Tomar del comentario dentro del archivo que le indica cómo ejecutarlo:

Analizar CQ `access.log` extrapolación de información diversa y producción de una salida Markdown en `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

puede proporcionar rutas personalizadas adicionales para analizar en la línea de comandos

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

se puede guardar la salida mediante una tubería simple

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
