---
title: Crear experiencias segmentadas en AEM Forms
seo-title: Create targeted experiences in AEM Forms
description: Use Target en AEM Forms para crear experiencias personalizadas para los clientes objetivo.
seo-description: Use Target in AEM Forms to create customized experiences for targeted customers.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Crear experiencias segmentadas en AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integración de Adobe Target con AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target integrado con AEM permite crear experiencias personalizadas para una audiencia objetivo. Con Adobe Target, puede crear pruebas A/B, medir la respuesta del usuario y generar contenido web personalizado para los usuarios objetivo. Puede integrar Adobe Target con AEM Forms para dirigirse a los componentes de imagen de los formularios adaptables y las comunicaciones interactivas.

Configure Adobe Target en AEM para utilizarlo con formularios adaptables y comunicaciones interactivas, consulte [Creación de una configuración de destino en AEM](/help/sites-administering/target.md) y [Agregar un marco](/help/sites-administering/target.md).

>[!NOTE]
>
>La segmentación funciona cuando el formulario adaptable o la comunicación interactiva se procesan con un nombre de host o una dirección IP. Se produce un error cuando el formulario adaptable o la comunicación interactiva se procesan mediante localhost.

## Creación de una actividad de Target {#creating-a-target-activity}

1. Toque **Adobe Experience Manager > Personalización > Actividades**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. En la página Actividades , pulse **Crear > Crear marca**.
1. Se le pide que elija una plantilla e introduzca propiedades.

   Seleccionar una plantilla, pulse **Siguiente.** Introduzca el título de la marca en la sección Propiedades y pulse **Crear.**
La marca ahora aparece en la página Actividades .

1. Pulse la marca en la página Actividades .
1. En el área principal de la marca, pulse **Crear** > **Crear actividad**.

   Cuando crea una actividad, especifica sus detalles, objetivos y configuración.

   La sección Detalles incluye nombre, motor de orientación y objetivo. Al seleccionar Adobe Target como motor de orientación, se habilita la opción de configuración de la nube de Target. Elija la configuración de la nube de Target, elija Tipo de actividad, proporcione el objetivo de la actividad y pulse **Siguiente**. La comunicación interactiva solo admite el tipo de actividad de segmentación de experiencias.

   La sección Target le permite añadir una experiencia de audiencia y ponerle un nombre. Haga clic en **Añadir experiencia** para habilitar la variable **Seleccionar audiencia** y **Experiencia de nombre** opciones. Toque **Seleccionar audiencia** para ver una lista de audiencias y su origen. Seleccione una audiencia en la lista Nombre de audiencia . Toque **Añadir experiencia** para asignar un nombre a la experiencia y pulse **Siguiente**.

   La sección Objetivos y configuración le permite programar y priorizar su actividad. Establezca la fecha de inicio, la fecha de finalización y la prioridad de la actividad, la métrica de objetivo, la métrica adicional y pulse **Guardar**.

   La actividad aparece ahora en la página de marca.

   >[!NOTE]
   >
   >Puede ignorar el error &quot;Su actividad se guardó, pero no se sincronizó con Target. Motivo: La siguiente experiencia no tiene ofertas&quot;, si se encuentra al guardar la actividad.

1. Para habilitar target, edite el archivo .jsp para incluir las bibliotecas de cliente que utiliza la plantilla de formularios adaptables.

   Por ejemplo, en la implementación predeterminada, haga clic en **Herramientas** >  **CRXDE Lite**.

   En la barra de direcciones del CRXDE Lite, escriba /libs/fd/af/components/page/base/head.jsp para editar el archivo head.jsp.

   Esta implementación utiliza la plantilla simpleEnSubscription . En esta implementación, modifique el archivo head.jsp para incluir las siguientes bibliotecas de cliente:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Para habilitar el marco de destino para formularios adaptables, vaya al formulario o a la comunicación interactiva y ábralo en modo de edición.

   Para abrir un formulario o una comunicación interactiva en modo de edición, pulse **Select** y, a continuación, toque **Apertura**.

   Alternativamente, aparecen cuatro botones al mover el puntero sobre el formulario o el icono de comunicación interactiva sin seleccionarlo. Puede pulsar el botón **Editar** para abrir el formulario en modo de edición.

1. En la barra de herramientas de la página, pulse **Información de la página** ![tema-opciones](assets/theme-options.png) > **Abrir propiedades**.
1. En la pestaña General , elija una configuración para la **Adobe Target** campo . Pulse **Guardar y cerrar**.

## Aplicación de la actividad creada a una imagen de formulario adaptable o a una imagen de comunicación interactiva {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Abra el formulario adaptable y la comunicación interactiva para editarlo. Si está abriendo una comunicación interactiva, abra el canal web.

1. En el modo de creación de la comunicación interactiva o el formulario adaptable, añada una imagen para dirigirla.

   >[!NOTE]
   >
   >AEM Forms solo admite componentes de imagen de destino. Asegúrese de que el panel que aloja el componente de imagen no contenga ningún otro componente y que el número de columnas para el panel esté establecido en 1.

1. Cambiar desde **Editar** a **Segmentación** en el menú contextual. La opción para cambiar de modo está cerca de la esquina superior derecha.
1. Seleccione un **MARCA**, seleccione **ACTIVIDAD** y toque **Iniciar segmentación**. La variable **Audiencias** aparece en la parte derecha del editor.

   ![targeting-menu](assets/targeting-menu.png)

1. Seleccione una audiencia de **Audiencias** y pulse la imagen a destino. Aparece un menú. En el menú , pulse **Target**. Toque la imagen y toque **Configurar**. En la ventana de propiedades, seleccione la imagen que desea mostrar para la audiencia seleccionada. Repita el paso para todas las audiencias. La segmentación de experiencias está habilitada para la imagen en la comunicación interactiva o en el formulario adaptable.

## Compruebe si la actividad creada se sincroniza con el servidor de Target {#check-if-the-created-activity-syncs-with-the-target-server}

Una actividad utilizada para segmentar se sincroniza con el servidor de Target. Para comprobar si la actividad está sincronizada con el servidor de Target, compruebe el estado de la actividad en la página de marca.

Asegúrese de que el estado de la actividad es Sincronizado.

## Validar comportamiento de Target {#validate-target-behavior}

Para validar el comportamiento de Target:

* Usar segmentación con `wcmmode preview` en el modo autor
* Usar segmentación con `wcmmode preview` y `wcmmode disabled` en el modo de publicación

## Orientación del monitor para el componente de imagen {#monitor-targeting-for-the-image-component}

Para supervisar la segmentación de los componentes de imagen en el formulario, publique sus imágenes, actividades y formularios adaptables.

## Problemas abiertos {#open-issues}

Expresión de visibilidad, error al definir el enfoque de las imágenes de destino en los formularios adaptables.
