---
title: Error en la implementación EAR en el servidor JEE WebLogic
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Pasos para resolver el error de implementación de EAR en el servidor JEE WebLogic
exl-id: 109d9182-5e3f-477e-9417-abc83d5ea3bc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
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
