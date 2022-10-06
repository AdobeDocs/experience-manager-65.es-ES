---
title: Introducción a la publicación de formularios en un portal
seo-title: Introduction to publishing forms on a portal
description: AEM Forms proporciona componentes que puede utilizar para crear su portal de formularios. En este artículo se describen los componentes disponibles del portal de formularios.
seo-description: AEM Forms provides with components that you can use to build your forms portal. This articles introduces you to the available forms portal components.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 19%

---

# Introducción a la publicación de formularios en un portal{#introduction-to-publishing-forms-on-a-portal}

## Descripción general de los componentes del portal de AEM Forms {#aem-forms-portal-components-overview}

En un escenario típico de implementación de portal centrado en formularios, el desarrollo de los formularios y el de portales son dos actividades separadas. Mientras los diseñadores de formularios diseñan y almacenan formularios en un repositorio, los desarrolladores web crean una aplicación web para enumerar formularios y administrar su envío. Los formularios se copian en el nivel web, ya que no hay ninguna comunicación entre el repositorio de formularios y la aplicación web.

Estos escenarios suelen dar lugar a problemas de administración y retrasos en la producción. Por ejemplo, si hay una versión más reciente de un formulario disponible en el repositorio, debe reemplazar el formulario en el nivel web, modificar la aplicación web y volver a implementar el formulario en el sitio público. La reimplementación de la aplicación web puede causar cierto tiempo de inactividad en el servidor. Normalmente, el tiempo de inactividad del servidor es una actividad planificada y, por lo tanto, los cambios no se pueden insertar instantáneamente en el sitio público.

AEM Forms proporciona componentes del portal que reducen los gastos generales de administración y los retrasos en la producción. Los componentes equipan a los desarrolladores web para crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM).

![Portal de AEM Forms](assets/aem-forms-portal.png)

Los componentes del portal de formularios le permiten añadir las siguientes funciones:

* Enumerar formularios en diseños personalizados. Se proporcionan los diseños predeterminados de vista de lista, vista de tarjeta y vista de panel. Puede crear sus propios diseños personalizados.
* Permite mostrar metadatos personalizados, así como acciones personalizadas al enumerarlos.
* Enumerar los formularios publicados por la interfaz de usuario de AEM Forms en la instancia Publicación en la que se utilizan los componentes del portal de Forms.
* Permita que los usuarios finales procesen formularios en formato HTML y PDF.
* Utilice un perfil de HTML personalizado para procesar formularios.
* Permite buscar formularios según diversos criterios, como propiedades, metadatos y etiquetas de formularios.
* Envíe datos de formulario a un servlet.
* Utiliza CSS personalizada para personalizar la apariencia del portal.
* Crea vínculos a formularios.
* Enumera borradores y envíos relacionados con el formulario adaptable creado por el usuario final.

## Componentes de portal de AEM Forms disponibles {#available-aem-forms-portal-components}

AEM Forms proporciona los siguientes componentes de portal predeterminados, agrupados en **Servicios de documentos** y **Predicados de servicios de documentos** grupos de componentes:

### Búsqueda y listador {#search-amp-lister}

El componente Buscar y listar le permite enumerar formularios del repositorio de formularios en la página del portal y proporciona opciones de configuración para enumerar formularios basados en criterios específicos. También le permite especificar criterios de búsqueda para permitir que los usuarios del portal busquen en la lista de formularios.

### Borradores y envíos {#drafts-amp-submissions}

Mientras que el componente Buscar y listar muestra los formularios que publica el autor de Forms, el componente Borradores y envíos muestra los formularios guardados como borrador para completarlos posteriormente y enviarlos. Este componente proporciona una experiencia personalizada a cualquier usuario que haya iniciado sesión.

### Vincular {#link}

El componente Vínculo permite crear un vínculo a un formulario en cualquier parte de la página. Imagine un escenario en el que ofrezca un programa de formación y desee que los usuarios envíen un formulario para registrarse en la formación. En su sitio web, ha publicado los detalles del programa. Debajo de los detalles, desea proporcionar un vínculo al formulario de registro. El componente Vínculo puede ayudarle a crear ese vínculo.

## Flujo de trabajo del portal de Forms {#forms-portal-workflow}

Portal de Forms le permite enumerar formularios del repositorio de formularios en la página del portal. También le permite especificar criterios de búsqueda para permitir que los usuarios del portal busquen en la lista de formularios. También puede utilizar el componente Borradores y envíos para mostrar los formularios guardados como borrador para completarlos posteriormente y enviarlos. Debe realizar un conjunto determinado de operaciones antes de que estas funcionalidades estén disponibles en una página Sitios . Siga los pasos de la secuencia indicada para que los componentes y las funcionalidades correspondientes estén disponibles en una página del sitio:

1. **Habilitar los componentes de Forms Portal**: De forma predeterminada, los componentes del portal de formularios no están disponibles para su uso. [Habilitar los componentes de AEM barra de tareas](/help/forms/using/enabling-forms-portal-components.md) para una página de AEM Sites.
1. **Enumerar formularios en una página (crear página de portal de formularios):** Los formularios se pueden enumerar tanto en páginas de AEM Sites como en páginas de sitios que no sean AEM. La lista contiene formularios disponibles en la instancia de publicación. Un usuario puede abrir formularios y empezar a rellenarlos. Cada vez que un usuario abre un formulario, se crea una nueva instancia del formulario:

   1. **Lista de formularios en una página de AEM Sites**: Agregue la variable **[Búsqueda y listado](../../forms/using/creating-form-portal-page.md)** a la página y configure el **[Panel de lista](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** para mostrar los formularios en una página. Agregue y configure la variable **Panel de búsqueda** al **Búsqueda y listado** también para añadir funcionalidad de búsqueda a la página. La página con el componente de portal de formularios se conoce como [página del portal de formularios](../../forms/using/creating-form-portal-page.md).

   1. **Enumerar formularios en una página que no sea de AEM Sites:** Utilice la variable [API de búsqueda del portal de formularios](/help/forms/using/listing-forms-webpage-using-apis.md) para consultar, recuperar y enumerar formularios en páginas que no sean de AEM Sites.

1. **Lista de borradores y formularios enviados en una página de portal de formularios**: Agregue y configure el componente Borradores y envíos en la página del portal de formularios. El componente enumera todos los formularios que están en estado de borrador y los formularios que ya se han enviado.

   Para permitir que un formulario adaptable enviado aparezca en la pestaña envíos , establezca la variable **Enviar acción** a **[Acción de envío del portal de Forms](configuring-submit-actions.md).** También puede activar la opción Envío del portal de Forms. Cada vez que un usuario envía el formulario, este se agrega a la ficha envíos.

1. **Configure el almacenamiento para los datos de formularios borrador y enviados:** De forma predeterminada, los datos de borradores y envíos se almacenan en el repositorio de AEM. En un entorno de producción, se recomienda no almacenar datos de formulario en borrador o enviados en AEM repositorio. [Configuración del componente del portal de formularios para guardar datos en una ubicación segura](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(Opcional) Personalización de los componentes del portal de formularios:** [Personalización de las plantillas de página del portal de formularios](../../forms/using/customizing-templates-forms-portal-components.md) para proporcionar un aspecto distintivo a los componentes.
1. **(Opcional) Añada metadatos personalizados a los formularios:** [Añadir metadatos personalizados a formularios](../../forms/using/customizing-templates-forms-portal-components.md) para mejorar la experiencia de búsqueda y listado.
1. **Publique la página del portal de formularios:** La página del portal de formularios ya está lista. Publique la página.

## Artículos relacionados {#related-articles}

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página de portal de formularios](../../forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](../../forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](../../forms/using/introduction-publishing-forms.md)
