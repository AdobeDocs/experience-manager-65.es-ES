---
title: Herramientas para desarrolladores de AEM para Eclipse
seo-title: Herramientas para desarrolladores de AEM para Eclipse
description: nulo
seo-description: nulo
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 1%

---


# Herramientas para desarrolladores de AEM para Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## Información general {#overview}

AEM Developer Tools para Eclipse es un complemento Eclipse basado en el [complemento Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) publicado bajo la Licencia Apache 2.

Oferta varias características que facilitan el desarrollo de AEM:

* Integración perfecta con instancias de AEM mediante el conector de servidor Eclipse.
* Sincronización para paquetes de contenido y OSGI.
* Compatibilidad de depuración con la capacidad de intercambio de código en caliente.
* Un sencillo arranque de AEM proyectos a través de un Asistente para la creación de proyectos específico.
* Fácil edición de las propiedades de JCR.

## Requisitos {#requirements}

Antes de utilizar las herramientas de desarrollo de AEM, debe:

* Descargue e instale [Eclipse IDE para desarrolladores de Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). AEM Developer Tools es compatible actualmente con Eclipse Kepler o versiones posteriores

* Puede utilizarse con AEM versión 5.6.1 o posterior
* Configure la instalación de eclipse para asegurarse de que tiene al menos 1 gigabyte de memoria de pila editando su archivo de configuración `eclipse.ini` como se describe en las [Preguntas más frecuentes sobre Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>En macOS, debe hacer clic con el botón derecho en **Eclipse.app** y luego seleccionar **Mostrar contenido del paquete** para encontrar su `eclipse.ini`**.**

## Cómo instalar las herramientas para desarrolladores de AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Una vez que haya cumplido los [requisitos](#requirements) anteriores, puede instalar el complemento de la siguiente manera:

1. Navegue por el [**sitio Web de herramientas de desarrollo** AEM](https://eclipse.adobe.com/aem/dev-tools/).

1. Copie el **Vínculo de instalación**.

   Tenga en cuenta que, como alternativa, puede descargar un archivo en lugar de utilizar el vínculo de instalación. Esto permite la instalación sin conexión, pero se perderán las notificaciones de actualización automática de esta manera.

1. En Eclipse, abra el menú **Ayuda**.
1. Haga clic en **Instalar nuevo software**.
1. Haga clic en **Agregar...**.
1. En **Nombre** escriba AEM Developer Tools.
1. En **Ubicación** copie la dirección URL de instalación.
1. Haga clic en **Aceptar**.
1. Compruebe los complementos **AEM** y **Sling**.
1. Haga clic en **Siguiente**. 
1. Haga clic en **Siguiente**. 
1. Acepte los acuerdos de lincesis y haga clic en **Finalizar**.
1. Haga clic en **Sí** para reiniciar Eclipse.

## Cómo importar proyectos existentes {#how-to-import-existing-projects}

>[!NOTE]
>
>Consulte [Cómo trabajar con un paquete en Eclipse cuando se descargó de AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## La perspectiva AEM {#the-aem-perspective}

Las herramientas de desarrollo AEM para Eclipse se envían con una perspectiva que le oferta el control total sobre sus proyectos e instancias de AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Proyecto de módulo múltiple de muestra {#sample-multi-module-project}

Las herramientas para desarrolladores de AEM para Eclipse incluyen un proyecto multimódulo de muestra que le ayuda a ponerse al día rápidamente con la configuración de un proyecto en Eclipse, además de servir como guía de prácticas recomendadas para varias funciones de AEM. [Obtenga más información sobre el arquetipo](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) del proyecto.

Siga estos pasos para crear el proyecto de ejemplo:

1. En el menú **Archivo** > **Nuevo** > **Proyecto**, vaya a la sección **AEM** y seleccione **AEM Ejemplo de proyecto de módulos múltiples**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Haga clic en **Siguiente**. 

   >[!NOTE]
   >
   >Este paso puede llevar un tiempo, ya que m2eclipse necesita analizar los catálogos de arquetipos.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Elija **com.adobe.granite.archetypes: sample-project-archetype : (número más alto)** del menú, luego haga clic en **Siguiente**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Rellene un **Nombre**, **Id. de grupo** y un **Id. de artefacto** para el proyecto de muestra. También puede optar por establecer algunas propiedades avanzadas.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. A continuación, debe configurar un servidor AEM al que se conectará Eclipse.

   Para utilizar la función de depurador, debe haber empezado a AEM en modo de depuración, lo que se puede lograr, por ejemplo, añadiendo lo siguiente a la línea de comandos:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Haga clic en **Finalizar**. Se crea la estructura del proyecto.

   >[!NOTE]
   >
   >En una instalación nueva (más específicamente: cuando no se hayan descargado nunca varias dependencias), es posible que el proyecto se cree con errores. En este caso, siga el procedimiento descrito en [Resolución de definiciones de proyecto no válidas](#resolving-invalid-project-definition).

## Solución de problemas {#troubleshooting}

### Resolución de definiciones de proyecto no válidas {#resolving-invalid-project-definition}

Para resolver dependencias no válidas y la definición del proyecto, siga estos pasos:

1. Seleccione todos los proyectos creados.
1. Haga clic con el botón secundario. En el menú **Maven** seleccione **Actualizar proyectos**.
1. Marque **Forzar actualizaciones de instantáneas/versiones**.
1. Haga clic en **Aceptar**. Eclipse intenta descargar las dependencias necesarias.

### Habilitación de la finalización automática de la biblioteca de etiquetas en archivos JSP {#enabling-tag-library-autocompletion-in-jsp-files}

El llenado automático de la biblioteca de etiquetas funciona de forma predeterminada, ya que se añaden al proyecto las dependencias correspondientes. Hay un problema conocido al usar el AEM Uber Jar, que no incluye los archivos tld y TagExtraInfo necesarios.

Para solucionarlo, asegúrese de que el artefacto org.apache.sling.scripting.jsp.taglib se encuentra en la ruta de clases antes del AEM Uber Jar. Para los proyectos de Maven, coloque la siguiente dependencia en el archivo pom.xml antes del archivo Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Asegúrese de agregar la versión adecuada para la implementación de AEM.

## Más información {#more-information}

El sitio web oficial del IDE de Apache Sling para Eclipse le proporciona información útil:

* La [**Guía del usuario del IDE de Apache Sling para Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentación le guiará a través de los conceptos generales, la integración del servidor y las capacidades de implementación que soportan las Herramientas de desarrollo de AEM.
* La sección [Resolución de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La [lista de problemas conocidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La siguiente documentación oficial de [Eclipse](https://eclipse.org/) puede ayudarle a configurar su entorno:

* [Introducción a Eclipse](https://eclipse.org/users/)
* [Sistema de ayuda de Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integración de Maven (m2eclipse)](https://www.eclipse.org/m2e/)

