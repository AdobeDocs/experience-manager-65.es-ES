---
title: Error en la implementación EAR en el servidor JEE WebLogic
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Pasos para resolver el error de implementación de EAR en el servidor JEE WebLogic
exl-id: 109d9182-5e3f-477e-9417-abc83d5ea3bc
source-git-commit: 04cdc51ea2059daed6573987052feb893bd5f634
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 14%
---
# Error de implementación de EAR en el servidor JEE WebLogic {#ear-deployment-failing-on-jee-weblogic-server}

## Problema {#issue}

Cuando un usuario intenta implementar `adobe-livecycle-weblogic.ear`, se encuentra la excepción `Null Pointer`

## Se aplica a {#applies-to}

Esta solución se aplica a:

* AEM Forms en el servidor WebLogic JEE versión 12.2.1.x.

## Solución {#solution}

Para resolver el problema, siga estos pasos:

1. Vaya al directorio `<domain_home>\bin` del servidor JEE de WebLogic instalado.

1. Edite el archivo `setDomainEnv.cmd` o `setDomainEnv.sh` como `applicable`.

1. Busque la última incidencia de `JAVA_OPTS` y agréguele `-DANTLR_USE_DIRECT_CLASS_LOADING=true`. Por ejemplo, la cadena actualizada aparece de la siguiente manera:

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Guarde los cambios.
