---
title: Integración con Adobe Campaign Classic
seo-title: Integrating with Adobe Campaign Classic
description: Aprenda a integrar AEM con Adobe Campaign Classic
seo-description: Learn how to integrate AEM with Adobe Campaign Classic
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 0%

---

# Integración con Adobe Campaign Classic{#integrating-with-adobe-campaign-classic}

>[!NOTE]
>
>En esta documentación se describe cómo integrar AEM con Adobe Campaign Classic, la solución local. Si utiliza Adobe Campaign Standard, consulte [Integración con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) para estas instrucciones.

Adobe Campaign permite administrar el contenido y los formularios de entrega por correo electrónico directamente en Adobe Experience Manager.

Para utilizar ambas soluciones juntas al mismo tiempo, primero debe configurarlas para conectarse entre sí. Esto implica pasos de configuración tanto en Adobe Campaign como en Adobe Experience Manager. Estos pasos se describen en detalle en este documento.

Trabajar con Adobe Campaign en AEM incluye la capacidad de enviar correos electrónicos a través de Adobe Campaign y se describe en [Uso de Adobe Campaign](/help/sites-authoring/campaign.md). También incluye el uso de formularios en páginas AEM para manipular datos.

Además, los siguientes temas pueden ser de interés al integrar AEM con [Adobe Campaign](https://helpx.adobe.com/support/campaign/classic.html):

* [Prácticas recomendadas para plantillas de correo electrónico](/help/sites-administering/best-practices-for-email-templates.md)
* [Resolución de problemas de la integración de Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md)

Si amplía la integración con Adobe Campaign, es posible que desee ver las páginas siguientes:

* [Creación de extensiones personalizadas](/help/sites-developing/extending-campaign-extensions.md)
* [Creación de asignaciones de formularios personalizados](/help/sites-developing/extending-campaign-form-mapping.md)

## Flujo de trabajo de integración de AEM y Adobe Campaign {#aem-and-adobe-campaign-integration-workflow}

En esta sección se describe un flujo de trabajo típico entre AEM y Adobe Campaign al crear campañas y entregar contenido.

El flujo de trabajo típico implica lo siguiente y se describe en detalle:

1. Empiece a crear la campaña (tanto en Adobe Campaign como en AEM).
1. Antes de vincular el contenido y la entrega, personalice el contenido en AEM y cree una entrega en Adobe Campaign.
1. Vincule contenido y envío en Adobe Campaign.

### Comenzar a crear la campaña {#start-building-your-campaign}

Empiece a crear una campaña en cualquier momento. Antes de vincular el contenido, AEM y AC son independientes. Esto significa que los especialistas en marketing pueden empezar a crear sus campañas y segmentación en Adobe Campaign, mientras que los creadores de contenido están trabajando en el diseño en AEM.

### Antes de vincular contenido y envío {#before-linking-content-and-delivery}

Antes de vincular el contenido y crear un mecanismo de envío, debe hacer lo siguiente:

**En AEM**

* Personalice utilizando los campos de personalización de la variable **Texto y personalización** componente

**En Adobe Campaign**

* Creación de una entrega de tipo **aemContent**

### Vinculación de contenido y configuración de envíos {#linking-content-and-setting-delivery}

Después de preparar el contenido para la vinculación y el envío, determina exactamente cómo y dónde se debe vincular el contenido.

Todos estos pasos se completan en Adobe Campaign.

1. Especifique qué instancia AEM usar.
1. Sincronice el contenido haciendo clic en el botón Synchronize .
1. Abra el selector de contenido para elegir el contenido.

### Si es nuevo en AEM {#if-you-are-new-to-aem}

Si es nuevo en AEM, puede que encuentre útiles los siguientes vínculos para comprender AEM:

* [Inicio de AEM](/help/sites-deploying/deploy.md)
* [Explicación de los agentes de replicación](/help/sites-deploying/replication.md)
* [Búsqueda y uso de archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)
* [Introducción a la plataforma AEM](/help/sites-deploying/platform.md)

## Configuración de Adobe Campaign {#configuring-adobe-campaign}

La configuración de Adobe Campaign implica lo siguiente:

1. Instalación del paquete de integración de AEM en Adobe Campaign.
1. Configuración de una cuenta externa.
1. Comprobando que AEMResourceTypeFilter está configurado correctamente.

Además, hay configuraciones avanzadas que puede realizar, como:

* Administración de bloques de contenido
* Administración de campos personalizados

Consulte [Configuraciones avanzadas](#advanced-configurations).

>[!NOTE]
>
>Para realizar estas operaciones, debe tener la variable **administración** en Adobe Campaign.

### Requisitos previos {#prerequisites}

Asegúrese de tener los siguientes elementos previamente:

* [Una instancia de creación de AEM](/help/sites-deploying/deploy.md#getting-started)
* [Una instancia de publicación AEM](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Una instancia de Adobe Campaign Classic](https://helpx.adobe.com/support/campaign/classic.html) : incluye un cliente y un servidor
* Internet Explorer 11

>[!NOTE]
>
>Si está ejecutando una versión anterior a la versión 8640 de Adobe Campaign Classic, consulte la [documentación de actualización](https://docs.campaign.adobe.com/doc/AC6.1/en/PRO_Updating_Adobe_Campaign_Upgrading.html) para obtener más información. Tenga en cuenta que tanto el cliente como la base de datos deben actualizarse a la misma compilación.

>[!CAUTION]
>
>Operaciones detalladas en la [Configuración de Adobe Campaign](#configuring-adobe-campaign) y [Configuración de Adobe Experience Manager](#configuring-adobe-experience-manager) son necesarias para que las funcionalidades de integración entre AEM y Adobe Campaign funcionen correctamente.

### Instalación del paquete de integración de AEM {#installing-the-aem-integration-package}

Debe instalar el **Integración AEM** en Adobe Campaign. Para ello:

1. Vaya a la instancia de Adobe Campaign con la que desee vincular AEM.
1. Select *Herramientas* > *Avanzadas* > *Importar paquete...*.

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. Haga clic en **Instalación de un paquete estándar** y, a continuación, seleccione **Integración AEM** paquete.

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. Haga clic en **Siguiente** y luego **Inicio**.

   Este paquete contiene el **aemserver** operador que se utilizará para conectar el servidor de AEM a Adobe Campaign.

   >[!CAUTION]
   >
   >De forma predeterminada, no hay ninguna zona de seguridad configurada para este operador. Para conectarse a Adobe Campaign mediante AEM, debe seleccionar una.
   >
   >En el **serverConf.xml** archivo, la variable **allowUserPassword** del área de seguridad seleccionada debe estar configurada en **true** para autorizar a AEM a conectar Adobe Campaign mediante inicio de sesión o contraseña.
   >
   >Recomendamos encarecidamente que cree una zona de seguridad dedicada a AEM para evitar problemas de seguridad. Para obtener más información, consulte [Guía de instalación](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html).

   ![chlimage_1-134](assets/chlimage_1-134a.png)

### Configuración de una cuenta externa AEM {#configuring-an-aem-external-account}

Debe configurar una cuenta externa que le permita conectar Adobe Campaign a la instancia de AEM.

>[!NOTE]
>
>* Al instalar el **Integración AEM** , se crea una cuenta de AEM externa. Puede configurar la conexión a la instancia de AEM desde ella o crear una nueva.
>* En AEM, asegúrese de establecer la contraseña para el usuario remoto de la campaña. Debe establecer esta contraseña para conectar Adobe Campaign con AEM. Inicie sesión como administrador y, en la consola de administración de usuarios, busque el usuario remoto de la campaña y haga clic en **Establecer contraseña**.
>


Para configurar una cuenta de AEM externa:

1. Vaya a la **Administración** > **Plataforma** > **Cuentas externas** nodo .
1. Cree una nueva cuenta externa y seleccione la opción **AEM** tipo .
1. Introduzca los parámetros de acceso para la instancia de creación de AEM: la dirección del servidor, así como el ID y la contraseña utilizados para conectarse a esta instancia. La contraseña de la cuenta de usuario de campaign-api es la misma que la del usuario remoto de campaign para la que se ha establecido una contraseña en AEM.

   >[!NOTE]
   >
   >Asegúrese de que la dirección del servidor **not** termine con una barra diagonal. Por ejemplo, introduzca `https://yourserver:4502` en lugar de `https://yourserver:4502/`

   ![chlimage_1-135](assets/chlimage_1-135a.png) ![chlimage_1-136](assets/chlimage_1-136a.png)

1. Asegúrese de que la variable **Habilitado** está seleccionada.

### Verificación de la opción AEMResourceTypeFilter {#verifying-the-aemresourcetypefilter-option}

La variable **AEMResourceTypeFilter** se utiliza para filtrar tipos de recursos de AEM que se pueden utilizar en Adobe Campaign. Esto permite a Adobe Campaign recuperar AEM contenido específicamente diseñado para utilizarse solo en Adobe Campaign.

Esta opción debe estar preconfigurada; sin embargo, si cambia esta opción, puede provocar que la integración no funcione.

Para verificar el **AEMResourceTypeFilter** está configurada:

1. Vaya a **Plataforma** >**Opciones**.
1. En el **AEMResourceTypeFilter** , compruebe que las rutas son correctas. Este campo debe contener el valor:

   **mcm/campaign/components/newsletter,mcm/campaign/components/campaign_newsletterpage,mcm/neolane/components/newsletter**

   O, en algunos casos, el valor es el siguiente:

   **mcm/campaign/components/newsletter**

   ![chlimage_1-137](assets/chlimage_1-137a.png)

## Configuración de Adobe Experience Manager {#configuring-adobe-experience-manager}

Para configurar AEM, debe hacer lo siguiente:

* Configure la replicación entre instancias.
* Conecte AEM a Adobe Campaign mediante Cloud Services.
* Configure el externalizador.

### Configuración de la replicación entre instancias AEM {#configuring-replication-between-aem-instances}

El contenido creado a partir de la instancia de creación de AEM se envía primero a la instancia de publicación. Debe publicar para que las imágenes de la newsletter estén disponibles en la instancia de publicación y para los destinatarios de la newsletter. Por lo tanto, el agente de replicación debe configurarse para replicarse desde la instancia de creación de AEM a la instancia de publicación de AEM.

>[!NOTE]
>
>Si no desea utilizar la URL de replicación y, en su lugar, utiliza la URL de cara al público, puede establecer la variable **URL pública** en el siguiente ajuste de configuración en OSGi (**Logotipo de AEM** >  **Herramientas** icono >  **Operaciones** > **Consola web** > **Configuración de OSGi** > **Integración de AEM Campaign: Configuración**):
**URL pública:** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

Este paso también es necesario para replicar ciertas configuraciones de instancia de creación en la instancia de publicación.

Para configurar la replicación entre instancias de AEM:

1. En la instancia de creación, seleccione **Logotipo de AEM**> **Herramientas** icono > **Implementación** > **Replicación** > **Agentes en autor** y haga clic en **Agente predeterminado**.

   ![chlimage_1-138](assets/chlimage_1-138a.png)

   >[!NOTE]
   Evite utilizar localhost (es decir, una copia local de AEM) al configurar la integración con Adobe Campaign a menos que la instancia de publicación y de autor estén en el mismo equipo.

1. Toque o haga clic **Editar** a continuación, seleccione la **Transporte** pestaña .
1. Configure el URI reemplazando **localhost** con la dirección IP o la dirección de la instancia de publicación de AEM.

   ![chlimage_1-139](assets/chlimage_1-139a.png)

### Conexión de AEM a Adobe Campaign {#connecting-aem-to-adobe-campaign}

Antes de poder usar AEM y Adobe Campaign juntos, debe establecer el vínculo entre ambas soluciones para que puedan comunicarse.

1. Conéctese a la instancia de creación de AEM.
1. Select **Logotipo de AEM** > **Herramientas** icono > **Implementación** > **Cloud Services**, luego **Configurar ahora** en la sección Adobe Campaign .

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. Cree una nueva configuración introduciendo una **Título** y haga clic en **Crear** o elija la configuración existente que desea vincular con la instancia de Adobe Campaign.
1. Edite la configuración para que coincida con los parámetros de la instancia de Adobe Campaign.

   * **Nombre de usuario**: **aemserver**, el operador de paquete de integración de Adobe Campaign AEM se utiliza para establecer el vínculo entre las dos soluciones.
   * **Contraseña**: Contraseña del operador de Adobe Campaign aemserver. Es posible que tenga que volver a especificar la contraseña de este operador directamente en Adobe Campaign.
   * **Punto final de API**: URL de instancia de Adobe Campaign.

1. Select **Conectarse a Adobe Campaign** y haga clic en **OK**.

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   >[!NOTE]
   Tras [cree su correo electrónico y publíquelo](/help/sites-authoring/campaign.md), debe volver a publicar la configuración en la instancia de publicación.

   ![chlimage_1-142](assets/chlimage_1-142a.png)

>[!NOTE]
Si la conexión falla, asegúrese de comprobar lo siguiente:
* Puede encontrar un problema de certificado al utilizar una conexión segura a una instancia de Adobe Campaign (https). Deberá añadir el certificado de instancia de Adobe Campaign al **cacerías** del JDK de su instancia de AEM.
* Se debe configurar una zona de seguridad para la variable [operador aemserver](#connecting-aem-to-adobe-campaign) en Adobe Campaign. Además, en la **serverConf.xml** archivo, la variable **allowUserPassword** de la zona de seguridad debe establecerse en **true** para autorizar AEM conexión a Adobe Campaign mediante el modo de inicio de sesión/contraseña.
>
Además, consulte [Resolución de problemas de integración de AEM/Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md).

### Configuración del externalizador {#configuring-the-externalizer}

Debe [configurar el externalizador](/help/sites-developing/externalizer.md) en AEM en la instancia de autor. El externalizador es un servicio OSGi que permite transformar una ruta de recurso en una dirección URL externa y absoluta. Este servicio proporciona un lugar central para configurar esas direcciones URL externas y crearlas.

Consulte [Configuración del externalizador](/help/sites-developing/externalizer.md) para instrucciones generales. Para la integración con Adobe Campaign, asegúrese de configurar el servidor de publicación en `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`no apunte a `localhost:4503` pero a un servidor al que se pueda acceder desde la consola de Adobe Campaign.

Si señala a `localhost:4503` o cualquier otro servidor al que Adobe Campaign no pueda acceder, las imágenes no aparecerán en la consola de Adobe Campaign.

![chlimage_1-143](assets/chlimage_1-143a.png)

## Configuraciones avanzadas {#advanced-configurations}

También puede realizar algunas configuraciones avanzadas, como:

* Administrar campos y bloques personalizados.
* Desactivar un bloque personalizado.
* Administre los datos de extensión de destino.

### Administración de campos y bloques personalizados {#managing-personalization-fields-and-blocks}

Adobe Campaign administra los campos y bloques disponibles para añadir personalización al contenido del correo electrónico en AEM.

Se proporciona una lista predeterminada, pero se puede modificar. También puede añadir u ocultar campos y bloques personalizados.

#### Adición de un campo personalizado {#adding-a-personalization-field}

Para añadir un nuevo campo de personalización a los que ya están disponibles, debe ampliar Adobe Campaign **nms:seedMember** esquema como se indica a continuación:

>[!CAUTION]
El campo que debe añadir ya debe haberse añadido a través de una extensión de esquema de destinatario (**nms:recipient**). Para obtener más información, consulte la [Configuración](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Editing_schemas.html) guía.

1. Vaya a la **Administración** > **Configuración** > **Esquemas de datos** en la navegación de Adobe Campaign.
1. Select **Nuevo**.

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. En la ventana emergente, seleccione **Ampliación de los datos de la tabla mediante un esquema de extensión** y haga clic en **Siguiente**.

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. Introduzca los diferentes parámetros del esquema ampliado:

   * **Esquema**: seleccione **nms:seedMember** esquema. Los demás campos de la ventana se completan automáticamente.
   * **Área de nombres**: personalice el área de nombres del esquema extendido.

1. Edite el código XML del esquema para especificar el campo que desea añadir allí. Para obtener más información sobre la ampliación de esquemas en Adobe Campaign, consulte la [Guía de configuración](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Extending_a_schema.html).
1. Guarde el esquema y, a continuación, actualice la estructura de la base de datos de Adobe Campaign mediante la variable **Herramientas** > **Avanzadas** > **Actualizar estructura de base de datos** en la consola.
1. Desconéctese y vuelva a conectarse a la consola de Adobe Campaign para guardar los cambios. El nuevo campo aparece ahora en la lista de campos personalizados disponibles en AEM.

#### Ejemplo {#example}

Para agregar un **Número de registro** , debe tener los siguientes elementos:

* La variable **nms:recipient** extensión de esquema denominada **cus:recipient** contiene:

```xml
<element desc="Recipient table (profiles)" img="nms:recipient.png" label="Recipients" labelSingular="Recipient" name="recipient">

  <attribute dataPolicy="smartCase" desc="Recipient registration number"
  label="Registration Number"
  length="50" name="registrationNumber" type="string"/>

</element>
```

La variable **nms:seedMember** extensión de esquema denominada **cus:seedMember** contiene:

```xml
<element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">

  <element name="custom_nms_recipient">
    <attribute name="registrationNumber"
    template="cus:recipient:recipient/@registrationNumber"/>
  </element>

</element>
```

La variable **Número de registro** ahora forma parte de los campos personalizados disponibles:

![chlimage_1-146](assets/chlimage_1-146.png)

#### Ocultar un campo personalizado {#hiding-a-personalization-field}

Para ocultar un campo de personalización entre los que ya están disponibles, debe ampliar Adobe Campaign **nms:seedMember** como se detalla en la sección [Adición de un campo personalizado](#adding-a-personalization-field) para obtener más información. Siga estos pasos:

1. Copie el campo que desea extraer de la variable **nms:seedMember** esquema en el esquema extendido (**cus:seedMember** por ejemplo).
1. Agregue la variable **advanced=&quot;true&quot;** Atributo XML al campo. Ya no aparece en la lista de campos personalizados disponibles en AEM.

   Por ejemplo, para ocultar la variable **Segundo nombre** , el campo **cud:seedMember** El esquema debe contener el siguiente elemento:

   ```xml
   <element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">
   
     <element name="custom_nms_recipient">
       <attribute advanced="true" name="middleName"/>
     </element>
   
   </element>
   ```

### Desactivación de un bloque personalizado {#deactivating-a-personalization-block}

Para desactivar un bloque personalizado entre los disponibles:

1. Vaya a la **Recursos** > **Campaign Management** > **Bloques personalizados** en la navegación de Adobe Campaign.
1. Seleccione el bloque personalizado que desea desactivar en AEM.
1. Borre la variable **Visible en los menús de personalización** y guarde los cambios. El bloque ya no aparece en la lista de bloques personalizados disponibles en Adobe Campaign.

   ![chlimage_1-147](assets/chlimage_1-147a.png)

### Administración de datos de extensión de destino {#managing-target-extension-data}

También puede insertar datos de extensión de destino para personalizarlos. Los datos de extensión de Target (también denominados &quot;datos de Target&quot;) proceden de enriquecer o añadir datos en una consulta en un flujo de trabajo de campaña, por ejemplo. Para obtener más información, consulte [Creación de consultas](https://docs.campaign.adobe.com/doc/AC/en/PTF_Creating_queries_About_queries_in_Campaign.html) y [Enriquecimiento de datos](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Enriching_data.html) secciones.

>[!NOTE]
Los datos del destino solo están disponibles si el contenido AEM se sincroniza con un envío de Adobe Campaign. Consulte [Sincronización del contenido creado en AEM con un envío de Adobe Campaign](/help/sites-authoring/campaign.md#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic).

![chlimage_1-148](assets/chlimage_1-148a.png)
