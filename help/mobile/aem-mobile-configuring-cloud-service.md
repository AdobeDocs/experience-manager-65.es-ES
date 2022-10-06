---
title: Configuración del Cloud Service de Adobe Target
seo-title: Configuring Adobe Target Cloud Service
description: Siga esta página para comprender cómo obtener el conjunto correcto de permisos para usuarios y grupos, crear servicios en la nube, configurar la aplicación para la actividad y finalmente generar el contenido.
seo-description: Follow this page to understand how to get right set of permissions for users and groups, creating cloud services, configuring the application for the activity, and finally generating the content.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 0%

---

# Configuración del Cloud Service de Adobe Target {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento forma parte del [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guía, punto de partida recomendado para la referencia de AEM Mobile.

Hay que realizar varios pasos para que los autores de contenido puedan empezar a generar contenido de destino para aplicaciones móviles: Se obtiene el conjunto correcto de permisos para usuarios y grupos, se crean servicios en la nube, se configura la aplicación para la actividad y, finalmente, se genera el contenido.

El supuesto a partir de ahora es que [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) se ha implementado correctamente y se puede acceder a él mediante el panel de AEM Mobile.

## Permisos {#permissions}

Los usuarios que necesitan acceso a la consola de personalización deben formar parte del `target-activity-authors` grupo. Se sugiere que, como parte de la configuración de usuarios y grupos, el grupo target-activity se añada al grupo apps-admins . Al agregar el grupo target-activity-authors , esto permitirá a los usuarios ver la entrada del menú de navegación de personalización .

Olvidar agregar los usuarios o grupos a los que desea tener acceso a Admin Console de personalización al grupo target-activity-authors impedirá que los usuarios vean la consola de personalización.

## Cloud Services {#cloud-services}

Para que el contenido de destino funcione en aplicaciones móviles, hay dos servicios que deben configurarse: El servicio de Adobe Target y el servicio de Adobe Mobile Services. El servicio Adobe Target proporciona el motor para procesar las solicitudes de los clientes y devolver el contenido personalizado. El servicio Adobe Mobile Services proporciona la conexión entre los servicios de Adobe y la aplicación móvil a través del archivo ADBMobileConfig.json que consume el complemento AMS Cordova. Desde el panel de AEM Mobile, puede configurar la aplicación agregando los dos servicios.

## Cloud Service de Adobe Target {#adobe-target-cloud-service}

En el panel de AEM Mobile, busque Administrar Cloud Services y haga clic en el botón + .

![Chlimage_1-8](assets/chlimage_1-8.png)

En el asistente Agregar Cloud Service, seleccione la tarjeta de servicio en la nube &quot;Adobe Target&quot; y haga clic en Siguiente.

![Chlimage_1-9](assets/chlimage_1-9.png)

En la lista desplegable Seleccionar una configuración puede crear una configuración nueva o seleccionar una existente. Para crear una nueva configuración, seleccione &quot;Crear configuración&quot; en la lista desplegable. Introduzca un título para la configuración de Target. Introduzca el código de cliente, el correo electrónico y la contraseña asociados a su cuenta de Target. Si no conoce los valores de estos campos, póngase en contacto con el servicio de asistencia técnica de Adobe Target. Haga clic en el botón &quot;Verificar&quot; para validar las credenciales. Una vez verificado, haga clic en el botón Submit para crear el servicio en la nube.

El servicio de nube que se crea se asocia automáticamente con la aplicación móvil mediante el asistente. El valor de la propiedad cq:cloudserviceconfigs se establece en el nodo jcr:content del nodo del grupo de aplicaciones. Para el ejemplo de aplicación híbrida, se establece en /content/mobileapps/hybrid-reference-app/jcr:content con el valor que señala al nodo de marco generado automáticamente ubicado en /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. El nodo del marco tiene dos propiedades definidas de forma predeterminada, sexo y edad. El marco solo se utiliza en la vista previa AEM y no tiene ningún impacto en el dispositivo.

Después de completar el asistente, el mosaico Administrar Cloud Service contendrá el servicio en la nube de Target, pero contiene una advertencia sobre la falta de una cuenta de Adobe Mobile Service.

![imagen_1-10](assets/chlimage_1-10.png)

## Servicio móvil de Adobe {#adobe-mobile-service}

Es necesario vincular una cuenta de Adobe Mobile Services (AMS) a la aplicación, el servicio AMS proporciona el archivo ADBMobileConfig.json necesario que contiene la información del código de cliente de Target. Antes de crear una asociación con la cuenta de AMS, la cuenta de AMS debe modificarla un usuario que tenga permisos para AMS.

### Código de cliente {#client-code}

Para iniciar sesión en los servicios de AMS, visite [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleccione la aplicación móvil y haga clic en la configuración . Busque el campo Opciones de SDK Target , coloque el código de cliente en el campo y haga clic en Guardar .

![imagen_1-11](assets/chlimage_1-11.png)

Ahora que el código de cliente se ha asociado con la aplicación móvil, cuando el servicio en la nube de AMS se configura mediante el panel móvil de Adobe, la configuración del servicio se enviará mediante el archivo ADBMobileConfig.json .

### Servicio móvil de Adobe podría funcionar {#adobe-mobile-service-could-service}

Ahora que se ha configurado AMS, es hora de asociar la aplicación móvil en el panel de control de Adobe Mobile. En el panel de AEM Mobile, busque Administrar Cloud Services y haga clic en el botón + .

![imagen_1-12](assets/chlimage_1-12.png)

Seleccione la tarjeta Adobe Mobile Services y haga clic en Siguiente.

![imagen_1-13](assets/chlimage_1-13.png)

En el paso Crear o Seleccionar asistente , seleccione la lista desplegable Servicio móvil y seleccione la entrada Crear configuración . Proporcione un título, empresa, nombre de usuario, contraseña y seleccione el centro de datos adecuado. Si no conoce estos valores, póngase en contacto con el administrador de Adobe Mobile Services para obtenerlos. Una vez rellenados todos los campos, haga clic en el botón Verify . El proceso de verificación va a AMS y verifica las credenciales de la cuenta. Una vez realizada la validación, se rellenará una lista de aplicaciones móviles donde se seleccionará la aplicación móvil asociada en la lista desplegable. Haga clic en el botón Enviar para completar el asistente. El proceso puede tardar un poco en obtener los datos de configuración y cualquier análisis asociado con la aplicación. Una vez completado el proceso, haga clic en el botón Listo del modal para volver al panel móvil de Adobe.

Si vuelve al panel móvil, el mosaico Administrar Cloud Services contendrá el servicio en la nube de AMS. También tendrá en cuenta que el mosaico Analizar métricas se rellenará con informes de ciclo vital.

![imagen_1-14](assets/chlimage_1-14.png)

## Gestores de sincronización de contenido de Target {#target-content-sync-handlers}

Para entregar contenido al contenido del dispositivo del usuario, se genera procesando las ofertas que crean los autores de contenido de AEM. Para gestionar la renderización de ofertas de destino, hay un nuevo controlador de sincronización de contenido que procesará las ofertas. Si utilizamos la aplicación de referencia híbrida como ejemplo, el paquete de contenido en (inglés) contiene ContentSyncConfig con un [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) controlador. El siguiente paso es crucial para procesar ofertas en el dispositivo. El controlador mobileappoffers tiene una propiedad path que identifica la ruta a la actividad de personalización que se va a utilizar para la aplicación.

Por ejemplo, si hay una actividad que se encuentra en */content/campaign/hybridref* copie esta ruta y péguela como valor en la variable *ruta* propiedad del controlador mobileappoffers.

Para la aplicación de referencia híbrida hay dos controladores de mobileappoffers: uno para el desarrollo y otro para las producciones.

Una vez que la ruta de las actividades se ha establecido en la propiedad ruta del controlador mobileappoffers, guarde el controlador. El controlador ya estará listo para iniciar el procesamiento de ofertas para nuestros dispositivos móviles.

### Modo de procesamiento {#render-mode}

El controlador mobileappoffers está configurado de forma diferente para las configuraciones de publicación y desarrollo. Para la configuración de publicación hay una propiedad llamada *renderMode* con un valor de *publicar* se establece en el nodo cq:ContentSyncConfig . El controlador mobileappoffers hace referencia al renderMode y, si se configura para publicar, modifica el id de mbox que se crea. De forma predeterminada, los mboxes creados por AEM tienen un valor —author anexado al id del mbox. Esto identifica que la actividad no se ha publicado y debe utilizar la campaña no publicada para las resoluciones de oferta.

Cuando el contenido se configura mediante el panel de Adobe móvil, el contenido preparado se considera contenido listo para la producción y se procesa mediante la configuración de sincronización de contenido que no es de desarrollo. Si se procesa de este modo, se eliminará —author de todos los id de mbox y se espera que una actividad publicada esté disponible en el servidor de Target. Antes de probar el contenido preparado, asegúrese de que la actividad se haya publicado.

## Creación de contenido {#creating-content}

Ahora que se han creado los servicios de nube y se ha configurado el controlador mobileappoffers, los autores de contenido ahora pueden empezar a generar experiencias segmentadas.
