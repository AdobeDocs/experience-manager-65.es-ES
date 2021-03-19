---
title: AEM herramientas para desarrolladores de Eclipse
seo-title: AEM herramientas para desarrolladores de Eclipse
description: AEM herramientas para desarrolladores de Eclipse
seo-description: nulo
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 1%

---


# AEM herramientas para desarrolladores de Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## Información general {#overview}

AEM Developer Tools para Eclipse es un complemento de Eclipse basado en el [complemento de Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) publicado con la licencia de Apache 2.

Ofrece varias funciones que facilitan el desarrollo de AEM:

* Integración perfecta con instancias de AEM mediante el conector de servidor de Eclipse.
* Sincronización para paquetes de contenido y OSGI.
* Compatibilidad con depuración con la capacidad de intercambio en caliente de código.
* Inicio sencillo de AEM proyectos a través de un Asistente para la creación de proyectos específico.
* Fácil edición de las propiedades JCR.

## Requisitos {#requirements}

Antes de utilizar las herramientas para desarrolladores de AEM, debe:

* Descargue e instale [Eclipse IDE para desarrolladores de Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). AEM herramientas para desarrolladores admiten actualmente Eclipse Kepler o versiones más recientes

* Se puede utilizar con AEM versión 5.6.1 o posterior
* Configure la instalación de eclipse para asegurarse de que tiene al menos 1 gigabyte de memoria en pilas editando su archivo de configuración `eclipse.ini` tal como se describe en las [Preguntas frecuentes sobre Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>En macOS, debe hacer clic con el botón derecho en **Eclipse.app** y seleccionar **Mostrar contenido del paquete** para encontrar el `eclipse.ini`**.**

## Instalación de las herramientas para desarrolladores de AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Una vez que haya cumplido los [requisitos](#requirements) anteriores, puede instalar el complemento de la siguiente manera:

1. Examine el [**AEM** Sitio Web de herramientas para desarrolladores](https://eclipse.adobe.com/aem/dev-tools/).

1. Copie el **Installation Link**.

   Tenga en cuenta que, de lo contrario, puede descargar un archivo en lugar de utilizar el vínculo de instalación. Esto permite la instalación sin conexión, pero de este modo se perderán las notificaciones de actualización automáticas.

1. En Eclipse, abra el menú **Help**.
1. Haga clic en **Instalar nuevo software**.
1. Haga clic en **Agregar...**.
1. En **Name** escriba AEM Herramientas para desarrolladores.
1. En **Ubicación** copie la dirección URL de instalación.
1. Haga clic en **Ok**.
1. Compruebe los complementos **AEM** y **Sling**.
1. Haga clic en **Siguiente**. 
1. Haga clic en **Siguiente**. 
1. Acepte los acuerdos de licencia y haga clic en **Finish**.
1. Haga clic en **Yes** para reiniciar Eclipse.

## Cómo importar proyectos existentes {#how-to-import-existing-projects}

>[!NOTE]
>
>Consulte [Cómo trabajar con un paquete en Eclipse cuando se descargó de AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## La perspectiva de AEM {#the-aem-perspective}

Las AEM herramientas de desarrollo para Eclipse se envían con una perspectiva que le ofrece control total sobre sus proyectos e instancias de AEM.

![Chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Proyecto de módulo múltiple de muestra {#sample-multi-module-project}

Las herramientas para desarrolladores de AEM para Eclipse incluyen un proyecto multimódulo de muestra que le ayuda a ponerse al día rápidamente con la configuración de un proyecto en Eclipse, así como que sirve como guía de prácticas recomendadas para varias funciones de AEM. [Obtenga más información sobre el tipo de archivo del proyecto](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Siga estos pasos para crear el proyecto de ejemplo:

1. En el menú **File** > **New** > **Project**, vaya a la sección **AEM** y seleccione **AEM ejemplo de proyecto de varios módulos**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Haga clic en **Siguiente**. 

   >[!NOTE]
   >
   >Este paso puede tardar un rato, ya que m2eclipse necesita analizar los catálogos de arquetipos.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Elija **com.adobe.granite.archetypes : sample-project-archetype : (número más alto)** en el menú y haga clic en **Siguiente**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Rellene un **Name**, **Group id** y un **Artifact id** para el proyecto de ejemplo. También puede optar por establecer algunas propiedades avanzadas.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. A continuación, debe configurar un servidor AEM al que se conectará Eclipse.

   Para utilizar la función Debugger, debe haber empezado a AEM en el modo de depuración, que se puede lograr, por ejemplo, añadiendo lo siguiente a la línea de comandos:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Haga clic en **Finish**. Se crea la estructura del proyecto.

   >[!NOTE]
   >
   >En una instalación nueva (más específicamente: cuando las dependencias maven nunca se hayan descargado), es posible que el proyecto se cree con errores. En este caso, siga el procedimiento descrito en [Resolver definición de proyecto no válida](#resolving-invalid-project-definition).

## Solución de problemas {#troubleshooting}

### Resolver definición de proyecto no válida {#resolving-invalid-project-definition}

Para resolver dependencias no válidas y la definición del proyecto, siga estos pasos:

1. Seleccione todos los proyectos creados.
1. Haga clic con el botón derecho. En el menú **Maven** seleccione **Actualizar proyectos**.
1. Compruebe **Forzar actualizaciones de instantáneas/versiones**.
1. Haga clic en **Aceptar**. Eclipse intenta descargar las dependencias requeridas.

### Habilitación del llenado automático de la biblioteca de etiquetas en archivos JSP {#enabling-tag-library-autocompletion-in-jsp-files}

El llenado automático de la biblioteca de etiquetas funciona de forma predeterminada, ya que se añaden las dependencias adecuadas al proyecto. Hay un problema conocido al usar el AEM Uber Jar, que no incluye los archivos tld y TagExtraInfo necesarios.

Para evitarlo, asegúrese de que el artefacto org.apache.sling.scripting.jsp.taglib esté ubicado en la ruta de clases antes del AEM Uber Jar. Para los proyectos de Maven, coloque la siguiente dependencia en el pom.xml antes de Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Asegúrese de agregar la versión adecuada para la implementación de AEM.

## Más información {#more-information}

La herramienta oficial Apache Sling IDE para el sitio web Eclipse le proporciona información útil:

* La [**Guía del usuario de Apache Sling IDE para Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentación le guiará a través de los conceptos generales, la integración del servidor y las funcionalidades de implementación compatibles con las herramientas de desarrollo de AEM.
* La [sección Resolución de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La [Lista de problemas conocidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La siguiente documentación oficial de [Eclipse](https://eclipse.org/) puede ayudarle a configurar su entorno:

* [Introducción a Eclipse](https://eclipse.org/users/)
* [Sistema de ayuda del Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integración de Maven (m2eclipse)](https://www.eclipse.org/m2e/)

