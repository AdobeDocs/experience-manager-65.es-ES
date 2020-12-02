---
title: Herramienta Repo AEM
seo-title: Herramienta Repo AEM
description: La herramienta Repo de AEM es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor AEM a través de la línea de comandos comparable a FTP. La herramienta AEM Repo es similar a la herramienta Jackrabbit FileVault, pero es más rápida, tiene dependencias mínimas y es un script bash simple.
seo-description: La herramienta Repo de AEM es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor AEM a través de la línea de comandos comparable a FTP. La herramienta AEM Repo es similar a la herramienta Jackrabbit FileVault, pero es más rápida, tiene dependencias mínimas y es un script bash simple.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Herramienta Repo AEM{#aem-repo-tool}

La herramienta Repo de AEM es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor AEM a través de la línea de comandos comparable a FTP. La herramienta AEM Repo es similar a la [herramienta Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), pero es más rápida, tiene dependencias mínimas y es un script bash simple.

Esta herramienta simplifica la transferencia de archivos para el desarrollador y también se puede integrar en IntelliJ y Eclipse para hacer el desarrollo aún más eficiente.

## Información general {#overview}

Para una ruta determinada dentro de una estructura de `jcr_root` filevault en el sistema de archivos, AEM herramienta Repo crea un paquete con un filtro único para todo el subárbol y lo envía al servidor (similar a FTP `put`), lo obtiene del servidor ( `get`) o compara las diferencias ( `status` y `diff`).

La herramienta no admite varias rutas de filtro ni las `filter.xml` de FileVault.

>[!CAUTION]
>
>Tenga en cuenta que la herramienta Repo AEM siempre sobrescribirá el archivo o directorio especificado.

## Descargar y documentación {#download-and-documentation}

La [Herramienta Repo de AEM está disponible en GitHub a través de este vínculo](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto con instrucciones detalladas de instalación y uso.

Si desea descargar la fuente de la herramienta Repo AEM, consulte el proyecto GitHub que se encuentra a continuación.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto de herramientas en GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

