---
title: No se ha iniciado la ejecución de varios servicios a pesar de AEM Forms.
description: Incluso si AEM Forms no se ha iniciado por completo, procesa varios servicios.
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 4%

---

# La ejecución de varios servicios a pesar de AEM Forms no se ha iniciado por completo{#steps-to-resolve-error-after-installing-service-pack}


## Problema {#issue}

Cuando el usuario reinicia AEM Forms, los procesos de llamada actuales continúan, como el procesamiento de documentos del PDF y mucho más. Esto provoca que el reinicio del servidor de AEM Forms no se inicie correctamente.

## Se aplica a lo siguiente: {#applies-to}

La solución se aplica a AEM Forms en el servidor JEE y a AEM Forms en el servidor OSGi.

## Solución {#solution}

Para resolver el problema, los usuarios agregan un argumento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` hasta [archivo por lotes](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) durante el inicio del servidor.





