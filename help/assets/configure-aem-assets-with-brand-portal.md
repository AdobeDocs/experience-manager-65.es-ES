---
title: Configuración de AEM Assets con Brand Portal
seo-title: Configuración de AEM Assets con Brand Portal
description: Obtenga información sobre cómo configurar Recursos AEM con Brand Portal para publicar recursos y colecciones en Brand Portal.
seo-description: Obtenga información sobre cómo configurar Recursos AEM con Brand Portal para publicar recursos y colecciones en Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: bdb26ba817e0599f811d7f4e131ec6ab356a4785

---


# Configuración de AEM Assets con Brand Portal {#configure-integration-65}

Los recursos de Adobe Experience Manager (AEM) se configuran con Brand Portal a través de Adobe I/O, que proporciona un distintivo IMS para la autorización del inquilino de Brand Portal.

>[!NOTE]
>
>La configuración de AEM Assets con Brand Portal mediante Adobe I/O es compatible con AEM 6.5.4.0 y versiones posteriores.
>
>Anteriormente, Brand Portal se configuraba en la IU clásica mediante OAuth Gateway heredado, que utiliza el intercambio de tokens JWT para obtener un Token de acceso IMS para la autorización.
>
>La configuración mediante OAuth heredado ya no se admite a partir del 6 de abril de 2020 y se cambia a la configuración mediante Adobe I/O.


>[!TIP]
>
>***Solo para clientes existentes***
>
>Se recomienda seguir utilizando la configuración heredada de OAuth Gateway. En caso de que surjan problemas con la configuración heredada de OAuth Gateway, elimine la configuración existente y cree una nueva configuración mediante Adobe I/O.



Esta ayuda describe los dos casos de uso siguientes:
* [Nueva configuración](#configure-new-integration-65): Si es un usuario nuevo de Brand Portal y desea configurar su instancia de autor de AEM Assets con Brand Portal, puede crear una nueva configuración en Adobe I/O.
* [Configuración](#upgrade-integration-65)de actualización: Si ya es usuario de Brand Portal y su instancia de autor de Recursos AEM está configurada con Brand Portal en OAuth Gateway heredado, se recomienda eliminar las configuraciones existentes y crear una nueva configuración en Adobe I/O.

La información proporcionada se basa en el supuesto de que cualquiera que lea esta Ayuda está familiarizado con las siguientes tecnologías:

* Instalación, configuración y administración de paquetes de Adobe Experience Manager y AEM

* Uso de sistemas operativos Linux y Microsoft Windows

## Requisitos previos {#prerequisites}

Para configurar Recursos AEM con Brand Portal, es necesario lo siguiente:

* Una instancia de creación de Recursos AEM activa y en ejecución con el último Service Pack.
* URL del inquilino de Brand Portal.
* Un usuario con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal.


[Descargar e instalar AEM 6.5](#aemquickstart)

[Descargar e instalar el último Service Pack de AEM](#servicepack)

### Descargar e instalar AEM 6.5 {#aemquickstart}

Se recomienda disponer de AEM 6.5 para configurar una instancia de creación de AEM. Si AEM no está en funcionamiento, descárguelo de las siguientes ubicaciones:

* Si ya es cliente de AEM, descargue AEM 6.5 del sitio web [de licencias de](http://licensing.adobe.com)Adobe.

* Si es un socio de Adobe, utilice [Adobe Partner Training Programa](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) para solicitar AEM 6.5.

Después de descargar AEM, para obtener instrucciones sobre cómo configurar una instancia de autor de AEM, consulte [Implementación y mantenimiento](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall).

### Descargar e instalar AEM Service Pack más reciente {#servicepack}

Para obtener instrucciones detalladas, consulte

* [Notas de la versión de Service Pack de AEM 6.5](https://helpx.adobe.com/experience-manager/6-5/release-notes/sp-release-notes.html)

**Póngase en contacto con la asistencia** si no puede encontrar el paquete de AEM o el Service Pack más recientes.

## Create configuration {#configure-new-integration-65}

Realice los siguientes pasos en la secuencia mostrada si va a configurar Recursos AEM con Brand Portal por primera vez:
1. [Obtener certificado público](#public-certificate)
1. [Creación de la integración de Adobe I/O](#createnewintegration)
1. [Crear configuración de cuenta IMS](#create-ims-account-configuration)
1. [Configurar servicio de nube](#configure-the-cloud-service)
1. [Configuración de prueba](#test-integration)

### Crear configuración de IMS {#create-ims-configuration}

La configuración de IMS autentica el inquilino de Brand Portal con la instancia de creación de AEM Assets.

La configuración de IMS incluye dos pasos:

* [Obtener certificado público](#public-certificate)
* [Crear configuración de cuenta IMS](#create-ims-account-configuration)

### Obtener certificado público {#public-certificate}

El certificado público le permite autenticar su perfil en Adobe I/O.

1. Inicie sesión en la instancia de creación de AEM AssetsDirección URL predeterminada: http:// localhost:4502/aem/start.html
1. En el panel **Herramientas** ![Herramientas](assets/tools.png) , vaya a **[!UICONTROL Seguridad]** >> Configuraciones de **[!UICONTROL Adobe IMS]**.

   ![Interfaz de usuario de configuración de cuenta de Adobe IMS](assets/ims-config1.png)

1. Se abre la página Configuraciones de IMS de Adobe.

   Haga clic en **[!UICONTROL Crear]**.

   Esto le llevará a la página de configuración **[!UICONTROL de la cuenta técnica de]** Adobe IMS.

1. De forma predeterminada, se abre la ficha **Certificado** .

   En **Cloud Solution**, seleccione **[!UICONTROL Adobe Brand Portal]**.

1. Marque la casilla de verificación **[!UICONTROL Crear nuevo certificado]** y especifique un **alias** para el certificado. El alias sirve como nombre del cuadro de diálogo.

1. Haga clic en **[!UICONTROL Crear certificado]**. Aparece un cuadro de diálogo. Haga clic en **[!UICONTROL Aceptar]** para generar el certificado público.

   ![Crear certificado](assets/ims-config2.png)

1. Haga clic en **[!UICONTROL Descargar clave]** pública y guarde el archivo de certificado *AEM-Adobe-IMS.crt* en el equipo. El archivo de certificado se utiliza para [crear la integración](#createnewintegration)de Adobe I/O.

   ![Descargar certificado](assets/ims-config3.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   En la ficha **Cuenta** , cree la cuenta de Adobe IMS, pero para ello necesitará los detalles de integración. Mantenga esta página abierta por ahora.

   Abra una pestaña nueva y [cree la integración](#createnewintegration) de Adobe I/O para obtener los detalles de integración de las configuraciones de cuenta de IMS.

### Creación de la integración de Adobe I/O {#createnewintegration}

La integración de Adobe I/O genera la clave de API, el secreto del cliente y la carga útil (JWT), que es necesaria para configurar las configuraciones de cuenta de IMS.

1. Inicie sesión en la consola de Adobe I/O con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal.

   Dirección URL predeterminada: [https://console.adobe.io/](https://console.adobe.io/)

1. Haga clic en **[!UICONTROL Crear integración]**.

1. Seleccione **[!UICONTROL Acceso a una API]** y haga clic en **[!UICONTROL Continuar]**.

   ![Crear nueva integración](assets/create-new-integration1.png)

1. Se abre una nueva página de integración.

   Seleccione su organización en la lista desplegable.

   En **[!UICONTROL Experience Cloud]**, seleccione **[!UICONTROL AEM Brand Portal]** y haga clic en **[!UICONTROL Continuar]**.

   Si la opción de Brand Portal está deshabilitada para usted, asegúrese de que ha seleccionado la organización correcta en el cuadro desplegable situado encima de la opción Servicios **[!UICONTROL de]** Adobe. Si no conoce su organización, póngase en contacto con su administrador.

   ![Crear integración](assets/create-new-integration2.png)

1. Especifique un nombre y una descripción para la integración. Haga clic en **[!UICONTROL Seleccionar un archivo del equipo]** y cargue el `AEM-Adobe-IMS.crt` archivo descargado en la sección [Obtener certificados](#public-certificate) públicos.

1. Seleccione el perfil de su organización.

   O bien, seleccione el portal **[!UICONTROL de marca perfil]** Assets y haga clic en **[!UICONTROL Crear integración]**. Se crea la integración.

1. Haga clic en **[!UICONTROL Continuar para ver los detalles]** de la integración y vista de la información de integración.

   Copiar la clave de **[!UICONTROL API]**

   Haga clic en **[!UICONTROL Recuperar secreto]** de cliente y copie la clave Secreto de cliente.

   ![Clave de API, Secreto de cliente e información de carga útil de una integración](assets/create-new-integration3.png)

1. Vaya a la ficha **[!UICONTROL JWT]** y copie la carga útil **[!UICONTROL JWT]**.

   La clave de API, la clave secreta del cliente y la información de carga útil de JWT se utilizarán para crear la configuración de la cuenta de IMS.

### Crear configuración de cuenta IMS {#create-ims-account-configuration}

Asegúrese de que ha realizado los siguientes pasos:

* [Obtener certificado público](#public-certificate)
* [Creación de la integración de Adobe I/O](#createnewintegration)

**Pasos para crear la configuración de cuenta de IMS:**

1. Abra la página Configuración de IMS, ficha **[!UICONTROL Cuentas]** . La página se ha mantenido abierta al final de la sección, [Obtención de un certificado](#public-certificate)público.

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En **[!UICONTROL Servidor]** de autorización, introduzca la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Pegue la clave de API, el secreto del cliente y la carga útil JWT que ha copiado al final de [Crear integración](#createnewintegration)de Adobe I/O.

   Haga clic en **[!UICONTROL Crear]**.

   Se crea la integración.

   ![Configuración de cuenta de IMS](assets/create-new-integration6.png)


1. Seleccione la configuración de IMS y haga clic en **[!UICONTROL Comprobar estado]**. Aparecerá un cuadro de diálogo.

   Haga clic en **[!UICONTROL Comprobar]**. Cuando la conexión se ha realizado correctamente, aparece el mensaje *Token recuperado correctamente* .

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Cree sólo una configuración IMS válida. No cree varias configuraciones de IMS.
>
> Asegúrese de que la configuración esté correcta. En caso de que la configuración no esté en buen estado, elimínela y cree una nueva configuración en buen estado.


### Configurar servicio de nube {#configure-the-cloud-service}

Siga estos pasos para crear la configuración del servicio en la nube de Brand Portal:

1. Inicie sesión en la instancia de creación de Recursos AEM

   Dirección URL predeterminada: http:// localhost:4502/aem/start.html
1. En el panel **Herramientas** ![Herramientas](assets/tools.png) , vaya a Servicios de **[!UICONTROL nube >> AEM Brand Portal]**.

   Se abre la página Configuraciones de Brand Portal.

1. Haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que ha creado en el paso, [cree la configuración](#create-ims-account-configuration)de la cuenta de IMS.

   En la URL **** del servicio, introduzca la URL del inquilino de Brand Portal.

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. Se crea la configuración de nube. La instancia de creación de Recursos AEM ahora está integrada con el inquilino de Brand Portal.

### Test configuration {#test-integration}

1. Inicie sesión en la instancia de creación de Recursos AEM

   Dirección URL predeterminada: http:// localhost:4502/aem/start.html

1. En el panel **Herramientas** ![Herramientas](assets/tools.png) , vaya a **[!UICONTROL Implementación >> Replicación]**.

   ![](assets/test-integration1.png)

1. Se abre la página Replicación.

   Haga clic en **[!UICONTROL Agentes en el autor]**.

   ![](assets/test-integration2.png)

1. Se crean cuatro agentes de replicación para cada inquilino.

   Busque los agentes de replicación del inquilino de Brand Portal.

   Haga clic en la dirección URL del agente de replicación.

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >Los agentes de replicación trabajan en paralelo y comparten la distribución del trabajo por igual, aumentando así la velocidad de publicación en cuatro veces la velocidad original. Una vez configurado el servicio en la nube, no se requiere una configuración adicional para habilitar los agentes de replicación activados de forma predeterminada para habilitar la publicación en paralelo de varios recursos.

   >[!NOTE]
   >
   >Evite desactivar cualquiera de los agentes de replicación, ya que puede provocar errores en la replicación de algunos de los recursos.


1. Para comprobar la conexión entre el autor de Recursos AEM y Brand Portal, haga clic en **[!UICONTROL Probar conexión]**.

   ![](assets/test-integration4.png)

1. Observe la parte inferior de los resultados de la prueba para verificar que la replicación se realizó correctamente.

   ![](assets/test-integration5.png)

   >[!NOTE]
   >
   >Los agentes de replicación trabajan en paralelo y comparten la distribución del trabajo por igual, aumentando así la velocidad de publicación en cuatro veces la velocidad original. Una vez configurado el servicio en la nube, no se requiere una configuración adicional para habilitar los agentes de replicación activados de forma predeterminada para habilitar la publicación en paralelo de varios recursos.

1. Compruebe los resultados de la prueba en los cuatro agentes de replicación uno por uno.


   >[!NOTE]
   >
   >Evite desactivar cualquiera de los agentes de replicación, ya que puede provocar errores en la replicación de algunos de los recursos.

Brand Portal se ha configurado correctamente con la instancia de creación de AEM Assets. Ahora puede:

* [Publicación de recursos de AEM Assets en Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publicación de carpetas de AEM Assets en Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publicación de colecciones de AEM Assets en Brand Portal](../assets/brand-portal-publish-collection.md)
* [Configure Asset Sourcing](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) para que los usuarios de Brand Portal puedan contribuir y publicar recursos en Recursos AEM.

## Configuración de actualización {#upgrade-integration-65}

Realice los siguientes pasos en la secuencia indicada para actualizar las configuraciones existentes:
1. [Verificar trabajos en ejecución](#verify-jobs)
1. [Eliminar configuraciones existentes](#delete-existing-configuration)
1. [Crear configuración](#configure-new-integration-65)

### Verificar trabajos en ejecución {#verify-jobs}

Asegúrese de que no se esté ejecutando ningún trabajo de publicación en la instancia de creación de Recursos AEM antes de realizar ninguna modificación. Para ello, puede verificar los cuatro agentes de replicación y asegurarse de que la cola sea ideal o esté vacía.

1. Inicie sesión en la instancia de creación de Recursos AEM

   Dirección URL predeterminada: http:// localhost:4502/aem/start.html

1. En el panel **Herramientas** ![Herramientas](assets/tools.png) , vaya a **[!UICONTROL Implementación >> Replicación]**.

1. Se abre la página Replicación.

   Haga clic en **[!UICONTROL Agentes en el autor]**.

   ![](assets/test-integration2.png)

1. Busque los agentes de replicación del inquilino de Brand Portal.

   Asegúrese de que la **cola esté inactiva** para todos los agentes de replicación y de que no haya ningún trabajo de publicación activo.

   ![](assets/test-integration3.png)

### Eliminar configuraciones existentes {#delete-existing-configuration}

Debe ejecutar la siguiente lista de comprobación mientras elimina las configuraciones existentes.
* Eliminar los cuatro agentes de replicación
* Eliminar servicio de nube
* Eliminar usuario de MAC

1. Inicie sesión en la instancia de creación de Recursos AEM y abra CRX Lite como administrador.

   Dirección URL predeterminada: http:// localhost:4502/crx/de/index.jsp

1. Navegue hasta los cuatro agentes de replicación del inquilino de Brand Portal `/etc/replications/agents.author` y elimínelos.

   ![](assets/delete-replication-agent.png)

1. Vaya a `/etc/cloudservices/mediaportal` y elimine la configuración **del servicio de** nube.

   ![](assets/delete-cloud-service.png)

1. Navegue hasta `/home/users/mac` y elimine el usuario **** MAC del inquilino de Brand Portal.

   ![](assets/delete-mac-user.png)


Ahora puede [crear la configuración](#configure-new-integration-65) en la instancia de creación de AEM 6.5 en Adobe I/O.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

Después de que la replicación se realice correctamente, puede publicar recursos, carpetas y colecciones en Brand Portal. Para obtener más información, consulte:

* [Publicación de recursos en Brand Portal](/help/assets/brand-portal-publish-assets.md)
* [Publicar carpetas en Brand Portal](/help/assets/brand-portal-publish-folder.md)
* [Publicar colecciones en Brand Portal](/help/assets/brand-portal-publish-collection.md)
