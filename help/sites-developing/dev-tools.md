---
title: Herramientas de desarrollo
seo-title: Herramientas de desarrollo
description: Para desarrollar sus aplicaciones JCR, Apache Sling o AEM, hay varios conjuntos de herramientas disponibles
seo-description: Para desarrollar sus aplicaciones JCR, Apache Sling o AEM, hay varios conjuntos de herramientas disponibles
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 3%

---


# Herramientas de desarrollo{#development-tools}

Para desarrollar sus aplicaciones JCR, Apache Sling o AEM, están disponibles los siguientes conjuntos de herramientas:

* un conjunto que consta de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) y WebDAV. El CRXDE Lite está incrustado en CRX/AEM y le permite realizar tareas de desarrollo estándar en el explorador. Con CRXDE Lite, puede crear y editar archivos (como .jsp y .java), carpetas, plantillas, componentes, cuadros de diálogo, nodos, propiedades y paquetes mientras registra e integra con SVN.

   Se recomienda utilizar CRXDE Lite cuando no tenga acceso directo al servidor CRX/AEM, cuando desarrolle una aplicación ampliando o modificando los componentes y paquetes Java predeterminados o cuando no necesite un depurador dedicado, la finalización del código y el resaltado de sintaxis.

* un conjunto que consiste en un entorno de desarrollo integrado (por ejemplo: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md)), una herramienta de compilación (por ejemplo: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault que ha sido desarrollado por Adobe para asignar un repositorio a un sistema de archivos, un sistema de control de versiones (por ejemplo: Subversión), un sistema de seguimiento de errores (por ejemplo: Jira), un sistema central de gestión de dependencias (por ejemplo: Apache Archiva) y un sistema de automatización de la compilación (por ejemplo: Apache Continuum).

   Esta configuración le permite integrar completamente su aplicación (contenido, código, configuración) en cualquier entorno y proceso de desarrollo. El vínculo entre los diferentes elementos es la representación del sistema de archivos del repositorio a través de FileVault, ya que todas las herramientas de desarrollo mencionadas pueden trabajar con archivos.

## Extensiones para entornos de desarrollo integrados {#extensions-for-integrated-development-environments}

Adobe ha lanzado las siguientes extensiones:

* [Extensión de AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Extensión de AEM Brackets](/help/sites-developing/aem-brackets.md)
* [Extensión de AEM IntelliJ](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf)  (desde el cable de encabezado)

### Otras herramientas {#other-tools}

AEM se envía con otras herramientas que facilitan el desarrollo:

* [Editor de cuadro de diálogo](/help/sites-developing/dialog-editor.md)
* [Uso del traductor para administrar diccionarios](/help/sites-developing/i18n-translator.md)
* [Administración de paquetes con Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Desarrollo de AEM proyectos con Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Cómo crear AEM proyectos con Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Desarrollo de AEM proyectos con IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Cómo utilizar la herramienta VLT](/help/sites-developing/ht-vlttool.md)
* [Cómo utilizar la herramienta Proxy Server](/help/sites-developing/ht-proxy-server.md)
* [Herramientas de modernización de AEM](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

Herramientas que facilitan la creación de nuevos proyectos:

* [Tipo de archivo del proyecto AEM](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [Plantillas AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>El siguiente tutorial puede ser de interés para iniciar un nuevo proyecto de AEM:
>[Introducción a AEM Sites, parte 1: Configuración del proyecto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

