---
title: Creación y edición de aplicaciones mediante la consola Aplicaciones
seo-title: Creating and Editing Apps Using the Apps Console
description: Siga esta página para obtener más información sobre la creación y edición de aplicaciones mediante la consola de aplicaciones.
seo-description: Follow this page to learn about creating and editing apps using apps console.
uuid: 4f7db978-ae2b-4ca6-89f1-26e091d9140a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 9890d045-cead-4d70-b797-95319284e0d8
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2615'
ht-degree: 0%

---

# Creación y edición de aplicaciones mediante la consola Aplicaciones{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El proceso AEM de desarrollo de aplicaciones móviles reconoce que los usuarios con diferentes conocimientos contribuyen al desarrollo de aplicaciones móviles. El siguiente mapa de procesos ilustra el orden general en el que los autores de contenido y los desarrolladores de aplicaciones realizan tareas.

![imagen_1-10](assets/chlimage_1-10.gif)

En esta página se muestra información sobre cómo realizar las tareas de experto en marketing. Para obtener información sobre las tareas de desarrollador, consulte Creación de aplicaciones PhoneGap.

## La estructura de las aplicaciones móviles {#the-structure-of-mobile-applications}

AEM Mobile proporciona el modelo de aplicación Phonegap para la creación de aplicaciones móviles. El modelo define la estructura de las aplicaciones que crea. Las solicitudes constan de los siguientes elementos:

* La página raíz.
* Variaciones de idioma de la aplicación.
* Página de inicio de la variación de idioma.

### La raíz de una aplicación PhoneGap {#the-root-of-a-phonegap-app}

La página raíz de las aplicaciones móviles que crea en AEM aparece en la consola Aplicaciones .

La página raíz se almacena debajo de la propiedad Ruta de destino de la aplicación que se especificó al crear la aplicación (la ruta predeterminada es /content/phonegap/apps). El nombre de página es la propiedad Name de la aplicación. Por ejemplo, la dirección URL predeterminada de la página raíz del sitio con el nombre `myphonegapapp` es `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### La variación de idioma de una aplicación PhoneGap {#the-language-variation-of-a-phonegap-app}

Las primeras páginas secundarias de la página raíz son las variaciones de idioma de la aplicación. El nombre de cada página es el idioma en el que se crea la aplicación. Por ejemplo, English es el nombre de la variación en inglés de la aplicación.

**Nota:** El modelo predeterminado de PhoneGap crea solo una aplicación en inglés. El desarrollador puede modificar el modelo para que pueda crear más variaciones de idioma.

![chlimage_1-147](assets/chlimage_1-147.png)

La página de idioma tiene dos propósitos:

* El contenido de la página es la página de paso para la variación de idioma de la aplicación.
* Las propiedades de página controlan varios aspectos de diseño de la aplicación, como la URL que se utiliza para solicitar actualizaciones de contenido y la información sobre la conexión a la versión de nube y la integración de Adobe Analytics Services.

![chlimage_1-148](assets/chlimage_1-148.png)

### La página principal {#the-home-page}

Cuando se abre la aplicación, aparece la página de inicio o la página index.html de una variación de idioma de una aplicación. La página de inicio proporciona a los usuarios un menú de vínculos a varias páginas de la aplicación. El sistema de párrafos le permite añadir componentes a la página para crear contenido.

## Creación de una aplicación móvil {#creating-a-mobile-application}

Las aplicaciones móviles se basan en un modelo que define una estructura y propiedades de página. Puede configurar las siguientes propiedades de aplicación:

* **Título:** El título de la aplicación.
* **Ruta de destino:** Ubicación en el repositorio donde se almacena la aplicación. Deje el valor predeterminado para crear una ruta basada en el nombre de la aplicación.

* **Nombre:** El valor predeterminado es el valor de la propiedad Título con caracteres de espacio eliminados. El nombre se utiliza dentro de CQ para hacer referencia a la aplicación, por ejemplo para el nodo de repositorio que representa la aplicación.
* **Descripción:** Descripción de la aplicación.
* **URL del servidor:** La URL que proporciona actualizaciones de contenido de OTA a la aplicación. El valor predeterminado es la URL del servidor de publicación de la instancia que se utiliza para crear una aplicación (tomada del servicio externalizador). Tenga en cuenta que debe ser una instancia de servidor de publicación en lugar de un autor, que requiere autenticación.

También puede proporcionar un archivo de imagen para utilizarlo como miniatura de la aplicación, seleccionar la configuración de PhoneGap Build que desea utilizar y seleccionar la configuración de análisis de aplicaciones móviles que desea utilizar. Esta imagen solo se utiliza como miniatura para representar la aplicación móvil en la consola de aplicaciones móviles en Experience Manager.

Existen pestañas adicionales (y opcionales) para crear el servicio de nube e integrar el complemento SDK de Adobe Mobile Services en la aplicación.

* Generar: Haga clic en administrar configuraciones y configure el servicio de compilación build.phonegap.com aquí. A continuación, desde la lista desplegable podrá seleccionar el servicio en la nube PhoneGap recién creado.
* Analytics: Haga clic en administrar configuraciones y configure su [SDK de Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) servicio en la nube. A continuación, desde la lista desplegable podrá seleccionar los servicios móviles recién creados para integrarlos en su aplicación móvil.

>[!NOTE]
>
>Los desarrolladores pueden utilizar el AEM PhoneGap Starter Kit para crear aplicaciones y agregarlas a la consola.

El siguiente procedimiento utiliza la IU táctil para crear una aplicación móvil.

1. En el carril , haga clic en Aplicaciones.
1. Toque o haga clic en el icono Crear .

   ![](do-not-localize/chlimage_1-7.png)

1. (Opcional) En la ficha Avanzado , proporcione una descripción para la aplicación y cambie la URL del servidor si es necesario.
1. (Opcional) Si está utilizando PhoneGap Build para compilar la aplicación, en la ficha Compilación , seleccione la Configuración que desea utilizar.

   Para crear una configuración de compilación de PhoneGap, haga clic en Administrar configuraciones.

1. (Opcional) Si utiliza SiteCatalyst para rastrear la actividad de la aplicación, en la pestaña Analytics , seleccione la configuración que desee utilizar.

   Para crear una configuración de aplicación móvil, haga clic en Administrar configuraciones.

1. (Opcional) Para proporcionar un icono de aplicación, haga clic en el botón Examinar, seleccione el archivo de imagen del sistema de archivos y haga clic en Abrir.
1. Haga clic en Crear.

### Cambio de las propiedades de una aplicación móvil {#changing-the-properties-of-a-mobile-application}

Después de crear una aplicación móvil, puede cambiar las propiedades.

#### Cambiar el título, la descripción y el icono {#change-the-title-description-and-icon}

1. En el carril, toque o haga clic en Aplicaciones.
1. Seleccione la aplicación que desea configurar y haga clic en el icono Ver propiedades de página .

   ![](do-not-localize/chlimage_1-8.png)

1. Para cambiar los valores de las propiedades, toque o haga clic en el icono Editar .

   ![](do-not-localize/chlimage_1-9.png)

1. Configure las propiedades Básico y Avanzado y, a continuación, toque o haga clic en el icono Listo .

   ![](do-not-localize/chlimage_1-10.png)

#### Configurar una variación de idioma de la aplicación {#configure-a-language-variation-of-the-application}

1. En el carril, toque o haga clic en Aplicaciones.
1. Haga clic en para explorar en profundidad la aplicación móvil que desea editar en la consola de administración de aplicaciones. Seleccione la versión de idioma de la aplicación para configurarla y haga clic en el icono Ver propiedades de la aplicación .

   ![](do-not-localize/chlimage_1-11.png)

1. Para cambiar los valores de las propiedades, toque o haga clic en el icono Editar .

   ![](do-not-localize/chlimage_1-12.png)

1. Configure las propiedades en las fichas Básico, Avanzado, Generar y Analytics y, a continuación, toque o haga clic en el icono Listo .

   ![](do-not-localize/chlimage_1-13.png)

### Creación del contenido de una aplicación móvil {#authoring-the-content-of-a-mobile-application}

Después de crear la aplicación móvil, añada contenido que se utilice como interfaz de usuario de la aplicación.

1. En el carril, toque o haga clic en Aplicaciones.
1. Toque o haga clic en la aplicación y, a continuación, toque o haga clic en inglés.
1. Edite la página principal o agregue las páginas secundarias que sean necesarias.

### Mover contenido a aplicaciones móviles {#moving-content-to-mobile-applications}

La caché de sincronización de contenido de la instancia de publicación de AEM se utiliza como repositorio de contenido para aplicaciones móviles:

* El contenido de la caché de Content Sync se incluye en la aplicación cuando los desarrolladores compilan la aplicación.
* El contenido de la caché está disponible para las aplicaciones móviles instaladas para actualizar el contenido de la aplicación.

Las aplicaciones móviles incluyen un comando Actualizaciones que descarga e instala el contenido actualizado de la aplicación. Cuando una instancia de aplicación envía una solicitud de actualización, la sincronización de contenido determina qué contenido ha cambiado desde la última vez que se actualizó o instaló la aplicación y proporciona el nuevo contenido.

![chlimage_1-149](assets/chlimage_1-149.png)

Para que el contenido actualizado esté disponible para las aplicaciones, actualice la caché de sincronización de contenido. La primera vez que actualice la caché, se añadirá todo el contenido publicado. Las actualizaciones posteriores agregan solo el contenido publicado que ha cambiado desde la actualización anterior.

La sincronización de contenido también rastrea cuándo se producen las actualizaciones. Con esta información, la sincronización de contenido puede determinar qué actualización de caché se enviará a una aplicación móvil.

Realice el siguiente procedimiento en la instancia en la que desea actualizar la caché. Por ejemplo, si la aplicación solicita actualizaciones de la instancia de publicación, realice el procedimiento en la instancia de publicación.

1. En el carril, toque o haga clic en Aplicaciones y, a continuación, toque o haga clic en su aplicación.
1. Seleccione la página de inicio y, a continuación, toque o haga clic en el icono Actualizar caché .

   ![](do-not-localize/chlimage_1-14.png)

### Uso de plantillas de aplicación {#using-app-templates}

Esta función está disponible con el paquete de funciones 2 de las aplicaciones 6.1 y ofrece una forma sencilla de aprovechar las plantillas de aplicación existentes para crear nuevas aplicaciones en AEM.

¿Qué es una plantilla de aplicación? Piense en ella como una colección de plantillas de página y componentes que representan una línea de base o una base de una aplicación.
Al crear una aplicación nueva basada en la plantilla de otra aplicación, obtendrá una aplicación que tenga un punto de partida representativo de la aplicación desde la que se creó.

Debe tener una plantilla de aplicación móvil existente (o una aplicación instalada que tenga una plantilla de aplicación) para poder usar esta función.

El último paquete de muestras de AEM Apps 6.1 incluye una versión actualizada de la aplicación de Geometrixx con una plantilla de aplicación. Como alternativa, puede instalar el StarterKit que también proporciona una plantilla.

Pasos para crear una aplicación nueva basada en una plantilla de aplicación:

1. Asegúrese de tener instalados el paquete de funciones y los paquetes de muestras de referencia de las aplicaciones de AEM 6.1 más recientes
1. Haga clic en Aplicaciones desde el carril izquierdo.

![Chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Haga clic en el botón + Crear en la parte superior y seleccione Crear aplicación.
1. Una vez que se le presente la lista de plantillas de aplicación, seleccione una:

![Chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Haga clic en Siguiente.
1. Proporcione un Id. de aplicación y un Título, aunque puede que desee incluir también un Nombre y una Descripción.

   1. Además, puede proporcionar un PNG (formato de icono de PhoneGap compatible) como icono navegando por AEM recursos.
   1. Recuerde que puede editar todos estos campos una vez creada la aplicación en el mosaico Administrar aplicación . Con la excepción del ID de aplicación, una vez configurado el ID de aplicación, no puede cambiarlo.

![chlimage_1-150](assets/chlimage_1-150.png)

1. Haga clic en el botón crear y se le presentarán dos opciones: Listo (vuelva a la vista del catálogo de aplicaciones) o Administrar aplicación (abra el panel de la aplicación).
1. Una vez creada, debería ver la nueva aplicación en el catálogo de aplicaciones:

![Chlimage_1-3](assets/chlimage_1-3.jpeg)

1. Haga clic en la aplicación para abrirla. Ha creado correctamente una nueva aplicación basada en la plantilla de una aplicación existente.

>[!NOTE]
>
>Si desinstala el paquete de aplicación de referencia de los Geometrixx Outdoors de AEM y tiene una aplicación creada en función de su plantilla, dicha aplicación ya no funcionará. La aplicación de Geometrixx Outdoors se puede eliminar, pero la plantilla de aplicación debe permanecer si la usan otras aplicaciones móviles.

## Exploración de la aplicación de Geometrixx Outdoors de muestra {#exploring-the-sample-geometrixx-outdoors-app}

La aplicación Geometrixx Outdoors es una aplicación PhoneGap de ejemplo que muestra las características del modelo predeterminado de la aplicación PhoneGap y los componentes móviles de ejemplo.

Para abrir la aplicación, en el carril haga clic en Aplicaciones móviles y, a continuación, seleccione Aplicación de Geometrixx Outdoors .

### Funciones comunes de la página: aplicación móvil de Geometrixx {#common-page-features-geometrixx-mobile-app}

Cada página de la aplicación móvil incluye las siguientes funciones:

* Botón Atrás para volver a la página principal. Tenga en cuenta que el botón Atrás no aparece en la página de inicio.
* Un carril expandible que ofrece un menú de comandos y vínculos:

   * Abra la página Ubicaciones .
   * Abra el carro de compras.
   * Inicie sesión.
   * Actualice la aplicación.

* El sistema de párrafos, para añadir componentes y crear contenido.

### Página principal: aplicación móvil de Geometrixx {#the-home-page-geometrixx-mobile-app}

El contenido de la página principal consta de las siguientes herramientas de navegación:

* Componente Lista de menús que proporciona vínculos a las páginas secundarias Engranaje, Reseñas, Noticias y Acerca de nosotros.
* Componente de carrusel de barrido que muestra las páginas secundarias.

### La página del engranaje: aplicación móvil de Geometrixx {#the-gear-page-geometrixx-mobile-app}

La página Engranaje proporciona a los usuarios acceso a las páginas de producto. Un componente Lista de menús proporciona acceso a las páginas secundarias de la página Engranaje. Las páginas secundarias son categorías de productos que incluye el sitio web.

* Temporada
* Ropa
* Sexo
* Actividad

Cada página de categoría utiliza la misma estructura de contenido que la página Engranaje . El carrusel proporciona acceso a páginas secundarias que son subcategorías de productos. Las páginas de subcategoría contienen listas de productos que proporcionan vínculos a páginas de productos.

### La página Productos: aplicación móvil de Geometrixx {#the-products-page-geometrixx-mobile-app}

La página Productos y su jerarquía de páginas secundarias implementan un sistema de clasificación para páginas de productos. Las páginas más bajas de cada rama de la jerarquía son una página de producto que contiene un componente de producto ng.

La página Productos no está disponible para los usuarios de la aplicación. La página Engranaje proporciona acceso a cada página de producto.

### Página Reseñas: Aplicación Móvil De Geometrixx {#the-reviews-page-geometrixx-mobile-app}

Contiene un botón Atrás. El sistema de párrafos le permite añadir componentes.

Al utilizar la aplicación, la página Reseñas está disponible en el carrusel de la página en inglés.

### Página de noticias: aplicación móvil de Geometrixx {#the-news-page-geometrixx-mobile-app}

Contiene un botón Atrás. El sistema de párrafos le permite añadir componentes.

Al utilizar la aplicación, la página Noticias está disponible desde el carrusel en la página en inglés.

### La página Acerca de nosotros: aplicación móvil de Geometrixx {#the-about-us-page-geometrixx-mobile-app}

La página Acerca de nosotros contiene varios componentes de fila de dos columnas . Cada columna contiene un componente Imagen o Texto . Los componentes son editables y el sistema de párrafos le permite añadir componentes.

Al utilizar la aplicación, la página Acerca de nosotros está disponible en el carrusel de la página en inglés.

### La página Ubicaciones: Aplicación móvil de Geometrixx {#the-locations-page-geometrixx-mobile-app}

La página Ubicaciones contiene un componente Ubicaciones .

Al utilizar la aplicación, la página Ubicaciones está disponible en la lista de menús de la página en inglés.

## Componentes móviles de muestra {#sample-mobile-components}

Hay varios componentes disponibles de forma inmediata en la barra de tareas al crear las páginas de una aplicación móvil. Los componentes pertenecen al grupo de componentes PhoneGap.

### Carrusel de barrido {#swipe-carousel}

El componente Carrusel de barrido es una herramienta para mostrar y navegar por las páginas del sitio. El componente incluye un carrusel que recorre las imágenes de las páginas situadas encima de una lista de vínculos de página. Edite el componente para especificar las páginas que desea mostrar y el comportamiento del carrusel.

Tenga en cuenta que las imágenes aparecen en el carrusel para las páginas que están asociadas a una imagen de una manera específica. Cuando las páginas no están asociadas con imágenes, solo aparece la lista de vínculos.

![chlimage_1-151](assets/chlimage_1-151.png)

**Pestaña Propiedades del carrusel**

Configure el comportamiento del carrusel:

* Velocidad de reproducción: Tiempo en milisegundos que cada imagen se muestra antes de mostrar la siguiente imagen.
* Tiempo de transición: Duración en milisegundos de la animación para transiciones de imágenes.
* Estilo de controles: Tipo de controles que se proporcionan para el desplazamiento entre imágenes.

**Ficha Propiedades de lista**

Especifique cómo se genera la lista de páginas:

* Lista de creación mediante: Método que se debe utilizar para especificar las páginas que se incluirán en el carrusel. Consulte Creación de la lista de páginas .
* Ordenar por: Seleccione una propiedad de página para utilizarla para ordenar la lista de páginas. Por ejemplo, seleccione jcr:title para ordenar las páginas alfabéticamente por título.
* Límite: Número máximo de páginas que se van a incluir. Esta propiedad es adecuada para métodos de búsqueda para crear la lista de páginas.

#### Creación de la lista de páginas {#building-the-page-list}

El componente Carrusel de barrido proporciona los siguientes valores para la propiedad Uso de la lista de compilación . El cuadro de diálogo de edición cambia según el valor que seleccione:

**Páginas secundarias**

El componente enumera todas las páginas secundarias de una página específica. Después de seleccionar este valor, seleccione la página en la ficha Páginas secundarias o especifique ningún valor para enumerar los elementos secundarios de la página actual.

**Lista fija**

Especifique una lista de páginas de inclusión. Después de seleccionar este valor, configure la lista en la ficha Lista fija que aparece al seleccionar Lista fija:

* Para agregar una página, haga clic en Agregar elemento y luego busque la página.
* Utilice los iconos de flecha hacia arriba y hacia abajo para mover la página dentro de la lista.
* Haga clic en el botón Eliminar para eliminar una página de la lista.

La propiedad Ordenar por no afecta al orden de las listas fijas.

**Buscar**

Rellene la lista con los resultados de una búsqueda de palabras clave. La búsqueda se realiza en los elementos secundarios de una página que especifique:

1. Para especificar la página raíz de la búsqueda, utilice la propiedad Iniciar en para seleccionar la ruta de la página. No especifique ninguna ruta para buscar debajo de la página actual.
1. En la propiedad Consulta de búsqueda , introduzca las palabras clave de búsqueda.

**Búsqueda avanzada**

Rellene la lista con un [Querybuilder](/help/sites-developing/querybuilder-api.md) consulta.

### Imagen {#image}

Añada una imagen al contenido de la aplicación.

### Texto {#text}

Agregue texto enriquecido al contenido de la aplicación.

### Ubicaciones de almacenes de campañas {#store-locations}

El componente Ubicaciones de la tienda proporciona a los usuarios herramientas para encontrar puntos de venta comerciales:

* Búsqueda
* Listas de ubicaciones cercanas o distantes a las coordenadas GPS del dispositivo.

El componente requiere que el repositorio contenga información de ubicación para cada almacén. Las ubicaciones de muestra se instalan en el nodo /etc/commerce/locations/adobe . ![chlimage_1-152](assets/chlimage_1-152.png)

### Fila de dos columnas {#two-column-row}

Permite agregar componentes en paralelo a una página.

![chlimage_1-153](assets/chlimage_1-153.png)
