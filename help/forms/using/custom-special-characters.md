---
title: Caracteres especiales personalizados en la administración de correspondencias
seo-title: Caracteres especiales personalizados en la administración de correspondencias
description: Obtenga información sobre cómo agregar caracteres especiales personalizados en Administración de correspondencia.
seo-description: Obtenga información sobre cómo agregar caracteres especiales personalizados en Administración de correspondencia.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 1%

---


# Caracteres especiales personalizados en Administración de correspondencia{#custom-special-characters-in-correspondence-management}

## Información general {#overview}

Correspondence Management dispone de compatibilidad integrada y predeterminada con 210 caracteres especiales que puede insertar fácilmente en letras.

Por ejemplo, puede insertar los siguientes caracteres especiales:

* Símbolos monetarios como €, ¥y £
* Matemáticas como la adrenalina, el rey, el rey, el rey y el símbolo ^
* Símbolos de puntuación como ‟ y&quot;

Puede insertar caracteres especiales en letras:

* En el [editor de texto](/help/forms/using/document-fragments.md#createtext)
* En un módulo en línea [editable en una correspondencia](../../forms/using/create-correspondence.md#managecontent)

![especialcaracterissinlinemodulo](assets/specialcharactersinlinemodule.png)

El administrador puede añadir compatibilidad con más caracteres especiales personalizados personalizándolos. Este artículo proporciona las instrucciones sobre cómo agregar compatibilidad para caracteres especiales personalizados adicionales.

## Añadir o modificar la compatibilidad con caracteres especiales personalizados en Administración de correspondencia {#creatingfolderstructure}

Siga estos pasos para añadir compatibilidad con caracteres especiales personalizados:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta con el nombre **[!UICONTROL caracteres especiales]** con una ruta/estructura similar a la carpeta de caracteres especiales (ubicada en la carpeta textEditorConfig en libs):

   1. Haga clic con el botón derecho en la carpeta **caracteres especiales** en la siguiente ruta y seleccione **Nodo superpuesto**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/caracteres especiales

      **Ubicación de superposición:** /apps/

      **Coincidir tipos de nodo:** activado

      >[!NOTE]
      >
      >No realice cambios en la rama /libs. Cualquier cambio que realice puede perderse, ya que esta rama puede cambiar siempre que:
      >
      >
      >
      >    * Actualizar en su instancia
      >    * Aplicar una corrección urgente
      >    * Instalación de un paquete de funciones


   1. Haga clic en **Aceptar** y, a continuación, haga clic en **Guardar todo**. La carpeta de caracteres especiales se crea en la ruta de acceso especificada.

      Después de crear la superposición, compruebe las etiquetas de estructura de nodos. Cada nodo creado en /apps que utiliza la superposición debe tener la misma clase y las mismas propiedades que se definen en /libs para ese nodo. Si falta alguna propiedad o etiqueta en la estructura de nodos en la ubicación /apps, sincronice sus etiquetas con el nodo correspondiente en /libs.



1. Asegúrese de que el nodo **[!UICONTROL textEditorConfig]** tiene las siguientes propiedades y valores:

   | Nombre | Tipo | Value |
   |---|---|---|
   | cmConfigurationType | Cadena | cmTextEditorConfiguration |
   | cssPath | Cadena | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Haga clic con el botón secundario en la carpeta **[!UICONTROL caracteres especiales]** en la siguiente ruta y seleccione **Crear > Nodo secundario** y, a continuación, haga clic en **Guardar todo**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter/&lt;YourChildNode>

1. Actualice la página Editor de texto\Crear interfaz de usuario de correspondencia. El nodo que ha agregado es el último de la lista de caracteres especiales en la interfaz de usuario.
1. Haga clic en **Guardar todo**.
1. Realice los cambios necesarios en los caracteres especiales:

<table>
 <tbody>
  <tr>
   <td><strong>A...</strong></td>
   <td><strong>Complete los siguientes pasos</strong></td>
  </tr>
  <tr>
   <td>Añadir un carácter especial personalizado</td>
   <td>
    <ol>
     <li>Añada un nodo secundario en "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter" con propiedades obligatorias.</li>
     <li>Haga clic en Guardar todo</li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Actualizar las propiedades de un carácter especial existente</td>
   <td>
    <ol>
     <li>Superponga el nodo que se va a actualizar como se explica más arriba y compruebe las etiquetas y las clases.</li>
     <li>Cambie los valores, como caption, value, endValue y multipleCaption. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ocultar un carácter especial</td>
   <td>
    <ol>
     <li>Superponga el nodo que se va a ocultar en "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter"</li>
     <li>Añada la propiedad sling:hideResource (Boolean) en el nodo (debajo de las aplicaciones) que se va a ocultar. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ocultar varios caracteres especiales</td>
   <td>
    <ol>
     <li>Añada la propiedad "sling:hideChildren (String o String[])" a "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter". </li>
     <li>Añada nombres de nodo (caracteres especiales que se ocultarán) como valores para la propiedad "sling:hideChildren". </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ordenar caracteres especiales</td>
   <td>
    <ol>
     <li>Añada un nodo secundario en "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter" con propiedades obligatorias. </li>
     <li>Añada la propiedad "sling:orderBefore (String)" en el nodo secundario recién creado. </li>
     <li>Añada el nombre del nodo como valor antes del cual se mostrará el carácter especial recientemente agregado. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

