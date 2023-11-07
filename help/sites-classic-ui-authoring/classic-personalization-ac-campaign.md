---
title: Uso de Adobe Campaign 6.1 y Adobe Campaign Standard
description: AEM Puede crear contenido de correo electrónico en y procesarlo en correos electrónicos de Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# Uso de Adobe Campaign 6.1 y Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

AEM Puede crear contenido de correo electrónico en y procesarlo en correos electrónicos de Adobe Campaign. Para ello, debe:

1. AEM Cree un boletín informativo en el que se le asigne un nombre a partir de una plantilla específica de Adobe Campaign.
1. Seleccionar [un servicio de Adobe Campaign](#selectingtheadobecampaigncloudservice) antes de editar el contenido para acceder a todas las funcionalidades.
1. Edite el contenido.
1. Valide el contenido.

A continuación, el contenido se puede sincronizar con una entrega en Adobe Campaign. Las instrucciones detalladas se describen en este documento.

>[!NOTE]
>
>AEM Antes de poder utilizar esta funcionalidad, debe configurar la integración de con el para que se integre con [Adobe Campaign](/help/sites-administering/campaignonpremise.md) o [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Envío de contenido de correo electrónico mediante Adobe Campaign {#sending-email-content-via-adobe-campaign}

AEM Después de configurar la y Adobe Campaign AEM, puede crear contenido de envío de correo electrónico directamente en la dirección de correo electrónico y, a continuación, procesarlo en Adobe Campaign.

Al crear contenido de Adobe Campaign AEM en la, debe vincular a un servicio de Adobe Campaign antes de editar el contenido para acceder a todas las funcionalidades.

Hay dos casos posibles:

* El contenido se puede sincronizar con una entrega desde Adobe Campaign. AEM Esto permite utilizar contenido de la en una entrega.
* (Solo Adobe Campaign local) El contenido se puede enviar directamente a Adobe Campaign, que genera automáticamente un nuevo envío de correo electrónico. Este modo tiene limitaciones.

Las instrucciones detalladas se describen en este documento.

### Creación de nuevo contenido de correo electrónico {#creating-new-email-content}

>[!NOTE]
>
>Al añadir plantillas de correo electrónico, asegúrese de añadirlas en **/content/campaigns** para que estén disponibles.
>

1. AEM En, seleccione la opción **Sitios web** a continuación, examine el explorador para encontrar dónde se administran las campañas de correo electrónico. En el ejemplo siguiente, el nodo correspondiente es **Sitios web** > **Campañas** > **Geometrixx Outdoors** > **Campañas de correo electrónico**.

   >[!NOTE]
   >
   >[Los ejemplos de correo electrónico solo están disponibles en Geometrixx](/help/sites-developing/we-retail.md#weretail). Descargar contenido de Geometrixx de muestra desde Package Share.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Seleccionar **Nuevo** > **Nueva página** para crear contenido de correo electrónico nuevo.
1. Seleccione una de las plantillas disponibles específicas de Adobe Campaign y rellene las propiedades generales de la página. Hay tres plantillas disponibles de forma predeterminada:

   * **Correo electrónico de Adobe Campaign (AC 6.1)**: permite añadir contenido a una plantilla predefinida antes de enviarlo a Adobe Campaign 6.1 para su envío.
   * **Correo electrónico de Adobe Campaign (ACS)**: permite añadir contenido a una plantilla predefinida antes de enviarlo a Adobe Campaign Standard para su envío.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Clic **Crear** para crear el correo electrónico o la newsletter.

### Selección del servicio en la nube y la plantilla de Adobe Campaign {#selecting-the-adobe-campaign-cloud-service-and-template}

Para integrarse con Adobe Campaign, debe añadir un servicio de nube de Adobe Campaign a la página. Al hacerlo, puede acceder a la personalización y a otra información de Adobe Campaign.

Además, es posible que también tenga que seleccionar la plantilla de Adobe Campaign, cambiar el asunto y añadir contenido de texto sin formato para los usuarios que no verán el correo electrónico en HTML.

1. Seleccione el **Página** en la barra de tareas y, a continuación, seleccione **Propiedades de página.**
1. En el **Cloud Services** en la ventana emergente, seleccione **Añadir servicio** para añadir el servicio Adobe Campaign, haga clic en **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Seleccione la configuración que coincida con la instancia de Adobe Campaign en la lista desplegable y haga clic en **OK**.

   >[!NOTE]
   >
   >Asegúrese de tocar o hacer clic en **OK** o **Aplicar** después de agregar el servicio en la nube. Esto habilita el **Adobe Campaign** para que funcione correctamente.

1. Si desea aplicar una plantilla de envíos de correo electrónico específica (de Adobe Campaign), distinta de la predeterminada **correo** plantilla, seleccione **Propiedades de página** otra vez. En el **Adobe Campaign** pestaña, introduzca el nombre interno de la plantilla de envíos de correo electrónico en la instancia de Adobe Campaign relacionada.

   En Adobe Campaign Standard, la plantilla es **AEM Entrega con contenido de**. En Adobe Campaign 6.1, la plantilla es **AEM Envío de correo electrónico con contenido de**.

   AEM Al seleccionar la plantilla, se activa automáticamente la opción de configuración de la plantilla de **Newsletter de Adobe Campaign** componentes.

### Edición de contenido de correo electrónico {#editing-email-content}

Puede editar el contenido del correo electrónico en la interfaz de usuario clásica o en la táctil.

1. Introduzca el asunto y la versión de texto del correo electrónico seleccionando **Propiedades de página** > **Correo electrónico** de la caja de herramientas.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. Edite el contenido del correo electrónico añadiendo los elementos que desee de los que están disponibles en la barra de tareas. Para ello, arrastre y suéltelos. A continuación, haga doble clic en el elemento que desee editar.

   Por ejemplo, puede agregar texto que contenga campos de personalización.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Consulte [Componentes de Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) para obtener una descripción de los componentes disponibles para los boletines informativos y las campañas de correo electrónico de Adobe Campaign.

   ![chlimage_1-177](assets/chlimage_1-177.png)

### Inserción de personalización {#inserting-personalization}

Al editar el contenido, puede insertar:

* Campos de contexto de Adobe Campaign. Son campos que se pueden insertar dentro del texto y que se adaptan a los datos del destinatario (por ejemplo, nombre, apellidos o cualquier dato de la dimensión objetivo).
* Bloques de personalización de Adobe Campaign. Son bloques de contenido predefinido que no están relacionados con los datos del destinatario, como un logotipo de una marca o un vínculo a una página espejo.

Consulte [Componentes de Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) para obtener una descripción completa de los componentes de Campaign.

>[!NOTE]
>
>* Solo los campos de Adobe Campaign **Perfiles** se tienen en cuenta las dimensiones de segmentación.
>* Al ver las propiedades de **Sites**, no tiene acceso a los campos de contexto de Adobe Campaign. Puede acceder a ellas directamente desde el correo electrónico mientras edita.
>

1. Insertar un nuevo **Newsletter** > **Texto y personalización (Campaign)** componente.
1. Abra el componente haciendo doble clic en él. El **Editar** tiene una funcionalidad que permite insertar los elementos personalizados.

   >[!NOTE]
   >
   >Los campos de contexto disponibles corresponden a la variable **Perfiles** dimensión de segmentación en Adobe Campaign.
   >
   >Consulte [AEM Vinculación de una página de a un correo electrónico de Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Seleccionar **Client Context** en la barra de tareas para probar los campos personalizados con los datos de los perfiles de persona.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Aparece una ventana que le permite seleccionar la persona que desee. Los campos personalizados se sustituyen automáticamente por los datos del perfil seleccionado.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### Previsualización de una newsletter {#previewing-a-newsletter}

Puede obtener una vista previa del aspecto que tendrá la newsletter y previsualizar la personalización.

1. Abra la newsletter que desee previsualizar y haga clic en Vista previa (lupa) para reducir la barra de tareas.
1. Haga clic en uno de los iconos del cliente de correo electrónico para ver el aspecto de la newsletter en cada cliente de correo electrónico.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. Expanda la barra de tareas para empezar a editar de nuevo.

### AEM Aprobación de contenido en la {#approving-content-in-aem}

Una vez finalizado el contenido, puede iniciar el proceso de aprobación. Vaya a la **Flujo de trabajo** de la caja de herramientas y seleccione la **Aprobar para Adobe Campaign** flujo de trabajo.

Este flujo de trabajo predeterminado tiene dos pasos: revisión y luego aprobación, o revisión y luego rechazo. Sin embargo, este flujo de trabajo se puede ampliar y adaptar a un proceso más complejo.

![chlimage_1-182](assets/chlimage_1-182.png)

Para aprobar el contenido de Adobe Campaign, aplique el flujo de trabajo seleccionando **Flujo de trabajo** en la barra de tareas y seleccionando **Aprobar para Adobe Campaign** y haga clic en **Iniciar flujo de trabajo**. Siga los pasos y apruebe el contenido. También puede rechazar el contenido seleccionando **Rechazar** en lugar de **Aprobar** en el último paso del flujo de trabajo.

![chlimage_1-183](assets/chlimage_1-183.png)

Una vez aprobado el contenido, aparece como aprobado en Adobe Campaign. A continuación, se puede enviar el correo electrónico.

En Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

En Adobe Campaign 6.1:

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>El contenido no aprobado se puede sincronizar con un envío en Adobe Campaign, pero el envío no se puede ejecutar. Solo se puede enviar contenido aprobado a través de envíos de Campaign.

## AEM Vinculación de con Adobe Campaign Standard y Adobe Campaign 6.1 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>Consulte [AEM Vinculación de con Adobe Campaign Standard y Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) bajo [Uso de Adobe Campaign 6.1 y Adobe Campaign Standard](/help/sites-authoring/campaign.md) en la documentación de creación estándar para obtener más información.
