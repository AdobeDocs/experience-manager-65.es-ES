---
title: AEM Integración de 6.5 con Adobe Campaign Standard
description: AEM Obtenga información sobre cómo integrar la versión 6.5 de con Adobe Campaign Standard.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 0%

---


# AEM Integración de 6.5 con Adobe Campaign Standard {#integrating-with-adobe-campaign-standard}

AEM Al integrar la versión 6.5 de con Adobe Campaign Standard AEM (ACS), puede administrar la entrega de correo electrónico, el contenido y los formularios directamente en la interfaz de usuario de. Los pasos de configuración tanto en Adobe Campaign Standard AEM como en la son necesarios para habilitar la comunicación bidireccional entre las soluciones.

AEM Esta integración permite que la integración de los segmentos de datos y de Adobe Campaign Standard se utilice de forma independiente. Los especialistas en marketing pueden crear campañas y utilizar la segmentación en Adobe Campaign AEM, mientras que los creadores de contenido en paralelo pueden trabajar en el diseño de contenido en el área de la distribución de contenido de la aplicación de forma. AEM Gracias a esta integración, el contenido y el diseño de la campaña creada en la pueden segmentarse y enviarse desde Adobe Campaign.

>[!INFO]
>
>Este documento detalla cómo integrar Adobe Campaign Standard AEM con la versión 6.5 de. AEM Para otras integraciones de Campaign, consulte el documento [Integración de 6.5 con Adobe Campaign.](campaign.md)

## Pasos de integración {#integration-steps}

AEM La configuración de la integración entre y Adobe Campaign Standard requiere varios pasos en ambas soluciones.

1. [Configure las variables ](#aemserver-user)
1. [Compruebe el ](#resource-type-filter)
1. [AEM Creación de una plantilla de envíos de correo electrónico específica de un en Campaign](#aem-email-delivery-template)
1. [AEM Configuración de la integración de Campaign en la](#campaign-integration)
1. [AEM Configuración de la replicación en la instancia de Publish](#replication)
1. [AEM Configuración del externalizador de](#externalizer)
1. [Configure las variables ](#campaign-remote-user)
1. [AEM Configuración de la cuenta externa de en Campaign](#acc-external-user)

Este documento le guía en detalle por cada uno de estos pasos.

## Requisitos previos {#prerequisites}

* Acceso de administrador a Adobe Campaign Standard
   * Si necesita más detalles sobre cómo configurar Adobe Campaign Standard, consulte la [documentación de Adobe Campaign Standard.](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* AEM Acceso de administrador a la

## Configuración del usuario de aemserver en Campaign {#aemserver-user}

Adobe Campaign Standard AEM viene de manera predeterminada con un usuario `aemserver` que utiliza el usuario para conectarse a Adobe Campaign de manera predeterminada. Asigne un grupo de seguridad apropiado para este usuario y establezca su contraseña.

1. Inicie sesión en Adobe Campaign como administrador.

1. Haga clic en el logotipo de Adobe Campaign en la parte superior izquierda de la barra de menús para abrir la navegación global y, a continuación, seleccione **Administración** > **Usuarios y seguridad** > **Usuarios** en el menú de navegación.

1. Haga clic en el usuario `aemserver` en la consola de usuarios.

1. Asegúrese de que el usuario `aemserver` esté asignado como mínimo a un grupo de seguridad que tenga el rol `deliveryPrepare` asignado. De manera predeterminada, el grupo `Standard Users` tiene esta función.

   ![usuario aemserver en Adobe Campaign](assets/acs-aemserver-user.png)

1. Haga clic en **Guardar** para guardar los cambios.

AEM El usuario de `aemserver` tiene ahora los derechos necesarios para que pueda usarlo para comunicarse con Adobe Campaign.

AEM Sin embargo, para poder usar el usuario `aemserver`, se debe establecer su contraseña. Esto no se puede hacer a través de Adobe Campaign. Debe ser realizado por un ingeniero de soporte de Adobe. [Envíe un ticket al Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/?support-tab=home#support) para solicitar el restablecimiento de la contraseña de `aemserver`. Una vez que tenga la contraseña del Servicio de atención al cliente de Adobe, manténgala en una ubicación segura.

## Verificación de AEMResourceTypeFilter en Campaign {#resource-type-filter}

`AEMResourceTypeFilter` es una opción de Adobe Campaign AEM que se usa para filtrar los recursos de la que se pueden usar en Adobe Campaign. AEM Debido a que contiene mucho contenido, esta opción actúa como un filtro que permite a Adobe Campaign AEM recuperar únicamente el contenido de la de los tipos diseñados específicamente para utilizarse en Adobe Campaign.

Esta opción está preconfigurada. AEM Sin embargo, es posible que tenga que actualizarla si ha personalizado los componentes de Campaign de la. Para comprobar que la opción `AEMResourceTypeFilter` está configurada, siga estos pasos.

1. Inicie sesión en Adobe Campaign como administrador.

1. Haga clic en el logotipo de Adobe Campaign en la parte superior izquierda de la barra de menús para abrir la navegación global y, a continuación, seleccione **Administración** > **Configuración de la aplicación** > **Opciones** en el menú de navegación.

1. Haga clic en `AEMResourceTypeFilter` en la consola de opciones.

1. Confirme la configuración de `AEMResourceTypeFilter`. Las rutas están delimitadas por comas y contienen, de forma predeterminada:

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. Haga clic en **Guardar** para guardar los cambios.

AEM Su `AEMResourceTypeFilter` se ha configurado para recuperar el contenido correcto de los recursos de la red de trabajo de la red de.

## AEM Creación de una plantilla de envíos de correo electrónico específica de un en Campaign {#aem-email-delivery-template}

AEM De forma predeterminada, la opción no está activada en las plantillas de correo electrónico de Adobe Campaign. AEM Configure una nueva plantilla de envíos de correo electrónico que se pueda utilizar para crear correos electrónicos con contenido de la. AEM Para crear una plantilla de envíos de correo electrónico específica de la, siga estos pasos.

1. Inicie sesión en Adobe Campaign como administrador.

1. Haga clic en el logotipo de Adobe Campaign en la parte superior izquierda de la barra de menús para abrir la navegación global y, a continuación, seleccione **Recursos** > **Plantillas** > **Plantillas de envío** en el menú de navegación.

1. En la consola de plantillas de envío, busque la plantilla de correo electrónico predeterminada **Enviar por correo electrónico (correo electrónico)** y pase el ratón sobre la tarjeta (o línea) que lo representa para mostrar las opciones. Haga clic en **Duplicar elemento**.

   ![Elemento duplicado](assets/acs-copy-template.png)

1. En el cuadro de diálogo **Confirmación**, haga clic en **Confirmar** para duplicar la plantilla.

   ![Cuadro de diálogo de confirmación](assets/acs-confirmation.png)

1. El editor de plantillas se abre con su copia de la plantilla **Enviar por correo electrónico (correo)**. Haga clic en el icono **Editar propiedades** en la parte superior derecha de la ventana.

   ![Editor de plantillas](assets/acs-template-editor.png)

1. AEM En la ventana de propiedades, cambie el campo **Label** para que sea descriptivo de la nueva plantilla de.

1. Haga clic en el encabezado **Contenido** para expandirlo y seleccione **Adobe Experience Manager** en la lista desplegable **Origen del contenido**.

1. Esto muestra el campo **cuenta de Adobe Experience Manager**. Utilice la lista desplegable para seleccionar **Adobe Experience Manager instance (aemInstance)** usuario. AEM Este es el usuario externo predeterminado para la integración de.

![Configurar propiedades de la plantilla](assets/acs-template-properties.png)

1. Haga clic en **Confirmar** para guardar los cambios en las propiedades.

1. AEM En el editor de plantillas, haga clic en **Guardar** para guardar la copia modificada de la plantilla de correo electrónico y usarla con los recursos de correo electrónico de la plantilla de correo electrónico para su uso con los recursos de la plantilla de correo electrónico.

AEM Ahora tiene una plantilla de correo electrónico que puede utilizar contenido de.

## AEM Configuración de la integración de Campaign en la {#campaign-integration}

AEM Se comunica con Adobe Campaign mediante una integración integrada y con el usuario `aemserver` que configuró en Adobe Campaign. Siga estos pasos para configurar esta integración.

1. AEM Inicie sesión en la instancia de creación de la como administrador.

1. En el carril lateral de navegación global, seleccione **Herramientas** > **Cloud Service** > **Cloud Service heredados** > **Adobe Campaign** y luego haga clic en **Configurar ahora**.

   ![Configurar Adobe Campaign](assets/configure-campaign-service.png)

1. En el cuadro de diálogo, cree una configuración de servicio de Campaign escribiendo un **Título** y haciendo clic en **Crear**.

   ![Cuadro de diálogo Configurar campaña](assets/configure-campaign-dialog.png)

1. Se abre una nueva ventana y un cuadro de diálogo para editar la configuración. Proporcione la información necesaria.

   * **Nombre de usuario** - Este es [el usuario `aemserver` en Adobe Campaign que configuró en un paso anterior.](#aemserver-user) De manera predeterminada es `aemserver`.
   * **Contraseña**: esta es la contraseña de [el usuario `aemserver` de Adobe Campaign que solicitó al Servicio de atención al cliente de Adobe en un paso anterior.](#aemserver-user)
   * **Punto final de API**: Esta es la URL de la instancia de Adobe Campaign.

   ![Configuración de Adobe Campaign AEM en el](assets/configure-campaign.png)

1. Seleccione **Conectarse a Adobe Campaign** para comprobar la conexión y, a continuación, haga clic en **Aceptar**.

AEM Ahora se puede comunicar con Adobe Campaign.

>[!NOTE]
>
>Asegúrese de que el servidor de Adobe Campaign esté accesible a través de Internet. AEM No se puede acceder a redes privadas.

## AEM Configuración de la replicación en la instancia de Publish {#replication}

AEM El contenido de la campaña lo crean los autores de contenido en la instancia de creación de la. Esta instancia solo suele estar disponible internamente en su organización. Para que el contenido, como las imágenes y los recursos, sea accesible a los destinatarios de la campaña, debe publicarlo.

AEM El agente de replicación es responsable de publicar el contenido de la instancia de autor de la en la instancia de publicación y debe configurarse para que la integración funcione correctamente. Este paso también es necesario para replicar determinadas configuraciones de instancia de creación en la instancia de publicación.

AEM Para configurar la replicación desde la instancia de autor de la a la instancia de publicación:

1. AEM Inicie sesión en la instancia de creación de la como administrador.

1. En el carril lateral de navegación global, seleccione **Herramientas** > **Implementación** > **Replicación** > **Agentes en el autor** y, a continuación, haga clic en **Agente predeterminado (publicar)**.

   ![Configurar agente de replicación](assets/acc-replication-config.png)

1. Haz clic en **Editar** y luego selecciona la pestaña **Transporte**.

1. AEM Configure el campo **URI** reemplazando el valor `localhost` predeterminado por la dirección IP de la instancia de publicación de la.

   ![Pestaña Transporte](assets/acc-transport-tab.png)

1. Haga clic en **Aceptar** para guardar los cambios en la configuración del agente.

AEM Ha configurado la replicación en la instancia de publicación de la para que los destinatarios de la campaña puedan acceder al contenido.

>[!NOTE]
>
>Si no desea utilizar la URL de replicación, sino utilizar la URL pública, puede establecer la URL pública en la siguiente configuración mediante OSGi
>
>AEM En el carril lateral de navegación global, seleccione **Herramientas** > **Operaciones** > **Consola web** > **Configuración de OSGi** y busque **Integración de Campaign - Configuración**. Edite la configuración y cambie el campo **URL pública** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## AEM Configuración del externalizador de {#externalizer}

AEM AEM [El externalizador](/help/sites-developing/externalizer.md) es un servicio OSGi en el que se transforma una ruta de recursos en una dirección URL externa y absoluta, lo cual es necesario para que los usuarios puedan usar el contenido de servicio que puede usar Campaign en el servicio de. Configúrela para que la integración de Campaign funcione.

1. AEM Inicie sesión en la instancia de creación de la como administrador.
1. En el carril lateral de navegación global, seleccione **Herramientas** > **Operaciones** > **Consola web** > **Configuración de OSGi** y busque **Externalizador de vínculos CQ por día**.
1. De manera predeterminada, la última entrada del campo **Dominios** está destinada a la instancia de publicación. Cambie la URL del valor predeterminado `http://localhost:4503` a la instancia de publicación disponible públicamente.

   ![Configuración del externalizador](assets/acc-externalizer-config.png)

1. Haga clic en **Guardar**.

Ha configurado el externalizador y Adobe Campaign puede acceder a su contenido.

>[!NOTE]
>
Se debe poder acceder a la instancia de publicación desde el servidor de Adobe Campaign. Si señala a `localhost:4503` u otro servidor al que Adobe Campaign no puede llegar, las imágenes de no aparecerán en la consola de Adobe Campaign, de lo contrario, no aparecerán en la pantalla de las imágenes de la consola de AEM.

## AEM Configuración del usuario remoto de la campaña en la interfaz de usuario de {#campaign-remote-user}

Del mismo modo que necesita un usuario en Adobe Campaign que pueda utilizar para comunicarse con Adobe Campaign, Adobe Campaign AEM AEM también necesita un usuario en la comunicación con el que se pueda establecer la comunicación con los usuarios de AEM, que también puede usar para comunicarse con los usuarios de. AEM De forma predeterminada, la integración de Campaign crea el usuario `campaign-remote` en la interfaz de usuario de. Siga estos pasos para configurar este usuario.

1. AEM Inicie sesión en el servicio de administración de.
1. En la consola de navegación principal, haga clic en **Herramientas** en el carril izquierdo.
1. A continuación, haga clic en **Seguridad** > **Usuarios** para abrir la consola de administración de usuarios.
1. Busque el usuario `campaign-remote`.
1. Seleccione el usuario `campaign-remote` y haga clic en **Propiedades** para editar el usuario.
1. En la ventana **Editar configuración de usuario**, haga clic en **Cambiar contraseña**.
1. Proporcione una nueva contraseña para el usuario y anote la contraseña en una ubicación segura para uso futuro.
1. Haga clic en **Guardar** para guardar el cambio de contraseña.
1. Haga clic en **Guardar y cerrar** para guardar los cambios del usuario `campaign-remote`.

## AEM Configuración de la cuenta externa de en Campaign {#acc-external-user}

AEM AEM Cuando [creó una plantilla de envíos de correo electrónico específica de la,](#aem-email-delivery-template) especificó que la plantilla debería usar la cuenta externa `aemInstance` para comunicarse con los usuarios de correo electrónico de la cuenta de correo electrónico de la cuenta de correo electrónico de la cuenta de correo electrónico de la cuenta de correo electrónico de la cuenta de correo electrónico de la cuenta de correo electrónico de {}. Para habilitar la comunicación bidireccional entre ambas soluciones, debe configurar esta cuenta en Adobe Campaign.

1. Inicie sesión en Adobe Campaign como administrador.

1. Haga clic en el logotipo de Adobe Campaign en la parte superior izquierda de la barra de menús para abrir la navegación global y, a continuación, seleccione **Administración** > **Configuración de la aplicación** > **Cuentas externas** en el menú de navegación.

1. Haga clic en el usuario **Adobe Experience Manager instance (aemInstance)** de la consola de usuarios.

1. Asegúrese de que el usuario tiene **Adobe Experience Manager** como **Tipo**.

1. En la sección **Conexión**, defina los siguientes campos:

   1. AEM Servidor: es la dirección URL del servidor de creación de. Esto no debe terminar en una barra oblicua.
   1. AEM Cuenta: Este es el usuario `campaign-remote` en el que [se configuró anteriormente en la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de ](#campaign-remote-user), que se configuró anteriormente en la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario de la cuenta de usuario .
   1. AEM Contraseña: Esta es la contraseña del `campaign-remote`usuario que [configuró anteriormente en el usuario de la cuenta de usuario de ](#campaign-remote-user).

   ![Editando el usuario de aemInstance](assets/acs-external-acount-editor.png)

1. Asegúrese de que la casilla de verificación **Habilitado** esté seleccionada y luego haga clic en **Guardar** para guardar los cambios.

Enhorabuena. AEM ¡Ha completado la integración entre y Adobe Campaign Standard!

## Siguientes pasos {#next-steps}

La integración ya se ha completado tanto con Adobe Campaign Classic AEM como con la configuración de la.

Ahora puede aprender a crear una newsletter en Adobe Experience Manager si continúa con [este documento.](/help/sites-authoring/campaign.md)
