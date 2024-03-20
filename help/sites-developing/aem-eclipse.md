---
title: Herramientas para desarrolladores de AEM para Eclipse
description: Obtenga información sobre las herramientas para desarrolladores de Adobe Experience Manager para Eclipse.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 3%

---

# Herramientas para desarrolladores de AEM para Eclipse{#aem-developer-tools-for-eclipse}

![AEM Motivo de imagen circular para herramientas de desarrollador de para Eclipse.](do-not-localize/chlimage_1-9.png)

## Información general {#overview}

AEM &quot;Herramientas para desarrolladores de&quot; es un complemento de Eclipse basado en [Complemento Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lanzado bajo la licencia Apache 2.

AEM Ofrece varias funciones que facilitan el desarrollo de la:

* AEM Integración perfecta con las instancias de la a través del conector del servidor Eclipse.
* Sincronización para paquetes OSGI y de contenido.
* Compatibilidad de depuración con la capacidad de intercambio en caliente de código.
* Bootstrap AEM simple de proyectos de la mediante un asistente de creación de proyectos específico.
* Edición sencilla de propiedades JCR.

## Requisitos  {#requirements}

AEM Antes de usar las herramientas para desarrolladores de, haga lo siguiente:

* Descargar e instalar [Eclipse IDE para desarrolladores de Java™ EE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). AEM Actualmente, las herramientas para desarrolladores son compatibles con Eclipse Kepler o posterior

* AEM Se puede utilizar con la versión 5.6.1 o posterior del
* Configure la instalación de Eclipse para asegurarse de que tiene al menos 1 GB de memoria de pila editando su `eclipse.ini` como se describe en la sección [Preguntas frecuentes sobre Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>En macOS, haga clic con el botón derecho **Eclipse.app**, y luego seleccione **Mostrar contenido del paquete** para encontrar su `eclipse.ini`.

## AEM Cómo instalar las herramientas para desarrolladores de para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Una vez que haya completado la [requisitos](#requirements) más arriba, puede instalar el complemento de la siguiente manera:

1. Examine la **AEM Herramientas para desarrolladores de** sitio web en `https://eclipse.adobe.com/aem/dev-tools/`.

1. Copie el **Vínculo de instalación**.

   También puede descargar un archivo en lugar de utilizar el vínculo de instalación. Al hacerlo, se puede realizar la instalación sin conexión, pero se pierden las notificaciones de actualización automática.

1. En Eclipse, abra el **Ayuda** menú.
1. Clic **Instalar nuevo software**.
1. Clic **Agregar...**.
1. Entrada **Nombre** AEM escriba Herramientas para desarrolladores.
1. Entrada **Ubicación** copie la dirección URL de instalación.
1. Clic **Ok**.
1. Marque ambos **AEM** y **Sling** complementos.
1. Haga clic en **Siguiente**.
1. Haga clic en **Siguiente**.
1. Acepte los acuerdos de licencia y haga clic en **Finalizar**.
1. Clic **Sí** para reiniciar Eclipse.

## Cómo Importar Proyectos Existentes {#how-to-import-existing-projects}

>[!NOTE]
>
>Consulte [AEM Cómo trabajar con un paquete en Eclipse cuando se descargó desde el servidor de correo electrónico de](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## AEM La perspectiva de la {#the-aem-perspective}

AEM AEM Las herramientas de desarrollo de la para Eclipse se envían con una perspectiva que le ofrece control total sobre sus proyectos e instancias de la.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Ejemplo de proyecto de varios módulos {#sample-multi-module-project}

AEM Las &quot;herramientas para desarrolladores&quot; incluyen un proyecto de muestra y varios módulos que le ayuda a ponerse al día rápidamente con la configuración de un proyecto en Eclipse. AEM También sirve como guía de prácticas recomendadas sobre varias funciones de la. [Más información sobre el Arquetipo del proyecto](https://github.com/adobe/aem-project-archetype).

Para crear el proyecto de ejemplo, complete los siguientes pasos:

1. En el **Archivo** > **Nuevo** > **Proyecto** , vaya a la **AEM** y seleccione **AEM Ejemplo de proyecto de varios módulos**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Haga clic en **Siguiente**.

   >[!NOTE]
   >
   >Este paso puede tardar un poco porque m2eclipse debe analizar los catálogos de tipo de archivo.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Elegir **com.adobe.granite.archetypes : sample-project-archetype : (número más alto)** en el menú, haga clic en **Siguiente**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Rellene un **Nombre**, **Identificador de grupo**, y un **ID del artefacto** para el proyecto de ejemplo. También puede optar por establecer algunas propiedades avanzadas.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. AEM Ahora configure un servidor de la al que se pueda conectar Eclipse.

   AEM Para utilizar la función del depurador, asegúrese de empezar a utilizar el modo de depuración, que se puede conseguir añadiendo lo siguiente a la línea de comandos:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Clic **Finalizar**. Se crea la estructura del proyecto.

   >[!NOTE]
   >
   >En una instalación nueva (más específicamente: cuando las dependencias de Maven nunca se han descargado), puede obtener el proyecto creado con errores. En este caso, siga el procedimiento descrito en [Resolver definición de proyecto no válida](#resolving-invalid-project-definition).

## Solución de problemas {#troubleshooting}

### Resolver definición de proyecto no válida {#resolving-invalid-project-definition}

Para resolver dependencias no válidas y la definición del proyecto, siga estos pasos:

1. Seleccione todos los proyectos creados.
1. Haga clic con el botón derecho. En el menú **Maven**, seleccione **Actualizar proyectos**.
1. Marque **Forzar actualizaciones de instantáneas/versiones**.
1. Haga clic en **Aceptar**. Eclipse intenta descargar las dependencias requeridas.

### Habilitar la finalización automática de bibliotecas de etiquetas en archivos JSP {#enabling-tag-library-autocompletion-in-jsp-files}

La finalización automática de la biblioteca de etiquetas funciona de forma predeterminada, dado que se añaden las dependencias adecuadas al proyecto. AEM Hay un problema conocido al usar el Jar de Uber de la, que no incluye los archivos tld y TagExtraInfo necesarios.

AEM Para solucionarlo, asegúrese de que el artefacto org.apache.sling.scripting.jsp.taglib está en la ruta de clase antes de Uber Jar de la interfaz de usuario de la aplicación de comandos de usuario (CLS) de Uber Jar. Para proyectos de Maven, coloque la siguiente dependencia en el archivo pom.xml antes de Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

AEM Asegúrese de añadir la versión adecuada para la implementación de la aplicación de.

## Más información {#more-information}

La página web oficial de Apache Sling IDE tooling for Eclipse le proporciona información útil:

* El [**Herramientas del IDE de Apache Sling para Eclipse** Guía del usuario](https://sling.apache.org/documentation/development/ide-tooling.html)AEM , esta documentación le guía a través de los conceptos generales, la integración del servidor y las capacidades de implementación admitidas por las herramientas de desarrollo de la.
* El [Sección Resolución de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* El [Lista de problemas conocidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

El siguiente funcionario [Eclipse](https://www.eclipse.org/) La documentación de puede ayudarle a configurar su entorno:

* [Introducción a Eclipse](https://eclipseide.org/getting-started/)
* [Sistema de ayuda de Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integración de Maven (m2eclipse)](https://www.eclipse.org/m2e/)
