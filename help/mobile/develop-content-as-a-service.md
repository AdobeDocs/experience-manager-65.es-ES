---
title: Envío de contenido
seo-title: Envío de contenido
description: nulo
seo-description: nulo
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---


# Envío de contenido{#content-delivery}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Las aplicaciones móviles deben poder utilizar todo el contenido de AEM según sea necesario para ofrecer la experiencia de aplicación de destino.

Esto incluye el uso de recursos, contenido del sitio, contenido de CaaS (sobre el aire) y contenido personalizado que puede tener su propia estructura.

>[!NOTE]
>
>**El** contenido de Over-the-Air puede provenir de cualquiera de los elementos anteriores a través de los controladores ContentSync. Se puede utilizar para empaquetar paquetes y envíos por lotes a través de zips, así como para mantener las actualizaciones de dichos paquetes.

Existen tres tipos principales de material que ofrece Content Services:

1. **Assets**
1. **Contenido HTML empaquetado (HTML/CSS/JS)**
1. **Contenido independiente del canal**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

Las colecciones de recursos son construcciones AEM que contienen referencias a otras colecciones.

Una colección de recursos se puede exponer a través de Content Services. Al llamar a una colección de recursos en una solicitud, se devuelve un objeto que es una lista de los recursos, incluidas sus direcciones URL. Se accede a los recursos a través de una dirección URL. La dirección URL se proporciona en un objeto. Por ejemplo:

* Una entidad de página devuelve JSON (objeto de página) que incluye una referencia de imagen. La referencia de imagen es una URL que se utiliza para obtener el binario de recursos para la imagen.
* Una solicitud de lista de recursos en una carpeta devuelve JSON con detalles sobre todas las entidades de dicha carpeta. Esa lista es un objeto. El JSON tiene referencias URL que se utilizan para obtener el binario de recursos para cada recurso de esa carpeta.

### Optimización de recursos {#asset-optimization}

Un valor clave de Content Services es la capacidad de devolver recursos optimizados para el dispositivo. Esto reduce las necesidades de almacenamiento del dispositivo local y mejora el rendimiento de la aplicación.

La optimización de recursos será una función del lado del servidor, basada en la información suministrada en la solicitud de API. Siempre que sea posible, las representaciones de recursos deben almacenarse en caché para que solicitudes similares no requieran una regeneración de la representación de recursos.

### Flujo de trabajo de recursos {#assets-workflow}

El flujo de trabajo de recursos es el siguiente:

1. Referencia de recursos disponible en AEM lista para usar
1. Crear entidad de referencia de recursos según su modelo
1. Editar entidad

   1. Seleccionar recurso o colección de recursos
   1. Personalización de la representación JSON

El diagrama siguiente muestra el **Flujo de trabajo de referencia de recursos**:

![chlimage_1-155](assets/chlimage_1-155.png)

### Administración de recursos {#managing-assets}

Content Services proporciona acceso a AEM recursos gestionados a los que no se puede hacer referencia mediante otro contenido AEM.

#### Recursos administrados existentes {#existing-managed-assets}

Un usuario existente de AEM Sites y Assets está utilizando AEM Assets para gestionar todo su material digital para todos los canales. Están desarrollando una aplicación móvil nativa y necesitan utilizar varios recursos que administra AEM Assets. Por ejemplo logotipos, imágenes de fondo, iconos de botón, etc.

Actualmente, estos se distribuyen alrededor del repositorio de recursos. Los archivos a los que debe hacer referencia la aplicación se encuentran en:

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Acceso a entidades de recursos de CS {#accessing-cs-asset-entities}

Dejemos a un lado los pasos de cómo la página está disponible a través de la API por ahora (estará cubierta por la descripción de la interfaz de usuario AEM) y supongamos que se ha realizado. Se han creado y agregado entidades de recursos al espacio &quot;appImages&quot;. Se crearon carpetas adicionales en el espacio para fines de organización. Por lo tanto, las entidades de recursos se almacenan en el JCR AEM como:

* /content/entity/appImages/logos/logo_light
* /content/entity/appImages/logos/logo_dark
* /content/entity/appImages/bkgnd/gray_blue
* /content/entity/appImages/icons/cart
* /content/entity/appImages/icons/home

#### Obtención de una lista de las entidades de recursos disponibles {#getting-a-list-of-available-asset-entities}

Un desarrollador de aplicaciones puede obtener una lista de los recursos disponibles, recuperando las entidades de recursos. El extremo de espacio de Content Services puede proporcionar esa información a través del SDK de la API de servicio web.

El resultado sería un objeto en formato JSON que proporcionaría una lista de los recursos de la carpeta &quot;icons&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Obtención de una imagen {#getting-an-image}

El JSON proporciona una URL para cada imagen, generada por Content Services para la imagen.

Para obtener el binario de la imagen &quot;carrito&quot;, se utiliza de nuevo la biblioteca cliente.

## Contenido HTML empaquetado {#packaged-html-content}

El contenido HTML es necesario para los clientes que necesitan mantener el diseño del contenido. Esto resulta útil para las aplicaciones nativas que utilizan un contenedor web (como una vista web de Cordova) para mostrar el contenido.

AEM Content Services podrá proporcionar contenido HTML a la aplicación móvil mediante la API. Los clientes que deseen exponer AEM contenido como HTML crearán una entidad de página HTML que apuntará a la fuente de contenido AEM.

Se consideran las siguientes opciones:

* **Archivo zip:** para tener la mejor oportunidad de mostrar correctamente en el dispositivo, todo el material referenciado de la página: css, JavaScript, recursos, etc. - se incluirá en un solo archivo comprimido con la respuesta. Las referencias de la página HTML se ajustarán para utilizar una ruta relativa a estos archivos.
* **Flujo continuo:** obtención de un manifiesto de los archivos necesarios de AEM. A continuación, utilice ese manifiesto para solicitar todos los archivos (HTML, CSS, JS, etc.) con solicitudes posteriores.

![chlimage_1-157](assets/chlimage_1-157.png)

## Contenido independiente de canal {#channel-independent-content}

El contenido independiente del canal es una forma de exponer construcciones de contenido AEM, como páginas, sin preocuparse por el diseño, los componentes u otra información específica del canal.

Estas entidades de contenido se generan utilizando un modelo de contenido para traducir las estructuras de AEM a un formato JSON. Los datos JSON resultantes contienen información sobre los datos del contenido, que se desvinculan del repositorio de AEM. Esto incluye devolver metadatos y vínculos de referencia AEM a los recursos, así como las relaciones entre las estructuras de contenido, incluida la jerarquía de entidades.

### Administración de contenido independiente de Canal {#managing-channel-independent-content}

El contenido puede acceder a la aplicación de varias formas.

1. GET de contenido ZIPS mediante AEM Over-the-Air

   * Los controladores de sincronización de contenido pueden actualizar el paquete zip directamente o llamando a los procesadores de contenido existentes

      * Controladores de plataforma
      * Controladores AEMM
      * Controladores personalizados

1. GET del contenido directamente a través de los procesadores de contenido

   * Representadores de Sling predeterminados listos para usar
   * Representadores de contenido de AEM Mobile/Content Services
   * Procesos personalizados

