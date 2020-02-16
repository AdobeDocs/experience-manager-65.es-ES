---
title: Introducción a la publicación de formularios en un portal
seo-title: Introducción a la publicación de formularios en un portal
description: AEM Forms incluye componentes que puede utilizar para crear el portal de formularios. En este artículo se describen los componentes disponibles del portal de formularios.
seo-description: AEM Forms incluye componentes que puede utilizar para crear el portal de formularios. En este artículo se describen los componentes disponibles del portal de formularios.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Introducción a la publicación de formularios en un portal{#introduction-to-publishing-forms-on-a-portal}

## Descripción general de los componentes del portal de AEM Forms {#aem-forms-portal-components-overview}

En un escenario típico de implementación de portal centrado en formularios, el desarrollo de formularios y el desarrollo de portales son dos actividades separadas. Mientras los diseñadores de formularios diseñan y almacenan formularios en un repositorio, los desarrolladores web crean una aplicación web para enumerar formularios y gestionar el envío de formularios. Los formularios se copian en el nivel web, ya que no hay comunicación entre el repositorio de formularios y la aplicación web.

Estos escenarios suelen provocar problemas de gestión y retrasos en la producción. Por ejemplo, si hay una versión más reciente de un formulario disponible en el repositorio, debe reemplazar el formulario en el nivel web, modificar la aplicación web y volver a implementar el formulario en el sitio público. La reimplementación de la aplicación web podría ocasionar cierto tiempo de inactividad en el servidor. Normalmente, el tiempo de inactividad del servidor es una actividad planificada y, por lo tanto, los cambios no se pueden trasladar al sitio público de forma instantánea.

AEM Forms proporciona componentes de portal que reducen los gastos generales de administración y los retrasos en la producción. Los componentes equipan a los desarrolladores web para crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM).

![Portal de AEM Forms](assets/aem-forms-portal.png)

Los componentes del portal de formularios le permiten agregar la siguiente funcionalidad:

* Muestra una lista de los formularios en diseños personalizados. Se proporcionan los diseños predeterminados de vista de lista, vista de tarjeta y vista de panel. Puede crear sus propios diseños personalizados.
* Le permite mostrar metadatos personalizados así como acciones personalizadas mientras los enumera.
* Enumere los formularios publicados por la interfaz de usuario de AEM Forms en la instancia de publicación donde se utilizan los componentes de Forms Portal.
* Permite a los usuarios finales procesar formularios en formato HTML y PDF.
* Utilice un perfil HTML personalizado para procesar formularios.
* Permite buscar formularios según varios criterios, como propiedades de formulario, metadatos y etiquetas.
* Enviar datos de formulario a un servlet.
* Utilice CSS personalizada para personalizar el aspecto del portal.
* Cree vínculos a formularios.
* Enumera borradores y envíos relacionados con el formulario adaptable creado por el usuario final.

## Componentes disponibles del portal de AEM Forms {#available-aem-forms-portal-components}

AEM Forms proporciona los siguientes componentes de portal predeterminados, agrupados en grupos de componentes de Predicados **de** Document Services **y** Document Services:

### Búsqueda y listador {#search-amp-lister}

El componente Buscar y listado le permite enumerar formularios del repositorio de formularios en la página de portal y proporciona opciones de configuración para enumerar formularios en función de criterios específicos. También permite especificar criterios de búsqueda para permitir que los usuarios del portal busquen en la lista de formularios.

### Borradores y envíos {#drafts-amp-submissions}

Mientras que el componente Buscar y listado muestra los formularios que el autor de Forms hace públicos, el componente Borradores y envíos muestra los formularios guardados como borrador para cumplimentar posteriormente y los formularios enviados. Este componente proporciona una experiencia personalizada a cualquier usuario que haya iniciado sesión.

### Vínculo {#link}

El componente Vínculo permite crear un vínculo a un formulario en cualquier lugar de la página. Imagine un escenario en el que ofrece un programa de formación y desea que los usuarios envíen un formulario para registrarse en la formación. En su sitio web, ha publicado los detalles del programa. Debajo de los detalles, debe proporcionar un vínculo al formulario de registro. El componente Vínculo puede ayudarle a crear ese vínculo.

## Flujo de trabajo de Forms Portal {#forms-portal-workflow}

Forms Portal le permite enumerar formularios del repositorio de formularios en la página del portal. También permite especificar criterios de búsqueda para permitir que los usuarios del portal busquen en la lista de formularios. También puede utilizar el componente Borradores y envíos para mostrar los formularios guardados como borrador para completarlos posteriormente y enviarlos. Debe realizar un determinado conjunto de operaciones antes de que estas funcionalidades estén disponibles en una página Sitios. Siga los pasos de la secuencia mostrada para que los componentes y las funciones respectivas estén disponibles en una página del sitio:

1. **Habilitar componentes** de Forms Portal:De forma predeterminada, los componentes del portal de formularios no están disponibles para su uso. [Habilite los componentes de la barra de tareas](/help/forms/using/enabling-forms-portal-components.md) de AEM para una página Sitios de AEM.
1. **** Mostrar los formularios en una página (crear página de portal de formularios): Puede enumerar los formularios tanto en páginas de AEM Sites como en páginas de AEM Site. La lista contiene formularios disponibles en la instancia de publicación. Un usuario puede abrir formularios y empezar a rellenarlos. Cada vez que un usuario abre un formulario, se crea una nueva instancia del mismo:

   1. **Mostrar los formularios en una página** Sitios de AEM: Agregue el componente **[Buscar y listado](../../forms/using/creating-form-portal-page.md)**a la página y configure el panel**[ de](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** lista para enumerar los formularios en una página. Agregue y configure el componente Panel **de** búsqueda al componente **Buscar y listado** para agregar funcionalidad de búsqueda a la página. La página con componente de portal de formularios se conoce como página [de portal de](../../forms/using/creating-form-portal-page.md)formularios.

   1. **** Enumere formularios en una página de sitios que no sean de AEM: Utilice las API [de búsqueda del portal de](/help/forms/using/listing-forms-webpage-using-apis.md) formularios para consultar, recuperar y enumerar formularios en páginas de sitios que no sean de AEM.

1. **Enumere los borradores y los formularios enviados en una página** de portal de formularios: Agregue y configure el componente Borradores y envíos a la página del portal de formularios. El componente enumera todos los formularios que están en estado de borrador y los formularios que ya se han enviado.

   Para que un formulario adaptable enviado aparezca en la ficha Envíos, defina la acción **** Enviar en Acción **[de envío de](configuring-submit-actions.md)Forms Portal.**También puede activar la opción Envío de Forms Portal. Cada vez que un usuario envía el formulario, éste se agrega a la ficha envíos.

1. **** Configure el almacenamiento para los datos de formularios de borrador y enviados: De forma predeterminada, los datos de borradores y envíos se almacenan en el repositorio de AEM. En un entorno de producción, se recomienda no almacenar datos de formulario enviados o borrador en el repositorio de AEM. [Configure el componente del portal de formularios para guardar datos en una ubicación](../../forms/using/draft-submission-component.md#customizing-the-storage)segura.
1. **** (Opcional) Personalización de los componentes del portal de formularios: [Personalice las plantillas](../../forms/using/customizing-templates-forms-portal-components.md) de página del portal de formularios para proporcionar un aspecto distintivo a los componentes.
1. **** (Opcional) Agregue metadatos personalizados a los formularios: [Agregue metadatos personalizados a los formularios](../../forms/using/customizing-templates-forms-portal-components.md) para mejorar la experiencia de búsqueda y de listado.
1. **** Publicar la página del portal de formularios: La página del portal de formularios ya está lista. Publique la página.

## Artículos relacionados {#related-articles}

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página del portal de formularios](../../forms/using/creating-form-portal-page.md)
* [Lista de formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](../../forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Ejemplo para integrar el componente de borradores y envíos con la base de datos](integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](../../forms/using/introduction-publishing-forms.md)

