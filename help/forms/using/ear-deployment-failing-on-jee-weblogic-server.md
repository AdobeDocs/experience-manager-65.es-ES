---
title: Error en la implementación EAR en el servidor JEE WebLogic
description: Pasos para resolver el error de implementación de EAR en el servidor JEE WebLogic
exl-id: b87a9eee-ee56-4dca-b4a3-a42c91db0b4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 7%

---

# Error de implementación de EAR en el servidor JEE WebLogic {#ear-deployment-failing-on-jee-weblogic-server}

## Problema {#issue}

Cuando un usuario intenta implementar el `adobe-livecycle-weblogic.ear`, el `Null Pointer` se ha encontrado una excepción

## Se aplica a lo siguiente: {#applies-to}

Esta solución se aplica a:

* AEM Forms en el servidor WebLogic JEE versión 12.2.1.x.

## Solución {#solution}

Para resolver el problema, siga estos pasos:

1. Vaya a la `<domain_home>\bin` del servidor JEE de WebLogic instalado.

1. Edite el `setDomainEnv.cmd` o `setDomainEnv.sh` archivo, como `applicable`.

1. Busque la última incidencia de `JAVA_OPTS` y agregue `-DANTLR_USE_DIRECT_CLASS_LOADING=true` a ella. Por ejemplo, la cadena actualizada aparece de la siguiente manera:

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Guarde los cambios.
