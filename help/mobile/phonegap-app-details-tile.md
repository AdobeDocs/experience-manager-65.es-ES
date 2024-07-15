---
title: Administrar mosaico de aplicación
description: Obtenga más información sobre el mosaico "Administrar aplicación" en el panel de la aplicación que proporciona le permite editar detalles sobre la aplicación.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 8bcf70ef-94d2-4958-90b5-bc375b360916
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 1%

---

# Administrar mosaico de aplicación{#manage-app-tile}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El mosaico **`Manage App`** en el panel de la aplicación le permite editar detalles sobre la aplicación. Para abrir la página Detalles, haga clic en el vínculo de detalles del mosaico **`Manage App`**. Desde la página **`Manage App`**, puede editar la configuración de la aplicación PhoneGap (config.xml) y preparar la aplicación para enviarla a las distintas tiendas de aplicaciones.

![chlimage_1-116](assets/chlimage_1-116.png)

## Explicación del mosaico `Manage App` {#understanding-the-manage-app-tile}

Puede explorar en profundidad cada mosaico del mosaico **`Manage App`** para ver o editar detalles haciendo clic en &#39;...&#39;, en la esquina inferior derecha.

### La pestaña Básico {#the-basic-tab}

En esta pestaña, puede editar **Nombre**, **Autor**, **Descripción breve** y **Descripción** para su aplicación.

![chlimage_1-117](assets/chlimage_1-117.png)

### La pestaña Avanzadas {#the-advanced-tab}

Cada plataforma de aplicación móvil describe qué datos se recopilan y se dirigen específicamente a cada almacén de aplicaciones.

Las plataformas mostradas se rigen por el contenido config.xml de PhoneGap:

```xml
<widget>
<gap:platform name="ios"/>
<gap:platform name="android"/>
</widget>
```

Cada tienda de aplicaciones de proveedores (por ejemplo, Apple App Store o Google Play Store) necesita una o más capturas de pantalla de su aplicación móvil para mostrar los detalles de su aplicación a los clientes. Estas capturas de pantalla pueden tener requisitos estrictos en cuanto a dimensiones y contenido (básicamente, deben representar realmente la aplicación). AEM Aplicaciones admite la selección y administración de estas capturas de pantalla para las plataformas admitidas y la visualización de dimensiones de puerto según lo requerido por la tienda de aplicaciones de cada proveedor.

>[!NOTE]
>
>AEM AEM La aplicación Verificar el le permite enviar capturas de pantalla directamente a los detalles de la aplicación en la aplicación de la manera más sencilla y sencilla.
>
>AEM Consulte [Inicio rápido móvil para la verificación de la](/help/mobile/phonegap-mobile-quickstart.md) para obtener más información.

![chlimage_1-118](assets/chlimage_1-118.png)

### Metadatos {#metadata}

>[!NOTE]
>
>Una vez que esté familiarizado con el mosaico **`Manage App`**, consulte [Edición de metadatos de aplicación](/help/mobile/phonegap-editmetadata.md) para ver y editar los metadatos.

#### Metadatos comunes {#common-metadata}

Cada aplicación debe tener metadatos asociados que ayuden a configurar diferentes aspectos de la aplicación. La página Administrar aplicación está separada en dos áreas diferentes relacionadas con la recopilación de metadatos. Metadatos específicos de la plataforma y metadatos comunes.

Hay configuraciones y metadatos comunes en todas las plataformas.

En esta sección, defina la URL del servidor de actualización de contenido, la página de aterrizaje de la aplicación móvil, la versión de PhoneGap para la compilación, la versión de la aplicación, el nombre, la descripción, etc.

**Versión de la aplicación** es la versión de trabajo de su aplicación. La práctica recomendada habitual es utilizar una notación de 3 decimales y comenzar por debajo de 1.0.0 antes de la primera versión.

**PhoneGap Version** es la versión en la que deseas compilar tu aplicación con PhoneGap. La práctica recomendada es mantenerse al día con la versión actual para asegurarse de obtener las últimas y mejores funciones y correcciones de errores.

**URL del servidor de actualización de contenido** es la URL que usa su aplicación para llamar a las actualizaciones de ContentSync. Se debe establecer en la dirección URL de Dispatcher o, si no utiliza un Dispatcher, en una de las instancias de publicación que se utiliza para proporcionar actualizaciones de ContentSync a la aplicación.

![chlimage_1-119](assets/chlimage_1-119.png)

>[!NOTE]
>
>Esta sección puede aparecer vacía a menos que haya datos rellenando los campos.
>
>En la parte superior de la vista de detalles, verá Versión de la aplicación, Versión de PhoneGap y Actualizar URL. Cada uno de estos valores se puede establecer en la sección Metadatos comunes. Sin embargo, el ID de aplicación no se puede editar.

#### Metadatos de plataforma {#platform-metadata}

Cada plataforma definida en el archivo config.xml de PhoneGap puede contener propiedades de plataforma personalizadas. AEM Un desarrollador de debe contribuir con la estructura de contenido para capturar estas propiedades. Se puede encontrar un ejemplo proporcionado de propiedades específicas de la plataforma para iOS.

Los metadatos de todas las plataformas configuradas ahora se muestran al mismo tiempo en la ficha Avanzadas del mosaico `Manage App`.

>[!NOTE]
>
>PhoneGap no utiliza las secciones de metadatos de plataforma durante una CLI o la compilación de PhoneGap remoto. AEM En su lugar, intenta capturar metadatos para plataformas de modo que se puedan utilizar más adelante al enviarlos al almacén de aplicaciones del proveedor de destino.

AEM AEM En el caso de las plataformas que no comprende el usuario, un desarrollador de aplicaciones aún puede ampliar la interfaz de usuario para capturar estos metadatos, que luego se pueden exportar y utilizar durante el proceso de envío de la aplicación.

#### Metadatos de iOS {#ios-metadata}

Apple AppStore requiere metadatos adicionales para enviar la aplicación y distribuirlos. La sección de metadatos de iOS intenta recopilar la información necesaria que puede utilizar la herramienta iTMSTransporter de Apple para publicar los metadatos en la cuenta del desarrollador de Apple asociado.

Para obtener los metadatos específicos de Apple, cree su aplicación en [https://itunesconnect.apple.com](https://itunesconnect.apple.com/). Al crear la aplicación, Apple genera los metadatos que requiere la sección de metadatos de iOS si desea utilizar la herramienta Apple iTMSTransporter para validar y cargar los metadatos en itunesconnect.apple.com. Si desea obtener los metadatos que desea recopilar, no tiene que rellenar los metadatos específicos de iOS. Puede seguir exportando los metadatos que combinan el iOS y los metadatos comunes, y recopilar todas las capturas de pantalla en un archivo zip que se puede descargar en cualquier momento.

El archivo zip descargado contiene un archivo itmsp que se puede inspeccionar para buscar el archivo metadata.xml. El archivo itmsp contiene los metadatos exportados (dentro del archivo metadata.xml ), junto con todas las capturas de pantalla asociadas.

La funcionalidad de exportación se utiliza para proporcionar una forma cómoda de recopilar las capturas de pantalla y los metadatos que se pueden pasar al editor de la aplicación para su entrada en el almacén de aplicaciones específico del proveedor.

![chlimage_1-120](assets/chlimage_1-120.png)

#### Metadatos de Android™ {#android-metadata}

Al seleccionar la plataforma Android™, no hay metadatos personalizados en este momento que se puedan configurar. Al hacer clic en el botón de descarga, se genera un archivo zip con un archivo de propiedades que contiene todos los metadatos y las capturas de pantalla asociadas.

La funcionalidad de exportación se utiliza para proporcionar una forma cómoda de recopilar las capturas de pantalla y los metadatos que se pueden pasar al editor de la aplicación para su entrada en el almacén de aplicaciones específico del proveedor.

![chlimage_1-121](assets/chlimage_1-121.png)

### URL de servidor de actualización de contenido {#content-update-server-url}

AEM Una de las características clave de las aplicaciones de la es la capacidad de tener una aplicación móvil que solicite nuevo contenido a través de ContentSync, donde el contenido puede ser recursos HTML, páginas, vídeo, imágenes, texto, y más. Después de que un autor de contenido haya actualizado el contenido y luego lo publique, el servidor pone la actualización de contenido a disposición de la aplicación móvil para que la descargue.

La propiedad URL del servidor de actualización de contenido es la dirección URL que debe señalar a una instancia de publicación; directamente o a través de Dispatcher o CDN. El formato de la dirección URL es simplemente el siguiente:

`https://[hostname]:[port]`

>[!NOTE]
>
>AEM Si la instancia del servidor de creación se está replicando en muchas instancias del servidor de publicación (arquitectura común para los servidores de publicación), cada servidor de publicación tendrá el mismo contenido de actualización. El motivo es que la actualización se basa en el autor y se replica en todas las instancias de publicación. Básicamente, el equilibrio de carga y la conmutación por error son totalmente compatibles.

### La pestaña Plugins {#the-plugins-tab}

La pestaña **Plugins** describe los plugins asociados con su aplicación. Esta información se utiliza para recuperar el complemento adecuado durante una compilación.

![chlimage_1-122](assets/chlimage_1-122.png)

### La pestaña Capturas de pantalla {#the-screenshots-tab}

La pestaña **Capturas de pantalla** muestra las resoluciones de captura de pantalla admitidas en diferentes plataformas.

![chlimage_1-123](assets/chlimage_1-123.png)

>[!NOTE]
>
>Para agregar y quitar capturas de pantalla, consulte [Edición de metadatos de aplicación](/help/mobile/phonegap-editmetadata.md).

### La pestaña Autenticación {#the-authentication-tab}

La pestaña **Authentication** le permite seleccionar un cliente de OAuth para asociarlo a su aplicación y permite a un desarrollador utilizar la autenticación OAuth de Adobe Experience Manager.

![chlimage_1-124](assets/chlimage_1-124.png)

### Pasos siguientes {#the-next-steps}

Una vez que haya aprendido a administrar el mosaico de la aplicación en el panel de aplicaciones, consulte los siguientes recursos para otras funciones de creación:

* [Edición de metadatos de aplicación](/help/mobile/phonegap-editmetadata.md)
* [Definiciones de aplicación](/help/mobile/phonegap-app-definitions.md)
* [Crear una aplicación nueva mediante el Asistente para crear aplicación](/help/mobile/phonegap-create-new-app.md)
* [Importar una aplicación híbrida existente](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Content Services](/help/mobile/develop-content-as-a-service.md)

### Otros recursos {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Desarrollo para Adobe PhoneGap AEM Enterprise con](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)
