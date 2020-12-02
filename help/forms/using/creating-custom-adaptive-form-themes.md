---
title: Creación de temáticas de formulario adaptables personalizadas
seo-title: Creación de temáticas de formulario adaptables personalizadas
description: Un tema de formulario adaptable es una AEM biblioteca de cliente que se utiliza para definir los estilos (aspecto y presentación) de un formulario adaptable. Obtenga información sobre cómo crear temáticas de formularios adaptables personalizadas.
seo-description: Un tema de formulario adaptable es una AEM biblioteca de cliente que se utiliza para definir los estilos (aspecto y presentación) de un formulario adaptable. Obtenga información sobre cómo crear temáticas de formularios adaptables personalizadas.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---


# Creación de temáticas de formularios adaptables personalizadas {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms proporciona la capacidad [Editor de temas](/help/forms/using/themes.md) para crear y modificar formularios adaptables [temáticas](/help/forms/using/themes.md). Siga los pasos que se indican en este artículo, solo si ha actualizado desde una versión que no tiene [Editor de temas](/help/forms/using/themes.md) y tiene una inversión existente en temáticas creadas con archivos Menor/CSS (método de editor previo al tema).

## Requisitos previos {#prerequisites}

* Conocimiento del marco LESS (CSS más inteligente)
* Cómo crear una biblioteca de cliente en Adobe Experience Manager
* [Creación de una ](/help/forms/using/custom-adaptive-forms-templates.md) plantilla de formulario adaptable para utilizar el tema que cree

## Tema de formulario adaptable {#adaptive-form-theme}

Un **tema de formulario adaptable** es una biblioteca de cliente AEM que se utiliza para definir los estilos (aspecto y presentación) de un formulario adaptable.

Puede crear una **plantilla adaptable** y aplicar el tema a la plantilla. A continuación, utilice esta plantilla personalizada para crear un **formulario adaptable**.

![Biblioteca de clientes y formularios adaptables](assets/hierarchy.png)

## Para crear un tema de formulario adaptable {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>El siguiente procedimiento se describe con nombres de ejemplo para objetos de AEM como nodos, propiedades y carpetas.
>
>Si sigue estos pasos utilizando los nombres, la plantilla resultante debería aparecer de forma similar a la siguiente instantánea:

![Instantánea de formulario adaptable con tema de bosque ](assets/thumbnail.png)
**Figura:Ejemplo de tema** *de bosque*

1. Cree un nodo de tipo `cq:ClientLibraryFolder` en el nodo `/apps`.

   Por ejemplo, cree el nodo siguiente:

   `/apps/myAfThemes/forestTheme`

1. Añada una propiedad de cadena con varios valores `categories` en el nodo y defina su valor correctamente.

   Por ejemplo, establezca la propiedad en: `af.theme.forest`.

   ![Instantánea del repositorio CRX](assets/3-2.png)

1. Añada dos carpetas, `less` y `css`, y un archivo `css.txt` al nodo creado en el paso 1:

   * `less` carpeta: Contiene los archivos  `less` variables en los que se definen las  `less` variables y  `less mixins` que se utilizan para administrar los estilos .css.

      Esta carpeta consta de `less` archivos variables, `less` archivos mixtos, `less` archivos que definen estilos usando mezclas y variables. Y todos estos menos archivos se importan en estilos.less.

   * `css`carpeta: Contiene los archivos .css en los que se definen los estilos estáticos que se utilizarán en el tema.

   **Menos archivos** de variables: Estos son los archivos en los que se definen o anulan las variables que se utilizan para definir estilos CSS.

   Los formularios adaptables proporcionan variables OOTB definidas en los siguientes archivos .less:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   Los formularios adaptables también proporcionan variables de terceros definidas en:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   Puede utilizar las menos variables proporcionadas con los formularios adaptables, puede anular estas variables o puede crear nuevas menos variables.

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

   Para anular las variables `less`:

   1. Importar variables de formulario adaptable predeterminadas:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. A continuación, importe el archivo menos que incluya variables anuladas.

   Ejemplo de nuevas definiciones de variables:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Menos archivos de mezcla:** puede definir las funciones que aceptan variables como argumentos. El resultado de estas funciones son los estilos resultantes. Utilice estas mezclas en diferentes estilos para evitar la repetición de estilos CSS.

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

   **Archivo Styles.less:** utilice este archivo para incluir todos los menos archivos (variables, mezclas, estilos) que necesite utilizar en la biblioteca del cliente.

   En el siguiente archivo de ejemplo `styles.less`, la sentencia import se puede colocar en cualquier orden.

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

   El `css.txt` contiene las rutas de los archivos .css que se van a descargar para la biblioteca.

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
   >El archivo style.less no es obligatorio. Esto significa que no necesita crear este archivo si no ha definido ningún estilo personalizado, variable o mezcla.
   >
   >Sin embargo, si no crea un archivo style.less, en el archivo css.txt, debe quitar el comentario de la línea siguiente:
   >
   >**`#base=less`**
   >
   >Y comenta la siguiente línea:
   >
   >**`styles.less`**

## Para utilizar un tema en un formulario adaptable {#to-use-a-theme-in-an-adaptive-form}

Después de crear un tema de formulario adaptable, realice los siguientes pasos para utilizar este tema en un formulario adaptable:

1. Para incluir el tema creado en la sección [para crear un tema de formulario adaptable](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p), cree una página personalizada de tipo `cq:Component`.

   Por ejemplo, `/apps/myAfCustomizations/myAfPages/forestPage`

   1. Añada una propiedad `sling:resourceSuperType` y defina su valor como `fd/af/components/page/base`.

      ![Instantánea del repositorio CRX](assets/1-2.png)

   1. Para utilizar un tema en la página, debe agregar un archivo de sobrescritura library.jsp al nodo.

      A continuación, importe el tema creado en Para crear una sección de tema de formulario adaptable de este artículo.

      El siguiente fragmento de código de ejemplo importa el tema `af.theme.forest`.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Opcional**: En la página personalizada, reemplace header.jsp, filename.jsp y body.jsp, según sea necesario.

1. Cree una plantilla personalizada (por ejemplo: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) cuyo jcr:content apunta a una página personalizada creada en el paso anterior (por ejemplo: `myAfCustomizations/myAfPages/forestPage)`.

   ![Instantánea del repositorio CRX](assets/2-1.png)

1. Cree un formulario adaptable con la plantilla creada en el paso anterior. El aspecto del formulario adaptable se define mediante el tema creado en Para crear una sección de tema de formulario adaptable de este artículo.

