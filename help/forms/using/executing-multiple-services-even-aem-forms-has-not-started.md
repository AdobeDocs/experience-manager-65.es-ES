---
title: No se ha iniciado la ejecución de varios servicios a pesar de AEM Forms.
description: Incluso si AEM Forms no se ha iniciado por completo, procesa varios servicios.
exl-id: 4ec40412-15b1-434b-a919-2cf23f48077c
source-git-commit: faa628ac4a4631564141f68f3efc9d69a67e5c40
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 4%

---

# La ejecución de varios servicios a pesar de AEM Forms no se ha iniciado por completo{#steps-to-resolve-error-after-installing-service-pack}


## Problema {#issue}

Cuando el usuario reinicia AEM Forms, los procesos de llamada actuales continúan, como el procesamiento de documentos del PDF y mucho más. Esto provoca que el reinicio del servidor de AEM Forms no se inicie correctamente.

## Se aplica a lo siguiente: {#applies-to}

La solución se aplica a AEM Forms en el servidor JEE y a AEM Forms en el servidor OSGi.

## Solución {#solution}

Para resolver el problema, agregue un argumento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` hasta [archivo por lotes](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) durante el inicio del servidor.
