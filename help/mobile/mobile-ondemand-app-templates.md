---
title: Creación y adición de plantillas y componentes
seo-title: Creating and Adding Templates and Components
description: Siga esta página para obtener más información sobre la creación y adición de plantillas y componentes a la aplicación. La página utiliza la aplicación Geometrixx Unlimited como aplicación que contiene una plantilla de aplicación y plantillas de página de ejemplo.
seo-description: Follow this page to learn about creating and adding templates and components to your app. The page uses Geometrixx Unlimited App as the app that contains a sample app template and page templates.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# Creación y adición de plantillas y componentes {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

AEM Mobile On-Demand proporciona una plantilla de aplicación totalmente configurada, una plantilla de artículo y componentes de artículo.

La aplicación We.Unlimited es una plantilla de ejemplo que representa el shell de una aplicación AEM Mobile On Demand totalmente configurable y manejable.

Al seleccionar esta plantilla de ejemplo al crear una aplicación nueva, se proporciona un tablero enriquecido de funciones de AEM Mobile.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>Para administrar el contenido de su aplicación y aplicación móvil desde el Centro de control de aplicaciones de AEM Mobile, consulte la [Panel de aplicaciones de AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## Creación de plantillas de aplicación {#creating-app-templates}

Las plantillas de aplicación se usan para crear una aplicación nueva y actúan como una colección de plantillas de página y componentes que representan una línea de base o una base de una aplicación. La plantilla marca algunas propiedades fundamentales para dirigir la aplicación de la forma adecuada. En general, un cliente no crearía demasiadas aplicaciones en total.

Las plantillas de aplicación proporcionan una manera sencilla de aprovechar los diseños existentes creados por los desarrolladores y utilizados para la creación de nuevas aplicaciones en AEM.

Al crear una aplicación nueva basada en la plantilla de otra aplicación, obtendrá una aplicación que tenga un punto de partida representativo de la aplicación desde la que se creó.

Pasos para crear una aplicación nueva basada en una plantilla de aplicación:

1. Vaya al catálogo de aplicaciones de AEM Mobile: *&lt;server-url>/aem/apps.html/content/mobileapps*
1. Select **Crear** —> **Aplicación** como se muestra a continuación

Una vez que haya creado una aplicación con esta plantilla, puede agregar artículos, banners y colecciones a la aplicación. Para volver a visitar, crear artículos, titulares y colecciones, consulte [Acciones de administración de contenido](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>También puede seleccionar una plantilla de aplicación de ejemplo, por ejemplo **We.Unlimited** aplicación, que un desarrollador de AEM le ha puesto a su disposición. Si utiliza esta plantilla de ejemplo para su aplicación, obtendrá algunos artículos y colecciones de ejemplo en los que trabajar. Tendrá la opción de usar las plantillas y los componentes de ejemplo, personalizar los existentes o crear otros nuevos para la aplicación.

>[!CAUTION]
>
>Configuración ***redirectTarget*** property
>
>Al usar una de las plantillas de aplicación, el desarrollador define el contenido de la aplicación. Sin embargo, el desarrollador debe saber dónde se crea la aplicación en el jcr y el valor de ***redirectTarget*** propiedad.
>
>La variable ***redirectTarget*** se calcula como parte de la operación crear aplicación y se intenta resolver una ruta, si hay una propiedad redirectTarget disponible como parte de la plantilla de aplicación y el valor de redirectTarget se define como relativo. Cuando el proceso de creación de la aplicación encuentra un valor relativo para redirectTarget en la plantilla de la aplicación, el valor se anexa a la ubicación resuelta en la que se creó la aplicación.
>
>Por ejemplo, si una plantilla de aplicación define una ***redirectTarget*** con el valor &quot;*administrador de idiomas/en*&quot;, y la aplicación se creó en &quot;*/content/mobileapps/fooApp*&quot;, el valor final para redirectTarget después de crear la aplicación será &quot;*/content/mobileapps/fooApp/language-masters/en*&quot;.

## Creación de plantillas de contenido {#creating-content-templates}

Cada tipo de entidad tiene dos plantillas listas para usar. Estos son:

* **Plantillas predeterminadas:** se utiliza para la creación de contenido con propiedades/estructura predeterminadas aplicables
* **Plantillas importadas:** se utiliza para importar contenido de AEM Mobile con propiedades/estructura predeterminadas aplicables

### Plantillas de artículo {#article-templates}

El artículo ilimitado es una plantilla de ejemplo que representa un diseño de artículo típico de AEM Mobile On-Demand.

1. Haga clic en **+** en **Administrar artículos** para crear un artículo nuevo. Puede elegir una **Artículo ilimitado** o **Artículo de texto enriquecido**. La siguiente imagen muestra la opción que le permite elegir entre cualquiera de estas dos plantillas de artículo.

1. Haga clic en **Siguiente** para definir metadatos de artículos como Nombre/título del artículo, Descripción, Autor, Resumen, Departamento, Imagen en miniatura, Acceso a artículos, etc.
1. Haga clic en **Siguiente** para rellenar las propiedades del anuncio.
1. Haga clic en **Siguiente** para introducir la imagen del artículo o la imagen de medios sociales
1. Haga clic en **Siguiente** para elegir un vínculo de recopilación, este nuevo artículo a.
1. Haga clic en **Siguiente** para introducir los detalles del uso compartido en redes sociales.
1. Haga clic en **Crear** para finalizar el proceso de creación de un artículo utilizando el ejemplo. Haga clic en **Listo** o **Editar artículo** para editar las propiedades de este artículo.

![chlimage_1-71](assets/chlimage_1-71.png)

### Adición de componentes al artículo {#adding-components-to-article}

Una vez creado, un autor puede editar el contenido de un artículo añadiendo componentes como texto e imágenes. Los artículos son una extensión de AEM plantillas de página.

Seleccione un artículo que desee editar y haga clic en **Editar** para añadir componentes al artículo.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

Elija el **+**&#39; en el panel izquierdo para añadir componentes al artículo.

![chlimage_1-74](assets/chlimage_1-74.png)

### Creación de plantillas integradas {#creating-out-of-the-box-templates}

No hay plantillas de artículo predeterminadas; sin embargo, hay una plantilla predeterminada que se debe ampliar; consulte Geometrixx Unlimited Aplicación [Ejemplo de plantilla de artículo](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article).

Entre las propiedades clave más allá de la plantilla AEM normal se incluyen las propiedades requeridas;

***dps-resourceType=&quot;dps:Article&quot;***

Esta propiedad garantiza que la página AEM se reconozca como página de artículos segmentados de AEM Mobile.

Según AEM plantillas, puede agregar cualquier propiedad predeterminada o nodo secundario al ***jcr:content***.

### Plantillas de pancarta y colección {#banner-and-collection-templates}

>[!CAUTION]
>
>Los titulares y las colecciones no tienen contenido, por lo que su creación no admite plantillas personalizadas.

## Creación y adición de componentes {#creating-and-adding-components}

Los componentes utilizan y permiten el acceso a los widgets, que se utilizan para procesar el contenido.

Se incluye un componente simple en el repositorio de código, cuya fuente se puede encontrar en AEM. Posteriormente, también se puede abrir localmente en CRXDE Lite.

>[!NOTE]
>
>Actualmente no hay componentes integrados proporcionados para AEM Mobile.

Puede añadir componentes a la página. Cualquier componente puede utilizarse en una aplicación de AEM Mobile, pero cuando se aplica, puede que no se represente correctamente.

Sin embargo, es posible que los componentes personalizados no exporten ni carguen correctamente en AEM Mobile On-demand Services sin un controlador de sincronización de contenido de exportación personalizado que se muestre en AEM.

Una vez que el componente ya se ha incluido en una página AEM, junto con otros componentes de bloque de creación, puede añadir otro componente a la página o editar uno existente.

**Para añadir otro componente a la página:**

1. Elija esa página y asegúrese de que está en el modo de edición, a través del menú desplegable en la parte superior derecha del encabezado del editor
1. Alternar el panel lateral con el icono situado más a la izquierda en el encabezado del editor
1. Seleccione el **Componentes** ficha
1. Arrastre y suelte uno de los componentes disponibles en la página

![chlimage_1-75](assets/chlimage_1-75.png)

**Para editar un componente existente:**

1. Elija esa página y asegúrese de que está en **Editar** y seleccione el componente
1. Pulse el icono de llave inglesa para configurar el componente

>[!NOTE]
>
>Puede crear un componente en AEM y personalizarlo utilizando [Desarrollo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Una vez que haya personalizado el componente existente según sus necesidades, puede agregarlo a su página utilizando la variable **Editar** opción bajo **Administrar artículos** como se muestra en la figura anterior.

>[!NOTE]
>
>Consulte [Prácticas recomendadas para el desarrollo de plantillas y componentes](/help/mobile/best-practices-aem-mobile.md) en AEM Mobile.

### Pasos siguientes {#the-next-steps}

* [Uso de las propiedades de contenido para exportar contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
