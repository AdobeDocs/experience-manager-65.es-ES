---
title: Administrar mosaico de aplicación
seo-title: Administrar mosaico de aplicación
description: Siga esta página para obtener más información sobre Administrar icono de aplicación en el panel de la aplicación, que permite modificar los detalles de la aplicación.
seo-description: Siga esta página para obtener más información sobre Administrar icono de aplicación en el panel de la aplicación, que permite modificar los detalles de la aplicación.
uuid: bde75ecd-8694-427c-9b16-2c4ab2fd4d8b
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: a87834c9-247c-49fa-9978-a969230db91c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administrar mosaico de aplicación{#manage-app-tile}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El icono **Administrar aplicación** del panel de la aplicación permite modificar los detalles de la aplicación. Para abrir la página Detalles, haga clic en el vínculo Administrar detalles del mosaico de la aplicación. Desde la página Administrar aplicación puede editar la configuración de la configuración de la aplicación PhoneGap (config.xml) y preparar la aplicación para enviarla a los distintos almacenes de aplicaciones.

![chlimage_1-116](assets/chlimage_1-116.png)

## Explicación del icono Administrar aplicación {#understanding-the-manage-app-tile}

Puede explorar en profundidad cada mosaico en el mosaico **Administrar aplicación** para ver o editar los detalles haciendo clic en el botón &#39;...&#39; en la esquina inferior derecha.

### Ficha Básico {#the-basic-tab}

Puede editar el **nombre**, el **autor**, la descripción **** breve y la **descripción** de la aplicación desde esta ficha.

![chlimage_1-117](assets/chlimage_1-117.png)

### Ficha Avanzado {#the-advanced-tab}

Cada plataforma de aplicaciones móviles describe los datos que se recopilan, dirigiéndose específicamente a cada almacén de aplicaciones.

Las plataformas mostradas están impulsadas por el contenido de PhoneGap config.xml:

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Cada tienda de aplicaciones de proveedores, como Apple App Store o Google Play Store, por ejemplo, requiere una o más capturas de pantalla de la aplicación móvil para mostrar los detalles de la aplicación a los clientes. Estas capturas de pantalla pueden tener requisitos estrictos en cuanto a dimensiones y contenido (básicamente deben representar realmente la aplicación). Las aplicaciones AEM son compatibles con la selección y administración de estas capturas de pantalla para las plataformas admitidas y con la visualización de las dimensiones del puerto según lo requiera el almacén de aplicaciones de cada proveedor.

>[!NOTE]
>
>La aplicación AEM Verify permite enviar capturas de pantalla directamente a los detalles de la aplicación en AEM.
>
>Consulte Inicio rápido [móvil para AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) para obtener más información.

![chlimage_1-118](assets/chlimage_1-118.png)

### Metadatos {#metadata}

>[!NOTE]
>
>Una vez familiarizado con el mosaico **Administrar aplicación** , consulte [Edición de metadatos](/help/mobile/phonegap-editmetadata.md) de la aplicación para ver y editar los metadatos.

#### Metadatos comunes {#common-metadata}

Cada aplicación debe tener metadatos asociados que ayuden a configurar diferentes aspectos de la aplicación. La página Administrar aplicación se divide en dos áreas diferentes relacionadas con la recopilación de metadatos. Metadatos específicos de la plataforma y metadatos comunes.

Hay una configuración común y metadatos para todas las plataformas.

En esta sección, define la URL de Content Update Server, la página de aterrizaje para la aplicación móvil, la versión de PhoneGap para la compilación, la versión de la aplicación, el nombre, la descripción y mucho más.

**Versión** de la aplicación es la versión de trabajo de la aplicación. La práctica recomendada habitual es utilizar una notación con 3 decimales y comenzar por debajo de 1.0.0 antes de la primera versión.

**PhoneGap Version** es la versión en la que desea compilar la aplicación con PhoneGap. Lo mejor es mantenerse al día con la versión actual para asegurarse de obtener las últimas y mejores funciones y correcciones de errores.

**Content Update Server URL** es la dirección URL que utilizará la aplicación para solicitar actualizaciones de ContentSync. Debe configurarse en la dirección URL del despachante o, si no utiliza un despachante, en una de las instancias de publicación que se utilizarán para proporcionar actualizaciones de ContentSync a la aplicación.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Esta sección puede aparecer vacía a menos que haya datos que completen los campos.
>
>En la parte superior de la vista de detalles, verá Versión de la aplicación, Versión de PhoneGap y Actualizar URL, cada uno de estos valores se puede establecer en la sección Metadatos comunes. Sin embargo, no se puede editar el ID de la aplicación.

#### Metadatos de plataforma {#platform-metadata}

Todas las plataformas definidas en PhoneGap config.xml pueden contener propiedades de plataforma personalizadas. Un desarrollador de AEM debe aportar la estructura de contenido para capturar estas propiedades. Se puede encontrar un ejemplo proporcionado de propiedades específicas de la plataforma para iOS.

Los metadatos de todas las plataformas configuradas ahora se muestran al mismo tiempo en la ficha Avanzadas del mosaico Administrar aplicación.

>[!NOTE]
>
>Las secciones de metadatos de plataforma no son utilizadas por PhoneGap durante una compilación de CLI o PhoneGap remoto, sino que AEM intenta capturar metadatos para plataformas de modo que se puedan utilizar posteriormente al enviar al almacén de aplicaciones del proveedor de destino.

En el caso de plataformas que AEM no conoce, un desarrollador de AEM puede ampliar la interfaz de usuario para capturar estos metadatos que posteriormente se pueden exportar y utilizar durante el proceso de envío de la aplicación.

#### Metadatos de iOS {#ios-metadata}

Apple AppStore requiere metadatos adicionales para enviar la aplicación para su distribución. La sección de metadatos de iOS intenta recopilar la información necesaria que puede utilizar la herramienta iTMSTransporter de Apple para publicar los metadatos en la cuenta del desarrollador de Apple asociado.

Para obtener los metadatos específicos de Apple, primero debe crear la aplicación en [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Al crear la aplicación, Apple generará los metadatos que requiere la sección de metadatos de iOS si desea utilizar la herramienta Apple iTMSTransporter para validar y cargar los metadatos en itunesconnect.apple.com. Si solo desea obtener los metadatos para recopilarlos, no es necesario rellenar necesariamente los metadatos específicos de iOS. Aún puede exportar los metadatos que combinarán el iOS y los metadatos comunes y recopilar todas las capturas de pantalla en un archivo zip que se puede descargar en cualquier momento.

El archivo zip descargado contiene un archivo itmsp que puede inspeccionarse para buscar el archivo metadata.xml. El archivo itmsp contiene los metadatos exportados (dentro del archivo metadata.xml), junto con todas las capturas de pantalla asociadas.

La funcionalidad de exportación se utiliza para proporcionar una manera conveniente de recopilar las capturas de pantalla y los metadatos que se pueden pasar al editor de la aplicación para su entrada en el almacén de aplicaciones específico del proveedor.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Metadatos de Android {#android-metadata}

Al seleccionar la plataforma de Android, no hay metadatos personalizados que se puedan definir en este punto. Al hacer clic en el botón de descarga como archivo zip, se generará con un archivo de propiedades que contiene todos los metadatos y las capturas de pantalla asociadas.

La funcionalidad de exportación se utiliza para proporcionar una manera conveniente de recopilar las capturas de pantalla y los metadatos que se pueden pasar al editor de la aplicación para su entrada en el almacén de aplicaciones específico del proveedor.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL de servidor de actualización de contenido {#content-update-server-url}

Una de las funciones clave de las aplicaciones de AEM es la capacidad de tener una solicitud de contenido nuevo para aplicaciones móviles mediante ContentSync, donde el contenido puede ser recursos HTML, páginas, vídeos, imágenes, texto y mucho más. Una vez que el autor del contenido ha actualizado el contenido y luego lo publica, el servidor hace que la actualización de contenido esté disponible para que la aplicación móvil la descargue.

La propiedad URL de Content Update Server es la dirección URL que debe apuntar a una instancia de publicación; directamente o a través del despachante o CDN. El formato de la dirección URL es simplemente:

`https://[hostname]:[port]`

>[!NOTE]
>
>Si la instancia del servidor de creación se está replicando en varias instancias del servidor de publicación (arquitectura común para AEM), cada servidor de publicación tendrá el mismo contenido de actualización porque la actualización se crea en el autor y se replica en todas las instancias de publicación. Básicamente, el equilibrio de carga y la conmutación por error son totalmente compatibles.

### Ficha Complementos {#the-plugins-tab}

La ficha **Complementos** describe los complementos asociados a la aplicación. Esta información se utilizará para recuperar el complemento adecuado durante una compilación.

![chlimage_1-122](assets/chlimage_1-122.png)

### Ficha Capturas de pantalla {#the-screenshots-tab}

La ficha **Capturas de pantalla** muestra las resoluciones de las capturas de pantalla admitidas en diferentes plataformas.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Para agregar y eliminar capturas de pantalla, consulte [Edición de metadatos](/help/mobile/phonegap-editmetadata.md)de la aplicación.

### Ficha Autenticación {#the-authentication-tab}

La ficha **Autenticación** permite seleccionar un cliente OAuth para asociarlo a la aplicación y permite que un desarrollador utilice la autenticación OAuth de Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Pasos siguientes {#the-next-steps}

Una vez que haya aprendido a administrar el icono de la aplicación en el panel de la aplicación, consulte los siguientes recursos para otras funciones de creación:

* [Edición de metadatos de la aplicación](/help/mobile/phonegap-editmetadata.md)
* [Definiciones de aplicaciones](/help/mobile/phonegap-app-definitions.md)
* [Creación de una aplicación nueva mediante el Asistente para crear aplicación](/help/mobile/phonegap-create-new-app.md)
* [Importar una aplicación híbrida existente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### Additional Resources {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los siguientes recursos:

* [Desarrollo para Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

