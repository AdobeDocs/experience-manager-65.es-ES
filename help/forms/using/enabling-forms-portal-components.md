---
title: Habilitación de componentes del portal de formularios
seo-title: Habilitación de componentes del portal de formularios
description: De serie, los componentes de Forms Portal están desactivados. Active los grupos Servicios de documentos y Predicados de servicios de documentos para habilitar los componentes de Forms Portal.
seo-description: De serie, los componentes de Forms Portal están desactivados. Active los grupos Servicios de documentos y Predicados de servicios de documentos para habilitar los componentes de Forms Portal.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Activación de los componentes del portal de formularios {#enabling-forms-portal-components}

De forma predeterminada, los componentes del portal de formularios no están disponibles para su uso. Para que los componentes aparezcan en la lista de componentes disponibles en AEM barra de tareas, realice los pasos siguientes:

1. Inicie sesión en la instancia de autor del sitio web y abra una página de AEM Sites.

1. Para las páginas que utilizan una plantilla estática, realice los siguientes pasos:

   1. En el encabezado de la página, pulse ![canvas-drop](assets/canvas-drop-down.png) > **Diseño** para abrir la página en modo Diseño.
   1. Pulse cualquier componente (con un borde azul) y, a continuación, pulse ![nivel de campo](assets/field-level.png) para seleccionar el sistema de párrafos que contiene el componente actual.
   1. En el sistema de párrafos, pulse ![settings_icon](assets/settings_icon.png) para abrir el cuadro de diálogo Editar para el sistema de párrafos.
   1. En la lista de **[!UICONTROL Componentes permitidos]**, habilite las casillas de verificación para los componentes **[!UICONTROL Servicios de documentos]** y **[!UICONTROL Predicados de servicios de documentos]**. Pulse **[!UICONTROL Aceptar]**.

1. Para las páginas que utilizan una plantilla dinámica, realice los pasos siguientes:

   1. En el encabezado de la página, pulse ![properties](assets/properties.png) > **Editar plantilla** para abrir la plantilla de la página.
   1. Pulse **Contenedor de diseño** y pulse ![Administración de fuentes](/help/forms/using/assets/feedmanagement.png). En la pestaña **Componentes permitidos**, habilite las opciones **Predicados de servicios de documentos y** y pulse ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>También puede habilitar componentes específicos de estas categorías seleccionando los componentes. Para obtener más información sobre los componentes y su uso, consulte [Creación de una página de portal de formulario](/help/forms/using/creating-form-portal-page.md) e [Incrustación del componente de vínculo en una página](/help/forms/using/embedding-link-component-page.md).

Ahora, las categorías de componentes Servicios de documentos y Predicados de servicios de documentos están disponibles en el navegador de componentes. Los componentes están habilitados para todas las páginas que utilizan la misma plantilla.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página de portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
