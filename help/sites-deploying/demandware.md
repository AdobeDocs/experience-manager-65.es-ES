---
title: Salesforce Commerce Cloud
seo-title: Salesforce Commerce Cloud / Demandware
description: Descubra cómo implementar el comercio electrónico con Salesforce Commerce Cloud/Demandware.
seo-description: Descubra cómo implementar el comercio electrónico con Salesforce Commerce Cloud/Demandware.
uuid: c0270632-bdd2-4dba-bbbe-312757ea20f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 52cc3162-b638-410d-854a-383399e2effb
docset: aem65
pagetitle: Deploying eCommerce with Demandware
redirecttarget: https //github.com/adobe/commerce-salesforce
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Salesforce Commerce Cloud{#salesforce-commerce-cloud}

La implementación de los paquetes de comercio electrónico necesarios proporcionará toda la funcionalidad del marco de comercio electrónico, junto con una implementación de referencia de la funcionalidad de comercio electrónico, tal como se proporciona con una implementación de Salesforce Commerce Cloud/Demandware (incluido un catálogo de demostración).

## Paquetes necesarios para el comercio electrónico con Salesforce Commerce Cloud {#packages-needed-for-ecommerce-with-salesforce-commerce-cloud}

Para instalar la funcionalidad de comercio electrónico necesita:

* Marco de comercio electrónico de AEM:

   * esto forma parte de una instalación estándar de AEM

* Paquete de contenido de AEM Demandware Commerce

   * cq-6.4.0-featurepack-10262

>[!NOTE]
>
>Esta integración admite instancias de Salesforce Commerce Cloud/Demandware configuradas para utilizar OCAPI versión 17.6 o posterior.

### Instalación de comercio electrónico con Salesforce Commerce Cloud {#installation-of-ecommerce-with-salesforce-commerce-cloud}

Para instalar AEM con una configuración de integración de Demandware Commerce (mediante el catálogo de demostración, Geometrixx Outdoors), los pasos básicos son:

1. [Instale AEM](/help/sites-deploying/deploy.md).
1. Instale el paquete de contenido mediante el administrador de [paquetes](/help/sites-administering/package-manager.md):
1. [Cree](/help/sites-authoring/page-authoring.md) cualquier página adicional que necesite en AEM.

>[!NOTE]
>
>Para descargar los paquetes, vaya a Uso compartido de [paquetes](/help/sites-administering/package-manager.md#package-share).

Es necesario configurar la conexión del servidor entre AEM y el Simulador para pruebas de Demandware. La mayor parte de la configuración ya está preconfigurada para funcionar con el paquete de contenido de demostración de SiteGenisis proporcionado mediante rutas, bibliotecas predeterminadas, etc. Si el conector se utiliza con otros sitios y bibliotecas, deberá actualizar esta configuración.

1. Vaya a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Haga clic en **Demandware Client**.
1. Introduzca el nombre de host o el ip del extremo de **instancia** según sea necesario.

   ![climage_1-5](assets/chlimage_1-5.png)

1. Haga clic en **Guardar**.
1. Haga clic en **Demandware TransportHandler Plugin for WebDAV**.
1. Establezca el usuario **** WebDAV y la contraseña **de usuario de** WebDAV.

   ![climage_1-6](assets/chlimage_1-6.png)

1. Haga clic en **Guardar**.

#### Replicación {#replication}

La replicación debe habilitarse después de la instalación del paquete, puede verificar que: [https://localhost:4502/etc/replication/agents.author/demandware.html](https://localhost:4502/etc/replication/agents.author/demandware.html)

>[!NOTE]
>
>El agente de replicación está configurado en el nivel de registro de información de forma predeterminada. Si desea obtener más información, puede cambiar el nivel de registro para depurar.

#### OAuth {#oauth}

El cliente OAuth está configurado para funcionar con una instancia de simulador de pruebas de Demandware. Para realizar pruebas, no es necesario realizar ningún cambio.

Para los sistemas de ensayo y producción, los clientes de OAuth deben configurarse con el ID de cliente y la contraseña adecuados.

1. Vaya a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. Haga clic en **Demandware Access Token provider**.

   ![climage_1-7](assets/chlimage_1-7.png)

1. Modifique los valores según sea necesario y haga clic en **Guardar**.

### Simulador para pruebas de Salesforce Commerce Cloud {#salesforce-commerce-cloud-sandbox}

El Simulador para pruebas de Demandware debe configurarse para ejecutar el nuevo motor de plantillas Velocity.

>[!NOTE]
>
>El siguiente asistente no forma parte del conector de AEM Demandware. Se proporciona como parte del paquete de contenido de demostración para ayudarle a configurar rápidamente las páginas de demostración de SiteGenesis.

1. Vaya a [https://localhost:4502/etc/demandware/init.html](https://localhost:4502/etc/demandware/init.html).
1. Haga clic en **Editar.**
1. Compruebe los valores y haga clic en **Aceptar**.
1. Haga clic en **Inicializar**.
1. Vaya a la carpeta WebDAV y busque los archivos de plantilla publicados, por ejemplo en `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Dynamic/SiteGenesis`.

   >[!NOTE]
   >
   >La extensión será `.vs`.

1. Compruebe también si hay archivos JS y CSS exportados, por ejemplo en `adobe01-tech-prtnr-na01-dw.demandware.net/on/demandware.servlet/webdav/Sites/Libraries/SiteGenesisSharedLibrary`.

