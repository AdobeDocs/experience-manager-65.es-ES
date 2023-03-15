---
title: AEM Repo Tool
seo-title: AEM Repo Tool
description: AEM AEM La Herramienta de Repo es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor de la a través de una línea de comandos comparable a la de FTP. AEM La herramienta de repo de datos es similar a la herramienta Jackrabbit FileVault, pero es más rápida, tiene dependencias mínimas y es un script bash simple.
seo-description: The AEM Repo Tool is a simple solution to transfer JCR content between your local filesystem and the AEM server via the command line comparable to FTP. The AEM Repo Tool is similar to the Jackrabbit FileVault tool, but is faster, has minimal dependencies, and is a simple bash script.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# AEM Repo Tool{#aem-repo-tool}

AEM AEM La Herramienta de Repo es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor de la a través de una línea de comandos comparable a la de FTP. AEM La herramienta de repo de datos es similar a la de la variable [Herramienta Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), pero es más rápido, tiene dependencias mínimas y es un script bash simple.

Esta herramienta simplifica la transferencia de archivos para el desarrollador y también se puede integrar en IntelliJ y Eclipse para hacer el desarrollo aún más eficiente.

## Información general {#overview}

Para una ruta determinada dentro de un `jcr_root` AEM filevault en el sistema de archivos, la herramienta de repo crea un paquete con un solo filtro para todo el subárbol y lo envía al servidor (similar al FTP) `put`), lo recupera del servidor ( `get`) o compara las diferencias ( `status` y `diff`).

La herramienta no admite varias rutas de filtro ni de FileVault `filter.xml`.

>[!CAUTION]
>
>AEM Tenga en cuenta que la herramienta de repo de siempre sobrescribirá todo el archivo o directorio especificado.

## Descarga y documentación {#download-and-documentation}

El [AEM La herramienta de repo está disponible en GitHub a través de este vínculo](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto con instrucciones detalladas de instalación y uso.

AEM Si desea descargar la fuente de la herramienta de repo de, consulte el proyecto de GitHub vinculado a continuación.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto de herramientas en GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
