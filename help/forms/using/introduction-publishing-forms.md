---
title: Introducción a la publicación de formularios en un portal
seo-title: Introducción a la publicación de formularios en un portal
description: AEM Forms proporciona componentes que puede utilizar para crear el portal de formularios. En este artículo se describen los componentes disponibles del portal de formularios.
seo-description: AEM Forms proporciona componentes que puede utilizar para crear el portal de formularios. En este artículo se describen los componentes disponibles del portal de formularios.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---


# Introducción a la publicación de formularios en un portal{#introduction-to-publishing-forms-on-a-portal}

## Introducción a los componentes del portal de AEM Forms {#aem-forms-portal-components-overview}

En un escenario típico de implementación de portal centrado en formularios, el desarrollo de formularios y el desarrollo de portales son dos actividades separadas. Mientras los diseñadores de formularios diseñan y almacenan formularios en un repositorio, los desarrolladores web crean una aplicación web para la lista de formularios y se encargan del envío de formularios. Forms se copia en el nivel web, ya que no hay comunicación entre el repositorio de formularios y la aplicación web.

Estos escenarios suelen provocar problemas de gestión y retrasos en la producción. Por ejemplo, si hay una versión más reciente de un formulario disponible en el repositorio, debe reemplazar el formulario en el nivel web, modificar la aplicación web y volver a implementar el formulario en el sitio público. La reimplementación de la aplicación web podría ocasionar cierto tiempo de inactividad en el servidor. Normalmente, el tiempo de inactividad del servidor es una actividad planificada y, por lo tanto, los cambios no se pueden trasladar instantáneamente al sitio público.

AEM Forms proporciona componentes del portal que reducen los gastos generales de administración y los retrasos en la producción. Los componentes equipan a los desarrolladores web para crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM).

![Portal de AEM Forms](assets/aem-forms-portal.png)

Los componentes del portal de formularios le permiten agregar la siguiente funcionalidad:

* Lista de formularios en diseños personalizados. Se proporcionan los diseños predeterminados de vista de Lista, vista de tarjetas y vista de panel. Puede crear sus propios diseños personalizados.
* Le permite mostrar metadatos personalizados así como acciones personalizadas mientras los enumera.
* Formularios de lista publicados por la interfaz de usuario de AEM Forms en la instancia de publicación donde se utilizan los componentes de Forms Portal.
* Permite a los usuarios finales procesar formularios en formato HTML y PDF.
* Utilice el perfil HTML personalizado para procesar formularios.
* Permite buscar formularios según varios criterios, como propiedades de formulario, metadatos y etiquetas.
* Enviar datos de formulario a un servlet.
* Utilice CSS personalizada para personalizar el aspecto del portal.
* Cree vínculos a formularios.
* Listas borradores y envíos relacionados con el formulario adaptable creado por el usuario final.

## Componentes disponibles del portal de AEM Forms {#available-aem-forms-portal-components}

AEM Forms proporciona los siguientes componentes del portal predeterminados, agrupados en **Documento Services** y **Documento Services Predicates** grupos de componentes:

### Búsqueda y listador {#search-amp-lister}

El componente Buscar y listado permite lista de formularios desde el repositorio de formularios a la página del portal y proporciona opciones de configuración para la lista de formularios según criterios específicos. También permite especificar criterios de búsqueda para permitir que los usuarios del portal busquen en la lista de formularios.

### Borradores y envíos {#drafts-amp-submissions}

Mientras que el componente Buscar y listado muestra los formularios que publica el autor de Forms, el componente Borradores y envíos muestra los formularios guardados como borrador para cumplimentar posteriormente y los formularios enviados. Este componente proporciona una experiencia personalizada a cualquier usuario que haya iniciado sesión.

### Vínculo {#link}

El componente Vínculo permite crear un vínculo a un formulario en cualquier lugar de la página. Imagine un escenario en el que ofrece un programa de formación y desea que los usuarios envíen un formulario para registrarse en la formación. En su sitio web, ha publicado los detalles del programa. Debajo de los detalles, debe proporcionar un vínculo al formulario de registro. El componente Vínculo puede ayudarle a crear ese vínculo.

## Flujo de trabajo de Forms Portal {#forms-portal-workflow}

El portal de Forms permite la lista de formularios desde el repositorio de formularios a la página del portal. También permite especificar criterios de búsqueda para permitir que los usuarios del portal busquen en la lista de formularios. También puede utilizar el componente Borradores y envíos para mostrar los formularios guardados como borrador para completarlos posteriormente y enviarlos. Debe realizar un determinado conjunto de operaciones antes de que estas funcionalidades estén disponibles en una página Sitios. Siga los pasos de la secuencia mostrada para que los componentes y las funciones respectivas estén disponibles en una página del sitio:

1. **Habilitar componentes** de Forms Portal: De forma predeterminada, los componentes del portal de formularios no están disponibles para su uso. [Habilite los componentes desde AEM ](/help/forms/using/enabling-forms-portal-components.md) sidekickpara una página de AEM Sites.
1. **formularios de lista en una página (crear página de portal de formularios):** Puede lista de formularios en páginas de AEM Sites y de sitios que no sean de AEM. La lista contiene formularios disponibles en la instancia de publicación. Un usuario puede abrir formularios y rellenar estos inicios. Cada vez que un usuario abre un formulario, se crea una nueva instancia del mismo:

   1. **Formularios de lista en una página** de AEM Sites: Añada el componente  **[Buscar y](../../forms/using/creating-form-portal-page.md)** listar a la página y configúrelo en el panel de  **[](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** Lista, para crear listas en los formularios de una página. Añada y configure el componente **Panel de búsqueda** en el componente **Buscar y listar** también para agregar funcionalidad de búsqueda a la página. La página con componente de portal de formularios se conoce como [página de portal de formularios](../../forms/using/creating-form-portal-page.md).

   1. **formularios de lista en una página que no sea de AEM Sites:** utilice las  [API de búsqueda del portal de formularios ](/help/forms/using/listing-forms-webpage-using-apis.md) para consulta, recuperación y lista de formularios en páginas que no sean de AEM Sites.

1. **Borrador de lista y envío de formularios en una página** de portal de formularios: Añada y configure el componente Borradores y envíos en la página del portal de formularios. El componente lista todos los formularios que están en estado borrador y los formularios que ya se han enviado.

   Para permitir que un formulario adaptable enviado aparezca en la ficha Envíos, establezca la **acción de envío** en **[Acción de envío de Forms Portal](configuring-submit-actions.md).** También puede activar la opción Enviar de Forms Portal. Cada vez que un usuario envía el formulario, éste se agrega a la ficha envíos.

1. **Configurar almacenamiento para los datos de formularios de borrador y enviados:** de forma predeterminada, los datos de borrador y envío se almacenan en el repositorio de AEM. En un entorno de producción, se recomienda no almacenar datos de formulario borrador o enviados en AEM repositorio. [Configure el componente del portal de formularios para guardar datos en una ubicación](../../forms/using/draft-submission-component.md#customizing-the-storage) segura.
1. **(Opcional) Personalización de los componentes del portal de formularios:** [Personalización de ](../../forms/using/customizing-templates-forms-portal-components.md) las plantillas de página del portal de formularios para proporcionar un aspecto distintivo a los componentes.
1. **(Opcional) Añada metadatos personalizados en formularios:** [Añada metadatos personalizados en ](../../forms/using/customizing-templates-forms-portal-components.md) formularios para mejorar la experiencia de búsqueda y de listado.
1. **Publicar la página del portal de formularios:** La página del portal de formularios ya está lista. Publique la página.

## Artículos relacionados {#related-articles}

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página del portal de formularios](../../forms/using/creating-form-portal-page.md)
* [Lista de formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](../../forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Ejemplo para integrar el componente de borradores y envíos con la base de datos](integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](../../forms/using/introduction-publishing-forms.md)

