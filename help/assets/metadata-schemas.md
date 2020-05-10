---
title: 'esquemas de metadatos para definir la presentación de la página de propiedades de metadatos en [!DNL Adobe Experience Manager Assets]. '
description: El esquema de metadatos define la presentación de la página de propiedades y las propiedades de metadatos que se muestran para los recursos. Obtenga información sobre cómo crear un esquema de metadatos personalizado, editar el esquema de metadatos y aplicar el esquema de metadatos a los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 739f1c6fcc910ed134849c27a44a6feccd1684c9
workflow-type: tm+mt
source-wordcount: '2738'
ht-degree: 10%

---


# Esquemas de metadatos {#metadata-schemas}

Las organizaciones cuentan con un modelo de metadatos que mejora la detección, el uso, la interoperabilidad de los recursos, etc. La aplicación correcta de metadatos es sacrosanta para mantener los procesos y flujos de trabajo basados en metadatos. Para atenerse a las normas y estrategias de metadatos de toda la organización, puede utilizar esquemas de metadatos que ayudan a los usuarios de DAM a alinearse. Adobe Experience Manager permite crear, mantener y aplicar esquemas de metadatos con métodos sencillos y flexibles.

En [!DNL Adobe Experience Manager Assets], los esquemas contienen campos específicos para la información específica que se debe rellenar. También contiene información de diseño para mostrar los campos de metadatos de forma sencilla. Las propiedades de metadatos incluyen título, descripción, tipos MIME, etiquetas y mucho más. Puede utilizar el editor de formularios [!UICONTROL Esquema de] metadatos para modificar los esquemas existentes o agregar esquemas de metadatos personalizados.

Para vista y edición de la página de propiedades de un recurso, siga estos pasos:

1. Toque o haga clic en el icono Propiedades **[!UICONTROL de la]** Vista en Acciones rápidas del mosaico del recurso en vista de tarjetas.

   ![Acciones rápidas en el mosaico de recursos](assets/chlimage_1-170.png)

1. Edite varias propiedades de metadatos en las distintas fichas. Sin embargo, no puede modificar el tipo de recurso en la página [!UICONTROL Propiedades] .

   ![Ficha Básico de Propiedades del recurso, donde no se puede cambiar el tipo de recurso](assets/asset-properties-basic-tab.png)

1. Puede editar varias propiedades de metadatos en las fichas disponibles. Sin embargo, no puede modificar el [!UICONTROL tipo] de recurso en la ficha [!UICONTROL Básico] de la página de propiedades.

   ![Ficha Básico de Propiedades del recurso, donde no se puede cambiar el tipo de recurso](assets/asset-properties-basic-tab.png)

*Figura: Ficha Básico de[!UICONTROL Propiedades]de recurso.*

Para modificar el tipo MIME de un recurso, utilice un formulario de esquema de metadatos personalizado o modifique un formulario existente. Consulte [Editar formularios](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) de Esquema de metadatos para obtener más información. Si modifica el esquema de metadatos para un tipo MIME determinado, se modificará la presentación de la página de propiedades de los recursos con el tipo MIME actual y todos los subtipos de recursos. Por ejemplo, la modificación de un esquema jpeg en `default/image` solo modifica la presentación de metadatos (propiedades del recurso) de los recursos con tipo MIME `image/jpeg`. Sin embargo, si edita el esquema predeterminado, los cambios modifican la presentación de los metadatos de todos los tipos de recursos.

## Formularios de esquema de metadatos {#default-metadata-schema-forms}

Para vista de una lista de formularios/plantillas, en [!DNL Experience Manager] la interfaz vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Esquemas **** de metadatos.

[!DNL Experience Manager] proporciona las siguientes plantillas de formulario de Esquema de metadatos:

| Plantillas |  | Descripción |
|---|---|---|
| [!UICONTROL predeterminada] |  | Formulario de esquema de metadatos base para los recursos. |
|  | Los siguientes formularios secundarios heredan las propiedades del formulario [!UICONTROL predeterminado] : |  |
|  | <ul><li> [!UICONTROL image]</li></ul> | Formulario de Esquema para recursos con el tipo MIME &quot;image&quot;, por ejemplo, image/jpeg, image/png, etc. <br> El formulario [!UICONTROL de imagen] tiene las siguientes plantillas de formulario secundarias: <ul><li> [!UICONTROL jpeg]: Formulario de Esquema para recursos con subtipo [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: Formulario de Esquema para los recursos con subtipo [!UICONTROL tiff].</li></ul> |
|  | <ul><li> [!UICONTROL aplicación]</li></ul> | Formulario de Esquema para recursos con tipo MIME &quot;aplicación&quot;, por ejemplo, application/ pdf, application/ zip, etc. <br>[!UICONTROL pdf]: Formulario de Esquema para recursos con subtipo pdf. |
|  | <ul><li>[!UICONTROL vídeo]</li></ul> | Formulario de Esquema para recursos con tipo MIME &quot;video&quot;, como video/avi, video/mp4, etc. |
| [!UICONTROL colección] |  | Formulario de Esquema para colecciones. |
| [!UICONTROL contentfragment] |  | Formulario de Esquema para fragmentos de contenido. |
| [!UICONTROL formularios] |  | Este formulario de esquema está relacionado con los formularios [de](/help/forms/home.md)Adobe Experience Manager. |

>[!NOTE]
>
>Para vista de los formularios secundarios de un formulario de esquema, haga clic en el nombre del formulario de esquema.

## Añadir un formulario de esquema de metadatos {#add-a-metadata-schema-form}

1. Para agregar una plantilla personalizada a la lista, haga clic en **[!UICONTROL Crear]** desde la barra de herramientas.

   >[!NOTE]
   >
   >Las plantillas sin editar tienen un icono de candado. Si personaliza cualquiera de las plantillas, el icono de bloqueo desaparece de antes de la plantilla.

1. En el cuadro de diálogo, introduzca el título del formulario de esquema y haga clic en **[!UICONTROL Crear]** para completar el proceso de creación del formulario.

## Editar formularios de esquema de metadatos {#edit-metadata-schema-forms}

Puede editar un formulario de esquema de metadatos que se acaba de agregar o que ya exista. El formulario de esquema de metadatos incluye fichas y elementos de formulario en fichas. Puede asignar/configurar estos elementos de formulario a un campo dentro de un nodo de metadatos en el repositorio de CRX. Puede agregar nuevas fichas o elementos de formulario al formulario de esquema de metadatos. Las fichas y los elementos de formulario derivados del elemento principal están en estado bloqueado. No se pueden alterar a nivel secundario.

1. In the Schema Forms page, select the check box before a form and then click **[!UICONTROL Edit]** on the toolbar.

1. En la página **[!UICONTROL Editor de esquemas de metadatos]**, personalice la página de propiedades del recurso arrastrando uno o varios componentes de la lista de tipos de componentes de la pestaña **[!UICONTROL Generar formulario]** a **[!UICONTROL Básico]**.

   ![Editor de Esquemas de metadatos para personalizar la página Propiedades del recurso](assets/metadata-schema-editor.png)

   *Figura:[!UICONTROL Ficha Básica]del editor de Esquema[!UICONTROL de]metadatos.*

1. Para configurar un componente, selecciónelo y modifique sus propiedades en la ficha **[!UICONTROL Configuración]** .

### Componentes de la ficha Formulario de compilación {#components-within-the-build-form-tab}

La ficha **[!UICONTROL Generar formulario]** lista los elementos de formulario que se utilizan en el formulario de esquema. La ficha **[!UICONTROL Configuración]** proporciona los atributos de cada elemento seleccionado en la ficha **[!UICONTROL Generar formulario]** . La siguiente tabla lista los elementos de formulario disponibles en la ficha **[!UICONTROL Generar formulario]** :

| Nombre del componente | Descripción |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL Sección de encabezado] | Añada un encabezado de sección para una lista de componentes comunes. |
| [!UICONTROL Texto de una sola línea] | Añada una propiedad de texto de una sola línea. Se almacena como una cadena. |
| [!UICONTROL Texto con varios valores] | Añada una propiedad de texto con varios valores. Se almacena como una matriz de cadenas. |
| [!UICONTROL Número] | Añada un componente numérico. |
| [!UICONTROL Fecha] | Añada un componente de fecha. |
| [!UICONTROL Lista desplegable] | Añada una lista desplegable. |
| [!UICONTROL Etiquetas estándar] | Añadir una etiqueta. |
| [!UICONTROL Etiquetas inteligentes] | Añada para aumentar las capacidades de búsqueda agregando automáticamente etiquetas de metadatos. |
| [!UICONTROL Campo oculto] | Añada un campo oculto. Se envía como parámetro POST cuando se guarda el recurso. |
| [!UICONTROL Recurso al que se hace referencia en] | Añada este componente a la lista de vista de los recursos a los que hace referencia el recurso. |
| [!UICONTROL Referencia de recursos] | Añada para mostrar una lista de recursos que hagan referencia al recurso. |
| [!UICONTROL Referencias de productos] | Añada para mostrar la lista de los productos vinculados con el recurso. |
| [!UICONTROL Clasificación del recurso] | Añada a las opciones de visualización para clasificar el recurso. |
| [!UICONTROL Metadatos de contexto] | Añada para controlar la visualización de otras fichas de metadatos en la página de propiedades de los recursos. |

<!-- TBD: Check against 6.5.4.0 if the list of components is complete.
-->

#### Edición del componente de metadatos {#edit-the-metadata-component}

Para editar las propiedades de un componente de metadatos en el formulario, haga clic en el componente y edite todas o un subconjunto de las siguientes propiedades en la ficha **[!UICONTROL Configuración]** .

**Etiqueta** de campo: Nombre de la propiedad de metadatos que se muestra en la página de propiedades del recurso.

**Asignar a propiedad**: Esta propiedad especifica la ruta/nombre relativos al nodo del recurso en el que se guarda en el repositorio de CRX. inicio con `./` porque indica que la ruta está debajo del nodo del recurso.

Los siguientes son los valores válidos para esta propiedad:

* `./jcr:content/metadata/dc:title`: Almacena el valor en el nodo de metadatos del recurso como propiedad `dc:title`.

* `./jcr:created`:: Muestra la propiedad JCR en el nodo del recurso. Si configura estas propiedades en propiedades de vista, le recomendamos que las marque como Deshabilitar edición, ya que están protegidas. Otherwise, the error [!UICONTROL Asset(s) failed to modify] results when you save the asset&#39;s properties.

Para asegurarse de que el componente se muestra correctamente en el formulario de esquema de metadatos, la ruta de la propiedad no debe incluir espacios.

* **Marcador de posición**: Utilice esta propiedad para especificar el texto del marcador de posición correspondiente a la propiedad metadata.
* **Requerido**: Utilice esta propiedad para marcar una propiedad de metadatos como obligatoria en la página de propiedades.
* **Deshabilitar Editar**: Utilice esta propiedad para que una propiedad de metadatos no se pueda editar en la página de propiedades.
* **Mostrar campo vacío en solo** lectura: Marque esta propiedad para mostrar una propiedad de metadatos en la página de propiedades aunque no tenga ningún valor. De forma predeterminada, cuando una propiedad de metadatos no tiene ningún valor, no se muestra en la página de propiedades.
* **Mostrar lista ordenada**: Utilice esta propiedad para mostrar una lista ordenada de las opciones
* **Opciones**: Utilice esta propiedad para especificar opciones en una lista
* **Descripción** : Utilice esta propiedad para agregar una breve descripción para el componente de metadatos.
* **Clase**: Clase de objeto con la que está asociada la propiedad.
* **Eliminar**: Haga clic en [!UICONTROL Eliminar] para eliminar un componente del formulario de esquema.

>[!NOTE]
>
>El componente Campo  oculto no incluye estos atributos. En su lugar, incluye propiedades, como los atributos Nombre, Valor, Etiqueta de campo y Descripción. Los valores del componente Campo oculto se envían como parámetro POST cada vez que se guarda el recurso. No se guarda como metadatos para el recurso.

Si selecciona la opción **[!UICONTROL Obligatorio]**, puede buscar recursos que no tengan metadatos obligatorios. En el panel **[!UICONTROL Filtros]**, expanda el predicado **[!UICONTROL Validación de metadatos]** y seleccione la opción **[!UICONTROL No válido]**. Los resultados de la búsqueda muestran los recursos que carecen de metadatos obligatorios configurados a través del formulario de esquema.

![Opción no válida seleccionada en el panel Filtros del predicado Validación de metadatos ](assets/chlimage_1-178.png)

Si agrega el componente Metadatos contextuales a cualquier ficha de cualquier formulario de esquema, el componente aparece como una lista en la página de propiedades de los recursos a los que se aplica el esquema concreto. La lista incluye todas las demás fichas excepto la ficha a la que se ha aplicado el componente Metadatos contextuales. Actualmente, esta función proporciona una funcionalidad básica para controlar la visualización de metadatos en función del contexto.

![Componente Metadatos contextuales que enumera fichas de propiedades de recursos](assets/chlimage_1-179.png)

Para mostrar cualquier ficha de la página de propiedades además de la ficha donde se aplica el componente Metadatos contextuales, seleccione la ficha en la lista. La ficha se agrega a la página de propiedades.

![La ficha seleccionada en la lista Metadatos contextuales se muestra en la página de propiedades del recurso](assets/contextual-metadata-asset-properties.png)

*Figura: Metadatos contextuales de la página de propiedades de recursos.*

### Especificar propiedades en el archivo JSON {#specify-properties-in-json-file}

En lugar de especificar propiedades para las opciones de la pestaña **[!UICONTROL Configuración]**, puede definir las opciones de un archivo JSON especificando los pares de clave-valor correspondientes. Especifique la ruta del archivo JSON en el campo **[!UICONTROL Ruta de JSON]**.

#### Añadir o eliminar una ficha del formulario de esquema {#adding-deleting-a-tab-in-the-schema-form}

El editor de esquemas permite agregar o eliminar una pestaña. The default schema form includes the **[!UICONTROL Basic]**, **[!UICONTROL Advanced]** , **[!UICONTROL IPTC]**, and **[!UICONTROL IPTC Extension]** tabs.

![Fichas predeterminadas del formulario de Esquema de metadatos](assets/chlimage_1-181.png)

Haga clic en `+` para agregar una nueva ficha a un formulario de esquema. De forma predeterminada, la nueva ficha tiene el nombre `Unnamed-1`. Puede modificar el nombre desde la ficha **[!UICONTROL Configuración]** .

Haga clic en `X` para eliminar una ficha.

![Añadir o eliminar una ficha mediante el Editor de Esquemas de metadatos](assets/chlimage_1-182.png)

## Eliminar formularios de esquema de metadatos {#delete-metadata-schema-forms}

[!DNL Experience Manager] permite eliminar únicamente formularios esquema personalizados. No permite eliminar los formularios o las plantillas de esquema predeterminados. Sin embargo, puede eliminar cualquier cambio personalizado en estos formularios.

Para eliminar un formulario, selecciónelo y haga clic en Eliminar.

>[!NOTE]
>
>* Después de eliminar los cambios personalizados a un formulario predeterminado, el icono de bloqueo vuelve a aparecer antes en la interfaz de Esquema de metadatos para indicar que el formulario ha vuelto a su estado predeterminado.
>* No puede eliminar los formularios de esquema de metadatos predeterminados en Recursos.


## Formularios de Esquema para tipos MIME {#schema-forms-for-mime-types}

Assets proporciona formularios predeterminados para varios tipos MIME predeterminados. Sin embargo, puede agregar formularios personalizados para recursos de varios tipos MIME.

### Añadir nuevos formularios para tipos MIME {#add-new-forms-for-mime-types}

Cree un nuevo formulario bajo el tipo de formulario correspondiente. For example, to add a new template for the `image/png` subtype, create the form under the &quot;image&quot; forms. El título del formulario de esquema es el nombre del subtipo. In this case, the title is `png`.

#### Usar una plantilla de esquema existente para varios tipos MIME {#use-an-existing-schema-template-for-various-mime-types}

Puede utilizar una plantilla existente para otro tipo MIME. Por ejemplo, utilice el `image/jpeg` formulario para recursos de tipo MIME `image/png`.

En este caso, cree un nuevo nodo en `/etc/dam/metadataeditor/mimetypemappings` el repositorio de CRX. Especifique un nombre para el nodo y defina las siguientes propiedades:

| Nombre | Descripción | Tipo | Value |
|------|-------------|------|-------|
| `exposedmimetype` | Nombre del formulario existente que se va a asignar | `String` | `image/jpeg` |
| `mimetypes` | Lista de tipos MIME que utilizan el formulario definido en el `exposedmimetype` atributo | `String` | `image/png` |

Assets asigna los siguientes tipos MIME y formularios de esquema:

| Formulario de Esquema | Tipos MIME |
| --------------------------- | --------------------------------------------------- |
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Conceder acceso a esquemas de metadatos {#grant-access-to-metadata-schemas}

La función Esquema de metadatos solo está disponible para los administradores. Sin embargo, los administradores pueden proporcionar acceso a los no administradores modificando algunos permisos. Los usuarios que no sean administradores deben tener permisos de creación, modificación y eliminación en la `/conf` carpeta.

## Aplicación de metadatos específicos de carpetas {#apply-folder-specific-metadata}

Recursos permite definir una variante de un esquema de metadatos y aplicarla a una carpeta específica.

Por ejemplo, puede definir una variante del esquema de metadatos predeterminado y aplicarla a una carpeta. Al aplicar el esquema modificado, se anula el esquema de metadatos predeterminado original que se aplica a los recursos de la carpeta.

Solo los recursos cargados en la carpeta a la que se aplica este esquema se ajustan a los metadatos modificados definidos en el esquema de metadatos de la variante. Los recursos de otras carpetas en las que se aplica el esquema original siguen ajustándose a los metadatos definidos en el esquema original.

La herencia de metadatos por recursos se basa en el esquema que se aplica a la carpeta de primer nivel de la jerarquía. Es decir, si una carpeta no contiene subcarpetas, los recursos de la carpeta heredarán los metadatos del esquema aplicado a la carpeta.

Si la carpeta tiene una subcarpeta, los recursos de la subcarpeta heredarán los metadatos del esquema aplicado en el nivel de subcarpeta si se aplica un esquema diferente en el nivel de subcarpeta. Sin embargo, si no se aplica ningún esquema o el mismo esquema en el nivel de subcarpeta, los recursos de subcarpeta heredarán los metadatos del esquema aplicado en el nivel de carpeta principal.

1. En [!DNL Experience Manager] la interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Esquemas **** de metadatos. Se muestra la página **[!UICONTROL Formularios de esquema de metadatos]**.
1. Seleccione la casilla de verificación situada antes de un formulario, por ejemplo el formulario de metadatos predeterminado, y haga clic en **[!UICONTROL Copiar]** y guárdelo como un formulario personalizado. Especifique un nombre personalizado para el formulario, por ejemplo `my_default`. También puede crear un formulario personalizado.

1. En la página Formularios **[!UICONTROL de Esquema de]** metadatos, seleccione el `my_default` formulario y, a continuación, haga clic en **[!UICONTROL Editar]**.

1. En la página Editor **[!UICONTROL de Esquemas de]** metadatos, agregue un campo de texto al formulario de esquema. Por ejemplo, agregue un campo con la **[!UICONTROL Categoría]** label.

   ![Campo de texto agregado al Editor de formularios de Esquema de metadatos](assets/text-field-metadata-schema-editor.png)

   *Figura: Campo de texto agregado al editor de formularios de esquema de metadatos.*

1. Haga clic en **[!UICONTROL Guardar.]** El formulario modificado aparece en la página **[!UICONTROL Metadatos Esquema Forms]** .
1. Haga clic en **[!UICONTROL Aplicar a carpetas]** en la barra de herramientas para aplicar los metadatos personalizados a una carpeta.

1. Seleccione la carpeta en la que desea aplicar el esquema modificado y, a continuación, haga clic en **[!UICONTROL Aplicar]**.

   ![Seleccionar la carpeta a la que aplicar el Esquema de metadatos](assets/chlimage_1-188.png)

1. Si la carpeta tiene el otro esquema de metadatos aplicado, aparecerá un mensaje en el que se advierte que está a punto de sobrescribir el esquema de metadatos existente. Haga clic en **Sobrescribir**.
1. Haga clic en **Aceptar** para cerrar el mensaje de éxito.
1. Vaya a la carpeta en la que ha aplicado el esquema de metadatos modificado.

## Definir metadatos obligatorios {#define-mandatory-metadata}

Puede definir campos obligatorios en un nivel de carpeta, que se aplican a los recursos que se cargan en la carpeta. Si carga recursos con metadatos que faltan para los campos obligatorios definidos anteriormente, aparecerá una indicación visual de los metadatos que faltan en los recursos de la vista de tarjetas.

>[!NOTE]
>
>Un campo de metadatos puede definirse como obligatorio en función del valor de otro campo. En la vista de la tarjeta, [!DNL Experience Manager] no muestra el mensaje de advertencia sobre la falta de metadatos para estos campos obligatorios de metadatos.

1. En [!DNL Experience Manager] la interfaz, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > Esquemas **** de metadatos. Se muestra la página **[!UICONTROL Formularios de esquema de metadatos]**.
1. Guarde el formulario de metadatos predeterminado como un formulario personalizado. Por ejemplo, guárdelo como `my_default`.

1. Edite el formulario personalizado. Añada un campo obligatorio. Por ejemplo, agregue un campo de **[!UICONTROL Categoría]** y convierta el campo en obligatorio.

   ![Añadir campo obligatorio en formulario de metadatos seleccionando Obligatorio en la ficha Reglas del Editor de formularios de Esquema de metadatos](assets/mandatory-field-metadata-schema-editor.png)

   *Figura: Campo obligatorio en el editor de formularios de esquema de metadatos.*

1. Haga clic en **[!UICONTROL Guardar.]** El formulario modificado aparece en la página **[!UICONTROL Metadatos Esquema Forms]** . Seleccione el formulario y, a continuación, haga clic en **[!UICONTROL Aplicar a carpetas]** en la barra de herramientas para aplicar los metadatos personalizados a una carpeta.

1. Vaya a la carpeta y cargue algunos recursos con metadatos que faltan en el campo obligatorio que ha agregado al formulario personalizado. Se muestra un mensaje para los metadatos que faltan en el campo obligatorio en la vista de tarjeta del recurso.

   ![Mensaje para los metadatos obligatorios que faltan en la vista de tarjetas de recursos al cargar recursos en la carpeta](assets/chlimage_1-192.png)

1. (Opcional) Acceso `https://[aem_server]:[port]/system/console/components/`. Configure y active `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` el componente que está deshabilitado de forma predeterminada. Defina una frecuencia con la que [!DNL Experience Manager] compruebe la validez de los metadatos en los recursos. Esta configuración agrega una propiedad `hasValidMetadata` a `jcr:content` los recursos. Si utiliza esta propiedad, [!DNL Experience Manager] puede que los resultados del filtro no sean válidos en una búsqueda. Si agrega un recurso después de una comprobación, el recurso no se marca con `hasValidMetadata` hasta la siguiente comprobación programada. Por lo tanto, los recursos no aparecen en los filtros de búsqueda para buscar metadatos no válidos hasta después de la siguiente comprobación programada.

   >[!CAUTION]
   >
   >Las comprobaciones de validación de metadatos requieren muchos recursos y pueden afectar al rendimiento del sistema. Programe las comprobaciones en consecuencia. Si el servidor no puede hacer frente a la carga, intente deshabilitar este trabajo.

<!-- TBD: Add this method to find invalid metadata in the metadata article later.
-->
