---
title: Activación de componentes del portal de formularios
seo-title: Activación de componentes del portal de formularios
description: De forma predeterminada, los componentes de Forms Portal están desactivados. Active los grupos de Document Services y Predicados de Document Services para activar los componentes de Forms Portal.
seo-description: De forma predeterminada, los componentes de Forms Portal están desactivados. Active los grupos de Document Services y Predicados de Document Services para activar los componentes de Forms Portal.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
translation-type: tm+mt
source-git-commit: a209b2dda04985a3f2d7c6838f11f0b5dc62d520

---


# Activación de componentes del portal de formularios {#enabling-forms-portal-components}

De forma predeterminada, los componentes del portal de formularios no están disponibles para su uso. Para que los componentes aparezcan en la lista de componentes disponibles en la barra de tareas de AEM, lleve a cabo los siguientes pasos:

1. Inicie sesión en la instancia de creación del sitio web y abra una página de sitios de AEM.

1. Para las páginas que utilizan una plantilla estática, realice los siguientes pasos:

   1. En el encabezado de página, toque ![lienzo-desplegable](assets/canvas-drop-down.png) > **Diseño** para abrir la página en modo Diseño.
   1. Toque cualquier componente (con un borde azul) y, a continuación, toque el nivel ![de](assets/field-level.png) campo para seleccionar el sistema de párrafos que contiene el componente actual.
   1. En el sistema de párrafos, toque ![settings_icon](assets/settings_icon.png) para abrir el cuadro de diálogo Editar del sistema de párrafos.
   1. En la lista de componentes **** permitidos, active las casillas de verificación de los componentes **[!UICONTROL Document Services]** y **[!UICONTROL Document Services Predicates]** . Toque **[!UICONTROL Aceptar]**.

1. Para las páginas que utilizan una plantilla dinámica, lleve a cabo los siguientes pasos:

   1. En el encabezado de página, toque ![propiedades](assets/properties.png) > **Editar plantilla** para abrir la plantilla de la página.
   1. Toque Contenedor **** de diseño y toque ![Administración de fuentes](/help/forms/using/assets/feedmanagement.png). En la ficha Componentes **** permitidos, active las opciones Predicados **de** Document Services y Document Services y toque ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>También puede activar componentes específicos de estas categorías seleccionando los componentes. Para obtener más información sobre los componentes y su uso, consulte [Creación de una página](/help/forms/using/creating-form-portal-page.md) de portal de formularios y [Incorporación del componente de vínculo en una página](/help/forms/using/embedding-link-component-page.md).

Ahora, las categorías de componentes Document Services y Document Services Predicates están disponibles en el navegador de componentes. Los componentes están habilitados para todas las páginas que utilizan la misma plantilla.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Crear página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Lista de formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Uso del componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalización del almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente de borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalización de plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
