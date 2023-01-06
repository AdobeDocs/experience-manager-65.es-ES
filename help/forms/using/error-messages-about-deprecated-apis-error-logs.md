---
title: Mensajes de error sobre API obsoletas en registros de errores
description: Mensajes de error sobre API obsoletas en registros de errores
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: ht
source-wordcount: '102'
ht-degree: 100%

---


# Mensajes de error sobre API obsoletas en registros de errores {#error-messages-about-deprecated-apis-in-error-logs}

El problema se aplica a las siguientes versiones:

* Experience Manager 6.5 Forms

## Problema {#issue}

* Los siguientes mensajes de error aparecen en el archivo error.log:
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## Resolución {#workaround}

1. Instalar [Experience Manager Forms Service Pack 13 o posterior (6.5.13.0 o posterior)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es)
1. Utilice el siguiente enlace para descargar el paquete (archivo .jar con la resolución) desde Distribución de software:

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. Abra el Administrador de configuración de Experience Manager e instale el archivo com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar descargado.

El problema se ha resuelto.