---
title: Caracteres especiales personalizados en la Administración de correspondencia
seo-title: Custom special characters in Correspondence Management
description: Aprenda a agregar caracteres especiales personalizados en Administración de correspondencia.
seo-description: Learn how to add custom special characters in Correspondence Management.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: ht
source-wordcount: '639'
ht-degree: 100%

---

# Caracteres especiales personalizados en la Administración de correspondencia{#custom-special-characters-in-correspondence-management}

## Información general {#overview}

Administración de correspondencia tiene soporte integrado y predeterminado para 210 caracteres especiales que puede insertar en cartas con facilidad.

Por ejemplo, puede insertar los siguientes caracteres especiales:

* Símbolos monetarios como €, ￥ y £
* Símbolos matemáticos como ∑, √, ∂ y ^
* Símbolos de puntuación como ‟ y &quot;

Puede insertar caracteres especiales en cartas:

* En el [editor de texto](/help/forms/using/document-fragments.md#createtext)
* En un módulo en línea editable [en una correspondencia](../../forms/using/create-correspondence.md#managecontent)

![specialcharactersinlinemodule](assets/specialcharactersinlinemodule.png)

El administrador puede agregar compatibilidad para más caracteres especiales personalizados mediante la personalización. Este artículo proporciona instrucciones sobre cómo agregar compatibilidad con caracteres especiales adicionales personalizados.

## Agregar o modificar la compatibilidad con caracteres especiales personalizados en Administración de correspondencia {#creatingfolderstructure}

Siga estos pasos para agregar compatibilidad con caracteres especiales personalizados:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta llamada **[!UICONTROL specialcharacters]** con una ruta/estructura similar a la carpeta de caracteres especiales (ubicada en la carpeta textEditorConfig en libs):

   1. Haga clic con el botón derecho en la carpeta **specialcharacters** en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **Ubicación de superposición:** /apps/

      **Coincidir tipos de nodo:** Comprobado

      >[!NOTE]
      >
      >No realice cambios en la rama /libs. Cualquier cambio que realice podría perderse, ya que esta rama puede cambiar siempre que haga lo siguiente:
      >
      >
      >
      >    * Actualice en su instancia
      >    * Aplique una corrección
      >    * Instale un paquete de características


   1. Haga clic en **Aceptar** y luego en **Guardar todo**. La carpeta de caracteres especiales se creará en la ruta de acceso especificada.

      Después de crear la superposición, compruebe las etiquetas de estructura de nodos. Cada nodo creado en /apps mediante superposición debe tener la misma clase y propiedades que se definen en /libs para ese nodo. Si falta alguna propiedad o etiqueta en la estructura de nodos de la ubicación /apps, sincronice sus etiquetas con el nodo correspondiente en /libs.

1. Asegúrese de que el nodo **[!UICONTROL textEditorConfig]** tiene las siguientes propiedades y valores:

   | Nombre | Tipo | Valor |
   |---|---|---|
   | cmConfigurationType | Cadena | cmTextEditorConfiguration |
   | cssPath | Cadena | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Haga clic con el botón derecho en la carpeta **[!UICONTROL specialcharacters]** en la siguiente ruta y seleccione **Crear > Nodo secundario** y haga clic en **Guardar todo**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. Actualice la página Editor de texto\Crear interfaz de usuario de correspondencia. El nodo que ha agregado es el último de la lista de caracteres especiales de la interfaz de usuario.
1. Haga clic en **Guardar todo**.
1. Realice los cambios necesarios en los caracteres especiales:

<table>
 <tbody>
  <tr>
   <td><strong>Para...</strong></td>
   <td><strong>Complete los siguientes pasos </strong></td>
  </tr>
  <tr>
   <td>Agregue un caracter especial personalizado</td>
   <td>
    <ol>
     <li>Agregue un nodo secundario en “/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters” con propiedades obligatorias.</li>
     <li>Haga clic en Guardar todo</li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Actualice las propiedades de un caracter especial existente</td>
   <td>
    <ol>
     <li>Superponga el nodo que desea actualizar como se explica más arriba y compruebe las etiquetas y las clases.</li>
     <li>Cambie cualquier valor, como caption, value, endValue y multipleCaption. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ocultar un caracter especial</td>
   <td>
    <ol>
     <li>Superponga el nodo que desea ocultar en “/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”</li>
     <li>Agregue la propiedad sling:hideResource (booleano) al nodo (debajo de las aplicaciones) para que ocultarlo. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ocultar varios caracteres especiales</td>
   <td>
    <ol>
     <li>Agregue la propiedad “sling:hideChildren (String or String[])” a “/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”. </li>
     <li>Agregue nombres de nodo (caracteres especiales que se ocultarán) como valores para la propiedad “sling:hideChildren” property. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ordenar caracteres especiales</td>
   <td>
    <ol>
     <li>Agregue un nodo secundario en “/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters” con propiedades obligatorias. </li>
     <li>Agregue la propiedad “sling:orderBefore (String)” al nodo secundario recién creado. </li>
     <li>Agregue el nombre del nodo como valor antes del cual se mostrará el carácter especial recién agregado. </li>
     <li>Haga clic en Guardar todo. </li>
     <li>Actualice el Editor de texto\Crear interfaz de usuario de correspondencia para ver los cambios.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
