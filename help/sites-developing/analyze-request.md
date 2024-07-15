---
title: Script de análisis de solicitud
description: El script de análisis de solicitud se realiza para facilitar el análisis de los archivos access.log y producir un informe legible para un procesamiento posterior
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Script de análisis de solicitud{#request-analysis-script}

## Descargar {#download}

Este script se crea para facilitar el análisis de los archivos de `access.log` y generar un informe legible para su procesamiento posterior.

[Obtener archivo](assets/analyse-access.sh)

## Descripción {#description}

Este script se crea para facilitar el análisis de los archivos de `access.log` y generar un informe legible para su procesamiento posterior.

Genera el número de solicitudes generales, GET frente a POST, distribución de solicitudes a lo largo del tiempo y más.

La salida está en sintaxis Markdown por lo tanto será más fácil convertirla en PDF con herramientas como pandoc o mostrarla en un navegador con complementos como Markdown viewer.

Puede analizar una ruta personalizada proporcionada en la línea de comandos.

Tomar del comentario dentro del archivo que le indica cómo ejecutarlo:

Analice CQ `access.log` extrapolando información diversa y generando un resultado de Markdown en `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

puede proporcionar rutas personalizadas adicionales para analizar en la línea de comandos

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

se puede guardar la salida mediante una tubería simple

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
