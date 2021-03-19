---
title: Entrega de contenido
seo-title: Entrega de contenido
description: Entrega de contenido
seo-description: nulo
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Entrega de contenido{#content-delivery}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las aplicaciones móviles deben poder usar cualquier contenido en AEM según sea necesario para ofrecer la experiencia de aplicación segmentada.

Esto incluye el uso de recursos, contenido del sitio, contenido de CaaS (sobre el terreno) y contenido personalizado que puede tener su propia estructura.

>[!NOTE]
>
>**El** contenido sobre el aire puede provenir de cualquiera de los controladores anteriores a través de los controladores de ContentSync. Se puede utilizar para agrupar paquetes y envíos a través de zips, así como para mantener actualizaciones para esos paquetes.

Los servicios de contenido ofrecen tres tipos principales de material:

1. **Assets**
1. **Contenido HTML empaquetado (HTML/CSS/JS)**
1. **Contenido independiente del canal**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

Las colecciones de recursos son construcciones AEM que contienen referencias a otras colecciones.

Una colección de recursos se puede exponer a través de Content Services. Llamar a una colección de recursos en una solicitud devuelve un objeto que es una lista de los recursos, incluidas sus direcciones URL. Se accede a los recursos a través de una dirección URL. La dirección URL se proporciona en un objeto. Por ejemplo:

* Una entidad de página devuelve un JSON (objeto de página) que incluye una referencia de imagen. La referencia de imagen es una URL que se utiliza para obtener el binario de recursos de la imagen.
* Una solicitud de una lista de activos de una carpeta devuelve JSON con detalles sobre todas las entidades de dicha carpeta. Esa lista es un objeto. El JSON tiene referencias URL que se utilizan para obtener el binario de recursos para cada recurso de esa carpeta.

### Optimización de recursos {#asset-optimization}

Un valor clave de Content Services es la capacidad de devolver recursos que están optimizados para el dispositivo. Esto reduce las necesidades de almacenamiento de dispositivos locales y mejora el rendimiento de la aplicación.

La optimización de recursos será una función del servidor basada en la información suministrada en la solicitud de API. Siempre que sea posible, las representaciones de recursos deben almacenarse en caché para que solicitudes similares no requieran una nueva generación de la representación de recursos.

### Flujo de trabajo de recursos {#assets-workflow}

El flujo de trabajo de recursos es el siguiente:

1. Referencia de recursos disponible en AEM lista para usar
1. Crear entidad de referencia de recurso según su modelo
1. Editar entidad

   1. Seleccionar recurso o colección de recursos
   1. Personalización de la renderización JSON

El diagrama siguiente muestra el **Flujo de trabajo de referencia de recursos**:

![chlimage_1-155](assets/chlimage_1-155.png)

### Administración de recursos {#managing-assets}

Los servicios de contenido proporcionan acceso a AEM recursos administrados a los que es posible que no se haga referencia a través de otro contenido de AEM.

#### Recursos administrados existentes {#existing-managed-assets}

Un usuario de AEM Sites y Assets existente utiliza AEM Assets para administrar todo el material digital de todos los canales. Están desarrollando una aplicación móvil nativa y necesitan utilizar varios recursos que administra AEM Assets. Por ejemplo: logotipos, imágenes de fondo, iconos de botón, etc.

Actualmente, se distribuyen alrededor del repositorio de Assets. Los archivos a los que debe hacer referencia la aplicación están en:

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Acceso a las entidades de recursos de CS {#accessing-cs-asset-entities}

Dejemos de lado los pasos de cómo la página está disponible a través de la API por ahora (estará cubierta por la descripción de la interfaz de usuario de AEM) y asumamos que se ha hecho. Se han creado y agregado entidades de recursos al espacio &quot;appImages&quot;. Se han creado carpetas adicionales en el espacio para fines de organización. Por lo tanto, las entidades de recursos se almacenan en el JCR de AEM como:

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icon/cart
* /content/entities/appImages/icon/home

#### Obtención de una lista de entidades de recursos disponibles {#getting-a-list-of-available-asset-entities}

Un desarrollador de aplicaciones puede obtener una lista de los recursos disponibles recuperando las entidades de recursos. El extremo de espacio de Content Services puede proporcionar esa información a través del SDK de la API del servicio web.

El resultado sería un objeto en formato JSON que proporcionaría una lista de los recursos de la carpeta &quot;iconos&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Obtención de una imagen {#getting-an-image}

El JSON proporciona una dirección URL para cada imagen, generada por los servicios de contenido a la imagen.

Para obtener el binario de la imagen &quot;carrito&quot;, se vuelve a utilizar la biblioteca cliente.

## Contenido HTML empaquetado {#packaged-html-content}

El contenido HTML es necesario para los clientes que necesitan mantener el diseño del contenido. Esto resulta útil para las aplicaciones nativas que utilizan un contenedor web, como una vista web de Cordova, para mostrar el contenido.

AEM Content Services podrá proporcionar contenido HTML a la aplicación móvil mediante la API. Los clientes que deseen exponer AEM contenido como HTML crearán una entidad de página HTML que apunte al origen de contenido de AEM.

Se tienen en cuenta las siguientes opciones:

* **Archivo zip:** para tener la mejor oportunidad de mostrar correctamente en el dispositivo, todo el material al que se hace referencia en la página: css, JavaScript, recursos, etc. : se incluye en un solo archivo comprimido con la respuesta . Las referencias en la página HTML se ajustarán para utilizar una ruta relativa a estos archivos.
* **Transmisión:** Obtención de un manifiesto de los archivos necesarios de AEM. A continuación, utilice ese manifiesto para solicitar todos los archivos (HTML, CSS, JS, etc.) con solicitudes posteriores.

![chlimage_1-157](assets/chlimage_1-157.png)

## Contenido independiente del canal {#channel-independent-content}

El contenido independiente del canal es una forma de exponer AEM construcciones de contenido, como páginas, sin tener que preocuparse por el diseño, los componentes u otra información específica del canal.

Estas entidades de contenido se generan utilizando un modelo de contenido para traducir las estructuras de AEM a un formato JSON. Los datos JSON resultantes contienen información sobre los datos del contenido, que están disociados del repositorio de AEM. Esto incluye devolver metadatos y vínculos de referencia AEM a recursos, así como las relaciones entre las estructuras de contenido, incluida la jerarquía de entidades.

### Administración del contenido independiente del canal {#managing-channel-independent-content}

El contenido puede acceder a la aplicación de varias formas.

1. GET del contenido ZIPS mediante AEM Over-the-Air

   * Los controladores de sincronización de contenido pueden actualizar el paquete zip directamente o llamando a los procesadores de contenido existentes

      * Controladores de plataforma
      * Gestores de AEM
      * Controladores personalizados

1. GET del contenido directamente a través de los procesadores de contenido

   * Representadores Sling predeterminados predefinidos
   * Representadores de contenido de AEM Mobile/Content Services
   * Representaciones personalizadas

