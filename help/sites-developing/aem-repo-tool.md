---
title: AEM Repo Tool
description: AEM AEM La Herramienta de Repo es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor de la a través de una línea de comandos comparable a la de FTP. AEM La herramienta de repo de datos es similar a la herramienta Jackrabbit FileVault, pero es más rápida, tiene dependencias mínimas y es un script bash simple.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '281'
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
>AEM La herramienta de repositorio de datos siempre sobrescribe todo el archivo o directorio especificado.

## Descarga y documentación {#download-and-documentation}

El [AEM La herramienta de repo está disponible en GitHub a través de este vínculo](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto con instrucciones detalladas de instalación y uso.

AEM Si desea descargar la fuente de la herramienta de repo de, consulte el proyecto de GitHub vinculado a continuación.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto de herramientas en GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
