---
title: Herramientas de desarrollo
seo-title: Development Tools
description: AEM Para desarrollar las aplicaciones JCR, Apache Sling o de la aplicación de la, hay disponibles varios conjuntos de herramientas
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: 4967a6d9ad92272a1ff442456fe65de51cc46a73
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 3%

---

# Herramientas de desarrollo{#development-tools}

AEM Para desarrollar las aplicaciones JCR, Apache Sling o, están disponibles los siguientes conjuntos de herramientas:

* un conjunto formado por [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) y WebDAV. CRXDE Lite AEM está incrustado en CRX/y le permite realizar tareas de desarrollo estándar en el explorador. Con CRXDE Lite, puede crear y editar archivos (como .jsp y .java), carpetas, plantillas, componentes, cuadros de diálogo, nodos, propiedades y paquetes al registrar e integrar con SVN.

   Se recomienda utilizar CRXDE Lite AEM cuando no tenga acceso directo al servidor CRX/, cuando desarrolle una aplicación ampliando o modificando los componentes predeterminados y los paquetes Java o cuando no necesite un depurador dedicado, la finalización del código y el resaltado de sintaxis.

* un conjunto formado por un entorno de desarrollo integrado (por ejemplo: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md)), una herramienta de compilación (por ejemplo: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault, que ha sido desarrollado por el Adobe para asignar un repositorio a un sistema de archivos, un sistema de control de versiones (por ejemplo: Subversion), un sistema de seguimiento de errores (por ejemplo: Jira), un sistema de administración de dependencias central (por ejemplo: Apache Archiva) y un sistema de automatización de compilación (por ejemplo: Apache Continuum).

   Esta configuración le permite integrar completamente su aplicación (contenido, código, configuración) en cualquier entorno y proceso de desarrollo. El vínculo entre los diferentes elementos es la representación del sistema de archivos del repositorio a través de FileVault, ya que todas las herramientas de desarrollo mencionadas anteriormente pueden trabajar con archivos.

## Extensiones para entornos de desarrollo integrados {#extensions-for-integrated-development-environments}

El Adobe ha lanzado las siguientes extensiones:

* [AEM Extensión de Eclipse de](/help/sites-developing/aem-eclipse.md)
* [AEM Extensión de corchetes de](/help/sites-developing/aem-brackets.md)

### Otras herramientas {#other-tools}

AEM Se envía con otras herramientas que facilitan el desarrollo:

* [Editor de diálogos](/help/sites-developing/dialog-editor.md)
* [Usar Translator para administrar diccionarios](/help/sites-developing/i18n-translator.md)
* [Administración de paquetes mediante Maven](/help/sites-developing/vlt-mavenplugin.md)
* [AEM Cómo desarrollar proyectos de mediante Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [AEM Cómo crear proyectos de con Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [AEM Cómo desarrollar proyectos de con IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Cómo utilizar la herramienta VLT](/help/sites-developing/ht-vlttool.md)
* [Cómo utilizar la herramienta de servidor proxy](/help/sites-developing/ht-proxy-server.md)
* [Herramientas de modernización de AEM](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

Herramientas que facilitan la creación de nuevos proyectos:

* [Tipo de archivo del proyecto AEM](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Plantillas de Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>AEM El siguiente tutorial puede ser de interés para iniciar un nuevo proyecto de:
>[Introducción a AEM Sites, parte 1: Configuración del proyecto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
