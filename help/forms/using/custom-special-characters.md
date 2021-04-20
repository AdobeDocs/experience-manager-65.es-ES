---
title: Caracteres especiales personalizados en la gestión de correspondencia
seo-title: Caracteres especiales personalizados en la gestión de correspondencia
description: Aprenda a añadir caracteres especiales personalizados en Gestión de Correspondencia.
seo-description: Aprenda a añadir caracteres especiales personalizados en Gestión de Correspondencia.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 1%

---


# Caracteres especiales personalizados en Administración de correspondencia{#custom-special-characters-in-correspondence-management}

## Información general {#overview}

La Gestión de Correspondencia tiene soporte integrado y predeterminado para 210 caracteres especiales que puede insertar en letras con facilidad.

Por ejemplo, puede insertar los siguientes caracteres especiales:

* Símbolos monetarios como €, Euros y £
* Símbolos matemáticos como la adminis... ...la adm., la j... ...la adm.
* Símbolos de puntuación como ‟ y&quot;

Puede insertar caracteres especiales en letras:

* En el [editor de texto](/help/forms/using/document-fragments.md#createtext)
* En un módulo en línea [editable en una correspondencia](../../forms/using/create-correspondence.md#managecontent)

![especialcaracterissinlinemodul](assets/specialcharactersinlinemodule.png)

El administrador puede añadir compatibilidad para más caracteres especiales personalizados mediante la personalización. Este artículo proporciona instrucciones sobre cómo agregar compatibilidad con caracteres especiales adicionales personalizados.

## Agregue o modifique la compatibilidad con caracteres especiales personalizados en Administración de correspondencia {#creatingfolderstructure}

Siga estos pasos para añadir compatibilidad con caracteres especiales personalizados:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada **[!UICONTROL caracteres especiales]** con una ruta o estructura similar a la carpeta de caracteres especiales (ubicada en la carpeta textEditorConfig en libs):

   1. Haga clic con el botón derecho en la carpeta **specialcharacter** en la siguiente ruta y seleccione **Overlay Node**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter

      **Ubicación de superposición:** /apps/

      **Coincidir tipos de nodo:** activado

      >[!NOTE]
      >
      >No realice cambios en la rama /libs. Cualquier cambio que realice puede perderse, ya que esta rama puede cambiar siempre que:
      >
      >
      >
      >    * Actualice en su instancia
      >    * Aplicar una corrección
      >    * Instalación de un paquete de características


   1. Haga clic en **Aceptar** y, a continuación, haga clic en **Guardar todo**. La carpeta de caracteres especiales se crea en la ruta de acceso especificada.

      Después de crear la superposición, compruebe las etiquetas de estructura de nodos. Cada nodo creado en /apps usando la superposición debe tener la misma clase y propiedades que se definen en /libs para ese nodo. Si falta alguna propiedad o etiqueta en la estructura de nodos de la ubicación /apps, sincronice sus etiquetas con el nodo correspondiente en /libs.



1. Asegúrese de que el nodo **[!UICONTROL textEditorConfig]** tiene las siguientes propiedades y valores:

   | Nombre | Tipo | Value |
   |---|---|---|
   | cmConfigurationType | Cadena | cmTextEditorConfiguration |
   | cssPath | Cadena | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Haga clic con el botón derecho en la carpeta **[!UICONTROL specialcharacter]** en la siguiente ruta, seleccione **Create > Child Node** y, a continuación, haga clic en **Save All**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter/&lt;YourChildNode>

1. Actualice la página Editor de texto\Crear interfaz de usuario de correspondencia . El nodo que ha agregado es el último de la lista de caracteres especiales de la interfaz de usuario.
1. Haga clic en **Guardar todo**.
1. Realice los cambios necesarios en los caracteres especiales:

<table>
 <tbody>
  <tr>
   <td><strong>A...</strong></td>
   <td><strong>Complete los pasos siguientes</strong></td>
  </tr>
  <tr>
   <td>Agregar un carácter especial personalizado</td>
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
     <li>Superponga el nodo que desea actualizar como se explica más arriba y verifique las etiquetas y las clases.</li>
     <li>Cambie cualquier valor, como caption, value, endValue y multipleCaption. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ocultar un carácter especial</td>
   <td>
    <ol>
     <li>Superponga el nodo que desea ocultar en "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter"</li>
     <li>Agregue la propiedad sling:hideResource (booleano) al nodo (debajo de las aplicaciones) para que se oculte. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ocultar varios caracteres especiales</td>
   <td>
    <ol>
     <li>Agregue la propiedad "sling:hideChildren (String o String[])" a "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter". </li>
     <li>Agregue nombres de nodo (caracteres especiales que se ocultarán) como valores para la propiedad "sling:hideChildren". </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ordenar caracteres especiales</td>
   <td>
    <ol>
     <li>Añada un nodo secundario en "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacter" con propiedades obligatorias. </li>
     <li>Agregue la propiedad "sling:orderBefore (String)" al nodo secundario recién creado. </li>
     <li>Agregue el nombre del nodo como valor antes del cual se mostrará el carácter especial recién agregado. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

