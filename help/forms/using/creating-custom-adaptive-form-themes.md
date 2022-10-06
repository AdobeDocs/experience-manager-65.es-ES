---
title: Creación de temas de formularios adaptables personalizados
seo-title: Creating custom adaptive form themes
description: Un tema de formulario adaptable es una AEM biblioteca de cliente que se utiliza para definir los estilos (aspecto y presentación) de un formulario adaptable. Aprenda a crear temas de formularios adaptables personalizados.
seo-description: An adaptive form theme is an AEM client library that you use to define the styles (look and feel) for an adaptive form. Learn how you can create custom adaptive form themes.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Creación de temas de formularios adaptables personalizados {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms proporciona la variable [Editor de temas](/help/forms/using/themes.md) capacidad para crear y modificar formularios adaptables [temáticas](/help/forms/using/themes.md). Realice los pasos enumerados en este artículo, solo si ha actualizado desde una versión que no tiene [Editor de temas](/help/forms/using/themes.md) y ya tiene una inversión en temas creados usando menos archivos CSS (método editor pre-tema).

## Requisitos previos {#prerequisites}

* Conocimiento del marco LESS (CSS más inteligente)
* Creación de una biblioteca de cliente en Adobe Experience Manager
* [Creación de una plantilla de formulario adaptable](/help/forms/using/custom-adaptive-forms-templates.md) para utilizar el tema que crea

## Tema de formulario adaptable {#adaptive-form-theme}

Un **tema de formulario adaptable** es una AEM biblioteca de cliente que se utiliza para definir los estilos (aspecto) de un formulario adaptable.

Puede crear un **plantilla adaptable** y aplique el tema a la plantilla. A continuación, utilice esta plantilla personalizada para crear un **formulario adaptable**.

![Formulario adaptable y biblioteca de cliente](assets/hierarchy.png)

## Creación de un tema de formulario adaptable {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>El siguiente procedimiento se describe con nombres de ejemplo para objetos AEM como nodos, propiedades y carpetas.
>
>Si sigue estos pasos utilizando los nombres, la plantilla resultante debería aparecer de forma similar a la siguiente instantánea:

![Instantánea del formulario adaptable con tema de bosque](assets/thumbnail.png)
**Figura:** *Ejemplo de tema de bosque*

1. Crear un nodo de tipo `cq:ClientLibraryFolder` en el `/apps`nodo .

   Por ejemplo, cree el siguiente nodo:

   `/apps/myAfThemes/forestTheme`

1. Agregar una propiedad de cadena de varios valores `categories` al nodo y establezca su valor apropiadamente.

   Por ejemplo, establezca la propiedad en: `af.theme.forest`.

   ![Instantánea del repositorio CRX](assets/3-2.png)

1. Añadir dos carpetas, `less` y `css`y un archivo `css.txt` al nodo creado en el paso 1:

   * `less` carpeta: Contiene el `less` archivos de variable en los que define `less` variables y `less mixins` que se utilizan para administrar los estilos .css.

      Esta carpeta consta de `less` archivos de variables, `less` archivos de mezcla, `less` archivos que definen estilos utilizando mezclas y variables. Y todos estos menos archivos se importan en estilos.less.

   * `css`carpeta: Contiene los archivos .css en los que se definen los estilos estáticos que se utilizarán en el tema.

   **Menos archivos de variables**: Estos son los archivos, donde se definen o anulan las variables que se utilizan para definir estilos CSS.

   Los formularios adaptables proporcionan variables OOTB definidas en los siguientes archivos .less:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   Los formularios adaptables también proporcionan variables de terceros definidas en:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   Puede utilizar las menos variables que se proporcionan con los formularios adaptables, puede anular estas variables o crear menos variables nuevas.

   >[!NOTE]
   >
   >Al importar los archivos del preprocesador menor, en la instrucción import especifique la ruta relativa de los archivos.

   Variables de anulación de muestra:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   Para anular la variable `less`variables:

   1. Importar variables de formulario adaptable predeterminadas:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. A continuación, importe el archivo menor que incluya variables anuladas.

   Ejemplo de nuevas definiciones de variables:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Menos archivos mixtos:** Puede definir las funciones que aceptan variables como argumentos. El resultado de estas funciones son los estilos resultantes. Utilice estas mezclas en diferentes estilos para evitar la repetición de estilos CSS.

   Los formularios adaptables proporcionan mezclas de OOTB definidas en:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   Los formularios adaptables también proporcionan mezclas de terceros definidas en:

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   Definición de mezcla de muestra:

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **Archivo Styles.less:** Utilice este archivo para incluir todos los menos archivos (variables, mezclas, estilos) que necesite utilizar en la biblioteca cliente.

   En el siguiente ejemplo `styles.less` , la instrucción import se puede colocar en cualquier orden.

   Las instrucciones para importar los siguientes archivos .less son obligatorias:

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   La variable `css.txt` contiene las rutas de los archivos .css que se van a descargar para la biblioteca.

   Por ejemplo:

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >El archivo style.less no es obligatorio. Esto significa que no es necesario crear este archivo si no se ha definido ningún estilo, variable o mezcla personalizado.
   >
   >Sin embargo, si no crea un archivo style.less, en el archivo css.txt debe descomentar la siguiente línea:
   >
   >**`#base=less`**
   >
   >Y comente la siguiente línea:
   >
   >**`styles.less`**

## Uso de un tema en un formulario adaptable {#to-use-a-theme-in-an-adaptive-form}

Después de crear un tema de formulario adaptable, realice los siguientes pasos para utilizar este tema de forma adaptativa:

1. Para incluir el tema creado en [para crear un tema de formulario adaptable](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) , cree una página personalizada de tipo `cq:Component`.

   Por ejemplo, `/apps/myAfCustomizations/myAfPages/forestPage`. 

   1. Agregue un `sling:resourceSuperType` y establezca su valor como `fd/af/components/page/base`.

      ![Instantánea del repositorio CRX](assets/1-2.png)

   1. Para utilizar un tema en la página, debe agregar un archivo de anulación library.jsp al nodo .

      A continuación, importe el tema creado en la sección Para crear un tema de formulario adaptable de este artículo.

      El siguiente fragmento de código de ejemplo importa el `af.theme.forest` tema.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Opcional**: En la página personalizada, reemplace header.jsp, footer.jsp y body.jsp, según sea necesario.

1. Cree una plantilla personalizada (por ejemplo: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) cuyo jcr:content apunta a la página personalizada creada en el paso anterior (por ejemplo: `myAfCustomizations/myAfPages/forestPage)`.

   ![Instantánea del repositorio CRX](assets/2-1.png)

1. Cree un formulario adaptable utilizando la plantilla creada en el paso anterior. El aspecto del formulario adaptable se define mediante el tema creado en la sección Creación de un tema del formulario adaptable de este artículo.
