---
title: AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento.
description: AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento en el servidor JEE y en el servidor OSGi.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 3%

---

# AEM Forms Server comienza a procesar los documentos incluso antes de que todos los servicios estén en funcionamiento{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problema {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Antes de que el servidor de AEM Forms esté completamente activo y todas las aplicaciones estén en funcionamiento, AEM Forms Server comienza a procesar los documentos.


## Se aplica a lo siguiente: {#applies-to}

La solución se aplica a AEM Forms en el servidor JEE y a AEM Forms en el servidor OSGi.

## Solución {#solution}

Para resolver el problema, agregue un argumento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` a la [archivo por lotes](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) durante el inicio del servidor.
