---
title: Herramientas de desarrollo
seo-title: Herramientas de desarrollo
description: Para desarrollar sus aplicaciones de JCR, Apache Sling o AEM, hay una serie de conjuntos de herramientas disponibles
seo-description: Para desarrollar sus aplicaciones de JCR, Apache Sling o AEM, hay una serie de conjuntos de herramientas disponibles
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 2%

---


# Herramientas de desarrollo{#development-tools}

Para desarrollar sus aplicaciones JCR, Apache Sling o AEM, están disponibles los siguientes conjuntos de herramientas:

* un conjunto compuesto por [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) y WebDAV. CRXDE Lite está integrado en CRX/AEM y le permite realizar tareas de desarrollo estándar en el explorador. Con CRXDE Lite, puede crear y editar archivos (como .jsp y .java), carpetas, plantillas, componentes, cuadros de diálogo, nodos, propiedades y paquetes al iniciar sesión e integrarlos con SVN.

   Se recomienda CRXDE Lite cuando no tenga acceso directo al servidor CRX/AEM, cuando desarrolle una aplicación ampliando o modificando los componentes listos para usar y los paquetes de Java o cuando no necesite un depurador dedicado, la finalización del código y el resaltado de sintaxis.

* un conjunto formado por un Entorno de desarrollo integrado (por ejemplo: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md)), una herramienta de compilación (por ejemplo: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault que ha sido desarrollado por Adobe para asignar un repositorio a un sistema de archivos, un sistema de control de versiones (por ejemplo: Subversion), un sistema de seguimiento de errores (por ejemplo: Jira), un sistema central de gestión de dependencias (por ejemplo: Apache Archiva) y un sistema de automatización de la compilación (por ejemplo: Apache Continuum).

   Esta configuración le permite integrar completamente su aplicación (contenido, código, configuración) en cualquier entorno y proceso de desarrollo.El vínculo entre los diferentes elementos es la representación del sistema de archivos del repositorio a través de FileVault, ya que todas las herramientas de desarrollo mencionadas anteriormente pueden trabajar con archivos.

## Extensiones para Entornos de desarrollo integrados {#extensions-for-integrated-development-environments}

Adobe ha lanzado las siguientes extensiones:

* [Extensión de Eclipse de AEM](/help/sites-developing/aem-eclipse.md)
* [Extensión de AEM corchetes](/help/sites-developing/aem-brackets.md)
* [Extensión](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf)  de AEM IntelliJ(desde el cable de la culata)

### Otras herramientas {#other-tools}

AEM buques con otras herramientas que facilitan el desarrollo:

* [Editor de cuadros de diálogo](/help/sites-developing/dialog-editor.md)
* [Uso del traductor para administrar diccionarios](/help/sites-developing/i18n-translator.md)
* [Administración de paquetes con Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Cómo desarrollar AEM proyectos con Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Cómo construir AEM proyectos con Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Cómo desarrollar AEM proyectos usando IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Cómo utilizar la herramienta VLT](/help/sites-developing/ht-vlttool.md)
* [Cómo utilizar la herramienta Servidor proxy](/help/sites-developing/ht-proxy-server.md)
* [Herramienta de conversión de cuadro de diálogo](/help/sites-developing/dialog-conversion.md)
* [Herramienta Repo AEM](/help/sites-developing/aem-repo-tool.md)

Herramientas que facilitan la creación de nuevos proyectos:

* [Tipo de archivo del proyecto AEM](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [Plantillas de AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>El siguiente tutorial puede ser de interés para iniciar un nuevo proyecto de AEM:
>[Introducción a AEM Sites Parte 1 - Configuración del proyecto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

