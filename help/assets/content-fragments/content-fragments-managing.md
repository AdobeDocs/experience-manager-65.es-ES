---
title: Administrar fragmentos de contenido
description: Aprenda a utilizar la consola Recursos para administrar los fragmentos de contenido AEM, la base del contenido sin encabezado.
feature: Content Fragments
role: User
source-git-commit: 251bf0ac672d516dd6b2018fc9cc804822f48e4c
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 11%

---

# Administrar fragmentos de contenido {#managing-content-fragments}

Aprenda a utilizar la consola Recursos para administrar los fragmentos de contenido AEM, la base del contenido sin encabezado.

Después de definir los [Modelos de fragmento de contenido](#creating-a-content-model) puede utilizarlos para [crear sus fragmentos de contenido](#creating-a-content-fragment).

El [Editor de fragmentos de contenido](#opening-the-fragment-editor) proporciona varios [modos](#modes-in-the-content-fragment-editor) que le permiten:

* [Edite el ](#editing-the-content-of-your-fragment) contenido y  [administre Variaciones](#creating-and-managing-variations-within-your-fragment)
* [Anotar el fragmento](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Asociar contenido al fragmento](#associating-content-with-your-fragment)
* [Configuración de los metadatos](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Ver el árbol de estructura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Vista previa de la representación JSON](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>Se pueden utilizar fragmentos de contenido:
>
>* al crear páginas; consulte [Creación de páginas con fragmentos de contenido](/help/sites-authoring/content-fragments.md).
>* para [Entrega de contenido sin encabezado mediante fragmentos de contenido con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).


>[!NOTE]
>
>Los fragmentos de contenido se almacenan como **Assets**, por lo que se administran principalmente desde la consola **Assets**.

## Creación de fragmentos de contenido {#creating-content-fragments}

### Creación de un modelo de contenido {#creating-a-content-model}

[Los ](/help/assets/content-fragments/content-fragments-models.md) modelos de fragmentos de contenido se pueden habilitar y crear antes de crear fragmentos de contenido con contenido estructurado.

### Creación de un fragmento de contenido {#creating-a-content-fragment}

El método para crear un fragmento de contenido es:

1. Vaya a la carpeta **Assets** en la que desea crear el fragmento.
1. Seleccione **Crear** y, a continuación, **Fragmento de contenido** para abrir el asistente.
1. El primer paso del asistente requiere que especifique la base del nuevo fragmento.

   * [Modelo](/help/assets/content-fragments/content-fragments-models.md) : se utiliza para crear un fragmento que requiere contenido estructurado; por ejemplo,  **** Adventuremodel

      * Se muestran todos los modelos disponibles.

   Después de la selección, utilice **Next** para continuar.

   ![base de fragmento](assets/cfm-managing-01.png)

1. En el paso **Propiedades**, especifique:

   * **Básico**

      * **Título**

         El título del fragmento.

         Obligatorio.

      * **Descripción**

      * **Etiquetas**
   * **Avanzado**

      * **Nombre**

         El nombre; se utilizará para formar la dirección URL.

         Obligatorio; se derivan automáticamente del título, pero se pueden actualizar.


1. Seleccione **Crear** para completar la acción y, a continuación, **Abra** el fragmento para editarlo o vuelva a la consola pulsando **Listo**.

   >[!NOTE]
   >En el modo **List** de la consola, puede actualizar la **View Settings** para habilitar la columna **Content Fragment Model**.

## Acciones para un fragmento de contenido en la consola Recursos {#actions-for-a-content-fragment-assets-console}

En la consola **Assets** hay una serie de acciones disponibles para los fragmentos de contenido:

* Desde la barra de herramientas; después de seleccionar el fragmento, están disponibles todas las acciones adecuadas.
* Como [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions); un subconjunto de acciones disponibles para las tarjetas de fragmento individuales.

![acciones](assets/cfm-managing-02.png)

Seleccione el fragmento para mostrar la barra de herramientas con las acciones aplicables:

* **Descargar**

   * Guarde el fragmento como archivo ZIP; puede definir si desea incluir elementos, variables y metadatos.

* **Crear**
* **Cierre de compra**
* **Propiedades**

   * Permite ver o editar los metadatos del fragmento.

* **Editar**

   * Le permite [abrir el fragmento para editar contenido](/help/assets/content-fragments/content-fragments-variations.md) junto con sus elementos, variaciones, contenido asociado y metadatos.

* **Administrar etiquetas**
* **A la colección**
* **Copiar**  (y  **pegar**)
* **Mover**
* **Publicación rápida**
* **Administrar publicación**
* **Eliminar**

>[!NOTE]
>
>Muchas de ellas son [acciones estándar para Assets](/help/assets/manage-assets.md) o [AEM aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es).

## Apertura del editor de fragmentos {#opening-the-fragment-editor}

Para abrir el fragmento para editarlo:

>[!CAUTION]
>
>Para editar un fragmento de contenido necesita [los permisos adecuados](/help/sites-developing/customizing-content-fragments.md#asset-permissions). Póngase en contacto con el administrador del sistema si tiene problemas.

>[!CAUTION]
>
>Para editar un fragmento de contenido, necesita los permisos adecuados. Póngase en contacto con el administrador del sistema si tiene problemas.

1. Utilice la consola **Assets** para desplazarse a la ubicación del fragmento de contenido.
1. Abra el fragmento para editarlo mediante:

   * Tocando o haciendo clic en el fragmento o vínculo de fragmento (depende de la vista de la consola).
   * Seleccione el fragmento y, a continuación, **Edit** en la barra de herramientas.

1. Se abrirá el editor de fragmentos. Realice los cambios según sea necesario:

   ![editor de fragmentos](assets/cfm-managing-03.png)

1. Después de realizar los cambios, utilice **Guardar y cerrar**.

<!-- 
1. After making changes, use **Save**, **Save & close** or **Close** as required.

   >[!NOTE]
   >
   >**Save & close** is available via the **Save** dropdown.

   >[!NOTE]
   >
   >Both **Save & Close** and **Close** will exit the editor - see [Save, Close and Versions](#save-close-and-versions) for full information on how the various options operate for content fragments.
-->

## Modos y acciones en el editor de fragmentos de contenido {#modes-actions-content-fragment-editor}

Hay varios modos y acciones disponibles en el Editor de fragmentos de contenido.

### Modos en el editor de fragmentos de contenido {#modes-in-the-content-fragment-editor}

Desplácese por los distintos modos utilizando los iconos del panel lateral:

* Variaciones: [Edición del contenido](#editing-the-content-of-your-fragment) y [Administración de las variaciones](#creating-and-managing-variations-within-your-fragment)

* [Anotaciones](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Contenido asociado](#associating-content-with-your-fragment)
* [Metadatos](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Árbol de estructura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Vista previa](/help/assets/content-fragments/content-fragments-json-preview.md)

![modos](assets/cfm-managing-04.png)

### Acciones de barra de herramientas en el editor de fragmentos de contenido {#toolbar-actions-in-the-content-fragment-editor}

Algunas funciones de la barra de herramientas superior están disponibles en varios modos:

<!-- screenshot changed from original text see commented out below -->

![modos](assets/cfm-managing-03.png)

* Se mostrará un mensaje cuando ya se haga referencia al fragmento en una página de contenido. Puede **Cerrar** el mensaje.

* El panel lateral se puede ocultar o mostrar mediante el icono **Alternar panel lateral**.

* Debajo del nombre del fragmento puede ver el nombre del [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) utilizado para crear el fragmento actual:

   * El nombre también es un vínculo que abrirá el editor de modelos.

* Ver el estado del fragmento; por ejemplo, información sobre cuándo se creó, modificó o publicó.

* **Guardar y cerrar**

<!--
Some features in the top toolbar are available from multiple modes:

![modes](assets/cfm-managing-top-toolbar.png)

* A message will be shown when the fragment is already referenced on a content page. You can **Close** the message.

* The side panel can be hidden/shown using the **Toggle Side Panel** icon.

* Underneath the fragment name you can see the name of the [Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md) used for creating the current fragment:

  * The name is also a link that will open the model editor.

* See the status of the fragment; for example, information about when it was created, modified or published. The status is also color-coded:

  * **New**: grey
  * **Draft**: blue
  * **Published**: green
  * **Modified**: orange
  * **Deactivated**: red

* **Save** provides access to the **Save & close** option.
  
* The three dots (**...**) drop-down provides access to additional actions:
  * **Update page references**
    * This updates any page references. 
  * **[Quick publish](#publishing-and-referencing-a-fragment)**
  * **[Manage Publication](#publishing-and-referencing-a-fragment)**
-->

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

<!--
## Save, Close and Versions {#save-close-and-versions}

>[!NOTE]
>
>Versions can also be [created, compared and reverted from the Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

The editor has various options:

* **Save** and **Save & close**

  * **Save** will save the latest changes and remain in the editor.
  * **Save & close** will save the latest changes and exit the editor.

  >[!CAUTION]
  >
  >To edit a content fragment you need [the appropriate permissions](/help/sites-developing/customizing-content-fragments.md#asset-permissions). Please contact your system administrator if you are experiencing issues. 

  >[!NOTE]
  >
  >It is possible to remain in the editor, making a series of changes, before saving.

  >[!CAUTION]
  >
  >In addition to simply saving your changes, the actions also update any references and ensures that the Dispatcher is flushed as required. These changes can take time to process. Due to this, there can be a performance impact on a large/complex/heavily-loaded system.
  >
  >Please bear this in mind when using **Save & close** and then quickly re-entering the fragment editor to make and save further changes.

* **Close**

  Will exit the editor without saving the latest changes (i.e made since the last **Save**).

While editing your content fragment AEM automatically creates versions to ensure that prior content can be restored if you cancel your changes (using **Close** without saving):

1. When a content fragment is opened for editing AEM checks for the existence of the cookie-based token that indicates whether an *editing session* exists:

   1. If the token is found, the fragment is considered to be part of the existing editing session.
   2. If the token is *not* available and the user starts editing content, a version is created and a token for this new editing session is sent to the client, where it is saved in a cookie.

2. While there is an *active* editing session, the content being edited is automatically saved every 600 seconds (default).

   >[!NOTE]
   >
   >The auto save interval is configurable using the `/conf` mechanism.
   >
   >Default value, see:
   >&nbsp;&nbsp;`/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. If the user cancels the edit, the version created at the start of the editing session is restored and the token is removed to end the editing session.
4. If the user selects to **Save** the edits, the updated elements/variations are persisted and the token is removed to end the editing session.
-->

## Edición del contenido del fragmento {#editing-the-content-of-your-fragment}

Una vez abierto el fragmento, puede utilizar la pestaña [Variations](/help/assets/content-fragments/content-fragments-variations.md) para crear el contenido.

## Creación y administración de variaciones dentro del fragmento {#creating-and-managing-variations-within-your-fragment}

Una vez creado el contenido principal, puede crear y administrar [Variaciones](/help/assets/content-fragments/content-fragments-variations.md) de dicho contenido.

## Asociación del contenido al fragmento {#associating-content-with-your-fragment}

También puede [asociar contenido](/help/assets/content-fragments/content-fragments-assoc-content.md) con un fragmento. Esto proporciona una conexión para que los recursos (es decir, las imágenes) se puedan utilizar (opcionalmente) con el fragmento cuando se añada a una página de contenido.

## Visualización y edición de los metadatos (propiedades) del fragmento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

Puede ver y editar las propiedades de un fragmento mediante la pestaña [Metadata](/help/assets/content-fragments/content-fragments-metadata.md).

## Cronología de los fragmentos de contenido {#timeline-for-content-fragments}

Además de las opciones estándar, [Línea de tiempo](/help/assets/manage-assets.md#timeline) proporciona información y acciones específicas para los fragmentos de contenido:

* Ver información sobre versiones, comentarios y anotaciones
* Acciones para las versiones

   * **[Revertir a esta versión](#reverting-to-a-version)**  (seleccione un fragmento existente y, a continuación, una versión específica)

   * **[Comparar con actual](#comparing-fragment-versions)**  (seleccione un fragmento existente y luego una versión específica)

   * Agregue una **Etiqueta** o **Comentario** (seleccione un fragmento existente y luego una versión específica)

   * **Guardar como versión**  (seleccione un fragmento existente y luego la flecha hacia arriba en la parte inferior de la línea de tiempo)

* Acciones para anotaciones

   * **Eliminar**

>[!NOTE]
>
>Los comentarios son:
>
>* Funcionalidad estándar para todos los recursos
>* Se ha realizado en la línea de tiempo
>* Relacionado con el recurso de fragmento

>
>Las anotaciones (para fragmentos de contenido) son:
>
>* Introducido en el editor de fragmentos
>* Específico para un segmento seleccionado de texto dentro del fragmento

>


Por ejemplo:

![cronología](assets/cfm-managing-05.png)

## Comparación de versiones de fragmento {#comparing-fragment-versions}

La acción **Comparar con actual** está disponible en la [Línea de tiempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) después de seleccionar una versión específica.

Se abrirá:

* la versión **actual** (más reciente) (izquierda)

* la versión seleccionada **v&lt;*x.y*** (derecha)

Se mostrarán una al lado de la otra, donde:

* Se resaltan todas las diferencias

   * Texto eliminado: rojo
   * Texto insertado - verde
   * Texto reemplazado - azul

* El icono de pantalla completa le permite abrir cualquiera de las versiones por su cuenta; a continuación, vuelva a la vista paralela
* Puede **Revertir** a la versión específica
* **** Donewill le devolverá a la consola

>[!NOTE]
>
>No se puede editar el contenido del fragmento al comparar fragmentos.

![comparar](assets/cfm-managing-06.png)

## Reversión a una versión  {#reverting-to-a-version}

Puede volver a una versión específica del fragmento:

* Directamente desde la [línea de tiempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Seleccione la versión requerida y luego la acción **Revertir a esta versión**.

* Mientras [compara una versión con la versión actual](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) puede **Revertir** a la versión seleccionada.

## Publicación y referencia de un fragmento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>Si el fragmento se basa en un modelo, debe asegurarse de que el modelo [se ha publicado](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
>Si publica un fragmento de contenido para el que el modelo aún no se ha publicado, una lista de selección lo indicará y el modelo se publicará con el fragmento.

Los fragmentos de contenido deben publicarse para su uso en el entorno de publicación. Se pueden publicar:

* Después de la creación; uso de [acciones disponibles en la consola de Assets](#actions-for-a-content-fragment-assets-console).
* Desde el [Editor de fragmentos de contenido](#toolbar-actions-in-the-content-fragment-editor).
* Cuando [publica una página que utiliza el fragmento](/help/sites-authoring/content-fragments.md#publishing); el fragmento se enumerará en las referencias de página.

>[!CAUTION]
>
>Después de publicar un fragmento o de hacer referencia a él, AEM mostrará una advertencia cuando un autor abra el fragmento para editarlo de nuevo. Esto sirve para advertir que los cambios en el fragmento también afectarán a las páginas a las que se hace referencia.

## Eliminación de un fragmento {#deleting-a-fragment}

Para eliminar un fragmento:

1. En la consola **Assets** vaya a la ubicación del fragmento de contenido.
2. Seleccione el fragmento.

   >[!NOTE]
   >
   >La acción **Delete** no está disponible como acción rápida.

3. Seleccione **Delete** en la barra de herramientas.
4. Confirme la acción **Delete**.

   >[!CAUTION]
   >
   >Si ya se hace referencia al fragmento en una página, verá un mensaje de advertencia y será necesario para confirmar que desea continuar con la **eliminación forzada**. El fragmento, junto con su componente de fragmento de contenido, se eliminará de cualquier página de contenido.
