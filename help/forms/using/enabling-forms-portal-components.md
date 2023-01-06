---
title: Habilitar componentes del portal de formularios
seo-title: Enabling forms portal components
description: De serie, los componentes del portal de formularios están deshabilitados. Habilite los grupos Servicios de documentos y Predicados de servicios de documentos para habilitar los componentes del portal de formularios.
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: ht
source-wordcount: '320'
ht-degree: 100%

---

# Habilitar componentes del portal de formularios {#enabling-forms-portal-components}

De forma predeterminada, los componentes del portal de formularios no están disponibles para su uso. Para que los componentes aparezcan en la lista de componentes disponibles en la barra de tareas de AEM, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor del sitio web y abra una página de AEM Sites.

1. Para las páginas que utilizan una plantilla estática, realice los siguientes pasos:

   1. En el encabezado de la página, pulse ![lista desplegable de lienzo](assets/canvas-drop-down.png) > **Diseño** para abrir la página en el modo Diseño.
   1. Pulse cualquier componente (con un borde azul) y, a continuación, pulse ![nivel de campo](assets/field-level.png) para seleccionar el sistema de párrafos que contiene el componente actual.
   1. En el sistema de párrafos, pulse ![settings_icon](assets/settings_icon.png) para abrir el cuadro de diálogo Editar del sistema de párrafos.
   1. De la lista de **[!UICONTROL Componentes permitidos]**, habilite las casillas de verificación para los componentes **[!UICONTROL Servicios de documentos]** y **[!UICONTROL Predicados de servicios de documentos]**. Pulse **[!UICONTROL Aceptar]**.

1. Para las páginas que utilizan una plantilla dinámica, realice los siguientes pasos:

   1. En el encabezado de la página, pulse ![propiedades](assets/properties.png) > **Editar plantilla** para abrir la plantilla de la página.
   1. Pulse **Contenedor de diseño** y pulse ![FeedManagement](/help/forms/using/assets/feedmanagement.png). En la pestaña **Componentes permitidos**, habilite **Predicados de servicios de documentos y Servicios de documentos** y pulse ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>También puede habilitar componentes específicos de estas categorías si selecciona los componentes. Para obtener más información sobre los componentes y su uso, consulte [Crear una página del portal de formularios](/help/forms/using/creating-form-portal-page.md) e [Incrustar un componente de vínculo en una página](/help/forms/using/embedding-link-component-page.md).

Ahora, las categorías de componentes Servicios de documentos y Predicados de servicios de documentos están disponibles en el explorador de componentes. Los componentes están habilitados para todas las páginas que utilizan la misma plantilla.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Creación de una página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar el componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalizar el almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizar plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
