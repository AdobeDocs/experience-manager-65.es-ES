---
title: Crear o personalizar temáticas de formularios adaptables
seo-title: How to create a theme for Adaptive Forms Core Components?
description: Aprenda a crear o personalizar temáticas para componentes principales de Forms adaptables mediante especificaciones de BEM
seo-description: Learn to create or customize themes for Adaptive Forms Core Components using BEM specifications
keywords: AEM crear una temática de componentes principales de formularios adaptables, crear una temática nueva, personalizar una temática, cargar una temática nueva, utilizar una temática en formularios, eliminar una temática, crear una temática en formularios 6.5 de
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 00f8b2c72aab37a57ab76e684f432250d2de3470
workflow-type: tm+mt
source-wordcount: '1968'
ht-degree: 9%

---


# Crear o personalizar una temática de formulario adaptable {#introduction-to-theme}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | Este artículo |
| AEM as a Cloud Service | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |

**Se aplica a:** ❎ de componentes principales de formulario adaptable ✅ [Componentes de base de formulario adaptable](/help/forms/using/themes.md).

En AEM Forms AEM 6.5, una temática es una biblioteca de cliente de que se utiliza para definir los estilos (aspecto y presentación) de un formulario adaptable. Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar una temática, el estilo especificado se refleja en los componentes correspondientes. Una temática se administra de forma independiente sin hacer referencia a un formulario adaptable y se puede reutilizar en varios formularios adaptables de Forms.

## Temas disponibles {#available-standard-theme}

AEM entorno de 6.5 proporciona los temas siguientes para los componentes principales basados en Forms adaptable:

* [Tema de lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

## Comprender la estructura de las temáticas {#understanding-structure-of-theme}

Una temática es un paquete que incluye el archivo CSS, los archivos JavaScript y los recursos (como iconos) que definen el estilo de su Forms adaptable. Una temática de formulario adaptable sigue una organización específica, que consta de los siguientes componentes:

* `src/theme.scss`: Esta carpeta incluye el archivo CSS que tiene un impacto amplio en toda la temática. Sirve como una ubicación centralizada para definir y administrar el estilo y el comportamiento de la temática. Al realizar ediciones en este archivo, puede realizar cambios que se apliquen universalmente en toda la temática, lo que influye en el aspecto y la funcionalidad tanto de las páginas de AEM Sites como de Forms adaptable.

* `src/site`AEM : esta carpeta contiene archivos CSS que se aplican a toda la página de un sitio de la red de distribución de contenido (CSS) de la página de un sitio de. AEM Estos archivos constan de código y estilos que afectan a la funcionalidad y al diseño generales de la página de su sitio de la red de la red de distribución de contenido (SITE) de su sitio de la red de distribución de contenido (OSGi). Cualquier modificación realizada aquí se reflejará en todas las páginas del sitio.

* `src/components`AEM : los archivos CSS de esta carpeta están diseñados para componentes principales individuales de la. Cada carpeta dedicada para un componente incluye una `.scss` que aplica estilo a ese componente en particular dentro de un formulario adaptable. Por ejemplo, la variable `/src/components/button/_button.scss` contiene información de estilo para el componente Botón de Forms adaptable.

  ![Estructura de la temática Lienzo](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`: esta carpeta contiene archivos estáticos como iconos, logotipos y fuentes. Estos recursos se utilizan para mejorar los elementos visuales y el diseño general del tema.

## Crear una temática

AEM Forms 6.5 proporciona las siguientes temáticas estándar para componentes principales basados en Forms adaptable.

* [Tema de lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

Puede [personalice cualquiera de estas temáticas estándar para crear una temática](#customize-a-theme-core-components).

## Personalizar una temática {#customize-a-theme-core-components-based-adaptive-forms}

La personalización de una temática hace referencia al proceso de modificación y personalización de la apariencia de una temática. Al personalizar una temática, se realizan cambios en los elementos de diseño, el diseño, los colores, la tipografía y, a veces, en el código subyacente. Esto le permite crear un aspecto único y personalizado para su sitio web o aplicación, al tiempo que mantiene la estructura y la funcionalidad básicas proporcionadas por la temática.

>[!NOTE]
>
> * Utilice el Administrador de paquetes para implementar un tema en todas las instancias de autor y publicación.
> * Una biblioteca de cliente de temas se importa o exporta mediante el Administrador de paquetes como cualquier otro paquete.

### Requisitos previos para personalizar una temática {#prerequisites}

* [Habilitar los componentes principales de formularios adaptables para su entorno.](/help/forms/using/enable-adaptive-forms-core-components.md)

* Instale la última versión de [Apache Maven.](https://maven.apache.org/download.cgi) Apache Maven es una herramienta de automatización de compilaciones que se utiliza comúnmente en proyectos Java™. La instalación de la última versión garantiza que tenga las dependencias necesarias para la personalización de temáticas.

* Obtenga información sobre cómo crear un [biblioteca de cliente en Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=es). AEM proporciona bibliotecas de cliente, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente.

* Instale un editor de texto sin formato. Por ejemplo, Microsoft® Visual Studio Code. Utilizar un editor de texto sin formato como Microsoft® Visual Studio Code proporciona un entorno fácil de usar para editar y modificar archivos de temas.

* Asegúrese de que su entorno de AEM Forms esté en funcionamiento.

### Consideraciones para personalizar una temática {#consideration}

* Asegúrese de utilizar [el tipo de archivo del proyecto utilizado para habilitar los componentes principales de Forms adaptable](/help/forms/using/enable-adaptive-forms-core-components.md) en su entorno para personalizar las temáticas.

* Al publicar un formulario adaptable, las bibliotecas de cliente no se publican automáticamente en la instancia de publicación. Asegúrese de publicar manualmente la biblioteca de cliente a la que se hace referencia en un formulario adaptable en los entornos de publicación.

* El Adobe recomienda no cambiar los nombres de clase de las bibliotecas de cliente.

### Personalizar una temática {#customize-a-theme-core-components}

Crear o personalizar una temática es un proceso de varios pasos. Realice los pasos en el orden indicado para crear o personalizar la temática:

1. [Clonar una temática estándar](#clone-git-repo-of-theme)
1. [Personalizar el aspecto de la temática](#customize-the-theme)
1. [Preparar el tema para la implementación local](#generate-the-clientlib)
1. [Implementar el tema en un entorno local](#deploy-the-theme-on-a-local-environment)
1. [Implementar el tema en el entorno de producción](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

Los ejemplos proporcionados en el documento se basan en la variable **Lienzo** tema, pero puede clonar cualquier tema estándar y personalizarlo con las mismas instrucciones. Estas instrucciones se aplican a cualquier tema, lo que le permite modificarlas según sus necesidades específicas.

#### 1. Clone el repositorio Git de la temática {#clone-git-repo-of-theme}

Para clonar una temática estándar para componentes principales basados en Forms adaptable, elija una de las siguientes temáticas estándar:

* [Tema de lienzo](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

Siga estas instrucciones para clonar una temática estándar:

1. Abra el símbolo del sistema o la ventana de terminal en su entorno de desarrollo local.

1. Ejecute el `git clone` para clonar una temática.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Reemplace el [Ruta del repositorio Git de la temática] con la URL real del repositorio de Git correspondiente de la temática

   Por ejemplo, para clonar la temática Lienzo, ejecute el siguiente comando:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. Seleccione **Confiar en los autores de todos los archivos de la carpeta principal** y haga clic en **Sí, confío en los autores**.

Después de ejecutar el comando correctamente, tiene una copia local del tema disponible en el equipo en el  `aem-forms-theme-canvas` carpeta.

#### 2. Personalizar la temática {#customize-the-theme}

Tiene la flexibilidad de personalizar componentes individuales o realizar cambios en el nivel de tema mediante las variables globales de un tema. La modificación de variables globales tiene un efecto en cascada en todos los componentes individuales. Por ejemplo, puede utilizar variables globales para cambiar el color del borde de todos los componentes de un formulario adaptable o aplicar un color de relleno vibrante a los botones de llamada a la acción (CTA). Puede hacer lo siguiente:

* [Establecer estilos de nivel de tema](#theme-customization-global-level)

* [Definir estilos de nivel de componente](#component-based-customization)

##### Establecer estilos de nivel de tema {#theme-customization-global-level}

El `variable.scss` contiene las variables globales de la temática. Al actualizar estas variables, puede realizar cambios relacionados con los estilos en el nivel de la temática. Para aplicar estilos de nivel de tema, siga estos pasos:

1. Abra el archivo `<your-theme-sources>/src/site/_variables.scss` para editarlo.
1. Cambie el valor de cualquier propiedad. Por ejemplo, el color de error predeterminado es rojo. Para cambiar el color del error de rojo a azul, cambie el código hexadecimal de color del `$error`variable. Por ejemplo, `$error: #196ee5`.

   ![Ejemplo: Color de error establecido en azul](/help/forms/using/assets/theme-level-changes.png)

1. Guarde y cierre el archivo.


Del mismo modo, puede utilizar la variable `variable.scss` archivo para establecer la familia y el tipo de fuente, los colores de la temática y la fuente, el tamaño de fuente, el espaciado del tema, el icono de error, los estilos de borde del tema y más variables que afectan a varios componentes del formulario adaptable.

##### Definir estilos de nivel de componente {#component-based-customization}

También tiene la opción de personalizar la fuente, el color, el tamaño y otras propiedades CSS de componentes principales específicos del formulario adaptable, como botones, casillas de verificación, contenedores, pies de página, etc. Al editar el archivo CSS asociado al componente específico, puede alinear su estilo con la marca de su organización. Para personalizar el estilo de un componente, siga estos pasos:

1. Abra el archivo `<your-theme-sources>/src/components/<component>/<component.scss>` para editar. Por ejemplo, para cambiar el color de fuente del componente Botón, abra el `<your-theme-sources>/src/components/button/button.scss`, archivo .
1. Cambie el valor de cualquiera según sus necesidades. Por ejemplo, para cambiar el color del componente Botón al pasar el ratón por encima a Verde, cambie el valor del `color: $white` propiedad en el `cmp-adaptiveform-button__widget:hover` de clase a código hexadecimal #12b453 o cualquier otro tono de verde. El código final tiene el siguiente aspecto:

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. Guarde y cierre el archivo.

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>
>
> Cuando se define un estilo tanto en el nivel de tema como de componente, el estilo definido en el nivel de componente tiene prioridad.


#### 3. Preparar el tema para la implementación {#generate-the-clientlib}

AEM Para implementar una temática en una instancia de, debe convertirse en una biblioteca de cliente. Siga estos pasos para convertir la temática en una biblioteca de cliente:

1. Abra el símbolo del sistema o la ventana de terminal.
1. Navegue hasta la carpeta `<your-theme-sources>`. Por ejemplo, `C:\aem-forms-theme-canvas`
1. Ejecute el siguiente comando:

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   Reemplazar `[yourtheme]` con el nombre de su temática personalizada. Por ejemplo, si el nombre del tema personalizado es `customcanvastheme`, ejecute el siguiente comando

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   Cuando se ejecuta correctamente el comando, se crea una carpeta de biblioteca de cliente en `themerepo\theme-clientlibs\[yourtheme]`.

   ![Generación de biblioteca de cliente](/help/forms/using/assets/clientlib_created.png)


   ![Ubicación de la biblioteca de cliente](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4. Implementar el tema en un entorno local {#deploy-the-theme-on-a-local-environment}

Para implementar el tema en el entorno de desarrollo o prueba local, siga estos pasos:

1. Copie la biblioteca de cliente, creada en la sección anterior, en el proyecto Archetype, en la siguiente ruta:

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. Abra el símbolo del sistema o el terminal.
1. AEM Vaya al directorio raíz del proyecto de tipo de archivo de la, el proyecto utilizado para habilitar los componentes principales del formulario adaptable.
1. Ejecute el siguiente comando para implementar el tema personalizado en su entorno:

   `mvn clean install`

   ![Compilación de biblioteca de cliente](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Tap **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Tap **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5. Implementar un tema en el entorno de producción {#deploy-theme}

Una vez que haya probado correctamente el tema en su entorno de desarrollo local, puede continuar implementando el tema en los entornos de producción, incluidas las instancias de autor y publicación. Siga estos pasos para implementar el tema en los entornos de producción:

1. AEM Inicie sesión en su entorno de.
1. Abra el Administrador de paquetes. La URL predeterminada es `https://localhost:4502/crx/packmgr/index.jsp`.
1. Clic **Cargar paquete** y haga clic en **Examinar**.
1. Vaya a y seleccione `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip`. Clic **Abrir**.
1. Haga clic en Instalar. Repita el paso en todos los entornos de producción.


Una vez instalado el paquete, la temática está disponible para su selección.

![Biblioteca de cliente de temas](/help/forms/using/assets/themeclientlibrary.png)

>
>
>Si tiene dificultades para acceder al cuadro de diálogo de inicio de sesión en una instancia de publicación para instalar el paquete a través del Administrador de paquetes, intente iniciar sesión a través de la siguiente URL: `http://[Publish Server URL]:[PORT]/system/console`. Esto permite el acceso para iniciar sesión en la instancia de publicación, lo que le permite continuar con el proceso de instalación.

## Aplicar una temática a un formulario adaptable {#using-theme-in-adaptive-form}

Los pasos para aplicar una temática a un formulario adaptable son los siguientes:

1. AEM Inicie sesión en la instancia local de autor de la.
1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.
1. Haga clic en **Crear** > **Formularios adaptables**.
1. Seleccione una plantilla de componentes principales de Forms adaptable y haga clic en **Siguiente**. El **Añadir propiedades** aparece
1. Especifique el **Nombre** para su formulario adaptable.


   >[!NOTE]
   >
   > * De forma predeterminada, la variable `adaptiveform.theme.canvas3` tema está seleccionado.
   > * Puede elegir una temática diferente de la siguiente **Biblioteca de cliente de temas** menú desplegable.

1. Haga clic en **Crear**.

Las temáticas se utilizan como parte de una plantilla de formulario adaptable para definir el estilo al crear un formulario adaptable.

## Eliminar una temática {#delete-a-theme}

Para eliminar temas no utilizados o no deseados:

1. Inicie sesión en la instancia de autor.
1. Abra `http://[Publish Server URL]:[PORT]/crx/de/index.jsp`
1. Navegue hasta `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`.
1. Elimine la carpeta de la temática y guarde los cambios.


## Pregunta más frecuente {#faq}

**P:** ¿Qué personalización tiene prioridad al realizar personalizaciones en una carpeta de temas tanto a nivel global como a nivel de componente?

**R:** Cuando se define un estilo tanto en el nivel de tema como de componente, el estilo definido en el nivel de componente tiene prioridad.

**P:** ¿Qué pasos se deben seguir si la temática personalizada no está visible en el **[!UICONTROL Biblioteca de cliente de temas]**?

**R:**  Si la temática personalizada no aparece en la **[!UICONTROL Biblioteca de cliente de temas]** , siga estos pasos:

1. Vaya a la ubicación en la que ha agregado la biblioteca de cliente de temas personalizada. La ruta recomendada es `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`.

1. Abra el `.content.xml` e incluir los siguientes metadatos:

   ```
       formstheme:true
       allowproxy:true
   ```

1. Guarde el archivo y vuelva a implementar la temática.

## Consulte también

* [Crear un formulario adaptable basado en componentes principales](create-an-adaptive-form-core-components.md)
* [Utilice el editor de reglas para agregar un comportamiento dinámico al formulario](rule-editor.md)
* [Crear o personalizar temáticas para componentes principales basados en Forms adaptable](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Crear una plantilla para componentes principales basados en Forms adaptable](template-editor.md)
* [Crear o agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](create-or-add-an-adaptive-form-to-aem-sites-page.md)

