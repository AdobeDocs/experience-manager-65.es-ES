---
title: Integración con Adobe Campaign Standard
seo-title: Integración con Adobe Campaign Standard
description: Integración con Adobe Campaign Standard.
seo-description: Integración con Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
translation-type: tm+mt
source-git-commit: f951c195c581f770dcc87fdf4a89d40ee6dd9ec0
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---


# Integración con Adobe Campaign Standard{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>En esta documentación se describe cómo integrar AEM con Adobe Campaign Standard, la solución basada en suscripciones. Si está utilizando Adobe Campaign 6.1, consulte [Integración con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) para estas instrucciones.

Adobe Campaign le permite administrar el contenido y los formularios de envío de correo electrónico directamente en Adobe Experience Manager.

Para utilizar ambas soluciones al mismo tiempo, primero debe configurarlas para conectarse entre sí. Esto implica pasos de configuración tanto en Adobe Campaign como en Adobe Experience Manager. Estos pasos se describen en detalle en este documento.

El trabajo con Adobe Campaign en AEM incluye la posibilidad de enviar correos electrónicos y formularios por Adobe Campaign y se describe en [Trabajo con Adobe Campaign](/help/sites-authoring/campaign.md).

Además, los siguientes temas pueden ser de interés al integrar AEM con [Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html):

* [Prácticas recomendadas para plantillas de correo electrónico](/help/sites-administering/best-practices-for-email-templates.md)
* [Solución de problemas con la integración de Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md)

Si está ampliando la integración con Adobe Campaign, es posible que desee ver las páginas siguientes:

* [Creación de extensiones personalizadas](/help/sites-developing/extending-campaign-extensions.md)
* [Creación de asignaciones de formularios personalizados](/help/sites-developing/extending-campaign-form-mapping.md)

## Configuración del Adobe Campaign {#configuring-adobe-campaign}

La configuración del Adobe Campaign implica lo siguiente:

1. Configuración del usuario de **aemserver** .
1. Creación de una cuenta externa dedicada.
1. Verificación de la opción AEMResourceTypeFilter.
1. Creación de una Plantilla de envíos dedicada.

>[!NOTE]
>
>Para realizar estas operaciones, debe tener la función de **administración** en Adobe Campaign.

### Requisitos previos {#prerequisites}

Asegúrese de que tiene los siguientes elementos de antemano:

* [Una instancia de creación de AEM](/help/sites-deploying/deploy.md#getting-started)
* [Una instancia de publicación de AEM](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Una instancia de Adobe Campaign](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>Las operaciones detalladas en las secciones [Configuración de Adobe Campaign](#configuring-adobe-campaign) y [Configuración de Adobe Experience Manager](#configuring-adobe-experience-manager) son necesarias para que las funcionalidades de integración entre AEM y Adobe Campaign funcionen correctamente.

### Configuración del usuario de aemserver {#configuring-the-aemserver-user}

El usuario de **aemserver** debe configurarse en Adobe Campaign. El **aemserver** es un usuario técnico que se utilizará para conectar el servidor AEM a Adobe Campaign.

Vaya a **Administración** > **Usuarios y seguridad** > **Usuarios** y seleccione el usuario de **aemserver** . Haga clic en él para abrir la configuración del usuario.

* Debe establecer una contraseña para este usuario. Esto no se puede realizar a través de la interfaz de usuario. Esta configuración debe realizarla en REST un administrador técnico.
* Puede asignar funciones específicas a este usuario, como **deliveryPrepare**, que permite al usuario crear y editar envíos.

### Configuración de una cuenta externa de Adobe Experience Manager {#configuring-an-adobe-experience-manager-external-account}

Debe configurar una cuenta externa que le permita conectar Adobe Campaign a su instancia de AEM.

>[!NOTE]
>
>En AEM, asegúrese de definir la contraseña para el usuario remoto de la campaña. Debe definir esta contraseña para conectar Adobe Campaign con AEM. Inicie sesión como administrador y, en la consola de administración de usuarios, busque el usuario remoto de campañas y haga clic en **Establecer contraseña**.

Para configurar una cuenta externa de AEM:

1. Vaya a **Administración** > Ajustes **** de aplicación > **Cuentas externas**.

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. Seleccione la cuenta externa **aemInstance** predeterminada o cree una nueva haciendo clic en el botón **Crear** .
1. Seleccione **Adobe Experience** Manager en el campo **Tipo** e introduzca los parámetros de acceso utilizados para la instancia de creación de AEM: dirección del servidor, nombre de cuenta y contraseña.

   >[!NOTE]
   >
   >Asegúrese de no agregar una barra **** o barra final al final de la dirección URL o de que la conexión no funcionará.

1. Asegúrese de que la casilla de verificación **Habilitado** está seleccionada y, a continuación, haga clic en **Guardar** para guardar las modificaciones.

### Verificación de la opción AEMResourceTypeFilter {#verifying-the-aemresourcetypefilter-option}

La opción **AEMResourceTypeFilter** se utiliza para filtrar los tipos de recursos de AEM que se pueden usar en Adobe Campaign. Esto permite a Adobe Campaign recuperar contenido de AEM que se ha diseñado específicamente para utilizarse solo en Adobe Campaign.

Esta opción viene preconfigurada; sin embargo, si cambia esta opción, puede provocar que la integración no funcione.

Para verificar que la opción **AEMResourceTypeFilter** está configurada:

1. Vaya a **Administración** > Ajustes **** de aplicación > **Opciones**.
1. En la lista, puede asegurarse de que se muestra la opción **AEMResourceTypeFilter** y de que las rutas son correctas.

### Creación de una Plantilla de envíos de correo electrónico específica de AEM {#creating-an-aem-specific-email-delivery-template}

De forma predeterminada, la función AEM no está activada en las plantillas de correo electrónico de Adobe Campaign. Puede configurar una nueva Plantilla de envíos de correo electrónico que se utilizará para crear correos electrónicos con contenido de AEM.

Para crear una Plantilla de envíos de correo electrónico específica de AEM:

1. Vaya a **Recursos** > **Plantillas** > **Plantillas de envíos**.
1. **Para activar la selección** , haga clic en la marca de verificación de la barra de acciones y seleccione la plantilla predeterminada existente de correo electrónico **estándar (correo)** . A continuación, haga clic en el icono **Copiar** y haga clic en **Confirmar** para obtener el duplicado.
1. Para desactivar el modo de selección, haga clic en la **x** y abra la plantilla recién creada **Copiar de correo electrónico estándar (correo)** y, a continuación, seleccione **Editar propiedades** en la barra de acciones del panel de plantillas.

   Puede modificar la **etiqueta** de la plantilla.

1. En la sección **Contenido** de las propiedades, cambie la fuente **** Contenido a **Adobe Experience Manager**. A continuación, seleccione la cuenta externa que se creó anteriormente y haga clic en **Confirmar**.

   Para guardar las modificaciones, haga clic en **Confirmar** y en **Guardar.**

   Los envíos de correo electrónico creados a partir de esta plantilla tendrán habilitada la función de contenido de AEM.

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## Configuring Adobe Experience Manager {#configuring-adobe-experience-manager}

Para configurar AEM, debe hacer lo siguiente:

* Configure la replicación entre instancias.
* Conecte AEM a Adobe Campaign.
* Configure el externalizador.

### Configuración de la replicación entre instancias de AEM {#configuring-replication-between-aem-instances}

El contenido creado a partir de la instancia de creación de AEM se envía primero a la instancia de publicación. A continuación, esta instancia de publicación transfiere el contenido a Adobe Campaign. Por lo tanto, el agente de replicación debe configurarse para replicarse desde la instancia de creación de AEM a la instancia de publicación de AEM.

>[!NOTE]
>
>Si no desea utilizar la URL de replicación, sino la URL pública, puede establecer la URL **** pública en la siguiente configuración en OSGi (**Herramientas** > Consola **** web > Configuración de **OSGi > Integración de Campaña de AEM - Configuración**):
**Dirección URL pública:** com.day.cq.mcm.campaña.impl.IntegrationConfigImpl#aem.mcm.campaña.publicUrl

Este paso también es necesario para replicar determinadas configuraciones de instancias de creación en la instancia de publicación.

Para configurar la replicación entre instancias de AEM:

1. En la instancia de creación, seleccione Logotipo **de** AEM > **Herramientas** > **Implementación** > **Replicación** > **Agentes en el autor****** y, a continuación, haga clic en Agente predeterminado.

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   Evite utilizar localhost (es decir, una copia local de AEM) al configurar la integración con Adobe Campaign, a menos que la instancia de publicación y de autor se encuentre en el mismo equipo.

1. Haga clic en **Editar** y, a continuación, seleccione la ficha **Transporte** .
1. Configure el URI reemplazando **localhost** por la dirección IP o la dirección de la instancia de publicación de AEM.

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### Conexión de AEM a Adobe Campaign {#connecting-aem-to-adobe-campaign}

Antes de poder usar AEM y Adobe Campaign juntos, debe establecer el vínculo entre ambas soluciones para que puedan comunicarse.

1. Conéctese a la instancia de creación de AEM.
1. Seleccione **Herramientas** > **Operaciones** > **Nube** > **Cloud Services** y, a continuación, **Configurar ahora** en la sección Adobe Campaign.

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. Cree una nueva configuración introduciendo un **Título** y haga clic en **Crear**, o elija la configuración existente que desee vincular con la instancia de Adobe Campaign.
1. Edite la configuración para que coincida con los parámetros de la instancia de Adobe Campaign.

   * **Nombre de usuario**: **aemserver**, el operador de paquete de integración AEM de Adobe Campaign que se utiliza para establecer el vínculo entre las dos soluciones.
   * **Contraseña**: Contraseña de operador de aemserver de Adobe Campaign. Es posible que tenga que volver a especificar la contraseña de este operador directamente en Adobe Campaign.
   * **Punto** final de API: URL de instancia de Adobe Campaign.

1. Seleccione **Conectar a Adobe Campaign** y haga clic en **Aceptar**.

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   Después de [crear el correo electrónico y publicarlo](/help/sites-authoring/campaign.md), debe volver a publicar la configuración en la instancia de publicación.

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
Si la conexión falla, asegúrese de comprobar lo siguiente:
* Puede encontrar un problema de certificado al usar una conexión segura con una instancia de Adobe Campaign (https). Deberá agregar el certificado de instancia de Adobe Campaign al archivo **cacerts **de su JDK.
* Además, consulte [Solución de problemas de la integración](/help/sites-administering/troubleshooting-campaignintegration.md)de AEM/Adobe Campaign.



### Configuración del externalizador {#configuring-the-externalizer}

Debe [configurar el externalizador](/help/sites-developing/externalizer.md) en AEM en la instancia de creación. Externalizador es un servicio OSGi que permite transformar una ruta de recursos en una dirección URL externa y absoluta. Este servicio proporciona un lugar central para configurar esas direcciones URL externas y generarlas.

Consulte [Configurar el externalizador](/help/sites-developing/externalizer.md) para obtener instrucciones generales. Para la integración de Adobe Campaign, asegúrese de configurar el servidor de publicación `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` no en un punto `localhost:4503` sino en un servidor al que se pueda acceder desde la consola de Adobe Campaign.

Si apunta a `localhost:4503` u otro servidor al que Adobe Campaign no puede acceder, las imágenes no aparecerán en la consola de Adobe Campaign.

![chlimage_1-131](assets/chlimage_1-131a.png)

