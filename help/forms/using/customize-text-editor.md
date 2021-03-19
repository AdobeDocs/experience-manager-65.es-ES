---
title: Personalizar editor de texto
seo-title: Personalizar editor de texto
description: Aprenda a personalizar el editor de texto.
seo-description: Aprenda a personalizar el editor de texto.
uuid: 598246fe-8f15-49b6-b6d3-9154bebcd27e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 666fee78-a103-44dc-afe7-71b90ce219b7
docset: aem65
feature: Administración de correspondencia
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---


# Personalizar editor de texto{#customize-text-editor}

## Información general {#overview}

Puede personalizar el editor de texto, en Administrar recursos y Crear interfaz de usuario de correspondencia, para agregar más fuentes y tamaños de fuente. Estas fuentes incluyen fuentes inglesas y no inglesas, como las japonesas.

Puede personalizar para cambiar lo siguiente en la configuración de fuente:

* Familia de fuentes y tamaño
* Propiedades como altura y espaciado entre letras
* Valores predeterminados de familia de fuentes y tamaño, altura, espaciado entre letras y formato de fecha
* Sangría de viñetas

Para ello, debe:

1. [Personalizar fuentes editando el archivo tbxeditor-config.xml en CRX](#customizefonts)
1. [Agregar fuentes personalizadas al equipo cliente](#addcustomfonts)

## Personalizar fuentes editando el archivo tbxeditor-config.xml en CRX {#customizefonts}

Para personalizar fuentes editando el archivo tbxeditor-config.xml, haga lo siguiente:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada config con una ruta/estructura similar a la carpeta de configuración, que se encuentra en libs/fd/cm/config, siguiendo los pasos siguientes:

   1. Haga clic con el botón derecho en la carpeta de elementos de la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/config`

      ![Nodo de superposición](assets/1-1.png)

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/config

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** seleccionados

      ![Nodo de superposición](assets/2.png)

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

   1. Haga clic en **Guardar todo**.

1. Cree una copia del archivo tbxeditor-config.xml en la carpeta de configuración recién creada, siguiendo los pasos siguientes:

   1. Haga clic con el botón derecho en el archivo tbxeditor-config.xml en libs/fd/cm/config y seleccione **Copy**.
   1. Haga clic con el botón derecho en la siguiente carpeta y seleccione **Pegar:**

      `apps/fd/cm/config`

   1. El nombre del archivo pegado, de forma predeterminada, es `copy of tbxeditor-config.xml.` Cambie el nombre del archivo a `tbxeditor-config.xml` y haga clic en **Guardar todo**.

1. Abra el archivo tbxeditor-config.xml en apps/fd/cm/config y luego realice los cambios necesarios.

   1. Haga doble clic en el archivo tbxeditor-config.xml en apps/fd/cm/config. Se abrirá el archivo .

      ```xml
      <editorConfig>
         <bulletIndent>0.25in</bulletIndent>
      
         <defaultDateFormat>DD-MM-YYYY</defaultDateFormat>
      
         <fonts>
            <default>Times New Roman</default>
            <font>_sans</font>
            <font>_serif</font>
            <font>_typewriter</font>
            <font>Arial</font>
            <font>Courier</font>
            <font>Courier New</font>
            <font>Geneva</font>
            <font>Georgia</font>
            <font>Helvetica</font>
            <font>Tahoma</font>
            <font>Times New Roman</font>
            <font>Times</font>
            <font>Verdana</font>
         </fonts>
      
         <fontSizes>
            <default>12</default>
            <fontSize>8</fontSize>
            <fontSize>9</fontSize>
            <fontSize>10</fontSize>
            <fontSize>11</fontSize>
            <fontSize>12</fontSize>
            <fontSize>14</fontSize>
            <fontSize>16</fontSize>
            <fontSize>18</fontSize>
            <fontSize>20</fontSize>
            <fontSize>22</fontSize>
            <fontSize>24</fontSize>
            <fontSize>26</fontSize>
            <fontSize>28</fontSize>
            <fontSize>36</fontSize>
            <fontSize>48</fontSize>
            <fontSize>72</fontSize>
         </fontSizes>
      
         <lineHeights>
            <default>2</default>     
            <lineHeight>2</lineHeight>
            <lineHeight>3</lineHeight>
            <lineHeight>4</lineHeight>
            <lineHeight>5</lineHeight>
            <lineHeight>6</lineHeight>
            <lineHeight>7</lineHeight>
            <lineHeight>8</lineHeight>
            <lineHeight>9</lineHeight>
            <lineHeight>10</lineHeight>
            <lineHeight>11</lineHeight>
            <lineHeight>12</lineHeight>
            <lineHeight>13</lineHeight>
            <lineHeight>14</lineHeight>
            <lineHeight>15</lineHeight>
            <lineHeight>16</lineHeight>
         </lineHeights>
      
         <letterSpacings>
            <default>0</default>
            <letterSpacing>0</letterSpacing>
            <letterSpacing>1</letterSpacing>
            <letterSpacing>2</letterSpacing>
            <letterSpacing>3</letterSpacing>
            <letterSpacing>4</letterSpacing>
            <letterSpacing>5</letterSpacing>
            <letterSpacing>6</letterSpacing>
            <letterSpacing>7</letterSpacing>
            <letterSpacing>8</letterSpacing>
            <letterSpacing>9</letterSpacing>
            <letterSpacing>10</letterSpacing>
            <letterSpacing>11</letterSpacing>
            <letterSpacing>12</letterSpacing>
            <letterSpacing>13</letterSpacing>
            <letterSpacing>14</letterSpacing>
            <letterSpacing>15</letterSpacing>
            <letterSpacing>16</letterSpacing>
         </letterSpacings>
      </editorConfig>
      ```

   1. Realice los cambios necesarios en el archivo para cambiar lo siguiente en la configuración de fuente:

      * Agregar o quitar la familia y el tamaño de fuente
      * Propiedades como altura y espaciado entre letras
      * Valores predeterminados de familia de fuentes y tamaño, altura, espaciado entre letras y formato de fecha
      * Sangría de viñetas

      Por ejemplo, para añadir una fuente japonesa denominada Sazanami Mincho Medium, debe introducir lo siguiente en el archivo XML: `<font>Sazanami Mincho Medium</font>`. También necesita tener esta fuente instalada en el equipo cliente para acceder y trabajar con la personalización de fuentes. Para obtener más información, consulte [Agregar fuentes personalizadas al equipo cliente](#addcustomfonts).

      También puede cambiar los valores predeterminados de varios aspectos del texto y, al eliminar las entradas, eliminar las fuentes del editor de texto.

   1. Haga clic en **Guardar todo**.


## Agregar fuentes personalizadas al equipo cliente {#addcustomfonts}

Cuando accede a una fuente en el editor de texto de Gestión de Correspondencia, debe estar presente en el equipo cliente que está utilizando para acceder a Gestión de Correspondencia. Para poder utilizar una fuente personalizada en el editor de texto, primero debe instalar la misma en el equipo cliente.

Para obtener más información sobre la instalación de fuentes, consulte lo siguiente:

* [Instalar o desinstalar fuentes en Windows](https://windows.microsoft.com/en-us/windows-vista/install-or-uninstall-fonts)
* [Conceptos básicos de Mac: Libro de fuentes](https://support.apple.com/en-us/HT201749)

## Acceso a las personalizaciones de fuente {#access-font-customizations}

Después de realizar cambios en las fuentes en el archivo tbxeditor-config.xml en CRX e instalar las fuentes requeridas en el equipo cliente utilizado para acceder a AEM Forms, los cambios aparecen en el editor de texto.

Por ejemplo, la fuente Sazanami Mincho Medium añadida en [Personalizar fuentes editando el archivo tbxeditor-config.xml en el procedimiento CRX](#customizefonts) aparece en la interfaz de usuario del editor de texto de la siguiente manera:

![sazanamiminchointext](assets/sazanamiminchointext.png)

>[!NOTE]
>
>Para ver texto en japonés, primero debe introducir el texto con caracteres japoneses. La aplicación de una fuente japonesa personalizada solo da formato al texto de una manera determinada. La aplicación de una fuente japonesa personalizada no cambia los caracteres ingleses u otros caracteres a los japoneses.

