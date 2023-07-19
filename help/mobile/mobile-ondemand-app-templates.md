---
title: Crear y agregar plantillas y componentes
seo-title: Creating and Adding Templates and Components
description: Siga esta página para obtener más información sobre la creación y adición de plantillas y componentes a la aplicación. La página utiliza la aplicación de Geometrixx Unlimited como la aplicación que contiene una plantilla de aplicación de ejemplo y plantillas de página.
seo-description: Follow this page to learn about creating and adding templates and components to your app. The page uses Geometrixx Unlimited App as the app that contains a sample app template and page templates.
uuid: 3a93017c-8094-413f-a01c-9b72025a2b20
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ec4ada04-e429-4ad4-a060-2dccac847cf0
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# Crear y agregar plantillas y componentes {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

AEM Mobile On-Demand proporciona una plantilla de aplicación completamente configurada, una plantilla de artículo y componentes de artículo.

La aplicación We.Unlimited es una plantilla de ejemplo que representa el shell de una aplicación de AEM Mobile On-Demand totalmente configurable y manejable.

Al seleccionar esta plantilla de muestra al crear una nueva aplicación, se muestra un panel con numerosas funciones de AEM Mobile.

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>Para administrar el contenido de su aplicación y aplicación móvil desde el Centro de control de aplicaciones de AEM Mobile, consulte la [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

## Creación de plantillas de aplicación {#creating-app-templates}

Una plantilla de aplicación se utiliza para crear una nueva aplicación y actúa como una colección de plantillas de página y componentes que representan una línea de base o una base de una aplicación. La plantilla elimina algunas propiedades fundamentales para guiar a la aplicación de la manera adecuada. En general, un cliente no crearía demasiadas aplicaciones en total.

AEM Las plantillas de aplicación ofrecen una forma sencilla de aprovechar los diseños existentes creados por desarrolladores y utilizados para la creación de nuevas aplicaciones dentro de los programas de desarrollo de aplicaciones de la aplicación de la aplicación de la plataforma de creación de aplicaciones de la plataforma de creación de aplicaciones de.

Al crear una aplicación nueva basada en la plantilla de otra aplicación, obtendrá una aplicación que tenga un punto de partida representativo de la aplicación en la que se creó.

Pasos para crear una nueva aplicación basada en una plantilla de aplicación:

1. Vaya al catálogo de aplicaciones de AEM Mobile: *&lt;server-url>/aem/apps.html/content/mobileapps*
1. Seleccionar **Crear** —> **Aplicación** como se muestra a continuación

Una vez creada una aplicación con esta plantilla, puede agregar artículos, titulares y colecciones a la aplicación. Para volver a visitar, crear artículos, titulares y colecciones, consulte [Acciones de administración de contenido](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

>[!NOTE]
>
>También puede seleccionar una plantilla de aplicación de ejemplo, por ejemplo **We.Unlimited** AEM aplicación, puesta a su disposición por un desarrollador de. Si utiliza esta plantilla de ejemplo para su aplicación, obtendrá algunos artículos y colecciones de ejemplo para trabajar. Tendrá la opción de utilizar las plantillas y los componentes de ejemplo, personalizar los existentes o crear nuevos para la aplicación.

>[!CAUTION]
>
>Configuración ***redirectTarget*** propiedad
>
>Al utilizar una de las plantillas de aplicación, el desarrollador define el contenido de la aplicación. Sin embargo, el desarrollador debe tener en cuenta dónde se crea la aplicación en jcr y el valor de ***redirectTarget*** propiedad.
>
>El ***redirectTarget*** se calcula como parte de la operación crear aplicación e intenta resolver una ruta si hay una propiedad redirectTarget disponible como parte de la plantilla de aplicación y el valor de redirectTarget se define como relativo. Cuando el proceso Crear aplicación encuentra un valor relativo para redirectTarget en la plantilla de aplicación, el valor se anexa a la ubicación resuelta de donde se creó la aplicación.
>
>Por ejemplo, si una plantilla de aplicación define una ***redirectTarget*** con un valor de &quot;*language-masters/es*&quot;, y la aplicación se creó en &quot;*/content/mobileapps/fooApp*&quot;, el valor final para redirectTarget después de crear la aplicación será &quot;*/content/mobileapps/fooApp/language-masters/es*&quot;.
>

## Creación de plantillas de contenido {#creating-content-templates}

Cada tipo de entidad tiene dos plantillas predeterminadas. Estos son:

* **Plantillas predeterminadas:** se utiliza para la creación de contenido con propiedades/estructura predeterminadas aplicables
* **Plantillas importadas:** se utiliza para importar contenido desde AEM Mobile con las propiedades/estructura predeterminadas aplicables

### Plantillas de artículo {#article-templates}

El artículo de Unlimited es una plantilla de muestra que representa un diseño de artículo típico de AEM Mobile On-Demand.

1. Haga clic en **+** in **Administrar artículos** para crear un nuevo artículo. Puede elegir una de estas opciones **Artículo de Unlimited** o una **Artículo de texto enriquecido**. La siguiente imagen muestra la opción que le permite elegir entre cualquiera de estas dos plantillas de artículo.

1. Clic **Siguiente** para definir metadatos de artículo, como nombre/título del artículo, descripción, autor, resumen, departamento, imagen en miniatura, acceso a artículos, etc.
1. Clic **Siguiente** para rellenar Propiedades del anuncio.
1. Clic **Siguiente** para introducir la imagen del artículo o la imagen de medios sociales
1. Clic **Siguiente** para elegir una colección, vincule este nuevo artículo a.
1. Clic **Siguiente** para introducir los detalles de uso compartido en medios sociales.
1. Clic **Crear** para finalizar el proceso de creación de un artículo con el ejemplo. Haga clic en **Listo** o **Editar artículo** para editar las propiedades de este artículo.

![chlimage_1-71](assets/chlimage_1-71.png)

### Agregar componentes al artículo {#adding-components-to-article}

Una vez creado, un autor puede editar el contenido de un artículo añadiendo componentes como texto e imágenes. AEM Los artículos son una extensión de las plantillas de página de la página de.

Seleccione un artículo que quiera editar y haga clic en **Editar** para agregar componentes al artículo.

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

Elija el &#39;**+**&quot; en el panel izquierdo para agregar componentes al artículo.

![chlimage_1-74](assets/chlimage_1-74.png)

### Creación de plantillas listas para usar {#creating-out-of-the-box-templates}

No hay plantillas de artículo listas para usar, pero hay una plantilla predeterminada que las plantillas personalizadas deben ampliar, consulte Plantillas de Geometrixx Unlimited [Muestra de plantilla de artículo](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article).

AEM Las propiedades clave más allá de las propiedades requeridas de la plantilla de normal incluyen:

***dps-resourceType=&quot;dps:Article&quot;***

AEM Esta propiedad garantiza que la página de destino de la página se reconozca como una página de artículo de destino de AEM Mobile.

AEM Según las plantillas de la plantilla, puede agregar cualquier propiedad predeterminada o nodo secundario a la plantilla ***jcr:contenido***.

### Plantillas de banner y colección {#banner-and-collection-templates}

>[!CAUTION]
>
>Los titulares y las colecciones no tienen contenido, por lo que su creación no admite plantillas personalizadas.

## Crear y agregar componentes {#creating-and-adding-components}

Los componentes utilizan y permiten el acceso a los widgets, que se utilizan para representar el contenido.

AEM En el repositorio de código se incluye un componente simple, cuyo origen se puede encontrar en la sección de componentes de la interfaz de usuario de. Posteriormente, también se puede abrir localmente en CRXDE Lite.

>[!NOTE]
>
>Actualmente no hay componentes listos para usar proporcionados para AEM Mobile.
>

Puede añadir componentes a la página. Cualquier componente se puede utilizar en una aplicación de AEM Mobile, pero cuando se aplica, es posible que no se represente correctamente.

Sin embargo, es posible que los componentes personalizados no se exporten y carguen en AEM Mobile On-demand Services AEM correctamente sin un controlador de sincronización de contenido de exportación personalizado que se procese en la.

AEM Una vez que el componente ya se ha incluido en una página de creación, junto con otros componentes de bloque de creación, puede agregar otro componente a la página o editar uno existente.

**Para agregar otro componente a la página:**

1. Elija esa página y asegúrese de que está en el modo de edición, a través del menú desplegable en la parte superior derecha del encabezado del editor
1. Cambie el panel lateral utilizando el icono situado más a la izquierda en el encabezado del editor
1. Seleccione el **Componentes** pestaña
1. Arrastre y suelte uno de los componentes disponibles en la página

![chlimage_1-75](assets/chlimage_1-75.png)

**Para editar un componente existente:**

1. Elija esa página y asegúrese de que está en **Editar** y seleccione el componente
1. Pulse el icono de la llave inglesa para configurar el componente

>[!NOTE]
>
>AEM Puede crear un componente en y personalizar el mismo en [Desarrollo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Una vez que haya personalizado el componente existente según sus necesidades, puede añadirlo en su página utilizando **Editar** opción en **Administrar artículos** como se muestra en la figura anterior.

>[!NOTE]
>
>Consulte [Prácticas recomendadas para el desarrollo de plantillas y componentes](/help/mobile/best-practices-aem-mobile.md) en AEM Mobile.

### Pasos siguientes {#the-next-steps}

* [Uso de propiedades de contenido para exportar contenido](/help/mobile/on-demand-content-properties-exporting.md)
* [Móvil con sincronización de contenido](/help/mobile/mobile-ondemand-contentsync.md)
