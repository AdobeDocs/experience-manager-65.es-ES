---
title: Añadir propiedades personalizadas a recursos de Correspondencia Management
seo-title: Añadir propiedades personalizadas a recursos de Correspondencia Management
description: Obtenga información sobre cómo agregar propiedades personalizadas a los recursos de Administración de correspondencia.
seo-description: Obtenga información sobre cómo agregar propiedades personalizadas a los recursos de Administración de correspondencia.
uuid: 4716e181-d3ea-424b-9544-376cc649bce7
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79437b96-7b57-4581-b7e7-fcaedc3d05de
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '4460'
ht-degree: 4%

---


# Añadir propiedades personalizadas a los recursos de Correspondence Management{#add-custom-properties-to-correspondence-management-assets}

## Información general {#overview}

Puede personalizar la interfaz de usuario de Correspondence Management y presentar a los usuarios un conjunto personalizado de propiedades y fichas. Esta personalización incluye la adición de campos/propiedades y fichas personalizados a tipos/letras de recursos específicos o a todos los tipos de recursos y letras.

## Añadir propiedades personalizadas a los recursos de Administración de correspondencia {#adding-custom-properties-to-correspondence-management-assets}

Los escenarios siguientes muestran cómo se pueden agregar propiedades/fichas a los recursos y letras de Correspondence Management:

* Añadir una propiedad común a todos los tipos de recursos
* Añadir una ficha común a todos los tipos de recursos
* Añadir propiedades personalizadas a tipos de recursos específicos

Al ajustar las propiedades, las rutas y los valores en estos escenarios, puede agregar propiedades y fichas personalizadas a un conjunto diferente de recursos según sus necesidades.

### Escenario: Añadir un campo común (propiedad) a todos los tipos de recursos {#scenario-adding-a-common-field-property-to-all-the-asset-types}

Este escenario muestra cómo se puede agregar una propiedad personalizada a todos los tipos de recursos (fragmentos de texto, lista, condición y diseño) y a las letras. Con este escenario, puede agregar una propiedad, Ubicación de destinatarios, a todos los recursos y letras. La propiedad Ubicación de destinatarios ayuda a identificar a qué área geográfica del envío es relevante un recurso o una letra.

>[!NOTE]
>
>Si ya ha agregado una propiedad personalizada, los inicios de propiedad aparecerán en la página de creación de recursos. Para ocultar una propiedad de este tipo, consulte Mostrar/ocultar propiedades personalizadas en las páginas Creación de recursos y Propiedades.

![Se agregó una propiedad personalizada a todos los tipos de recursos](assets/lcoationofrecipientsui.png)

Complete los siguientes pasos para agregar una propiedad personalizada a todos los tipos de recursos y letras:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada css con una ruta/estructura similar a la carpeta css (ubicada en la carpeta ccrui) siguiendo los pasos siguientes:

   1. Haga clic con el botón derecho en la carpeta items en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![Nodo Overlay](assets/itemsoverlaynode.png)

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmmetadataproperties/common properties/col1/items

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** Seleccionado

      ![Nodo Overlay](assets/cmmetapropertiesoverlaynode.png)

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

   1. Haga clic en **Guardar todo**.

1. En la carpeta de elementos recién creada, agregue un nodo para la propiedad personalizada en todo el recurso (Ejemplo: GeoLocation) mediante los siguientes pasos:

   1. Haga clic con el botón derecho en la carpeta items y seleccione **Crear** > **Crear nodo**.

      ![Crear nodo en CRX](assets/itemscreatenode.png)

   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** GeoLocation (o el nombre que desea asignar a esta propiedad)

      **Tipo:** nt:no estructurados

      ![Crear nodo: GeoLocation](assets/geographicallocationcreatenode.png)

   1. Haga clic en el nuevo nodo que ha creado (aquí GeoLocation). CRX muestra las propiedades del nodo.
   1. Añada las siguientes propiedades al nodo (aquí GeoLocation):

      | **Nombre** | **Tipo** | **Value** |
      |---|---|---|
      | fieldLabel | Cadena | Nombre que desea asignar al campo o propiedad. (Aquí: Ubicación de los destinatarios) |
      | name | Cadena | `./extendedproperties/GeoLocation` (Mantenga el mismo valor que el nombre del campo creado en el nodo items) |
      | representarReadOnly | Booleano | verdadero |
      | sling:resourceType | Cadena | `granite/ui/components/coral/foundation/form/textfield` |

   1. Haga clic en **Guardar todo**.

1. Para vista de la personalización, pase el ratón sobre un recurso (texto, lista, condición o fragmento de diseño) o una letra, haga clic en **Propiedades de Vista** y haga clic en **Editar**. El nuevo campo (Ubicación de destinatarios) aparece en la ficha Básico de las propiedades de recurso/carta.

   >[!NOTE]
   >
   >Es posible que tenga que borrar la caché del explorador antes de que la personalización aparezca en la interfaz de usuario.

   ![Se agregó una propiedad personalizada a todos los recursos](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >Las propiedades comunes de todos los recursos que agregue aparecerán en la ficha básica de las propiedades del recurso. De forma predeterminada, las propiedades comunes agregadas para todos los recursos aparecen en la página de propiedades, así como en la página de creación de recursos. Para ocultar las propiedades comunes, debe <!--link to show / hide properties]-->.

### Escenario: Añadir la lista desplegable y los valores personalizados a una propiedad o campo personalizados {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

Este escenario muestra cómo se puede agregar una propiedad personalizada a todos los tipos de recursos y agregar valores desplegables.

1. Haga clic con el botón derecho en la carpeta items en la siguiente ruta y seleccione **Nodo de superposición**:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. En el nodo de superposición recién creado (/apps/fd/cm/ma/gui/content/cmmetadataproperties/common properties/col1/items)
Cree un nodo para cada una de las propiedades (campos) para las que necesita crear una lista desplegable (aquí `geographicallocation`) del tipo nt:unestructure.
1. Añada las siguientes propiedades en el nodo (aquí geographiclocation) y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Value</strong></td>
   </tr>
   <tr>
      <td>fieldLabel</td>
      <td>Cadena</td>
      <td>Nombre que desea asignar al campo o propiedad. (Aquí: asignación geográfica)</td>
   </tr>
   <tr>
      <td>name</td>
      <td>Cadena</td>
      <td>./extendedproperties/geographiclocation (Mantenga el valor igual que el nombre del campo creado en el nodo items)</td>
   </tr>
   <tr>
      <td>representarReadOnly</td>
      <td>Booleano</td>
      <td>verdadero</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>Cadena</td>
      <td>granito/ui/components/coral/foundation/form/select<br /> </td>
   </tr>
   </tbody>
   </table>

1. En el nodo de propiedad (aquí asignación geográfica), agregue un nuevo nodo con el nombre `items`. En el nodo items, agregue un nodo para cada uno de los valores de la lista desplegable. Como práctica recomendada, agregue el primer nodo como en blanco para que sirva como valor predeterminado de la lista desplegable y una opción para que el usuario no especifique ningún valor para el campo. Para agregar varias opciones o valores desplegables, repita los siguientes pasos:

   1. Haga clic con el botón derecho en el nodo de propiedad (aquí geographiclocation) y seleccione **Crear** > **Crear nodo**.
   1. Escriba el nombre del campo como `item1,` retener tipo como nt:unestructure y haga clic en **Aceptar**.
   1. Añada las siguientes propiedades al nodo recién creado (aquí item1) y haga clic en **Guardar todo**:

      <table>
         <tbody>
         <tr>
          <td><strong>Nombre</strong></td>
          <td><strong>Tipo</strong></td>
          <td><strong>Valor</strong></td>
         </tr>
         <tr>
          <td>text</td>
          <td>Cadena</td>
          <td>Es el valor de la opción desplegable que está visible para el usuario. Déjelo en blanco para el valor en blanco (predeterminado) o introduzca el valor, como <strong>Internacional</strong> o <strong>En EE.UU.</strong>.<br /> </td>
         </tr>
         <tr>
          <td>seleccionado</td>
          <td>Cadena</td>
          <td>Valor almacenado en CRXDE para el texto. Escriba cualquier palabra clave única. <br /> </td>
         </tr>
         </tbody>
   </table>

   ![personalizacióndropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

El menú desplegable personalizado aparece como sigue en las propiedades de los recursos:

![drop-down_customization](assets/drop-down_customization.png)

### Escenario: Ficha común para todos los tipos de recursos {#scenario-common-tab-for-all-asset-types}

Este escenario muestra cómo se puede agregar una ficha personalizada, Destinatarios, a todos los tipos de recursos (fragmentos de texto, lista, condición y diseño) y a las letras. En la ficha Destinatarios puede planificar la colocación de todas las propiedades personalizadas relevantes para los destinatarios.

![Ficha personalizada agregada para todos los tipos de recursos](assets/recipientstab.png)

Con el procedimiento siguiente, puede agregar una ficha con un campo a todos los recursos:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada cmmetadataproperties con una ruta o estructura similar a la carpeta cmmetadataproperties (ubicada en la carpeta de contenido) siguiendo estos pasos:

   1. Haga clic con el botón derecho en la carpeta cmmetadataproperties en la siguiente ruta y seleccione **Nodo superpuesto**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![Nodo Overlay](assets/cmmetadatapropertiesoverlaynode.png)

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      ![Estructura de carpetas de superposición creada en CRX](assets/cmmetadatapropertiesappsfolder.png)

      Haga clic en **Guardar todo**.

1. En la carpeta cmmetadataproperties, agregue un nodo para crear una ficha personalizada para todos los recursos (ejemplo: ficha común) mediante los siguientes pasos:

   1. Haga clic con el botón derecho en la carpeta cmmetadataproperties y seleccione **Crear** > **Crear nodo**.

      ![Crear nodo](assets/cmmetadatapropertiescreatenode.png)

   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** common tab (o el nombre que desea asignar a esta propiedad)

      **Tipo:** nt:no estructurados

   1. Haga clic en el nuevo nodo que ha creado (aquí, ficha común). CRX muestra las propiedades del nodo.
   1. Añada las siguientes propiedades en el nodo (aquí, ficha común):

      <table>
         <tbody>
         <tr>
          <td><strong>Nombre</strong></td>
          <td><strong>Tipo</strong></td>
          <td><strong>Valor</strong></td>
         </tr>
         <tr>
          <td>jcr:title</td>
          <td>Cadena</td>
          <td>El nombre que desea asignar a la columna. (Aquí: Destinatarios)</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>Cadena</td>
          <td>granito/ui/componentes/coral/fundación/contenedor<br /> </td>
   </tr>
         </tbody>
       </table>

   1. Haga clic en **Guardar todo**.

1. Para el nodo de ficha creado en el último paso (aquí, ficha en común), cree un nodo denominado elemento con el siguiente paso:

   1. Haga clic con el botón derecho en el nodo relevante (aquí, ficha común) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** elementos

      **Tipo:** nt:no estructurados

   1. Haga clic en **Guardar todo:**

1. En el nodo de elementos que creó en el paso anterior (en la ficha Completo), agregue un nodo para crear una columna (aquí Columna1) en la ficha personalizada (ficha Completo) siguiendo los pasos siguientes (para agregar más columnas, repita este paso):

   1. Haga clic con el botón derecho en el nodo items y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** Columna1 (o el nombre que desea asignar al nodo; este nombre no aparece en la interfaz de usuario).

      **Tipo:** nt:no estructurados

   1. Añada la siguiente propiedad al nodo (Aquí Columna1) y haga clic en **Guardar todo**:

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Cadena</td>
           <td>granito/ui/componentes/coral/fundación/contenedor<br /> </td>
         </tr>
         </tbody>
       </table>

1. En el nodo creado en el paso anterior (aquí Columna1), agregue un nodo denominado elementos mediante los siguientes pasos:

   1. Haga clic con el botón derecho en el nodo (aquí Columna1) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** elementos

      **Tipo:** nt:no estructurados

   1. Haga clic en **Guardar todo**.

1. Para crear un campo en la ficha personalizada (aquí Destinatarios), agregue un nodo (aquí GeographicLocation). Esta propiedad corresponde a la columna que ha creado. Siga los pasos siguientes para crear el campo (para crear más campos/nodos, repita estos pasos).::

   1. Haga clic con el botón derecho en el nodo items y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** GeographicLocation (u otro nombre para la propiedad field)

      **Tipo:** nt:no estructurados

   1. Añada las siguientes propiedades en el nodo de campo (aquí GeographicLocation) y haga clic en **Guardar todo**.

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | fieldLabel | Cadena | Ubicación de destinatarios (o el nombre que desea asignar al campo). |
      | name | Cadena | ./extendedproperties/GeographicLocation |
      | representarReadOnly | Booleano | verdadero |
      | sling:resourceType | Cadena | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. Para agregar esta ficha para Cartas, cree una carpeta de superposición con una ruta/estructura similar a la siguiente carpeta de elementos en la siguiente ruta:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   Para crear una superposición para una letra o un recurso diferente, utilice la siguiente ruta reemplazando [assettype] por texto, condición, lista, datadictivo o fragmento:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. Haga clic con el botón derecho en la carpeta items en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** Seleccionado

   1. Haga clic en **Aceptar**. Se crea la carpeta. Haga clic en **Guardar todo**.

1. En la carpeta de elementos recién creada, agregue un nodo para la ficha personalizada del recurso (aquí mytab - este nombre no se muestra en la interfaz de usuario) mediante los siguientes pasos:

   1. Haga clic con el botón derecho en la carpeta items y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** mytab (o el nombre que desea asignar a esta propiedad)

      **Tipo:** nt:no estructurados

   1. Haga clic en el nuevo nodo que ha creado (aquí mytab). CRX muestra las propiedades del nodo.
   1. Añada las dos propiedades siguientes al nodo (aquí customtab):

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor</strong></td>
         </tr>
         <tr>
           <td>path<br /> </td>
           <td>Cadena</td>
           <td>fd/cm/ma/gui/content/cmmetadataproperties/common tab<br /> </td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Cadena</td>
           <td>granito/ui/components/coral/foundation/include<br /> </td>
         </tr>
         </tbody>
       </table>

   1. Haga clic en **Guardar todo**.

1. Para realizar la vista de la personalización, pase el ratón por encima del recurso relevante (aquí una letra), haga clic en Propiedades de la Vista y, a continuación, haga clic en **Editar**. La nueva ficha (Destinatarios) y el nuevo campo (Ubicación de Destinatarios) aparecen en la interfaz de usuario.

   >[!NOTE]
   >
   >Es posible que tenga que borrar la caché del explorador antes de que la personalización aparezca en la interfaz de usuario.

   ![Ficha personalizada agregada a las letras](assets/recipientstab-1.png)

### Escenario: Añadir propiedades personalizadas para tipos de recursos específicos {#scenario-adding-custom-properties-for-specific-asset-types}

Este escenario muestra cómo se puede agregar una propiedad a un tipo de recurso concreto, como un campo a todos los recursos de texto. Con este proceso, puede agregar propiedades a una de las siguientes opciones:

* Texto
* Condición
* Lista
* Fragmento de diseño
* Diccionario de datos
* Carta

Por ejemplo, solo en los recursos de texto, se desea agregar una propiedad, Ubicación de destinatarios, para identificar a qué área geográfica es relevante un recurso.  ![Propiedad personalizada agregada a un recurso](assets/newtabui.png)

Para agregar una propiedad a un tipo de recurso, complete los siguientes pasos:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. Para crear una ficha en un tipo de recurso (como Texto), cree la siguiente estructura de carpetas en la carpeta de aplicaciones:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [AssetType] = texto, condición, lista, letra, datadictivo o fragmento

   A continuación se indican los pasos para crear esta estructura de carpetas:

   1. Haga clic con el botón derecho en la carpeta items en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      Por ejemplo, si desea crear una propiedad para recursos de texto, seleccione la siguiente carpeta:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![Nodo Overlay](assets/textitemstabsitemsoverlaynode1.png)

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmmetadataproperties/[AssetType]/items/tab/items

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      Haga clic en **Guardar todo**.

1. En la carpeta de elementos recién creada, agregue un nodo para la ficha personalizada en el recurso (Ejemplo: custom tab) siguiendo estos pasos:

   1. Haga clic con el botón derecho en la carpeta items y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** customtab (o el nombre que desea asignar a esta propiedad)

      **Tipo:** nt:no estructurados

   1. Haga clic en el nuevo nodo que ha creado (aquí customtab). CRX muestra las propiedades del nodo.
   1. Añada las dos propiedades siguientes al nodo (aquí customtab):

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | sling:resourceType | Cadena | granito/ui/componentes/coral/cimientos/contenedor |
      | jcr:title | Cadena | Nombre del campo en la interfaz de usuario (aquí Mi ficha) |

   1. Haga clic en **Guardar todo**.

1. En el nodo que creó en el paso anterior (aquí customtab), agregue un nodo denominado elementos mediante los siguientes pasos:

   1. Haga clic con el botón derecho en el nodo (aquí customtab) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** elementos

      **Tipo:** nt:no estructurados

   1. Haga clic en **Guardar todo**.

1. En el nodo de elementos que creó en el paso anterior (en la ficha personalizada), agregue un nodo para crear una columna (aquí Columna1) en la ficha personalizada mediante los siguientes pasos (para agregar más columnas, repita este paso):

   1. Haga clic con el botón derecho en el nodo items y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** Columna1 (o el nombre que desea asignar al nodo)

      **Tipo:** nt:no estructurados

   1. Añada la siguiente propiedad al nodo (Aquí Columna1) y haga clic en **Guardar todo**.

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Cadena</td>
           <td>granito/ui/componentes/coral/fundación/contenedor<br /> </td>
         </tr>
         </tbody>
       </table>

1. Para cada columna que cree (como se especifica en el paso anterior - aquí Columna1), cree un nodo denominado elemento mediante los siguientes pasos:

   1. Haga clic con el botón derecho en el nodo de columna correspondiente (aquí Columna1) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** elementos

      **Tipo:** nt:no estructurados

   1. Haga clic en **Guardar todo:**

1. Para cada una de las columnas creadas, cree un nodo en el nodo items para crear un campo en la nueva ficha de la interfaz de usuario. Repita este paso para crear más campos en la columna:

   1. Haga clic con el botón derecho en el nodo relevante (aquí elementos en Columna1) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** nombre de su elección (aquí GeoLocation)

      **Tipo:** nt:no estructurados

   1. Añada las siguientes propiedades al nodo y haga clic en **Guardar todo**.

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | fieldLabel | Cadena | Ubicación de destinatarios (o el nombre que desea asignar al campo). |
      | name | Cadena | `./extendedproperties/GeoLocation` |
      | representarReadOnly | Booleano | verdadero |
      | sling:resourceType | Cadena | granito/ui/componentes/coral/fundación/formulario/campo de texto |

1. Para vista de la personalización, pase el ratón sobre el recurso relevante (aquí un texto), haga clic en Propiedades de la Vista y, a continuación, haga clic en **Editar**. La nueva ficha y campo (Ubicación de Destinatarios) aparecen en la interfaz de usuario.

   >[!NOTE]
   >
   >Es posible que tenga que borrar la caché del explorador antes de que la personalización aparezca en la interfaz de usuario.

   ![Propiedad personalizada agregada a un recurso específico](assets/newtabui-1.png)

### Mostrar propiedades personalizadas en la página de creación de recursos {#display-custom-properties-on-the-asset-creation-page}

De forma predeterminada, las propiedades personalizadas agregadas a las fichas nuevas solo son visibles en la página de propiedades y no en la página de creación de recursos, ya que la página de creación de recursos no tiene presentación de fichas. Para mostrar las propiedades personalizadas en la página de creación de recursos junto con otras propiedades, debe hacer lo siguiente:

1. Haga clic con el botón derecho en la carpeta items en la siguiente ruta y seleccione **Nodo de superposición**:

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores, por letra. Para otros tipos de recursos, la ruta se indica en la tabla siguiente:

   **Ruta:** /libs/fd/cm/ma/gui/content/create_asset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/properties/items/letterproperties/items

   **Ubicación:** /apps/

   **Coincidir tipos de nodo:** Seleccionado

   Según el tipo de recurso, la ruta debe ser la siguiente:

   | **Tipo de recurso/documento** | **Ruta que se agregará** |
   |---|---|
   | Texto | /libs/fd/cm/ma/gui/content/create_asset/createtext/jcr:content/body/items/form/items/textWizard/items/editproperties/items/properties/items/items/tab/items1/items |
   | Lista | /libs/fd/cm/ma/gui/content/createAsset/createlist/jcr:content/body/items/form/items/listWizard/items/editproperties/items/properties/items/items/tab/items1 |
   | Condición | /libs/fd/cm/ma/gui/content/create_asset/create/econdition/jcr:content/body/items/form/items/conditionWizard/items/editproperties/items/properties/items/items/tab/items1/items |
   | Fragmento | /libs/fd/cm/ma/gui/content/create_asset/createfragment/jcr:content/body/items/form/items/fragmentWizard/items/properties/properties/properties/items/tab2/items/tab1/items |
   | Carta | /libs/fd/cm/ma/gui/content/createAsset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/properties/items/letterproperties/items |

1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

1. Bajo el nodo elementos de superposición que ha creado, cree un nodo con el nombre col4 (o cualquier otro nombre) y haga clic en **Guardar todo**.

   Por ejemplo, a continuación se muestra el nodo de superposición creado para las letras.

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. Añada las siguientes propiedades al nodo recién creado (aquí col4) y haga clic en **Guardar todo**:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td>path</td>
   <td>Cadena</td>
   <td><p>Esta ruta es el puntero a la columna creada en:</p>
    <ul>
     <li>Ficha común para todos los tipos de recursos: /apps/fd/cm/ma/gui/content/cmmetadataproperties/common tab/items/col1</li>
     <li>Para diferentes propiedades para distintos tipos de recursos: /apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tab/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Cadena</td>
   <td> granito/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![personalizfieldappear inmainproperties](assets/customfieldappearinginmainproperties.png)

Propiedad personalizada, Idioma, que aparece en la interfaz de usuario para crear una carta

## Personalice la vista de lista para mostrar propiedades personalizadas {#customize-the-list-view-to-show-custom-properties}

Después de agregar una propiedad personalizada a los recursos de Administración de correspondencia, debe realizar más cambios en CRX/DE para asegurarse de que la propiedad personalizada se muestra en la interfaz de usuario de Administración de correspondencia.

Complete los siguientes pasos para mostrar la propiedad personalizada en la interfaz de usuario de lista de recursos de Correspondence Management:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. Cree la siguiente estructura de carpetas en la carpeta de aplicaciones:

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   A continuación se indican los pasos para crear esta estructura de carpetas:

   1. Haga clic con el botón derecho en la carpeta columns en la siguiente ruta y seleccione **Overlay Node**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/gui/content/cmassets/jcr:content/vistas/listas/columnas

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      Haga clic en **Guardar todo**.

1. Para cada una de las propiedades creadas, cree un nodo en el nodo de columnas para crear una columna en la interfaz de usuario. Repita este paso para crear más columnas en la interfaz de usuario:

   1. Haga clic con el botón derecho en el nodo (columnas) relevante y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** Nombre de su elección (aquí GeographicLocation)

      **Tipo:** nt:no estructurados

   1. Añada las siguientes propiedades al nodo y haga clic en **Guardar todo**.

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor</strong></td>
         </tr>
         <tr>
           <td>jcr:primaryType</td>
           <td>Nombre</td>
           <td><p>nt:unstructured</p> </td>
         </tr>
         <tr>
           <td>jcr:title</td>
           <td>Cadena</td>
           <td><p>Ubicación geográfica</p> <p>Este valor aparece como el encabezado de columna en la interfaz de usuario. </p> </td>
         </tr>
         <tr>
           <td>sortable</td>
           <td>Booleano</td>
           <td><p>verdadero</p> <p>Un valor true significa que el usuario puede ordenar los valores de esta columna. </p> </td>
         </tr>
         </tbody>
       </table>

1. Cree la siguiente estructura de carpetas en la carpeta de aplicaciones:

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   A continuación se indican los pasos para crear esta estructura de carpetas:

   1. Haga clic con el botón derecho en la carpeta columns en la siguiente ruta y seleccione **Overlay Node**:

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/components/admin/child-pagerenderer/child-pagePágina

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      Haga clic en **Guardar todo**.

1. Copie el archivo childPage.jsp de la siguiente ubicación:

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   Pegue el archivo en la siguiente ubicación:

   /apps//fd/cm/ma/gui/components/admin/childEnderer/childPage/.

1. Abra el archivo childPage.jsp (/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp) y realice los siguientes cambios:

   1. Añada lo siguiente a la línea 19 del archivo (siguiendo la declaración de copyright).

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. Añada el siguiente código de una función que obtiene el valor de cada propiedad personalizada hasta el final del archivo:

      ```jsp
      <%!
          private String getCustomPropertyValue(Map<String, Object> extendedProperties, String propertyName) {
      
              String propertyValue = "";
              if (extendedProperties.containsKey(propertyName)) {
                  propertyValue = (String) extendedProperties.get(propertyName);
              }
      
              return propertyValue;
          }
      %>
      ```

   1. Añada lo siguiente antes del inicio de la etiqueta &lt;tr> (&lt;tr &lt;%= attrs.build() %>>):

      ```jsp
      <%
          String GeoLocation = "";
          if (asset != null) {
                  Map<String, Object> extendedProperties = asset.getExtendedProperties();
                  if (extendedProperties != null) {
                      GeoLocation = getCustomPropertyValue(extendedProperties,"GeoLocation");
                  }
          }
      %>
      ```

      En el código, GeoLocation es el valor que se establece en la propiedad name al crear el nodo o campo personalizado. Al crear un nodo o campo personalizado, especificó el nombre de la propiedad con ./extendedproperties/ prefix: ./extendedproperties/GeoLocation. En el código, el prefijo no es obligatorio.

   1. Para mostrar la nueva propiedad en la interfaz de usuario, agregue una etiqueta TD como se indica a continuación antes de la etiqueta tr de cierre (&lt;/tr>):

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      Para agregar más columnas, repita los pasos 6.3 y 6.4.

   1. Haga clic en **Guardar todo**.

1. Para vista de la personalización, abra la vista de lista de fragmentos de documento o letras en las que haya agregado la propiedad personalizada.

   La columna UI y la propiedad agregadas en este procedimiento se muestran para todos los tipos de recursos. Sin embargo, los valores de estas propiedades se pueden introducir y mostrar solo para los tipos de recursos para los que se agregó originalmente la propiedad personalizada.

   Por ejemplo, con el escenario: Si añade propiedades personalizadas para tipos de recursos específicos y agrega una propiedad personalizada a los recursos de texto, puede introducir propiedades personalizadas solo para los recursos de texto. Sin embargo, si muestra esa propiedad personalizada en la interfaz de usuario, la columna aparece para todos los tipos de recursos.

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. (Opcional) De forma predeterminada, la nueva columna aparece como la última columna en la interfaz de usuario. Para que la columna aparezca en una posición específica, agregue la siguiente propiedad al nodo de columna:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td>sling:orderBefore</td>
   <td>Cadena</td>
   <td><p>Nombre del nodo de columna en la ruta "/libs/fd/cm/ma/gui/content/cmassets/jcr:content/vistas/lista/columnas" antes de la cual debe aparecer la columna personalizada en la interfaz de usuario.</p> <p>Aquí, si desea que la columna Ubicación geográfica aparezca antes (a la izquierda) de la columna Versión, agregue la propiedad sling:orderBefore al nodo GeoLocation en la ruta ""/apps/fd/cm/ma/gui/content/cmassets/jcr:content/vistas/lista/columns/GeoLocation" y defina el valor de propiedad en version.</p> </td>
  </tr>
 </tbody>
</table>

Cuando se agrega la propiedad sling:orderBefore para especificar la ubicación de la columna, también es necesario actualizar el orden de la etiqueta &lt;td> correspondiente especificada en el paso 6.4 de este procedimiento. Por ejemplo, en este caso, debe asegurarse de que la etiqueta &lt;td> de Ubicación geográfica se coloque antes que la etiqueta &lt;td> de la columna Versión:

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## Habilitar la búsqueda de propiedades personalizadas {#enable-search-for-custom-properties}

De forma predeterminada, la búsqueda de texto completo no incluye las propiedades personalizadas que se agregan a la interfaz de usuario con CRX/DE.

Para incluir las propiedades personalizadas en la búsqueda, debe permitir la indexación de las propiedades personalizadas.

Para permitir la indexación de propiedades personalizadas, complete los siguientes pasos:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. Vaya a `/oak:index/cmLucene`y agregue un nodo denominado **agregados** debajo de él.

   1. Haga clic con el botón derecho en la carpeta cmLucene y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** agregados

      **Tipo:** nt:no estructurados

   1. Haga clic en **Guardar todo**.

1. En la carpeta de agregados recién creada, agregue un nodo cm:resource. Y en cm:resource, agregue un nodo llamado include0.

   1. Haga clic con el botón derecho en la carpeta de agregados y seleccione **Crear** > **Crear nodo**. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** cm:recurso

      **Tipo:** nt:no estructurados

   1. Haga clic con el botón derecho en la carpeta cm:resource y seleccione **Crear** > **Crear nodo**. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** include0

      **Tipo:** nt:no estructurados

   1. Haga clic en el nuevo nodo que ha creado (aquí include0). CRX muestra las propiedades del nodo.
   1. Añada la siguiente propiedad al nodo (aquí include0):

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor</strong></td>
         </tr>
         <tr>
           <td>path</td>
           <td>Cadena</td>
           <td>expandedProperties<br /> </td>
         </tr>
         </tbody>
       </table>

   1. Haga clic en **Guardar todo**.

1. Vaya a las propiedades en la siguiente ubicación y agregue una ubicación de nodo debajo de ella: `/oak:index/cmLucene/indexRules/cm:resource/properties`

   Repita este paso para cada una de las propiedades personalizadas que desee agregar a la búsqueda.

   1. Haga clic con el botón derecho en la carpeta de propiedades y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los valores siguientes y haga clic en **Aceptar**:

      **Nombre:** ubicación (o el nombre de la propiedad personalizada que desea agregar a la búsqueda)

      **Tipo:** nt:no estructurados

   1. Haga clic en el nuevo nodo que ha creado (aquí ubicación). CRX muestra las propiedades del nodo.
   1. Añada las siguientes propiedades en el nodo (aquí ubicación):

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | analizado | Cadena | verdadero |
      | name | Cadena | expandedProperties/location (o el nombre de la propiedad que desea agregar a la búsqueda) |
      | propertyIndex | Booleano | verdadero |
      | useInSugger | Booleano | verdadero |

   1. Haga clic en **Guardar todo**.

1. Ahora puede utilizar valores de propiedad personalizados en la búsqueda de texto completo para localizar recursos relevantes.

>[!NOTE]
>
>Si todavía no puede realizar la búsqueda, puede deberse a un problema de indexación. Para volver a indexar, vaya al nodo siguiente y cambie el valor de la propiedad &quot;re-index&quot; a true:
>
>/oak:index/cmLucene&quot; y cambiar el valor de la propiedad

## Cambiar la vista predeterminada de la página de búsqueda {#change-default-view-of-the-search-page}

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta con el nombre lista con una ruta/estructura similar a la carpeta de listas ubicada en /libs/granite/ui/content/shell/omnisearch/searchresults/singlerresults/vistas:

   1. Haga clic con el botón derecho en la carpeta items en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/granite/ui/content/shell/omnisearch/searchresults/singlerresults/vistas/lista

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

   1. Haga clic en **Guardar todo**.

1. En la lista del nodo recién creado, agregue la siguiente propiedad y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>Cadena</td>
      <td>tarjeta</td>
   </tr>
   </tbody>
   </table>

1. La personalización muestra los resultados de búsqueda en la vista de Listas para todas las consolas, incluidos Forms y Documentos, Recursos y Sitios.

## Cambiar la vista predeterminada de la página de recursos {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>Estos pasos cambian la vista predeterminada de todas las consolas, como Forms y Documentos, Recursos y Sitios.

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta con el nombre lista con una ruta/estructura similar a la carpeta de listas ubicada en:

   /libs/fd/cm/ma/gui/content/cmassets/jcr:content/vistas/

   1. Haga clic con el botón derecho en la carpeta items en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tiene los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/vistas/lista

      **Ubicación:** /apps/

      **Coincidir tipos de nodo:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

   1. Haga clic en **Guardar todo**.

1. En la lista del nodo recién creado, agregue la siguiente propiedad y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>Cadena</td>
      <td>tarjeta</td>
   </tr>
   </tbody>
   </table>

1. Borre las cookies del navegador o utilice el modo incógnito del navegador para realizar la vista de los recursos. De forma predeterminada, la página de recursos aparece en el diseño de la tarjeta.

## Mostrar u ocultar propiedades personalizadas en páginas de propiedades y creación de recursos {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

Para mostrar u ocultar las propiedades personalizadas, complete los siguientes pasos:

1. Bajo el nodo de propiedad personalizado, como la asignación geográfica, cree un nuevo nodo con el nombre &quot;granite:rendercondition&quot; de tipo &quot;nt:unstructure&quot;.
1. Añada la siguiente propiedad al nodo y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor</strong></td>
   </tr>
   <tr>
      <td>sling:resourceType<br /> </td>
      <td>Cadena</td>
      <td>fd/cm/ma/gui/components/admin/assetsproperties/custompropertyconfig<br /> </td>
   </tr>
   </tbody>
   </table>

1. Para ocultar esta propiedad en la página de creación de recursos, añada la siguiente propiedad y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor</strong></td>
   </tr>
   <tr>
      <td>hideOnCreate<br /> </td>
      <td>Booleano</td>
      <td>verdadero<br /> </td>
   </tr>
   </tbody>
   </table>

1. Para ocultar la propiedad personalizada en la página de propiedades de los recursos, añada la siguiente propiedad y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor</strong></td>
   </tr>
   <tr>
      <td>hideOnEdit<br /> </td>
      <td>Booleano</td>
      <td>verdadero<br /> </td>
   </tr>
   </tbody>
   </table>

   Para volver a mostrar los valores, restablezca los valores de propiedad a `false` o elimine las entradas de propiedad.
