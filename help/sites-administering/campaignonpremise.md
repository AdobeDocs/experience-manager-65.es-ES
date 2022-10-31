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
source-git-commit: 4712f57808ae769646b00d1098648686815121b6
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 1%

---


# Integración con Adobe Campaign Classic {#integrating-campaign-classic}

Al integrar AEM con Adobe Campaign, puede administrar la entrega de correo electrónico, el contenido y los formularios directamente en AEM. Se necesitan pasos de configuración tanto en Adobe Campaign Classic como en AEM para habilitar la comunicación bidireccional entre soluciones.

Esta integración permite utilizar AEM y Adobe Campaign Classic de forma independiente. Los especialistas en marketing pueden crear campañas y utilizar la segmentación en Adobe Campaign, mientras que los creadores de contenido en paralelo pueden trabajar en el diseño de contenido en AEM. Con la integración, el contenido y el diseño de la campaña creada en AEM pueden ser dirigidos y entregados por Adobe Campaign.

## Pasos de la integración {#integration-steps}

La integración entre AEM y Campaign requiere una serie de pasos en ambas soluciones.

1. [Instale el paquete de integración de AEM en Campaign.](#install-package)
1. [Creación de un operador para AEM en Campaign](#create-operator)
1. [Configuración de la integración de Campaign en AEM](#campaign-integration)
1. [Configuración del AEM externalizador](#externalizer)
1. [Configure el usuario remoto de la campaña en AEM](#configure-user)
1. [Configuración de la cuenta externa AEM en Campaign](#acc-setup)

Este documento le guía por cada uno de estos pasos en detalle.

## Requisitos previos {#prerequisites}

* Acceso de administrador a Adobe Campaign Classic
   * Para realizar la integración, necesita una instancia de Adobe Campaign Classic en funcionamiento, incluida una base de datos configurada.
   * Si necesita más información sobre cómo configurar y configurar Adobe Campaign Classic, consulte la [documentación de Adobe Campaign Classic,](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html) especialmente la guía de instalación y configuración.
* Acceso de administrador a AEM

## Instalación del paquete de integración de AEM en Campaign {#install-package}

La variable **Integración AEM** en Adobe Campaign incluye una serie de configuraciones estándar necesarias para conectarse a AEM.

1. Como administrador, inicie sesión en la instancia de Adobe Campaign mediante la consola del cliente.

1. Select **Herramientas** > **Avanzadas** > **Importar paquete...**.

   ![Importar paquete](assets/import-package.png)

1. Haga clic en **Instalación de un paquete estándar** y haga clic en **Siguiente**.

1. Marque la **Integración AEM** paquete.

   ![Instalación de un paquete estándar](assets/select-package.png)

1. Haga clic en **Siguiente** y luego **Inicio** para iniciar la instalación.

   ![Progreso de instalación](assets/installation.png)

1. Haga clic en **Cerrar** cuando se complete la instalación.

El paquete de integración ya está instalado.

## Creación del operador para AEM en Campaign {#create-operator}

El paquete de integración crea automáticamente el `aemserver` operador que AEM utiliza para conectarse a Adobe Campaign. Debe definir una zona de seguridad para este operador y establecer su contraseña.

1. Inicie sesión en Adobe Campaign como administrador mediante la consola del cliente.

1. Select **Herramientas** -> **Explorer** en la barra de menús.

1. En el explorador, vaya a la **Administración** > **Gestión de acceso** > **Operadores** nodo .

1. Seleccione el `aemserver` operador.

1. En el **Editar** del operador, seleccione **Derechos de acceso** y, a continuación, haga clic en la pestaña **Editar los parámetros de acceso...** vínculo.

   ![Establecer zona de seguridad](assets/access-rights.png)

1. Seleccione la zona de seguridad adecuada y defina la máscara IP de confianza según sea necesario.

1. Haga clic en **Guardar**.

1. Cierre la sesión del cliente de Adobe Campaign.

1. En el sistema de archivos del servidor de Adobe Campaign, vaya a la ubicación de instalación de Campaign y edite el `serverConf.xml` como administrador. Este archivo generalmente se encuentra en:
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf` en Windows.
   * `/usr/local/neolane/nl6/conf/eng` en Linux.

1. Buscar `securityZone` y asegúrese de que los siguientes parámetros están establecidos para la zona de seguridad del operador AEM.

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`.

1. Guarde el archivo.

1. Asegúrese de que la zona de seguridad no se sobrescriba con la configuración correspondiente en la variable `config-<server name>.xml` archivo.

   * Si el archivo de configuración contiene una configuración de zona de seguridad independiente, cambie la variable `allowUserPassword` atributo a `true`.

1. Si desea cambiar el puerto del servidor de Adobe Campaign Classic, sustituya `8080` con el puerto deseado.

   >[!CAUTION]
   >
   >De forma predeterminada, no hay ninguna zona de seguridad configurada para el operador. Para que AEM se conecte a Adobe Campaign, debe seleccionar una zona como se detalla en los pasos anteriores.
   >
   >Adobe recomienda encarecidamente crear una zona de seguridad dedicada a AEM para evitar problemas de seguridad. Para obtener más información, consulte la [Documentación de Adobe Campaign Classic.](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html)

1. En el cliente de Campaign, vuelva a la `aemserver` y seleccione **General** pestaña .

1. Haga clic en el **Restablecer contraseña...** vínculo.

1. Especifique una contraseña y guárdela en una ubicación segura para uso futuro.

1. Haga clic en **OK** para guardar la contraseña de `aemserver` operador.

## Configuración de la integración de Campaign en AEM {#campaign-integration}

AEM usa [el operador que ya ha configurado en Campaign](#create-operator) para comunicarse con Campaign

1. Inicie sesión en la instancia de creación de AEM como administrador.

1. En el carril lateral de navegación global, seleccione **Herramientas** > **Cloud Services** > **Cloud Services heredados** > **Adobe Campaign** y haga clic en **Configurar ahora**.

   ![Configuración de Adobe Campaign](assets/configure-campaign-service.png)

1. En el cuadro de diálogo, cree una configuración de servicio de Campaign introduciendo una **Título** y haga clic en **Crear**.

   ![Cuadro de diálogo Configurar campaña](assets/configure-campaign-dialog.png)

1. Se abre una nueva ventana y un cuadro de diálogo para editar la configuración. Proporcione la información necesaria.

   * **Nombre de usuario** - Esto es [el operador de paquete Adobe Campaign AEM Integration creado en el paso anterior.](#create-operator) De forma predeterminada, es `aemserver`.
   * **Contraseña** - Esta es la contraseña de [el operador de paquete Adobe Campaign AEM Integration creado en el paso anterior.](#create-operator)
   * **Punto final de API** : Esta es la URL de instancia de Adobe Campaign.

   ![Configuración de Adobe Campaign en AEM](assets/configure-campaign.png)

1. Select **Conectarse a Adobe Campaign** para verificar la conexión y, a continuación, haga clic en **OK**.

AEM ahora puede comunicarse con Adobe Campaign.

>[!NOTE]
>
>Asegúrese de que el servidor de Adobe Campaign esté disponible a través de Internet. AEM puede acceder a redes privadas.

## Configurar la replicación en la instancia de publicación de AEM {#replication}

El contenido de la campaña lo crean los autores de contenido en la instancia de creación de AEM. Esta instancia solo suele estar disponible internamente en su organización. Para que los destinatarios de la campaña puedan acceder a contenido como imágenes y recursos, debe publicar ese contenido.

El agente de replicación es responsable de publicar el contenido desde la instancia de autor de AEM a la instancia de publicación y debe configurarse para que la integración funcione correctamente. Este paso también es necesario para replicar ciertas configuraciones de instancia de creación en la instancia de publicación.

Para configurar la replicación de la instancia de autor de AEM a la instancia de publicación:

1. Inicie sesión en la instancia de creación de AEM como administrador.

1. En el carril lateral de navegación global, seleccione **Herramientas** > **Implementación** > **Replicación** > **Agentes en autor** y, a continuación, toque o haga clic en **Agente predeterminado (publicar)**.

   ![Configurar el agente de replicación](assets/acc-replication-config.png)

1. Toque o haga clic **Editar** a continuación, seleccione la **Transporte** pestaña .

1. Configure las variables **URI** reemplazando el valor predeterminado `localhost` con la dirección IP de la instancia de publicación de AEM.

   ![Ficha Transporte](assets/acc-transport-tab.png)

1. Toque o haga clic **OK** para guardar los cambios en la configuración del agente.

Ha configurado la replicación en la instancia de publicación de AEM para que los destinatarios de la campaña puedan acceder al contenido.

>[!NOTE]
>
>Si no desea utilizar la URL de replicación, sino utilizar la URL de cara al público, puede establecer la URL pública en la siguiente configuración a través de OSGi
>
>En el carril lateral de navegación global, seleccione **Herramientas** > **Operaciones** > **Consola web** > **Configuración de OSGi** y busque **Integración de AEM Campaign: Configuración**. Editar la configuración y cambiar el campo **URL pública** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## Configuración del AEM externalizador {#externalizer}

[El externalizador](/help/sites-developing/externalizer.md) es un servicio OSGi en AEM que transforma una ruta de recurso en una URL externa y absoluta, que es necesario para que AEM el contenido que Campaign puede utilizar. Debe configurarlo para que funcione la integración de Campaign.

1. Inicie sesión en la instancia de creación de AEM como administrador.
1. En el carril lateral de navegación global, seleccione **Herramientas** > **Operaciones** > **Consola web** > **Configuración de OSGi** y busque **Externalizador de vínculos de CQ de día**.
1. De forma predeterminada, la última entrada de la variable **Dominios** está diseñado para la instancia de publicación. Cambiar la dirección URL de la predeterminada `http://localhost:4503` a su instancia de publicación disponible públicamente.

   ![Configuración del externalizador](assets/acc-externalizer-config.png)

1. Haga clic o pulse **Guardar**.

Ha configurado el externalizador y Adobe Campaign ahora puede acceder al contenido.

>[!NOTE]
Se debe poder acceder a la instancia de publicación desde el servidor de Adobe Campaign. Si señala a `localhost:4503` Para otro servidor al que Adobe Campaign no pueda acceder, las imágenes de AEM no aparecerán en la consola de Adobe Campaign.

## Configuración del usuario remoto de la campaña en AEM {#configure-user}

Para que Campaign se comunique con AEM, debe establecer una contraseña para la variable `campaign-remote` usuario en AEM.

1. Inicie sesión en AEM como administrador.
1. En la consola de navegación principal, haga clic en **Herramientas** en el carril izquierdo.
1. A continuación, haga clic en **Seguridad** -> **Usuarios** para abrir la consola de administración de usuarios.
1. Busque la variable `campaign-remote` usuario.
1. Seleccione el `campaign-remote` usuario y haga clic en **Propiedades** para editar el usuario.
1. En el **Editar configuración de usuario** ventana, haga clic en **Cambiar contraseña**.
1. Proporcione una nueva contraseña para el usuario y anote la contraseña en una ubicación segura para uso futuro.
1. Haga clic en **Guardar** para guardar el cambio de contraseña.
1. Haga clic en **Guardar y cerrar** para guardar los cambios en la variable `campaign-remote` usuario.

## Configuración de la cuenta externa de AEM en Campaign {#acc-setup}

When [instalación del **Integración AEM** paquete en Campaign,](#install-package) se crea una cuenta externa para AEM. Al configurar esta cuenta externa, Adobe Campaign puede conectarse a AEM, lo que permite una comunicación bidireccional entre las soluciones.

1. Inicie sesión en Adobe Campaign como administrador mediante la consola del cliente.

1. Select **Herramientas** -> **Explorer** en la barra de menús.

1. En el explorador, vaya a la **Administración** > **Plataforma** > **Cuentas externas** nodo .

   ![Cuentas externas](assets/external-accounts.png)

1. Busque la cuenta de AEM externa. De forma predeterminada, tiene los valores siguientes:

   * **Tipo** - `AEM`
   * **Etiqueta** - `AEM Instance`
   * **Nombre interno** - `aemInstance`

1. En el **General** de esta cuenta, introduzca la información de usuario que definió en la [Establecer la contraseña de usuario remota de la campaña](#set-campaign-remote-password) paso a paso.

   * **Servidor** - La dirección del servidor de autor de AEM
      * Se debe poder acceder al servidor de creación de AEM desde la instancia de servidor de Adobe Campaign Classic.
      * Asegúrese de que la dirección del servidor **not** termine con una barra diagonal.
   * **Cuenta** - De forma predeterminada, esta es la variable `campaign-remote` que haya establecido en AEM en la [Establecer la contraseña de usuario remota de la campaña](#set-campaign-remote-password) paso a paso.
   * **Contraseña** - Esta contraseña es la misma que la `campaign-remote` que haya establecido en AEM en la [Establecer la contraseña de usuario remota de la campaña](#set-campaign-remote-password) paso a paso.

1. Seleccione el **Habilitado** casilla de verificación.

1. Haga clic en **Guardar**.

Adobe Campaign ahora puede comunicarse con AEM.

## Pasos siguientes {#next-steps}

Con Adobe Campaign Classic y AEM configurados, la integración ya se ha completado.

Ahora puede aprender a crear una newsletter en Adobe Experience Manager continuando con [este documento.](/help/sites-authoring/campaign.md)
