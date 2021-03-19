---
title: Creación de una página de portal de formularios
seo-title: Creación de una página de portal de formularios
description: Forms Portal equipa a los desarrolladores web con componentes para crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM).
seo-description: Forms Portal equipa a los desarrolladores web con componentes para crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---


# Creación de una página de portal de formularios{#creating-a-forms-portal-page}

Los componentes del portal de Forms equipan a los desarrolladores web con componentes para crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM). Para obtener una descripción general rápida del portal de formularios, consulte [Introducción a la publicación de formularios en un portal](../../forms/using/introduction-publishing-forms.md).

## Requisitos previos {#prerequisites}

Los componentes del portal de Forms no están disponibles para su uso de forma predeterminada. Asegúrese de que las siguientes categorías de componentes del portal de formularios estén habilitadas tal como se describe en [Habilitación de componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md).

**Servicios de** documentosIncluye los componentes Búsqueda y listado, Vínculo y Borradores y envíos.

**Predicados de servicios de** documentosIncluye componentes de Predicado de fecha, Predicado de texto completo, Predicado de propiedades y Predicado de etiquetas. Estos componentes se utilizan para configurar la búsqueda en el componente Búsqueda y lista .

Una vez que se activan en una página de sitios AEM, estas categorías de componentes están disponibles para su uso en el navegador de componentes.

![Componentes del portal de AEM Forms en el navegador de componentes](assets/component-categories.png)

Categorías de componentes del portal de Forms

## Componente de búsqueda y lista {#search-amp-lister-component}

El componente Buscar y listar, disponible en la categoría de componente Servicios de documento, se utiliza para enumerar formularios en una página e implementar la búsqueda en los formularios enumerados. El componente incluye dos paneles:

* Panel de lista donde se muestran los formularios.
* Panel de búsqueda donde se agrega la funcionalidad de búsqueda.

Puede arrastrar y soltar el componente Buscar y listar de la categoría de componente Servicios de documento en el navegador de componentes a la página. El componente, cuando se añade, tiene un aspecto similar al siguiente.

![Componente de búsqueda y listado en una página](assets/fp-grid-viw.png)

Componente de búsqueda y lista en una página con diseño de cuadrícula

### Panel de lista {#list-pane}

El panel Lista es un área en la que se muestran los formularios. El componente Búsqueda y lista proporciona varias opciones de configuración que puede utilizar para controlar la visualización de formularios en el panel Lista.

Para configurar el panel Lista, pulse el componente Búsqueda y lista y, a continuación, pulse ![settings_icon](assets/settings_icon.png). Se abre el cuadro de diálogo **[!UICONTROL Editar componente]**.

![Panel de lista en modo de edición](assets/edit-list.png)

Panel de lista en modo de edición

El cuadro de diálogo **Editar** incluye varias pestañas que proporcionan opciones de configuración descritas en la siguiente tabla. Toque **Aceptar** para guardar la configuración, cuando haya terminado.

<table>
 <tbody>
  <tr>
   <th>Ficha</th>
   <th>Configuración</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Carpetas de recursos</strong></code></td>
   <td>Añadir elemento</td>
   <td>Configura las carpetas en las que los recursos se cargan mediante la interfaz de usuario de AEM Forms. De forma predeterminada, muestra todos los recursos cargados. Para obtener más información sobre la interfaz de usuario de AEM Forms, consulte <a href="../../forms/using/introduction-managing-forms.md" target="_blank">Introducción a la administración de formularios</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>Mostrar</strong></code></p> </td>
   <td>Texto del título</td>
   <td>Título del componente Búsqueda y lista . El título predeterminado es <strong>Forms Portal.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Diseño de los recursos. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Deshabilitar búsqueda avanzada</td>
   <td>Cuando está activado, oculta el icono de búsqueda avanzada.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Desactivar búsqueda de texto</td>
   <td>Cuando está activada, oculta la barra de búsqueda de texto completo.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Resultado</strong></code></td>
   <td>Número De Resultados Por Página</td>
   <td>Configura el número máximo de formularios que desea mostrar en una página.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Texto de resultados</td>
   <td><p>Configura el texto de los resultados (por ejemplo, 1-12 de 601 <strong>Results</strong>). El valor predeterminado es <strong>Results</strong>.</p> <p>Por ejemplo, si especifica <strong>Forms </strong>en este campo y hay un total de 601 formularios, el texto resultante cambia a 1-12 de 601 <strong>Forms.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Texto de página</td>
   <td><p>Configura el texto de la página (por ejemplo, <strong>Página </strong>1 de 51). El valor predeterminado es <strong>Página</strong>.</p> <p>Por ejemplo, si especifica <strong>Application Form </strong>en este campo y hay 51 páginas, el texto de la página cambia a <strong>Application Form </strong>1 de 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>De texto</td>
   <td><p>Reemplaza la palabra <strong>de</strong> por el texto especificado (Página 1 <strong>de </strong>51). El valor predeterminado es <strong>de</strong>.</p> <p>Por ejemplo, si especifica <strong>de </strong>en este campo, el texto cambia a Página 1 <strong>de </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Vínculo de formulario</strong></code></td>
   <td>Tipo de procesamiento</td>
   <td>Controla la lista de formularios en función del tipo de renderización especificado. Las opciones disponibles son PDF y HTML. Por ejemplo, si selecciona solo HTML como tipo de renderización, los PDF forms se filtran hacia fuera.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Perfil HTML</td>
   <td>Configura el perfil HTML que se utiliza para la renderización. Todos los perfiles disponibles se enumeran en la lista desplegable.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Dirección URL de envío</td>
   <td><p>Configura un servlet en el que se envían los datos del formulario.</p> <p><strong>Nota:</strong> <em>La dirección URL de envío de un formulario se puede especificar en varios lugares y su orden de prioridad es el siguiente:</em></p>
    <ol>
     <li><em>La dirección URL de envío incrustada en el formulario (en el botón Enviar) tiene la prioridad más alta.</em></li>
     <li><em>La dirección URL de envío que se menciona en la interfaz de usuario de AEM Forms tiene la segunda prioridad más alta.</em></li>
     <li><em>Enviar URL mencionada en el portal de formularios tiene la prioridad más baja.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Información del objeto Acción de procesamiento HTML</td>
   <td>Configura el texto de la información del objeto, que se muestra al pasar el puntero por encima de <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (el icono HTML5).</td>
  </tr>
  <tr>
   <td> </td>
   <td>Información del objeto Acción de procesamiento de PDF</td>
   <td>Configura el texto de la información del objeto, que se muestra al pasar el puntero por encima de <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (el icono PDF).</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Estilo</strong></code></td>
   <td>Tipo de estilo</td>
   <td>Permite especificar <strong>Sin estilo, Estilo predeterminado</strong> o <strong>Estilo personalizado </strong>para enumerar los formularios.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Ruta de estilo personalizada</td>
   <td>Si seleccionó Personalizado como Tipo de estilo, busque para especificar la ruta al CSS personalizado y, de lo contrario, seleccione Predeterminado.</td>
  </tr>
 </tbody>
</table>

### Panel de búsqueda {#search-pane}

El panel Buscar permite agregar los componentes Predicado de fecha, Predicado de texto completo, Predicado de propiedades y Predicado de etiquetas de la categoría Predicados de servicios de documentos de AEM barra de tareas. Estos componentes implementan la funcionalidad de búsqueda para que los usuarios realicen búsquedas en los formularios enumerados.

**Sugerencia:** *Puede controlar la lista de formularios mostrados en el portal de formularios en función de criterios preestablecidos y ocultar la funcionalidad de búsqueda para los usuarios finales. Para controlar la lista de formularios, utilice los componentes de predicado para aplicar filtros de búsqueda. También puede especificar los valores de filtro predeterminados y desactivar la búsqueda desde la pestaña Mostrar del cuadro de diálogo Editar componente.*

![Panel de búsqueda con predicado Fecha, Texto completo, Propiedades y Etiquetas](assets/search-with-predicates.png)

Panel de búsqueda con predicado Fecha, Texto completo, Propiedades y Etiquetas

#### Predicado de fecha {#date-predicate}

Cuando se agrega el componente Predicado de fechas, permite buscar en los formularios enumerados que se modificaron durante una duración especificada.

Para configurar el componente Predicado de fecha:

1. Pulse el componente y, a continuación, pulse ![settings_icon](assets/settings_icon.png). Se abre el cuadro de diálogo Editar.
1. Especifique lo siguiente:

   * **Tipo:** la única opción disponible es Fecha de  **última modificación**

   * **Texto:** etiqueta o rótulo para el componente predicado de fecha. El valor predeterminado es **Última fecha de modificación.**

   * **Etiqueta de fecha de inicio:** etiqueta o rótulo del campo de fecha de inicio
   * **Etiqueta de fecha de finalización:** etiqueta o rótulo para el campo de fecha de finalización
   * **Ocultar:** para aplicar el filtro de fechas predeterminado a los formularios de lista

1. Toque **Aceptar**

#### Predicado de texto completo {#full-text-predicate}

El componente Predicado de texto completo implementa la búsqueda de texto completo en los datos del formulario, como el nombre y la descripción. Los usuarios pueden buscar cualquier cadena de texto para devolver formularios que contengan el texto en su nombre o descripción.

Para configurar el componente predicado de texto completo:

1. Pulse el componente y, a continuación, pulse ![settings_icon](assets/settings_icon.png). Se abre el cuadro de diálogo Editar.
1. Especifique el título en el campo **Título principal**.
1. Toque **Ok**

#### Predicado de propiedades {#properties-predicate}

El componente Predicado de propiedades implementa la búsqueda de formularios en función de las propiedades del formulario, como título, autor y descripción.

Para configurar el componente Predicado de propiedades :

1. Pulse el componente y, a continuación, pulse ![settings_icon](assets/settings_icon.png). Se abre el cuadro de diálogo Editar.
1. En la pestaña General , especifique la etiqueta de búsqueda. El valor predeterminado es **Properties**

1. En la ficha Opciones, pulse **Agregar elemento.**
1. Seleccione una propiedad de la lista desplegable y especifique una etiqueta de búsqueda para ella en el campo situado debajo de la lista desplegable.
1. Repita el paso 4 para añadir más propiedades. También puede especificar un valor de filtro predeterminado para enumerar formularios en función de los criterios especificados y ocultar la propiedad para que la busquen los usuarios finales. Seleccione la casilla Ocultar de una propiedad y especifique el valor de filtro predeterminado.
Por ejemplo, si desea mostrar formularios que contengan &quot;Viaje&quot; en sus títulos, seleccione Ocultar junto a la propiedad Título . Además, especifique Viaje en el cuadro de texto valor de filtro predeterminado.

1. Toque **Aceptar**

#### Predicado de etiquetas {#tags-predicate}

El componente Predicado de etiquetas implementa la búsqueda de formularios en función de las etiquetas definidas en Forms Manager.

Para configurar el componente Predicado de etiquetas:

1. Pulse el componente y, a continuación, pulse ![settings_icon](assets/settings_icon.png). Se abre el cuadro de diálogo Editar.
1. Pulse el botón de flecha hacia abajo situado junto al campo Etiquetas .
1. Seleccionar las etiquetas adecuadas
1. Toque **Aceptar**

Las etiquetas seleccionadas aparecen en el panel Buscar junto con las casillas de verificación para su selección. Ahora los usuarios pueden limitar la búsqueda en función de las etiquetas .

## Lista de formularios en una página {#list-forms-on-a-page-br}

Para enumerar formularios en una página, agregue el componente **[!UICONTROL Search &amp; Lister]** a la página y configure el **[!UICONTROL Panel de lista]**. Para permitir que los usuarios finales busquen formularios con fecha, texto y etiquetas, agregue un componente **[!UICONTROL Panel de búsqueda]**.

Para vincular un formulario desde cualquier lugar de la página, utilice el componente Vínculo . Para obtener más información sobre el componente de vínculo, consulte [Incrustación del componente de vínculo en una página](../../forms/using/embedding-link-component-page.md).

Para enumerar los formularios que están en estado de borrador y los formularios que ya se han enviado, utilice el componente **[!UICONTROL Borradores y envíos]**. Para obtener más información, consulte [Personalización del componente Borradores y envíos](../../forms/using/draft-submission-component.md).

## Facilidad de uso del dispositivo móvil {#mobile-device-friendliness}

El componente Búsqueda y lista del portal de Forms es sencillo para dispositivos móviles y se adapta en consecuencia. Las tres vistas predeterminadas: Cuadrícula, Tarjeta, Presentaciones de panel según el dispositivo en el que se abra el sitio, siempre que la página web también se adapte. El simple hecho es que Search &amp; Lister es un componente solamente y no controla el estilo de nivel de página.

La siguiente imagen muestra el componente Búsqueda y lista cuando se abre en un dispositivo móvil:

![Captura de pantalla del componente Búsqueda y lista](assets/search_lister.png)

Componente Búsqueda y listado

## Personalización de una página de portal de formularios {#customizing-a-forms-portal-page-br}

Puede personalizar una página del portal de formularios para que la página tenga un aspecto distinto. También puede agregar metadatos para mejorar la experiencia de búsqueda, cambiar el diseño de la página y agregar estilos CSS personalizados. Para obtener más información, consulte [Personalización de plantillas para componentes del portal de Forms](../../forms/using/customizing-templates-forms-portal-components.md).

La interfaz de usuario de AEM Forms permite agregar metadatos personalizados a los formularios. Los metadatos personalizados son útiles para ofrecer a los usuarios finales una experiencia de listado y búsqueda de formularios. Para obtener más información sobre los metadatos personalizados, consulte [Personalización de plantillas para componentes del portal de Forms](../../forms/using/customizing-templates-forms-portal-components.md).

De forma predeterminada, el portal de formularios proporciona acciones de renderización. Puede personalizar el portal de formularios para agregar más acciones. Para obtener información detallada, consulte [Adición de una acción personalizada en elementos de la lista de formularios.](../../forms/using/add-custom-action-form-lister.md)

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página de portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
