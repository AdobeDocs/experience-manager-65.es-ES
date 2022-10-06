---
title: Personalización de contenido de AEM Mobile
seo-title: AEM Mobile content personalization
description: Siga esta página para obtener más información sobre la función de personalización de contenido de AEM Mobile que permite a los autores de AEM personalizar el contenido de las aplicaciones móviles mediante Adobe Target.
seo-description: Follow this page to learn about AEM Mobile content personalization feature that allows AEM authors to personalize mobile app content by leveraging Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 0%

---

# Personalización de contenido de AEM Mobile{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento forma parte del [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guía, punto de partida recomendado para la referencia de AEM Mobile.

La función de personalización de contenido de AEM Mobile permite [Autores de AEM](#author) para personalizar el contenido de las aplicaciones móviles mediante [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). Esto permite la entrega de ofertas de destino a usuarios de aplicaciones móviles. Adobe Experience Manager Mobile ofrece la capacidad de crear, dirigir y entregar contenido que proporcionará al usuario contenido específico para sus propios gustos individuales.

Como suele suceder en AEM, para que los autores empiecen a crear este contenido, los administradores y desarrolladores deben preparar primero el entorno.

[AEM administradores](#administrator) para establecer una conexión entre AEM Mobile y el Cloud Service de Adobe Target.

Mientras tanto, AEM Mobile [desarrolladores](#developer) es necesario modificar las secuencias de comandos existentes para facilitar la creación de contenido dirigido.

## Para administradores {#for-administrators}

Hay que realizar varios pasos para que los autores de contenido puedan empezar a generar contenido de destino para aplicaciones móviles: Se obtiene el conjunto correcto de permisos para usuarios y grupos, se crean servicios en la nube, se configura la aplicación para la actividad y, finalmente, se genera el contenido.

Este artículo le guiará a través del proceso utilizado para configurar la variable [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) para la segmentación.

En adelante, se supone que la aplicación de referencia híbrida de AEM Mobile se ha implementado correctamente y se puede acceder a ella a través del panel de AEM Mobile.

Para que los autores puedan generar contenido de destino en una aplicación, la instancia de AEM debe ser [configurado con el Cloud Service de Adobe Target.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Permisos {#permissions}

Los usuarios que necesitan acceso a la consola de personalización deben formar parte del `target-activity-authors` grupo.

Se sugiere que, como parte de la configuración de usuarios y grupos, el grupo target-activity se añada al grupo apps-admins . Al agregar el grupo target-activity-authors , esto permitirá a los usuarios ver la entrada del menú de navegación de personalización .

>[!NOTE]
>
>Olvidar agregar los usuarios o grupos a los que desea tener acceso a Admin Console de personalización al grupo target-activity-authors impedirá que los usuarios vean la consola de personalización.

### Cloud Services {#cloud-services}

Para que el contenido de destino funcione en aplicaciones móviles, hay dos servicios que deben configurarse: El servicio de Adobe Target y el servicio de Adobe Mobile Services. El servicio Adobe Target proporciona el motor para procesar las solicitudes de los clientes y devolver el contenido personalizado. El servicio Adobe Mobile Services proporciona la conexión entre los servicios de Adobe y la aplicación móvil a través del archivo ADBMobileConfig.json que consume el complemento AMS Cordova. Desde el panel de AEM Mobile, puede configurar la aplicación agregando los dos servicios.

En el panel de AEM Mobile, busque Administrar Cloud Services y haga clic en el botón + .

![chlimage_1-38](assets/chlimage_1-38.png)

En el asistente Agregar Cloud Service, seleccione la tarjeta de servicio en la nube &quot;Adobe Target&quot; y haga clic en Siguiente.

![chlimage_1-39](assets/chlimage_1-39.png)

En el menú desplegable Seleccionar una configuración puede crear una configuración nueva o seleccionar una existente. Para crear una nueva configuración, seleccione &quot;Crear configuración&quot; en la lista desplegable. Introduzca un título para la configuración de Target. Introduzca el código de cliente, el correo electrónico y la contraseña asociados a su cuenta de Target. Si no conoce los valores de estos campos, póngase en contacto con el servicio de asistencia técnica de Adobe Target. Haga clic en el botón &quot;Verificar&quot; para validar las credenciales. Una vez verificado, haga clic en el botón Submit para crear el servicio en la nube.

>[!NOTE]
>
>El servicio de nube que se crea se asocia automáticamente con la aplicación móvil mediante el asistente. El valor de la propiedad cq:cloudserviceconfigs se establece en el nodo jcr:content del nodo del grupo de aplicaciones. Para el ejemplo de aplicación híbrida, se establece en /content/mobileapps/hybrid-reference-app/jcr:content con el valor que señala al nodo de marco generado automáticamente ubicado en /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. El nodo del marco tiene dos propiedades definidas de forma predeterminada, sexo y edad. El marco solo se utiliza en la vista previa AEM y no tiene ningún impacto en el dispositivo.

Después de completar el asistente, el mosaico Administrar Cloud Service contendrá el servicio en la nube de Target, pero contiene una advertencia sobre la falta de una cuenta de Adobe Mobile Service.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

Es necesario vincular una cuenta de Adobe Mobile Services (AMS) a la aplicación, el servicio AMS proporciona el archivo ADBMobileConfig.json necesario que contiene la información del código de cliente de Target. Antes de crear una asociación con la cuenta de AMS, la cuenta de AMS debe modificarla un usuario que tenga permisos para AMS.

### Código de cliente {#client-code}

Para iniciar sesión en los servicios de AMS, visite [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleccione la aplicación móvil y haga clic en la configuración . Busque el campo Opciones de SDK Target , coloque el código de cliente en el campo y haga clic en Guardar .

![imagen_1-41](assets/chlimage_1-41.png)

Ahora que el código de cliente se ha asociado con la aplicación móvil, cuando el servicio en la nube de AMS se configura mediante el panel móvil de Adobe, la configuración del servicio se enviará mediante el archivo ADBMobileConfig.json .

### Cloud Service de servicios móviles de Adobe {#adobe-mobile-service-cloud-service}

Ahora que se ha configurado AMS, es hora de asociar la aplicación móvil en el panel de control de Adobe Mobile. En el panel de AEM Mobile, busque Administrar Cloud Services y haga clic en el botón + .

![imagen_1-42](assets/chlimage_1-42.png)

Seleccione la tarjeta Adobe Mobile Services y haga clic en Siguiente.

![imagen_1-43](assets/chlimage_1-43.png)

En el paso Crear o Seleccionar asistente , seleccione la lista desplegable Servicio móvil y seleccione la entrada Crear configuración . Proporcione un título, empresa, nombre de usuario, contraseña y seleccione el centro de datos adecuado. Si no conoce estos valores, póngase en contacto con el administrador de Adobe Mobile Services para obtenerlos. Una vez rellenados todos los campos, haga clic en el botón Verify . El proceso de verificación va a AMS y verifica las credenciales de la cuenta. Una vez realizada la validación, se rellenará una lista de aplicaciones móviles donde se seleccionará la aplicación móvil asociada en la lista desplegable. Haga clic en el botón Enviar para completar el asistente. El proceso puede tardar un poco en obtener los datos de configuración y cualquier análisis asociado con la aplicación. Una vez completado el proceso, haga clic en el botón Listo del modal para volver al panel móvil de Adobe.

Si vuelve al panel móvil, el mosaico Administrar Cloud Services contendrá el servicio en la nube de AMS. También tendrá en cuenta que el mosaico Analizar métricas se rellenará con informes de ciclo vital.

![imagen_1-44](assets/chlimage_1-44.png)

## Para autores {#for-authors}

**Requisito previo:** Como se ha mencionado anteriormente, los administradores deben configurar la conexión con el servicio de Adobe Target antes de que los autores puedan generar nuevo contenido de destino.

Una vez que el administrador ha configurado los dos servicios de nube y el desarrollador ha configurado el controlador de mobileappoffers, los autores de contenido ahora pueden empezar a generar experiencias segmentadas.

La creación de contenido de destino dentro de una aplicación de AEM Mobile sigue un procedimiento similar al de creación de AEM Sites:

Consulte aquí para obtener una descripción general completa sobre [Creación de contenido de destino en AEM](/help/sites-authoring/personalization.md)

## Para desarrolladores {#for-developers}

AEM desarrolladores que crean aplicaciones móviles deben seguir los patrones que se utilizan habitualmente a lo largo del AEM al desarrollar componentes. Aquí, le explicaremos los pasos necesarios para permitir a los autores de contenido crear contenido de destino:

### Controladores de Adobe Target ContentSync {#adobe-target-contentsync-handlers}

Para entregar contenido al contenido del dispositivo del usuario, se genera procesando las ofertas que crean los autores de contenido de AEM. Para gestionar la renderización de ofertas de destino, hay un nuevo controlador de sincronización de contenido que procesará las ofertas. Si utilizamos la aplicación de referencia híbrida como ejemplo, el paquete de contenido en (inglés) contiene ContentSyncConfig con un [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) controlador. El siguiente paso es crucial para procesar ofertas en el dispositivo. El controlador mobileappoffers tiene una propiedad path que identifica la ruta a la actividad de personalización que se va a utilizar para la aplicación.

Por ejemplo, si hay una actividad que se encuentra en */content/campaign/hybridref* copie esta ruta y péguela como valor en la variable *ruta* propiedad del controlador mobileappoffers.

>[!NOTE]
>
>Para la aplicación de referencia híbrida hay dos controladores de mobileappoffers: uno para el desarrollo y otro para las producciones.

Una vez que la ruta de las actividades se ha establecido en la propiedad ruta del controlador mobileappoffers, guarde el controlador. El controlador ya estará listo para iniciar el procesamiento de ofertas para nuestros dispositivos móviles.

### Modo de procesamiento {#render-mode}

El controlador mobileappoffers está configurado de forma diferente para las configuraciones de publicación y desarrollo. Para la configuración de publicación hay una propiedad llamada *renderMode* con un valor de *publicar* se establece en el nodo cq:ContentSyncConfig . El controlador mobileappoffers hace referencia al renderMode y, si se configura para publicar, modifica el id de mbox que se crea. De forma predeterminada, los mboxes creados por AEM tienen un valor —author anexado al id del mbox. Esto identifica que la actividad no se ha publicado y debe utilizar la campaña no publicada para las resoluciones de oferta.

Cuando el contenido se configura mediante el panel de Adobe móvil, el contenido preparado se considera contenido listo para la producción y se procesa mediante la configuración de sincronización de contenido que no es de desarrollo. Si se procesa de este modo, se eliminará —author de todos los id de mbox y se espera que una actividad publicada esté disponible en el servidor de Target. Antes de probar el contenido preparado, asegúrese de que la actividad se haya publicado.

### Personalización del desarrollo de aplicaciones {#personalization-app-development}

#### Componentes {#components}

La base de cualquier contenido suele ser un componente de página que amplía uno de los componentes de página de base AEM wcm/foundation/components/page o foundation/components/page, dependiendo de si utiliza HTL o JSP. La duración de estos pasos se centrará en el uso del componente wcm/foundation/components/page . La estructura básica del componente de página se desglosa en varios scripts, cada uno de los cuales proporciona el propósito específico de permitir al desarrollador organizar y anular su código si es necesario. Los dos scripts que son de interés para la personalización son head.html y body.html. Estas dos secuencias de comandos proporcionan un área en la que se puede insertar código para admitir la creación de ContextHub, Cloud Services y dispositivos móviles.

A continuación se muestra una descripción general de las dos secuencias de comandos principales utilizadas para habilitar la segmentación de contenido.

#### head.html {#head-html}

Para que el autor pueda dirigir su contenido, es necesario añadir el menú de destino a la página para que el autor pueda cambiar el contexto del modo de edición al modo de orientación. Para habilitar esta función, el desarrollador debe modificar el script head.html para incluir el siguiente fragmento de código cerca de la parte superior del head.html o tan cerca del &lt;title>&lt;/title> como sea posible.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Tenga en cuenta que el script solo debe incluirse cuando el modo WCM no se ha deshabilitado, de modo que cuando el modo WCM esté desactivado (consulte la sección del controlador ContentSync para obtener más información), el script no se incluirá en el código de la aplicación final.

Para que los autores puedan obtener una vista previa del contenido de destino, el editor debe poder localizar la configuración del servicio en la nube de Adobe Target. El bloque de código siguiente añade dos secuencias de comandos importantes. El primero que agrega la capacidad de la página para localizar el servicio de nube de Target asociado y realizar las llamadas a Adobe Target. El segundo es la adición de la categoría cq.apps.targeting .

La variable **cq.apps.targeting** reemplaza el componente predeterminado cq/personalization/component/target y utiliza el componente mobileapps/components/target que procesa ofertas específicas para el consumo de aplicaciones móviles. Para obtener más información, consulte la sección Componente de destino .

El código debe añadirse en head.html y colocarse justo antes del final del &lt;/head> elemento.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Tenga en cuenta que el bloque de código se ajusta dentro de un modo WCM, no se desactiva, por lo que solo entra en juego mientras el autor del contenido está trabajando en la creación de contenido. Los scripts del servicio de nube no se agregarán al código de tiempo de ejecución móvil generado.

#### body.html {#body-html}

Para habilitar al autor de contenido la capacidad de probar diferentes personalidades, la secuencia de comandos body.html debe incluir el siguiente bloque de código como el primer elemento secundario del elemento body.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

El último bit de código requerido se encuentra en la parte inferior del body.html. Este bit de código busca el servicio de nube asociado e introduce el código de motor de targeting apropiado.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Aplicación de referencia {#reference-application}

Se pueden encontrar ejemplos de head.html y body.html en la [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) mostrar al desarrollador dónde colocar los bloques de script dentro de los dos scripts.

### Gestores de sincronización de contenido {#content-sync-handlers}

Cuando el autor de contenido ha terminado de crear contenido para la aplicación móvil, el siguiente paso es descargar la fuente y crear la aplicación, o configurar el contenido que se va a publicar. El desarrollador participa en varios pasos para que esto suceda. Para facilitar la renderización del contenido, AEM Mobile utiliza controladores de sincronización de contenido para procesar y empaquetar el contenido. Se ha introducido un nuevo controlador de sincronización de contenido para que el caso de uso Personalización represente el contenido de destino. El controlador &quot;mobileappoffers&quot; sabe cómo procesar las ofertas de destino asociadas que ha creado el autor del contenido. El controlador mobileappoffers extiende el controlador de actualización de páginas abstractas, por lo que muchas de las propiedades son similares. Los detalles del controlador mobileappoffers tienen las siguientes propiedades.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>reescribir</td>
   <td>+ relationParentPath<p> - "/"</p> </td>
   <td>La propiedad rewrite identifica cómo se deben reescribir las rutas dentro del contenido.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offer proxy"</p> </td>
   <td>La propiedad includePageTypes es opcional, de forma predeterminada se establece en páginas que tienen tipos de recurso cq/personalization/components/teaserpage y cq/personalization/components/offer proxy. Estos dos tipos de recurso son los tipos de recurso predeterminados que se utilizan cuando se segmenta el contenido. Si es necesario admitir tipos de recursos adicionales, estos se deben agregar a la lista de includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>La ubicación de la aplicación.</td>
  </tr>
  <tr>
   <td>type</td>
   <td>mobileappoffers</td>
   <td>Nombre del controlador que es mobileappoffers.</td>
  </tr>
  <tr>
   <td>selector</td>
   <td>tandt</td>
   <td>El selector de tendencias se utiliza para procesar el contenido de destino. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>El directorio raíz donde se debe mantener el contenido representado.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Si es true, se procesarán las imágenes incluidas en la oferta. Si se omiten imágenes falsas.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>Si es true, se procesarán los vídeos incluidos en la oferta. Si se omiten vídeos falsos.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/igns/&lt;brand&gt;</td>
   <td>Señala la marca de la campaña en la que participan las ofertas. Actualmente, todas las ofertas deben proceder de la misma campaña.</td>
  </tr>
  <tr>
   <td>profundo</td>
   <td>true | false</td>
   <td>Si el valor "true" se procesa varias veces en todas las páginas secundarias, si el valor "false" no se repite. </td>
  </tr>
  <tr>
   <td>Extensión</td>
   <td>html</td>
   <td>Establece la extensión del recurso que se está procesando. Se establece en html de forma que las páginas tengan una extensión .html .</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>La variable [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) tiene la configuración predeterminada del controlador mobileappoffer. La propiedad path del ejemplo está vacía, ya que depende de la ubicación de la campaña. Una vez que el autor de una campaña ha creado una campaña, el administrador de aplicaciones debe asociar la campaña con el controlador especificando la propiedad de ruta que señala a la campaña.

### Componente de destino {#target-component}

Para ayudar a procesar contenido específicamente para aplicaciones móviles, AEM Mobile utiliza el componente mobileapps/components/target . El componente de destino móvil amplía el componente cq/personalization/components/target y anula el script engine_tnt.jsp. Al anular engine_tnt.jsp , AEM Mobile puede controlar el HTML generado para el caso de uso de las aplicaciones móviles. Para cada componente dirigido por un autor de contenido, engine_tnt.jsp crea un mbox asociado.

Para cada mbox, un atributo de **cq-targeting** se añade permitiendo a los desarrolladores de aplicaciones escribir código personalizado para consumir y usar lo que deseen. La variable [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) tiene un ejemplo de directiva de Angular que utiliza el atributo cq-targeting. El concepto de reemplazo de contenido cuando y cómo se realiza depende en gran medida del desarrollador de aplicaciones móviles. Hay un SDK móvil que se entrega a través de AEM /etc/clientlibs/mobileapps/js/mobileapps.js que proporciona una API para llamar al servicio de Targeting de Adobe. Depende del desarrollador de la aplicación especificar cuándo se debe realizar esa llamada según el diseño de su aplicación.

## Siguientes pasos? {#what-s-next}

1. [Iniciar mi experiencia en la aplicación de AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Administrar el contenido de mi aplicación](/help/mobile/phonegap-manage-app-content.md)
1. [Generar mi aplicación](/help/mobile/building-app-mobile-phonegap.md)
1. [Seguimiento del rendimiento de mi aplicación con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Ofrecer una experiencia de aplicación personalizada con Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensajes importantes a mis usuarios](/help/mobile/phonegap-push-notifications.md)
