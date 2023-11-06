---
title: ¿Cómo se habilitan los componentes principales de Forms AEM adaptable en Forms de la versión 6.5 de?
description: Guía paso a paso para ayudarle a habilitar los componentes principales de Forms AEM adaptables en un entorno de Forms de 6.5.
keywords: Habilite Componentes principales, Componentes principales, Forms adaptable, Componentes principales en 6.5, Componentes principales de Forms adaptable en 6.5, Componentes principales de AF en 6.5, Componentes principales de Forms en 6.5, y Componentes principales de AEM AEM AEM en 6.5, y en la versión 6.5, respectivamente.
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
source-git-commit: 1da3abac8a7f09d41127818a5abacf29524f1365
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 52%

---

# Habilitación de los componentes principales de Forms AEM adaptable en Forms de la versión 6.5 de {#enable-adaptive-forms-core-components}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=es) |
| AEM 6.5 | Este artículo |

**Se aplica a:** ✅ Componentes Principales Del Formulario Adaptable ❎ Componentes Básicos Del Formulario Adaptable.

Al habilitar los componentes principales de Forms adaptable, puede empezar a crear, publicar y entregar contenido [Componentes principales basados en Forms adaptable](create-an-adaptive-form-core-components.md) y [Forms adaptable sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es) AEM desde su entorno de Forms de 6.5.

Para habilitar los componentes principales de Forms AEM adaptable en su entorno de Forms de la versión 6.5 de la plataforma de datos de, configure e implemente un [AEM Tipo de archivo 41 o posterior de](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) proyecto basado en (con las opciones de formularios activadas) en todas las instancias de autor y publicación.

AEM AEM Este artículo contiene instrucciones detalladas para configurar e implementar un proyecto basado en el tipo de archivo 41 o posterior en su entorno de Forms de la versión 6.5 de para habilitar los componentes principales de Forms adaptables. Puede consultar la lista siguiente para **AEM,5** versiones compatibles para habilitar los componentes principales de Forms:

## Requisitos previos {#prerequisites}

Antes de habilitar los componentes principales de Forms AEM adaptable en un entorno de Forms de 6.5:

* [Actualizar al Service Pack 16 de AEM 6.5 Forms (6.5.16.0) o posterior](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=es).

* Instalar la última versión de [Apache Maven](https://maven.apache.org/download.cgi).

* Instale un editor de texto sin formato. Por ejemplo, Microsoft Visual Studio Code.

## Crear e implementar el último proyecto basado en el arquetipo de AEM

Para crear un proyecto basado en el arquetipo de AEM 41 o [posterior](https://github.com/adobe/aem-project-archetype) e implementarlo en todas las instancias de autor y publicación:

1. AEM Inicie sesión en el equipo, aloje y ejecute la instancia de Forms de.5 como administrador.
1. AEM Abra el símbolo del sistema o el terminal y ejecute el siguiente comando para crear proyecto Archetype (con las opciones de formularios habilitadas):

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux o Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   Cuando ejecute el comando anterior, asegúrese de tener en cuenta los siguientes puntos:

   * No cambie el valor del `aemVersion` propiedad de `6.5.15.0` a cualquier otra cosa.

   * Configure las variables `archetypeVersion` propiedad a `41` o más tarde. Para ver la versión más reciente, consulte la sección Requisitos del sistema en [AEM Tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype) documentación.

   * Actualice el comando para reflejar los valores específicos de su entorno, incluido el `appTitle`, `appId`, y `groupId`. Además, establezca el valor de  `includeFormsenrollment` propiedad a `y`. Si utiliza el Portal de Forms, establezca la opción `includeExamples=y` para que incluya los componentes principales del Portal de Forms en el proyecto.


1. (Solo para proyectos basados en la versión 41 del arquetipo) Una vez creado el proyecto de arquetipo de AEM, habilite las temáticas para formularios adaptables basados en componentes principales. Para habilitar las temáticas, haga lo siguiente:

   1. Abra la [Carpeta de proyecto de arquetipo de AEM]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html para editarla:

   1. Agregue el siguiente código en la línea 21:

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Agregue el código mencionado anteriormente en la línea 21](/help/forms/using/assets/code-to-enable-themes.png)

   1. Guarde y cierre el archivo.

1. Actualizar el proyecto para que incluya la última versión de los componentes principales de Forms:

   1. Abra la [Carpeta de proyecto de arquetipo de AEM]/pom.xml para editarla.
   1. Establecer versión de `core.forms.components.version` y `core.forms.components.af.version` hasta [Últimos componentes principales de Forms](https://github.com/adobe/aem-core-forms-components/tree/release/650#system-requirements) y se aseguran de que ambas tengan la misma versión que **Componentes principales de Forms** mencionado en la tabla y establezca la versión de `core.wcm.components.version` tal como se indica en la **Componentes principales de WCM**.

      >[!WARNING]
      >
      >* Al crear un proyecto de tipo de archivo con `version 45`, el [AEM Carpeta de proyecto de tipo de archivo]/pom.xml establece inicialmente la versión de los componentes principales de formularios en `1.1.28`. Antes de crear o implementar el proyecto Archetype, actualice la versión de los componentes principales de Forms a `1.1.26`.


      >[!NOTE]
      >
      >* Si configura cualquier otra topología, asegúrese de agregar las direcciones URL de envío, de relleno previo y de otro tipo a la lista de permitidos en la capa de Dispatcher.

   1. Guarde y cierre el archivo.


1. Una vez que el proyecto de arquetipo de AEM se haya creado correctamente, cree el paquete de implementación para su entorno. Haga clic para generar el paquete:

   1. Vaya al directorio raíz del proyecto del arquetipo de AEM.

   1. Ejecute el siguiente comando para compilar el proyecto de arquetipo de AEM para su entorno:

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   Una vez que el proyecto de arquetipo de AEM se haya compilado correctamente, se generará un paquete de AEM. Puede encontrar el paquete en [Carpeta de proyecto de arquetipo de AEM]\all\target\[appid].all-[versión].zip

1. Utilice el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es) para implementar la [Carpeta de proyecto de arquetipo de AEM]\all\target\[appid].all-[versión].zip en el entorno de instancias de autor y publicación.

>[!NOTE]
>
>
>
> * Si tiene dificultades para acceder al cuadro de diálogo de inicio de sesión en una instancia de publicación, para instalar el paquete a través del Administrador de paquetes, intente utilizar la URL: `http://[Publish Server URL]:[PORT]/system/console` para iniciar sesión. Esto permite acceder a la página de inicio de sesión en una instancia de publicación, lo que le permite continuar con el proceso de instalación.
> * No elimine ni descarte el proyecto Archetype después de implementarlo en su entorno. El proyecto de tipo de archivo es necesario para agregar temas personalizados y nuevos de componentes principales de Forms adaptables a su entorno.

Los componentes principales están habilitados para su entorno. Se implementan una plantilla de formularios adaptables basados en componentes principales en blanco y una temática de Lienzo 3.0 que le permiten [crear formularios adaptables basados en los componentes principales](create-an-adaptive-form-core-components.md).

## Preguntas frecuentes

### ¿Qué son los componentes principales?

Los [componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) son un conjunto de componentes estandarizados de la administración de contenido web (WCM) para AEM con el objetivo de acelerar el tiempo de desarrollo y reducir el coste de mantenimiento de sus sitios web.

### ¿Qué funcionalidades completas se añaden al habilitar los componentes principales?


Cuando los componentes principales de formularios adaptables se habilitan para su entorno, se agrega a este una plantilla de formulario adaptable basada en componentes principales en blanco y una temática de Lienzo 3.0. Tras habilitar los componentes principales de formularios adaptables para su entorno, puede:

* Crear componentes principales basados en formularios adaptables.
* Crear componentes principales basados en plantillas de formulario adaptable.
* Crear temáticas personalizadas para componentes principales basadas en plantillas de formulario adaptable.
* Proporcione representaciones JSON de un formulario adaptable basado en componentes principales a canales como móvil, web, apps nativas y servicios que requieren la representación sin encabezado de un formulario.

## Siguientes pasos

* [Crear un formulario adaptable basado en componentes principales](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Crear o agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Crear temáticas para componentes principales basados en Forms adaptable](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Crear una plantilla para componentes principales basados en Forms adaptable](template-editor.md)
