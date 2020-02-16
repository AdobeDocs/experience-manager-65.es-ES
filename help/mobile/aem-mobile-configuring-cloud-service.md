---
title: Configuración del servicio de nube de Adobe Target
seo-title: Configuración del servicio de nube de Adobe Target
description: Siga esta página para comprender cómo obtener el conjunto correcto de permisos para usuarios y grupos, crear servicios en la nube, configurar la aplicación para la actividad y finalmente generar el contenido.
seo-description: Siga esta página para comprender cómo obtener el conjunto correcto de permisos para usuarios y grupos, crear servicios en la nube, configurar la aplicación para la actividad y finalmente generar el contenido.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración del servicio de nube de Adobe Target {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento forma parte de la Guía de [introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md) , un punto de partida recomendado para la referencia de AEM Mobile.

Hay que realizar varios pasos para que los autores de contenido puedan empezar a generar contenido de destino para las aplicaciones móviles: Se obtiene el conjunto correcto de permisos para usuarios y grupos, se crean servicios en la nube, se configura la aplicación para la actividad y, finalmente, se genera el contenido.

A partir de ahora, se supone que la aplicación [de referencia híbrida de](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) AEM Mobile se ha implementado correctamente y se puede acceder a ella a través del panel de AEM Mobile.

## Permisos {#permissions}

Los usuarios que necesiten acceder a la consola de personalización deben formar parte del `target-activity-authors` grupo. Se sugiere que, como parte de la configuración de usuarios y grupos, el grupo de actividad de destino se agregue al grupo de administradores de aplicaciones. Al agregar el grupo target-activity-author, esto permitirá a los usuarios ver la entrada del menú de navegación Personalización.

Olvidar agregar los usuarios o grupos a los que desea tener acceso a la consola de administración de personalización al grupo target-activity-author impedirá que los usuarios vean la consola de personalización.

## Servicios de nube {#cloud-services}

Para que el contenido objetivo funcione en aplicaciones móviles, hay dos servicios que deben configurarse: El servicio Adobe Target y el servicio Adobe Mobile Services. El servicio Adobe Target proporciona el motor para procesar solicitudes de cliente y devolver el contenido personalizado. El servicio Adobe Mobile Services proporciona la conexión entre los servicios de Adobe y la aplicación móvil mediante el archivo ADBMobileConfig.json que consume el complemento AMS Cordova. Desde el panel de AEM Mobile, puede configurar la aplicación agregando los dos servicios.

## Servicio de nube de Adobe Target {#adobe-target-cloud-service}

En el panel de AEM Mobile, busque Administrar servicios de nube y haga clic en el botón +.

![chlimage_1-8](assets/chlimage_1-8.png)

En el Asistente para agregar servicios en la nube, seleccione la tarjeta de servicio en la nube &quot;Adobe Target&quot; y haga clic en Siguiente.

![chlimage_1-9](assets/chlimage_1-9.png)

En el menú desplegable Seleccionar una configuración puede crear una nueva configuración o seleccionar una existente. Para crear una nueva configuración, seleccione &quot;Crear configuración&quot; en el menú desplegable. Escriba un título para la configuración de Target. Introduzca el código de cliente, el correo electrónico y la contraseña asociados a su cuenta de Target. Si no conoce los valores de estos campos, póngase en contacto con la asistencia técnica de Adobe Target. Haga clic en el botón &quot;Verificar&quot; para validar las credenciales. Una vez verificado, haga clic en el botón Enviar para crear el servicio en la nube.

El servicio en la nube que se crea se asocia automáticamente con la aplicación móvil mediante el asistente. El valor de la propiedad cq:cloudserviceconfigs se establece en el nodo jcr:content del nodo del grupo de aplicaciones. Para el ejemplo de aplicación híbrida, se establece en /content/mobileapps/hybrid-reference-app/jcr:content con el valor que apunta al nodo de marco generado automáticamente ubicado en /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. El nodo de marco tiene dos propiedades definidas de forma predeterminada: sexo y edad. El marco solo se utiliza en la vista previa de AEM y no tiene ningún impacto en el dispositivo.

Tras completar el asistente, el mosaico Administrar servicio de nube contendrá el servicio de nube de Target, aunque contiene una advertencia sobre la falta de una cuenta de Adobe Mobile Service.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

También es necesario vincular una cuenta de Adobe Mobile Services (AMS) a la aplicación; el servicio AMS proporciona el archivo ADBMobileConfig.json necesario que contiene la información del código de cliente de Target. Antes de crear una asociación con la cuenta de AMS, la cuenta de AMS debe ser modificada por un usuario que tenga permisos para AMS.

### Código de cliente {#client-code}

Para iniciar sesión en los servicios de AMS, visite [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleccione la aplicación móvil y haga clic en la configuración. Busque el campo Opciones de SDK Target, coloque el código de cliente en el campo y haga clic en Guardar.

![chlimage_1-11](assets/chlimage_1-11.png)

Ahora que el código de cliente se ha asociado con la aplicación móvil, cuando el servicio en la nube de AMS se configura mediante el panel de Adobe Mobile, la configuración de la configuración del servicio se enviará mediante el archivo ADBMobileConfig.json.

### Adobe Mobile Service podría servir {#adobe-mobile-service-could-service}

Ahora que AMS se ha configurado, es hora de asociar la aplicación móvil en el panel de Adobe Mobile. En el panel de AEM Mobile, busque Administrar servicios de nube y haga clic en el botón +.

![chlimage_1-12](assets/chlimage_1-12.png)

Seleccione la tarjeta de Adobe Mobile Services y haga clic en Siguiente.

![chlimage_1-13](assets/chlimage_1-13.png)

En el paso Crear o seleccionar del asistente, seleccione la lista desplegable Servicio móvil y seleccione la entrada Crear configuración. Proporcione un título, empresa, nombre de usuario, contraseña y seleccione el centro de datos adecuado. Si no conoce estos valores, póngase en contacto con el administrador de Adobe Mobile Service para obtenerlos. Una vez completados todos los campos, haga clic en el botón Verificar. El proceso de verificación se dirige a AMS y verifica las credenciales de la cuenta. Una vez realizada la validación, se rellenará una lista de aplicaciones móviles donde se selecciona la aplicación móvil asociada en el menú desplegable. Haga clic en el botón Enviar para completar el asistente. El proceso puede tardar un poco en obtener los datos de configuración y los análisis asociados con la aplicación. Una vez completado el proceso, haga clic en el botón Finalizado del modal para volver al panel de Adobe Mobile.

Si vuelve al Mobile Dashboard, el mosaico Administrar servicios de nube contendrá el servicio de nube de AMS. También observará que el mosaico Analizar métricas se rellenará con informes del ciclo vital.

![chlimage_1-14](assets/chlimage_1-14.png)

## Controladores de sincronización de contenido de Target {#target-content-sync-handlers}

Para entregar contenido al contenido del dispositivo del usuario, se genera representando las ofertas creadas por los autores de contenido de AEM. Para gestionar el procesamiento de ofertas de destino, hay un nuevo controlador de sincronización de contenido que procesará las ofertas. Utilizando la Aplicación de referencia híbrida como ejemplo, el paquete de contenido en (inglés) contiene ContentSyncConfig con un controlador [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) . El siguiente paso es crucial para procesar ofertas en el dispositivo. El controlador mobileappoffers tiene una propiedad path que identifica la ruta a la actividad de personalización que se va a utilizar para la aplicación.

Por ejemplo, si hay una actividad ubicada en */content/campaign/hybridref* , copie esta ruta y péguela como valor en la propiedad *path* del controlador mobileappoffers.

Para la Aplicación de referencia híbrida hay dos controladores mobileappoffers: uno para el desarrollo y otro para las producciones.

Una vez configurada la ruta de actividades en la propiedad path del controlador mobileappoffers, guarde el controlador. El controlador estará listo para iniciar la representación de ofertas para nuestros dispositivos móviles.

### Modo de procesamiento {#render-mode}

El controlador mobileappoffers está configurado de forma diferente para la configuración de publicación y desarrollo. Para la configuración de publicación, hay una propiedad denominada *renderMode* con un valor de *publicación* establecido en el nodo cq:ContentSyncConfig. El controlador mobileappoffers hace referencia al parámetro rendoMode y, si se establece para publicación, modificará la ID de mbox que se crea. De forma predeterminada, los mboxes creados por AEM tienen un valor —author anexado a la ID de mbox. Esto identifica que la actividad no se ha publicado y debe utilizar la campaña sin publicar para las resoluciones de ofertas.

Cuando el contenido se organiza mediante el panel de Adobe Mobile, el contenido escalonado se considera contenido listo para la producción y se procesa mediante la configuración de sincronización de contenido que no es de desarrollo. Si se procesa de este modo, se eliminará —author de todos los identificadores de mbox y se espera que una actividad publicada esté disponible en el servidor de Target. Antes de probar el contenido de ensayo, asegúrese de que la actividad se ha publicado.

## Creación de contenido {#creating-content}

Ahora que se han creado los servicios en la nube y se ha configurado el controlador mobileappoffers, los autores de contenido pueden empezar a generar experiencias de objetivo.
