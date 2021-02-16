---
title: Crear experiencias con objetivos en AEM Forms
seo-title: Crear experiencias con objetivos en AEM Forms
description: Utilice Destinatario en AEM Forms para crear experiencias personalizadas para clientes objetivo.
seo-description: Utilice Destinatario en AEM Forms para crear experiencias personalizadas para clientes objetivo.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# Crear experiencias con objetivos en AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrar Adobe Target con AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target integrado con AEM le permite crear experiencias personalizadas para una audiencia de destinatario. Con Adobe Target, puede crear pruebas A/B, medir la respuesta del usuario y generar contenido web personalizado para los usuarios objetivo. Puede integrar Adobe Target con AEM Forms en componentes de imagen de destinatario de formularios adaptables y comunicaciones interactivas.

Configure Adobe Target en AEM para utilizarlo con formularios adaptables y comunicaciones interactivas, consulte [Creación de una configuración de Destinatario en AEM](/help/sites-administering/target.md) y [Añada un módulo](/help/sites-administering/target.md).

>[!NOTE]
>
>La segmentación funciona cuando el formulario adaptable o la comunicación interactiva se procesan con un nombre de host o una dirección IP. Falla cuando el formulario adaptable o la comunicación interactiva se procesan con localhost.

## Creación de una Actividad de Destinatario {#creating-a-target-activity}

1. Toque **Adobe Experience Manager > Personalización > Actividades**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. En la página Actividades, toque **Crear > Crear marca**.
1. Se le pedirá que elija una plantilla e introduzca las propiedades.

   Seleccione una plantilla, toque **Siguiente.** Escriba el título de la marca en la sección Propiedades y toque  **Crear.**
Su marca ahora aparece en la página Actividades.

1. Toque su marca en la página Actividades.
1. En el área maestra de la marca, toque **Crear** > **Crear Actividad**.

   Cuando se crea una actividad, se especifican sus detalles, destinatarios y ajustes.

   La sección Detalles incluye nombre, motor de objetivo y objetivo. Al seleccionar Adobe Target como motor de determinación de objetivos, se activa la opción de configuración de nube de Destinatario. Elija la configuración de la nube de Destinatario, elija el tipo de Actividad, proporcione el objetivo de la actividad y toque **Siguiente**. La comunicación interactiva solo admite el tipo de Actividad de segmentación de experiencias.

   La sección Destinatario permite agregar una experiencia de audiencia y asignarle un nombre. Haga clic en **Añadir experiencia** para habilitar las opciones **Seleccionar Audiencia** y **Asignar nombre a la experiencia**. Toque **Seleccionar Audiencia** para ver una lista de audiencias y su origen. Seleccione una audiencia en la lista Nombre de Audiencia. Toque **Añadir experiencia** para asignar un nombre a la experiencia y toque **Siguiente**.

   La sección Objetivos y configuración le permite programar y priorizar su actividad. Establezca la fecha de inicio, la fecha de finalización y la prioridad de la actividad, métrica de objetivo, métrica adicional y toque **Guardar**.

   La actividad aparece ahora en la página de su marca.

   >[!NOTE]
   >
   >Puede omitir el error &quot;Se guardó la actividad, pero no se sincronizó con el Destinatario. Motivo: La siguiente experiencia no tiene ofertas&quot;, si se encuentra al guardar la actividad.

1. Para habilitar el destinatario, edite el archivo .jsp para incluir las bibliotecas de cliente que utiliza la plantilla de formularios adaptables.

   Por ejemplo, en la implementación lista para usar, haga clic en **Herramientas** > **CRXDE Lite**.

   En la barra de direcciones del CRXDE Lite, escriba /libs/fd/af/components/page/base/head.jsp para editar el archivo head.jsp.

   Esta implementación utiliza una plantilla simpleMatriculación. En esta implementación, modifique el archivo head.jsp para incluir las siguientes bibliotecas de cliente:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Para habilitar la estructura de destinatario para formularios adaptables, navegue hasta el formulario o la comunicación interactiva y ábralo en modo de edición.

   Para abrir un formulario o una comunicación interactiva en modo de edición, toque **Seleccionar** y, a continuación, toque **Abrir**.

   Como alternativa, aparecen cuatro botones al mover el puntero sobre el formulario o el icono de comunicación interactiva sin seleccionarlo. Puede tocar el botón **Editar** que aparece para abrir el formulario en modo de edición.

1. En la barra de herramientas de la página, toque **Información de la página** ![opciones del tema](assets/theme-options.png) > **Abrir propiedades**.
1. En la ficha General, elija una configuración para el campo **Adobe Target**. Toque **Guardar y cerrar**.

## Aplicación de la actividad creada a una imagen de formulario adaptable o a una imagen de comunicación interactiva {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Abra el formulario adaptable y la comunicación interactiva para editarlo. Si está abriendo una comunicación interactiva, abra el Canal Web.

1. En el modo de creación de la comunicación interactiva o el formulario adaptable, agregue una imagen para el destino.

   >[!NOTE]
   >
   >AEM Forms solo admite componentes de imagen de destino. Asegúrese de que el panel que aloja el componente de imagen no contenga ningún otro componente y de que el número de columnas del panel esté establecido en 1.

1. Cambie del modo **Editar** al modo **Segmentación**. La opción para cambiar de modo está cerca de la esquina superior derecha.
1. Seleccione una **MARCA**, seleccione **ACTIVIDAD** y toque **Objetivo de Inicio**. El menú **Audiencias** aparece en la parte derecha del editor.

   ![targeting-menu](assets/targeting-menu.png)

1. Seleccione una audiencia en el menú **Audiencias** y toque la imagen en destinatario. Aparece un menú. En el menú, toque **Destinatario**. Toque la imagen y toque **Configurar**. En la ventana de propiedades, seleccione la imagen que desea mostrar para la audiencia seleccionada. Repita el paso para todas las audiencias. La segmentación de experiencias está habilitada para la imagen en la comunicación interactiva o en el formulario adaptable.

## Compruebe si la actividad creada se sincroniza con el servidor de Destinatario {#check-if-the-created-activity-syncs-with-the-target-server}

Actividad utilizada para dirigir sincronizaciones con el servidor de Destinatario. Para comprobar si la actividad está sincronizada con el servidor de destinatario, compruebe el estado de la actividad en la página de marca.

Asegúrese de que el estado de la actividad es Sincronizado.

## Validar comportamiento de Destinatario {#validate-target-behavior}

Para validar el comportamiento de Destinatario:

* Usar objetivos con `wcmmode preview` en el modo de creación
* Usar objetivos con `wcmmode preview` y `wcmmode disabled` en el modo de publicación

## Monitoreo del objetivo para el componente de imagen {#monitor-targeting-for-the-image-component}

Para supervisar la segmentación de componentes de imagen en el formulario, publique sus imágenes, actividades y formularios adaptables.

## Problemas abiertos {#open-issues}

Expresión de visibilidad, error de enfoque establecido para imágenes de destino en formularios adaptables.
