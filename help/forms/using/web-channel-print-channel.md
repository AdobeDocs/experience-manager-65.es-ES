---
title: Canal de impresión y canal web
seo-title: Canal de impresión y canal web
description: Importación de plantillas de canal de impresión y creación y activación de plantillas de canal web
seo-description: Importación de plantillas de canal de impresión y creación y activación de plantillas de canal web
uuid: 2361b1ee-c789-4a5a-9575-8b62b603da1e
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 96d2b1cc-3252-4cc7-8b06-a897cbef8599
docset: aem65
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# Canal de impresión y canal web{#print-channel-and-web-channel}

Las comunicaciones interactivas se pueden entregar a través de dos canales: imprimir y Web. El canal de impresión se utiliza para crear archivos PDF y comunicaciones en papel, como una carta impresa como recordatorio de pago de primas de seguro, mientras que el canal web se utiliza para ofrecer experiencias en línea, como un extracto de tarjeta de crédito en un sitio web.

Los autores de comunicación interactiva pueden reutilizar recursos como fragmentos de documento e imágenes para crear versiones impresas y web de la comunicación interactiva.

Uno de los requisitos previos para [Crear una comunicación interactiva](../../forms/using/create-interactive-communication.md) es tener las plantillas para impresión o canal web disponibles en el servidor. Mientras los autores de plantillas crean la plantilla de canal web en AEM, la plantilla de canal de impresión XDP se crea en Adobe Forms Designer y se carga en el servidor.

## Canal de impresión {#printchannel}

El canal de impresión de una comunicación interactiva utiliza la plantilla de formulario XFA, XDP. Un XDP está diseñado en Adobe Forms Designer. Para obtener más información sobre la creación de plantillas de canal de impresión, consulte [Diseño de diseño](../../forms/using/layout-design-details.md). Para utilizar una plantilla de canal de impresión en la comunicación interactiva, debe cargar la plantilla en el servidor de AEM Forms.

### Cargar plantilla de canal de impresión de comunicación interactiva {#upload-interactive-communication-print-channel-template}

Para cargar la plantilla, debe ser miembro del grupo de usuarios de formularios. Siga los siguientes pasos para cargar la plantilla de canal de impresión (XDP) en AEM Forms:

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.

1. Pulse **[!UICONTROL Crear]** > **[!UICONTROL Cargar archivo]**.

   Desplácese y seleccione la plantilla de canal de impresión (XDP) adecuada y pulse **[!UICONTROL Abrir]**.

## Canal web {#web-channel}

Los autores y administradores de plantillas pueden crear, editar y habilitar plantillas web. Para permitir que otros usuarios creen plantillas web, debe otorgarles derechos. Para obtener más información, consulte [Administración de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md).

### Creación de plantillas de canal web {#authoring-web-channel-template}

Para crear una plantilla de canal web, primero debe crear una carpeta de plantilla . Una vez que haya creado una plantilla web dentro de una carpeta de plantillas, debe activar la plantilla para permitir a los usuarios de los formularios crear un canal web de una comunicación interactiva basada en la plantilla.

Para crear una plantilla de canal web Complete los siguientes pasos:

1. Cree una carpeta de plantilla para mantener las plantillas web de comunicación interactiva, si aún no dispone de una. Para obtener más información, consulte Carpetas de plantilla en [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md).

   1. Pulse **[!UICONTROL Herramientas]** ![herramientas](assets/tools.png) > **[!UICONTROL Explorador de configuración]**.
      * Consulte la documentación [Configuration Browser](/help/sites-administering/configurations.md) para obtener más información.
   1. En la página Explorador de configuración, pulse **[!UICONTROL Crear]**.
   1. En el cuadro de diálogo Crear configuración, especifique un título para la carpeta, marque **[!UICONTROL Plantillas editables]** y pulse **[!UICONTROL Crear]**.

      La carpeta se crea y se enumera en la página Explorador de configuración .

1. Vaya a la carpeta de plantillas adecuada y cree una plantilla web.

   1. Vaya a la carpeta de plantillas adecuada seleccionando **[!UICONTROL Tools]** > **[!UICONTROL Templates]** > **`[Folder]`**.
   1. Toque **[!UICONTROL Crear]**.
   1. Seleccione **[!UICONTROL Interactive Communication - Web Channel]** y pulse **[!UICONTROL Next]**.
   1. Introduzca un título y una descripción de plantilla y, a continuación, pulse **[!UICONTROL Crear]**.

      La plantilla se crea y aparece un cuadro de diálogo.

   1. Pulse **[!UICONTROL Abrir]** para abrir la plantilla que ha creado en el editor de plantillas.

      Aparecerá el Editor de plantillas.

      ![webchanneltemplate](assets/webchanneltemplate.png)

      Al crear o editar una plantilla, hay varios aspectos que puede definir un autor de plantillas. Crear o editar una plantilla es similar a crear páginas. Para obtener más información, consulte Edición de plantillas: autores de plantillas en [Creación de plantillas de página](/help/sites-authoring/templates.md).

1. Para permitir el uso de esta plantilla para la creación de comunicación interactiva, habilite la plantilla .

   1. Pulse **[!UICONTROL Herramientas]** ![herramientas](assets/tools.png) > **[!UICONTROL Plantillas]**.
   1. Vaya a la plantilla adecuada, selecciónela y pulse **[!UICONTROL Habilitar]** y, en el mensaje de alerta, pulse **[!UICONTROL Habilitar]**.

      La plantilla está activada y su estado se muestra como Activada. Ahora puede continuar creando una comunicación interactiva en la que puede utilizar la plantilla de canal web recién creada.

### Imprimir canal como maestro para el canal web {#print-channel-as-master-for-web-channel}

Durante la creación de una comunicación interactiva, los autores pueden seleccionar esta opción para crear el canal web sincronizado con el canal de impresión. El uso del canal de impresión como maestro para el canal web garantiza que el contenido, la herencia y el enlace de datos del canal web se deriven del canal de impresión y que los cambios realizados en el canal de impresión se puedan reflejar en el canal web. Sin embargo, los autores de la comunicación interactiva pueden romper la herencia de componentes específicos del canal web, según sea necesario.

![Imprimir el canal como canal ](assets/create_ic_print_master_new.png) ![maestroWeb con el canal de impresión como maestro](assets/create_ic_print_master_web_new.png)

