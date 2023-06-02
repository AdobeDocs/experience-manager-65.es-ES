---
title: Error en la implementación EAR en el servidor JEE WebLogic
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Pasos para resolver el error de implementación de EAR en el servidor JEE WebLogic
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 6%

---


# Error de implementación de EAR en el servidor JEE WebLogic {#ear-deployment-failing-on-jee-weblogic-server}

## Problema {#issue}

Cuando un usuario intenta implementar el `adobe-livecycle-weblogic.ear`, el `Null Pointer` se ha encontrado una excepción

## Se aplica a {#applies-to}

Esta solución se aplica a:

* AEM Forms en el servidor WebLogic JEE versión 12.2.1.x.

## Solución {#solution}

Para resolver el problema, siga estos pasos:

1. Vaya a la `<domain_home>\bin` del servidor JEE de WebLogic instalado.

1. Edite el `setDomainEnv.cmd` o `setDomainEnv.sh` archivo, como `applicable`.

1. Busque la última incidencia de `JAVA_OPTS` y agregue `-DANTLR_USE_DIRECT_CLASS_LOADING=true` a ella. Por ejemplo, la cadena actualizada aparece de la siguiente manera:

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Guarde los cambios.


