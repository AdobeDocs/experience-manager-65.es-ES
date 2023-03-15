---
title: Introducción a la publicación de formularios en un portal
seo-title: Introduction to publishing forms on a portal
description: AEM Forms proporciona componentes que puede utilizar para crear un portal de formularios. Este artículo describe los componentes del portal de formularios disponibles.
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
ht-degree: 100%

---

# Introducción a la publicación de formularios en un portal{#introduction-to-publishing-forms-on-a-portal}

## Descripción general de los componentes del portal de AEM Forms {#aem-forms-portal-components-overview}

En un escenario típico de implementación de portal centrado en formularios, el desarrollo de los formularios y el de portales son dos actividades separadas. Mientras los diseñadores de formularios diseñan y almacenan formularios en un repositorio, los desarrolladores web crean una aplicación web para enumerar formularios y administrar su envío. Los formularios se copian en el nivel web, ya que no hay ninguna comunicación entre el repositorio de formularios y la aplicación web.

Estos escenarios suelen dar lugar a problemas de administración y retrasos en la producción. Por ejemplo, si hay una versión más reciente de un formulario disponible en el repositorio, debe reemplazar el formulario en el nivel web, modificar la aplicación web y volver a implementar el formulario en el sitio público. La reimplementación de la aplicación web puede causar cierto tiempo de inactividad en el servidor. Normalmente, el tiempo de inactividad del servidor es una actividad planificada y, por lo tanto, los cambios no se pueden insertar instantáneamente en el sitio público.

AEM Forms proporciona componentes de portal que reducen los gastos generales de administración y los retrasos en la producción. Los componentes permiten a los desarrolladores web crear y personalizar un portal de formularios en sitios web creados con Adobe Experience Manager (AEM).

![Portal de AEM Forms](assets/aem-forms-portal.png)

Los componentes de portal de formularios le permiten agregar las siguientes funcionalidades:

* Muestre una lista de formularios en diseños personalizados. Se proporcionan los diseños Vista de lista, Vista de tarjeta y Vista de panel. Puede crear sus propios diseños personalizados.
* Permite mostrar metadatos y acciones personalizados en forma de lista.
* Muestre una lista de los formularios publicados por la interfaz de usuario de AEM Forms en la instancia de publicación en la que se utilizan los componentes del portal de formularios.
* Permita que los usuarios finales procesen formularios en formato HTML y PDF.
* Utilice un perfil HTML personalizado para procesar formularios.
* Permita buscar formularios según diversos criterios, como propiedades, metadatos y etiquetas de formularios.
* Envíe datos de formulario a un servlet.
* Utiliza CSS personalizada para personalizar la apariencia del portal.
* Crea vínculos a formularios.
* Muestra una lista de los borradores y los envíos relacionados con los formularios adaptables que ha creado el usuario final.

## Componentes del portal de AEM Forms disponibles {#available-aem-forms-portal-components}

AEM Forms proporciona los siguientes componentes de portal predeterminados, agrupados en los grupos de componentes **Document Services** y **Document Services Predicates**:

### Búsqueda y lista {#search-amp-lister}

El componente Búsqueda y lista permite mostrar una lista de los formularios del repositorio de formularios en la página del portal y proporciona opciones de configuración para mostrar una lista de los formularios en función de criterios específicos. También le permite especificar criterios de búsqueda para permitir que los usuarios del portal busquen en la lista de formularios.

### Borradores y envíos {#drafts-amp-submissions}

Mientras que el componente Búsqueda y lista muestra los formularios que publica el autor de Forms, el componente Borradores y envíos muestra los formularios guardados como borrador para completarlos posteriormente y enviarlos. Este componente proporciona una experiencia personalizada a cualquier usuario que haya iniciado sesión.

### Vínculo {#link}

Vínculo: este componente le permite crear un vínculo a un formulario en cualquier parte de la página. Imagine un escenario en el que ofrece un programa de formación y desea que los usuarios envíen un formulario para registrarse en él. Ha publicado los detalles del programa en su sitio web. Debajo de estos, desea proporcionar un vínculo al formulario de registro. El componente Vínculo puede ayudarle a crear ese vínculo.

## Flujo de trabajo del portal de formularios {#forms-portal-workflow}

El portal de formularios le permite mostrar una lista de los formularios del repositorio de formularios en la página del portal. También le permite especificar criterios de búsqueda para permitir que los usuarios del portal busquen en la lista de formularios. También puede utilizar el componente Borradores y envíos para mostrar los formularios guardados como borrador para completarlos posteriormente y los formularios enviados. Debe realizar un conjunto determinado de operaciones antes de que estas funcionalidades estén disponibles en una página de Sites. Siga los pasos de la secuencia indicada para poder acceder a los componentes y las funcionalidades correspondientes desde una página de Sites:

1. **Habilitar los componentes del portal de formularios**: los componentes del portal de formularios no están disponibles para su uso de forma predeterminada. [Habilite los componentes de la barra de tareas de AEM](/help/forms/using/enabling-forms-portal-components.md) en una página de AEM Sites.
1. **Mostrar una lista de formularios en una página (cree una página del portal de formularios):** los formularios se pueden mostrar en forma de lista tanto en páginas de AEM Sites como en páginas de sitios que no sean de AEM. La lista contiene los formularios disponibles en la instancia de publicación. Un usuario puede abrir los formularios y empezar a rellenarlos. Cada vez que un usuario abre un formulario, se crea una nueva instancia del formulario:

   1. **Mostrar una lista de formularios en una página de AEM Sites**: agregue el componente **[Búsqueda y lista](../../forms/using/creating-form-portal-page.md)** a la página y configure el **[Panel Lista](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** para mostrar una lista de formularios en una página. Agregue también el componente **Panel Buscar** al componente **Búsqueda y lista** y configúrelo para añadir la funcionalidad de búsqueda a la página. La página con el componente del portal de formularios se conoce como [página del portal de formularios](../../forms/using/creating-form-portal-page.md).

   1. **Mostrar una lista de formularios en una página que no sea de AEM Sites:** utilice la [API de búsqueda del portal de formularios](/help/forms/using/listing-forms-webpage-using-apis.md) para consultar, recuperar y mostrar una lista de formularios en páginas que no sean de AEM Sites.

1. **Mostrar una lista de los borradores y los formularios enviados en una página del portal de formularios**: agregue y configure el componente Borradores y envíos en la página del portal de formularios. El componente muestra una lista de todos los formularios que están en estado de borrador y los formularios que ya se han enviado.

   Para permitir que un formulario adaptable enviado aparezca en la pestaña Envíos, establezca la acción **Acción de envío** en **[Acción de envío del portal de formularios](configuring-submit-actions.md).** También puede activar la opción Envío del portal de formularios. Cada vez que un usuario envía el formulario, este se agrega a la pestaña Envíos.

1. **Configurar el almacenamiento de los datos de los borradores y los formularios enviados:** los datos de los borradores y los envíos se almacenan en el repositorio de AEM de forma predeterminada. En un entorno de producción, se recomienda no almacenar datos de formularios en borradores o enviados en el repositorio de AEM. [Configure el componente del portal de formularios para guardar datos en una ubicación segura](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(Opcional) Personalización de los componentes del portal de formularios:** [personalice las plantillas de página del portal de formularios](../../forms/using/customizing-templates-forms-portal-components.md) para proporcionar un aspecto distintivo a los componentes.
1. **(Opcional) Añadir metadatos personalizados a los formularios:** [agregue metadatos personalizados a los formularios](../../forms/using/customizing-templates-forms-portal-components.md) para mejorar la experiencia de búsqueda y listado.
1. **Publicar la página del portal de formularios:** la página del portal de formularios ya está lista. Publique la página.

## Artículos relacionados {#related-articles}

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Creación de una página del portal de formularios](../../forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar el componente Borradores y envíos](../../forms/using/draft-submission-component.md)
* [Personalizar el almacenamiento de borradores y formularios enviados](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](integrate-draft-submission-database.md)
* [Personalizar plantillas para componentes del portal de formularios](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](../../forms/using/introduction-publishing-forms.md)
