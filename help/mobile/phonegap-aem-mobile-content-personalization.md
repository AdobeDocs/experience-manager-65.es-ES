---
title: Personalización de contenido de AEM Mobile
seo-title: AEM Mobile content personalization
description: Siga esta página para obtener más información sobre la función de personalización de contenido de AEM Mobile AEM que permite a los autores de la aplicación personalizar el contenido de la aplicación móvil mediante el uso de Adobe Target.
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
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento forma parte del [Introducción a AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guía, un punto de partida recomendado para referencia de AEM Mobile.

La función de personalización de contenido de AEM Mobile permite [Autores AEM](#author) para personalizar el contenido de la aplicación móvil mediante [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). Esto permite enviar ofertas segmentadas a usuarios de aplicaciones móviles. Adobe Experience Manager Mobile permite crear, segmentar y entregar contenido que proporcione al usuario contenido específico para sus propios gustos individuales.

AEM Como suele suceder en los casos de las, para que los autores empiecen a crear este contenido, los administradores y desarrolladores deben preparar primero el entorno.

[AEM ministros de la](#administrator) son necesarios para establecer una conexión entre AEM Mobile y el Cloud Service de Adobe Target.

Mientras tanto, AEM Mobile [desarrolladores](#developer) Necesitan modificar sus scripts existentes para facilitar la creación de contenido de destino.

## Para administradores {#for-administrators}

Es necesario realizar una serie de pasos antes de que los autores de contenido puedan empezar a generar contenido de destino para aplicaciones móviles: se obtiene el conjunto adecuado de permisos para usuarios y grupos, se crean servicios en la nube, se configura la aplicación para la actividad y, finalmente, se genera el contenido.

Este artículo le guiará a través del proceso utilizado para configurar la variable [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) para la segmentación.

En adelante, se supone que la aplicación de referencia híbrida de AEM Mobile se ha implementado correctamente y se puede acceder a ella desde el panel de AEM Mobile.

AEM Para que los autores puedan generar contenido de destino dentro de una aplicación, la instancia de debe ser [configurado con el Cloud Service de Adobe Target.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Permisos {#permissions}

Los usuarios que necesitan acceder a la consola de personalización deben formar parte de `target-activity-authors` grupo.

Se sugiere que, como parte de la configuración de usuarios y grupos, el grupo de actividad de destinatario se agregue al grupo de administradores de aplicaciones. Al agregar el grupo target-activity-authors, esto permite a los usuarios ver la entrada del menú de navegación Personalización.

>[!NOTE]
>
>Si se olvida agregar los usuarios o grupos a los que desea tener acceso a Admin Console de personalización al grupo target-activity-authors, los usuarios no podrán ver la consola de personalización.

### Cloud Services {#cloud-services}

Para que el contenido de destino funcione para aplicaciones móviles, hay dos servicios que deben configurarse: el servicio Adobe Target y el servicio Adobe Mobile Services. El servicio Adobe Target proporciona el motor para procesar las solicitudes de los clientes y devolver el contenido personalizado. El servicio de Adobe Mobile Services proporciona la conexión entre los servicios de Adobe y la aplicación móvil a través del archivo ADBMobileConfig.json, que consume el complemento AMS Cordova. Desde AEM Mobile Dashboard puede configurar la aplicación agregando los dos servicios.

En el panel de AEM Mobile, busque Administrar Cloud Services y haga clic en el botón +.

![chlimage_1-38](assets/chlimage_1-38.png)

En el asistente Agregar Cloud Service, seleccione la tarjeta de servicio en la nube &quot;Adobe Target&quot; y haga clic en Siguiente.

![chlimage_1-39](assets/chlimage_1-39.png)

En el menú desplegable Seleccionar una configuración, puede crear una configuración nueva o seleccionar una existente. Para crear una nueva configuración, seleccione &quot;Crear configuración&quot; en el menú desplegable. Introduzca un título para la configuración de Target. Introduzca el código de cliente, el correo electrónico y la contraseña asociados a su cuenta de Target. Si no conoce los valores de estos campos, póngase en contacto con el servicio de asistencia de Adobe Target. Haga clic en el botón &quot;Verificar&quot; para validar las credenciales. Una vez verificado, haga clic en el botón Enviar para crear el servicio en la nube.

>[!NOTE]
>
>El servicio en la nube que se crea se asocia automáticamente a la aplicación móvil mediante el asistente. El valor de la propiedad cq:cloudserviceconfigs se establece en el nodo jcr:content del nodo de grupo de aplicaciones. Para el ejemplo de aplicación híbrida, se establece en /content/mobileapps/hybrid-reference-app/jcr:content con el valor que señala al nodo de marco de trabajo generado automáticamente ubicado en /etc/cloudservices/testandtarget/adobe-target-aem-apps/framework. El nodo de marco de trabajo tiene dos propiedades establecidas de forma predeterminada: sexo y edad. AEM El marco de trabajo solo se utiliza con la vista previa de la vista previa de la y no tiene ningún impacto en el dispositivo.

Una vez completado el asistente, el mosaico Administrar Cloud Service contendrá el servicio en la nube de Target, pero contiene una advertencia sobre la falta de una cuenta de Adobe Mobile Service.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

Es necesario vincular también una cuenta de Adobe Mobile Services (AMS) a la aplicación. El servicio AMS proporciona el archivo ADBMobileConfig.json requerido que contiene la información del código de cliente de Target. Antes de crear una asociación con la cuenta de AMS, la cuenta de AMS debe ser modificada por un usuario que tenga permisos de AMS.

### Código de cliente {#client-code}

Para iniciar sesión en los servicios de AMS, visite [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleccione la aplicación móvil y haga clic en la configuración. Busque el campo Opciones de Target de SDK, coloque el código de cliente en el campo y haga clic en Guardar.

![chlimage_1-41](assets/chlimage_1-41.png)

Ahora que el código de cliente se ha asociado a la aplicación móvil, cuando el servicio en la nube de AMS se configura mediante el Panel de control móvil de Adobe, los ajustes de los servicios se entregarán mediante el archivo ADBMobileConfig.json.

### Cloud Service de Adobe Mobile Services {#adobe-mobile-service-cloud-service}

Ahora que AMS está configurado, es hora de asociar la aplicación móvil al Tablero móvil de Adobe. En el panel de AEM Mobile, busque Administrar Cloud Services y haga clic en el botón +.

![chlimage_1-42](assets/chlimage_1-42.png)

Seleccione la tarjeta de Adobe Mobile Services y haga clic en Siguiente.

![chlimage_1-43](assets/chlimage_1-43.png)

En el paso del asistente Crear o Seleccionar, seleccione la lista desplegable Mobile Service y la entrada Crear configuración. Proporcione un título, una empresa, un nombre de usuario y una contraseña, y seleccione el centro de datos adecuado. Si no conoce estos valores, póngase en contacto con el administrador de Adobe Mobile Services para obtenerlos. Una vez rellenados todos los campos, haga clic en el botón Verificar. El proceso de verificación va a AMS y verifica las credenciales de la cuenta. Una vez validada correctamente, se rellenará una lista de aplicaciones móviles en la que se seleccionará la aplicación móvil asociada en el menú desplegable. Haga clic en el botón Enviar para completar el asistente. El proceso puede tardar un poco en obtener los datos de configuración y cualquier análisis asociado con la aplicación. Una vez completado el proceso, haga clic en el botón Listo del modal para volver al panel de Adobe Mobile.

Si vuelve al panel móvil, el mosaico Administrar Cloud Services contendrá el servicio en la nube de AMS. También tendrá en cuenta que el mosaico Analizar métricas se rellenará con informes de ciclo vital.

![chlimage_1-44](assets/chlimage_1-44.png)

## Para autores {#for-authors}

**Requisito previo:** Como se ha mencionado anteriormente, los administradores deben configurar la conexión con el servicio de Adobe Target para que los autores puedan generar nuevo contenido de destino.

Una vez que el administrador ha configurado los dos servicios en la nube y el desarrollador ha configurado el controlador de ofertas móviles, los autores de contenido ahora pueden empezar a generar experiencias segmentadas.

La creación de contenido de destino en una aplicación de AEM Mobile sigue un procedimiento similar al de la creación de AEM Sites:

Consulte aquí una descripción general completa de [AEM Creación de contenido segmentado en el](/help/sites-authoring/personalization.md)

## Para desarrolladores {#for-developers}

AEM AEM Los desarrolladores de aplicaciones móviles deben seguir siguiendo los patrones que se usan con frecuencia a lo largo de los procesos de desarrollo de componentes en las aplicaciones móviles de los. Aquí, le guiaremos por los pasos necesarios para permitir que los autores de contenido creen contenido de destino:

### Controladores ContentSync de Adobe Target {#adobe-target-contentsync-handlers}

AEM Para enviar contenido al dispositivo del usuario, el contenido se genera procesando las ofertas creadas por los autores de contenido de la lista de distribución de contenido Para gestionar la renderización de ofertas de destino, hay un nuevo controlador de sincronización de contenido que procesará las ofertas. Utilizando la aplicación de referencia híbrida como ejemplo, el paquete de contenido en (inglés) contiene ContentSyncConfig con un [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) controlador. El siguiente paso es crucial para procesar ofertas en el dispositivo. El controlador de ofertas móviles tiene una propiedad path que identifica la ruta a la actividad de personalización que se va a utilizar para la aplicación.

Por ejemplo, si hay una actividad ubicada en */content/campaigns/hybridref* copie esta ruta y péguela como el valor en *ruta* propiedad del controlador mobileapps.

>[!NOTE]
>
>Para la aplicación de referencia híbrida hay dos controladores de ofertas móviles, uno para desarrollo y otro para producciones.

Una vez establecida la ruta de las actividades en la propiedad path del controlador de ofertas móviles, guarde el controlador. El controlador ahora estará listo para iniciar la representación de ofertas para nuestros dispositivos móviles.

### Modo de procesamiento {#render-mode}

El controlador mobileapps está configurado de forma diferente para las configuraciones de publicación y desarrollo. Para las configuraciones de publicación hay una propiedad llamada *renderMode* con un valor de *publicar* se establece en el nodo cq:ContentSyncConfig. El controlador mobileapps hace referencia a renderMode y, si se establece en publish, modifica el ID de mbox que se crea. AEM De forma predeterminada, los mboxes que crea el usuario tienen el valor —author anexado al id de mbox. Esto identifica que la actividad no se ha publicado y debe utilizar la campaña sin publicar para las resoluciones de oferta.

Cuando el contenido se almacena en zona intermedia mediante el panel de Adobe Mobile, el contenido almacenado en zona intermedia se considera contenido listo para la producción y se procesa mediante la configuración de sincronización de contenido no desarrollada. Procesar de esta manera hará que —author se elimine de todos los id de mbox y espere que una actividad publicada esté disponible en el servidor de Target. Antes de probar el contenido ensayado, asegúrese de que la actividad se ha publicado.

### Personalization App Development {#personalization-app-development}

#### Componentes {#components}

AEM La base de cualquier contenido suele ser un componente de página que amplía uno de los componentes de página base wcm/foundation/components/page o foundation/components/page, en función de si utiliza HTL o JSP. La duración de estos pasos se centrará en el uso del componente wcm/foundation/components/page. La estructura básica del componente de página se desglosa en varios scripts, cada uno de los cuales proporciona el propósito específico de permitir al desarrollador organizar y anular su código si es necesario. Los dos scripts de interés para la personalización son head.html y body.html. Estos dos scripts proporcionan un área en la que se puede insertar código para admitir ContextHub, Cloud Services y Mobile Authoring.

A continuación se ofrece una descripción general de los dos scripts principales utilizados para habilitar la segmentación de contenido.

#### head.html {#head-html}

Para proporcionar al autor la capacidad de segmentar su contenido, es necesario añadir el menú objetivo a la página para que el autor pueda cambiar el contexto del modo de edición al modo de segmentación. Para habilitar esta función, el desarrollador debe modificar la secuencia de comandos head.html para incluir el siguiente fragmento de código cerca de la parte superior de head.html o lo más cerca posible de &lt;title>&lt;/title> como sea posible.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Tenga en cuenta que la secuencia de comandos solo debe incluirse cuando el modo WCM no se ha deshabilitado, de modo que cuando el modo WCM está deshabilitado (consulte la sección del controlador ContentSync para obtener más información), la secuencia de comandos no se incluirá en el código final de la aplicación.

Para proporcionar a los autores la capacidad de previsualizar el contenido de destino, el editor debe poder localizar la configuración del servicio en la nube de Adobe Target. El bloque de código siguiente agrega dos scripts importantes. La primera es añadir la capacidad de la página para localizar el servicio en la nube de Target asociado y realizar las llamadas a Adobe Target. El segundo es la adición de la categoría cq.apps.targeting.

El **cq.apps.targeting** la categoría anula el componente cq/personalization/component/target predeterminado y utiliza el componente mobileapps/components/target que procesa ofertas específicas para el consumo de aplicaciones móviles. Se tratarán más detalles sobre esto en la sección Componente de Target.

El código debe añadirse en head.html y colocarse justo antes del final del &lt;/head> Elemento.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Tenga en cuenta que el bloque de código se envuelve dentro de un Modo WCM sin desactivarse, por lo que solo entra en juego mientras el autor del contenido trabaja en la creación de contenido. Los scripts del servicio en la nube no se agregarán al código de tiempo de ejecución móvil generado.

#### body.html {#body-html}

Para permitir al autor del contenido probar diferentes personalidades, el script body.html debe incluir el siguiente bloque de código como primer elemento secundario del elemento body.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

El último bit de código requerido está en la parte inferior del body.html. Este bit de código busca el servicio en la nube asociado e inserta el código de motor de segmentación adecuado.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Aplicación de referencia {#reference-application}

Encontrará ejemplos de head.html y body.html en la [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) mostrando al desarrollador dónde colocar los bloques de script dentro de los dos scripts.

### Controladores de sincronización de contenido {#content-sync-handlers}

Cuando el autor del contenido ha terminado de crear contenido para la aplicación móvil, el siguiente paso es descargar la fuente y crear la aplicación o almacenar en zona intermedia el contenido que se va a publicar. El desarrollador debe seguir una serie de pasos para que esto suceda. Para ayudar a procesar el contenido, AEM Mobile utiliza controladores de sincronización de contenido para procesar y empaquetar el contenido. Se ha introducido un nuevo controlador de sincronización de contenido para el caso de uso Personalización para procesar contenido de destino. El controlador &quot;mobileapps&quot; sabe cómo procesar las ofertas de destino asociadas que ha creado el autor del contenido. El controlador mobileapps amplía el controlador de actualización de páginas abstractas, por lo que muchas de las propiedades son similares. Los detalles del controlador mobileapps tienen las siguientes propiedades.

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>reescribir</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>La propiedad rewrite identifica cómo se deben reescribir las rutas dentro del contenido.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>La propiedad includePageTypes es opcional y su valor predeterminado son las páginas que tienen tipos de recursos de cq/personalization/components/teaserpage y cq/personalization/components/offerProxy. Estos dos tipos de recursos son los tipos de recursos predeterminados que se usan cuando se segmenta el contenido. Si es necesario admitir tipos de recursos adicionales, estos deben agregarse a la lista de includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>La ubicación de la aplicación.</td>
  </tr>
  <tr>
   <td>type</td>
   <td>mobileappoffers</td>
   <td>El nombre del controlador que se ofrece en mobileappfers.</td>
  </tr>
  <tr>
   <td>selector</td>
   <td>tandt</td>
   <td>El selector estándar se utiliza para procesar el contenido segmentado. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>El directorio raíz en el que se debe conservar el contenido procesado.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Si el valor es True, se procesarán las imágenes incluidas en la oferta. Si es false, las imágenes se omitirán.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>Si el valor es True, se procesarán los vídeos incluidos en la oferta. Si es falso, se omitirán los vídeos.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>Señala a la marca de la campaña en la que participan las ofertas. Actualmente, todas las ofertas deben provenir de la misma campaña.</td>
  </tr>
  <tr>
   <td>profundo</td>
   <td>true | false</td>
   <td>Si es true, procesa recursivamente todas las páginas secundarias; si es false, no se repite. </td>
  </tr>
  <tr>
   <td>extensión</td>
   <td>html</td>
   <td>Establece la extensión del recurso que se está representando. Configúrelo en html de forma que las páginas tengan la extensión .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>El [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) tiene la configuración predeterminada del controlador mobileappfer. La propiedad path del ejemplo está vacía, ya que depende de la ubicación de la campaña. Después de que un autor de Campaign haya creado una campaña, el administrador de aplicaciones debe asociar la campaña con el controlador especificando la propiedad de ruta de acceso para que apunte a la campaña.

### Componente de destino {#target-component}

Para ayudar a procesar contenido específicamente para aplicaciones móviles, AEM Mobile utiliza el componente mobileapps/components/target. El componente target móvil amplía el componente cq/personalization/components/target y anula el script engine_tnt.jsp. Al anular engine_tnt.jsp, AEM Mobile puede controlar el HTML que se genera en el caso de uso de las aplicaciones móviles. Para cada componente segmentado por un autor de contenido, el archivo engine_tnt.jsp crea un mbox asociado.

Un atributo de cada mbox **cq-targeting** se agrega permitiendo a los desarrolladores de aplicaciones escribir código personalizado para consumirlo y utilizarlo como les plazca. El [Aplicación de referencia híbrida de AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) tiene un ejemplo de una directiva de Angular que utiliza el atributo cq-targeting. El concepto de reemplazo de contenido cuando y cómo se realiza depende en gran medida del desarrollador de aplicaciones móviles. AEM Hay un SDK móvil que se entrega a través de /etc/clientlibs/mobileapps/js/mobileapps.js que proporciona una API para llamar al servicio de segmentación de Adobe. Depende del desarrollador de la aplicación especificar cuándo se debe realizar esa llamada según el diseño de la aplicación.

## Siguientes pasos? {#what-s-next}

1. [Iniciar la experiencia de mi aplicación de AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Administrar el contenido de mi aplicación](/help/mobile/phonegap-manage-app-content.md)
1. [Generar mi aplicación](/help/mobile/building-app-mobile-phonegap.md)
1. [Realizar un seguimiento del rendimiento de mi aplicación con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Ofrezca una experiencia de aplicación personalizada con Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensajes importantes a mis usuarios](/help/mobile/phonegap-push-notifications.md)
