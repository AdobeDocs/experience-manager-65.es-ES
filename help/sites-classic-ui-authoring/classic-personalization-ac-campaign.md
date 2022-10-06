---
title: Trabajo con Adobe Campaign 6.1 y Adobe Campaign Standard
seo-title: Working with Adobe Campaign 6.1 and Adobe Campaign Standard
description: Puede crear contenido de correo electrónico en AEM y procesarlo en los mensajes de correo electrónico de Adobe Campaign.
seo-description: You can create email content in AEM and process it in Adobe Campaign emails.
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 63%

---

# Trabajo con Adobe Campaign 6.1 y Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

Puede crear contenido de correo electrónico en AEM y procesarlo en los mensajes de correo electrónico de Adobe Campaign. Para ello, debe hacer lo siguiente:

1. Cree una newsletter nueva en AEM a partir de una plantilla específica de Adobe Campaign.
1. Seleccione [un servicio de Adobe Campaign](#selectingtheadobecampaigncloudservice) antes de editar el contenido para acceder a toda la funcionalidad.
1. Edite el contenido.
1. Valide el contenido.

A continuación, el contenido se puede sincronizar con un envío en Adobe Campaign. Las instrucciones detalladas se describen en este documento.

>[!NOTE]
>
>Antes de poder usar esta funcionalidad, debe configurar AEM para integrarse con [Adobe Campaign](/help/sites-administering/campaignonpremise.md) o [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Enviar el contenido de correo electrónico a través de Adobe Campaign {#sending-email-content-via-adobe-campaign}

Después de configurar AEM y Adobe Campaign, puede crear contenido de envío de correo electrónico directamente en AEM y, a continuación, procesarlo en Adobe Campaign.

Al crear contenido de Adobe Campaign en AEM, debe vincular a un servicio de Adobe Campaign antes de editar el contenido para acceder a todas las funciones.

Existen dos casos posibles:

* El contenido se puede sincronizar con un envío de Adobe Campaign. Esto le permite utilizar el contenido de AEM en un envío.
* (solo instalación local de Adobe Campaign) El contenido se puede enviar directamente a Adobe Campaign, que genera automáticamente un nuevo envío de correo electrónico. Este modo tiene limitaciones.

Las instrucciones detalladas se describen en este documento.

### Creación de nuevo contenido de correo electrónico {#creating-new-email-content}

>[!NOTE]
>
>Al añadir plantillas de correo electrónico, asegúrese de agregarlas en **/content/igns** para que estén disponibles.

1. En AEM, seleccione la opción **Sitios web** a continuación, examine el explorador para encontrar dónde se administran las campañas de correo electrónico. En el ejemplo siguiente, el nodo correspondiente es **Sitios web** > **Campañas** > **Geometrixx Outdoors** > **Campañas de correo electrónico**.

   >[!NOTE]
   >
   >[Los ejemplos de correo electrónico solo están disponibles en Geometrixx](/help/sites-developing/we-retail.md#weretail). Descargue el contenido de ejemplo de Geometrixx de Uso compartido de paquetes.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Select **Nuevo** > **Nueva página** para crear contenido de correo electrónico nuevo.
1. Seleccione una de las plantillas disponibles específicas de Adobe Campaign y rellene las propiedades generales de la página. De forma predeterminada, están disponibles tres plantillas:

   * **Correo electrónico de Adobe Campaign (AC 6.1)**: permite añadir contenido a una plantilla predefinida antes de enviarlo a Adobe Campaign 6.1 para su envío.
   * **Correo electrónico de Adobe Campaign (ACS)**: permite añadir contenido a una plantilla predefinida antes de enviarlo a Adobe Campaign Standard para su envío.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Haga clic en **Crear** para crear su correo electrónico o newsletter.

### Selección del servicio de nube y de la plantilla de Adobe Campaign {#selecting-the-adobe-campaign-cloud-service-and-template}

Para integrar con Adobe Campaign, debe añadir un servicio de nube de Adobe Campaign a la página. Al hacerlo, tendrá acceso a la personalización y a otro tipo de información de Adobe Campaign.

Además, puede que deba seleccionar la plantilla de Adobe Campaign, cambiar el asunto y añadir contenido con texto sin formato para aquellos usuarios que no puedan ver el correo electrónico en HTML.

1. Seleccione el **Página** en la barra de tareas y, a continuación, seleccione **Propiedades de página.**
1. En el **Servicios de nube** en la ventana emergente, seleccione **Añadir servicio** para añadir el servicio Adobe Campaign y haga clic en **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Seleccione la configuración que coincida con su instancia de Adobe Campaign en la lista desplegable y haga clic en **OK**.

   >[!NOTE]
   >
   >Asegúrese de tocar o de hacer clic en **OK** o **Aplicar** después de añadir el servicio de nube. Esto permite que la pestaña **Adobe Campaign** funcione correctamente.

1. Si desea aplicar una plantilla de envío de correo electrónico específica (de Adobe Campaign) distinta de la predeterminada **correo** plantilla, seleccione **Propiedades de página** de nuevo. En el **Adobe Campaign** , introduzca el nombre interno de la plantilla de envío de correo electrónico en la instancia de Adobe Campaign relacionada.

   En Adobe Campaign Standard, la plantilla es **Envío con contenido de AEM**. En Adobe Campaign 6.1, la plantilla es **Envío de correo electrónico con contenido de AEM**.

   Al seleccionar la plantilla, AEM activa automáticamente la variable **Newsletter de Adobe Campaign** componentes.

### Edición del contenido de correo electrónico {#editing-email-content}

Puede editar el contenido de correo electrónico en la interfaz de usuario clásica o en la interfaz de usuario táctil.

1. Introduzca el asunto y la versión de texto del correo electrónico seleccionando **Propiedades de página** > **Correo electrónico** del cuadro de herramientas.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. Para editar el contenido del mensaje de correo electrónico, añada los elementos que desee de los que se encuentran disponibles en la barra de tareas. Para ello, arrástrelos y colóquelos. A continuación, haga doble clic en el elemento que desee editar.

   Por ejemplo, puede añadir texto que contenga campos de personalización.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Consulte [Componentes de Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) para obtener una descripción de los componentes disponibles para las newsletters o las campañas de correo electrónico de Adobe Campaign.

   ![chlimage_1-177](assets/chlimage_1-177.png)

### Inserción de personalización {#inserting-personalization}

Al editar el contenido, puede insertar:

* Campos de contexto de Adobe Campaign. Son campos que puede insertar en el texto y que se adaptarán según los datos del destinatario (por ejemplo, nombre, apellido o cualquier dato de la dimensión de destino).
* Bloques de personalización de Adobe Campaign. Son bloques de contenido predefinido que no están relacionados con los datos del destinatario, como un logotipo de marca o un vínculo a una página espejo.

Consulte [Componentes de Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) para obtener una descripción exhaustiva de los componentes de Campaign.

>[!NOTE]
>
>* Solo se tienen en cuenta los campos de la dimensión objetivo **Perfiles** de Adobe Campaign.
>* Al ver las propiedades desde **Sitios**, no tiene acceso a los campos de contexto de Adobe Campaign. Puede acceder a ellos directamente desde el correo electrónico durante la edición.
>


1. Insertar un nuevo **Newsletter** > **Texto y personalización (Campaign)** componente.
1. Haga doble clic en el componente para abrirlo. La ventana **Editar** tiene una funcionalidad que le permite insertar los elementos de personalización.

   >[!NOTE]
   >
   >Los campos de contexto disponibles corresponden a la dimensión objetivo **Perfiles** de Adobe Campaign.
   >
   >Consulte [Vinculación de una página AEM a un correo electrónico de Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Select **ClientContext** en la barra de tareas para probar los campos de personalización utilizando los datos de los perfiles de persona.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Aparece una ventana en que puede seleccionar el perfil que desee. Los datos del perfil seleccionado sustituyen automáticamente los campos de personalización.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### Vista previa de un formulario {#previewing-a-newsletter}

Puede previsualizar el aspecto que tendrá la newsletter, así como la personalización.

1. Abra la newsletter que desee previsualizar y haga clic en Vista previa (lupa) para reducir el tamaño de la barra de tareas.
1. Haga clic en uno de los iconos del cliente de correo electrónico para ver el aspecto que tendrá la newsletter en cada cliente de correo electrónico.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. Expanda la barra de tareas para volver a comenzar a editar.

### Aprobación de contenido en AEM {#approving-content-in-aem}

Una vez terminado el contenido, puede iniciar el proceso de aprobación. Vaya a la **Flujo de trabajo** del cuadro de herramientas y seleccione la **Aprobar para Adobe Campaign** flujo de trabajo.

Este flujo de trabajo listo para usar tiene dos pasos: revisión y aprobación, o revisión y rechazo. Sin embargo, este flujo de trabajo puede ampliarse y adaptarse a un proceso más complejo.

![chlimage_1-182](assets/chlimage_1-182.png)

Para aprobar contenido para Adobe Campaign, seleccione **Flujo de trabajo** en la barra de tareas, después **Aprobar para Adobe Campaign** y haga clic en **Iniciar flujo de trabajo para aplicarlo**. Siga los pasos y apruebe el contenido. También puede rechazar el contenido. Para ello, seleccione **Rechazar** en lugar de **Aprobar** en el último paso del flujo de trabajo.

![chlimage_1-183](assets/chlimage_1-183.png)

Una vez aprobado el contenido, aparece como aprobado en Adobe Campaign. A continuación, se puede enviar el correo electrónico.

En Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

En Adobe Campaign 6.1:

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>El contenido no aprobado se puede sincronizar con un envío en Adobe Campaign, pero el envío no se puede ejecutar. Solo se puede enviar contenido aprobado a través de envíos de Campaign.

## Vinculación de AEM con Adobe Campaign Standard y Adobe Campaign 6.1 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>Consulte [Vinculación de AEM con Adobe Campaign Standard y Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) under [Uso de Adobe Campaign 6.1 y Adobe Campaign Standard](/help/sites-authoring/campaign.md) en la documentación de creación estándar para obtener más información.
