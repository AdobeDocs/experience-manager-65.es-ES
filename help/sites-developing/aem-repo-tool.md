---
title: AEM Repo Tool
seo-title: AEM Repo Tool
description: La herramienta AEM Repo es una solución sencilla para transferir contenido JCR entre su sistema de archivos local y el servidor de AEM a través de la línea de comandos comparable a FTP. La herramienta AEM Repo es similar a la herramienta Jackrabbit FileVault, pero es más rápida, tiene dependencias mínimas y es un script bash simple.
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

# Herramienta AEM Repositorio{#aem-repo-tool}

La herramienta AEM Repo es una solución sencilla para transferir contenido JCR entre su sistema de archivos local y el servidor de AEM a través de la línea de comandos comparable a FTP. La herramienta Repositorio de AEM es similar a la [Herramienta Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), pero es más rápido, tiene dependencias mínimas y es un script bash simple.

Esta herramienta simplifica la transferencia de archivos para el desarrollador y también se puede integrar en IntelliJ y Eclipse para que el desarrollo sea aún más eficiente.

## Información general {#overview}

Para una ruta determinada dentro de un `jcr_root` estructura filevault en el sistema de archivos, AEM herramienta Repo crea un paquete con un filtro único para todo el subárbol y lo empuja al servidor (similar a FTP) `put`), lo recupera del servidor ( `get`) o compara las diferencias ( `status` y `diff`).

La herramienta no admite varias rutas de filtro ni las de FileVault `filter.xml`.

>[!CAUTION]
>
>Tenga en cuenta que la herramienta AEM Repositorio siempre sobrescribirá todo el archivo o directorio especificado.

## Descargar y documentación {#download-and-documentation}

La variable [AEM herramienta Repositorio está disponible en GitHub a través de este enlace](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto con instrucciones detalladas de instalación y uso.

Si desea descargar la fuente de la herramienta de cesión temporal AEM, consulte el proyecto de GitHub que se muestra a continuación.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto de herramientas en GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
