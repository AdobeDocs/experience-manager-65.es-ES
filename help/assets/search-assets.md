---
title: Buscar recursos e imágenes digitales en AEM
description: Obtenga información sobre cómo encontrar los recursos necesarios en AEM mediante el panel Filtros y cómo utilizar los recursos que aparecen en la búsqueda.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Buscar recursos en AEM {#search-assets-in-aem}

Recursos Adobe Experience Manager (AEM) proporciona métodos sólidos de detección de recursos que le ayudan a lograr una mayor velocidad de contenido. Sus equipos reducen el tiempo de salida al mercado con una experiencia de búsqueda inteligente y sin inconvenientes utilizando la funcionalidad lista para usar y los métodos personalizados. La búsqueda de recursos es fundamental para el uso de un sistema de gestión de activos digitales, ya sea para su uso ulterior por parte de los creativos, para una gestión sólida de los recursos por parte de los usuarios y especialistas en marketing del negocio o para la administración por parte de los administradores de DAM. Las búsquedas simples, avanzadas y personalizadas que puede realizar mediante la interfaz de usuario de Recursos AEM u otras aplicaciones y superficies ayudan a cumplir estos casos de uso.

AEM admite los siguientes casos de uso y en este artículo se describen el uso, los conceptos, las configuraciones, las limitaciones y la resolución de problemas de estos casos de uso.

| Búsqueda de recursos | Configuración y administración | Trabajar con resultados de búsqueda |
|---|---|---|
| [Búsquedas básicas](#searchbasics) | [Índice de búsqueda](#searchindex) | [Ordenar resultados](#sort) |
| [Comprender la IU de búsqueda](#searchui) | [Búsqueda visual o de similitudes](#configvisualsearch) | [Comprobar propiedades y metadatos de un recurso](#checkinfo) |
| [Sugerencias de búsqueda](#searchsuggestions) | [Metadatos obligatorios](#mandatorymetadata) | [Descargar](#download) |
| [Comprender los resultados y el comportamiento de la búsqueda](#searchbehavior) | [Modificar facetas de búsqueda](#searchfacets) | [Actualizaciones masivas de metadatos](#metadataupdates) |
| [Buscar clasificación y aumentar](#searchrank) | [Extracción de texto](#extracttextupload) | [Colecciones inteligentes](#collections) |
| [Búsqueda avanzada: filtrado y ámbito de búsqueda](#scope) | [Predicados personalizados](#custompredicates) | [Comprender los resultados inesperados y solucionar problemas](#troubleshoot-unexpected-search-results-and-issues) |
| [Buscar desde otras soluciones y aplicaciones](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[Aplicación de escritorio de AEM](#desktopapp)</li><li>[Imágenes de Adobe Stock](#adobestock)</li><li>[Recursos de Dynamic Media](#dynamicmedia)</li></ul> |  |  |
| [Selector/selector de recursos](#assetselector) |  |  |
| [Limitaciones](#limitations) y [sugerencias](#tips) |  |  |
| [Ejemplos ilustrados](#samples) |  |  |

Busque recursos utilizando el campo Omniture en la parte superior de la interfaz web de AEM. Vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]** en AEM, haga clic en el icono de búsqueda de la barra superior, introduzca la palabra clave de búsqueda y pulse Retorno. Alternativamente, utilice el método abreviado de palabra clave / (barra diagonal) para abrir el campo Omniture Search. Ubicación:Recursos está preseleccionado para limitar las búsquedas a recursos DAM. AEM proporciona sugerencias para empezar a escribir una palabra clave de búsqueda.

Utilice el panel **[!UICONTROL Filtros]** para limitar la búsqueda filtrando los resultados de la búsqueda según las distintas opciones (predicados), como el tipo de archivo, el tamaño de archivo, la fecha de la última modificación, el estado del recurso, los datos de perspectivas y las licencias de Adobe Stock. Los administradores pueden personalizar el panel Filtros y agregar o eliminar predicados de búsqueda mediante facetas de búsqueda.

La función de búsqueda de AEM admite la búsqueda de colecciones y la búsqueda de recursos dentro de una colección. Consulte [Buscar colecciones](/help/assets/managing-collections-touch-ui.md).

## Comprender la interfaz de búsqueda {#searchui}

Familiarícese con la interfaz de búsqueda y las acciones disponibles.

![Explicación de partes de la interfaz de resultados de búsqueda de recursos](assets/aem_search_results.png)

*Figura: Explicación de partes de la interfaz de resultados de búsqueda de recursos*

**A.** Guarde la búsqueda como una colección inteligente. **B.** Filtros (predicados) para reducir los resultados de búsqueda. **C.** Muestre archivos, carpetas o ambos en los resultados de la búsqueda. **D.** Haga clic en Filtros para abrir o cerrar el carril izquierdo. **E.** La ubicación de búsqueda es DAM. ************ F. Campo Omnisearch con palabra clave de búsqueda proporcionada por el usuario. **G. Casilla de verificación para seleccionar todos los resultados de búsqueda.** H. Número de resultados de búsqueda mostrados del total de resultados de búsqueda. **Yo. Cierre la búsqueda** J. Cambie entre la vista de tarjeta y la vista de lista.

### Facetas de búsqueda dinámica {#dynamicfacets}

Puede descubrir los recursos deseados más rápido desde la página de resultados de búsqueda utilizando el número de resultados de búsqueda esperados que se ha actualizado dinámicamente en las facetas de búsqueda. El número esperado de recursos se actualiza incluso antes de aplicar el filtro de búsqueda. Ver el recuento esperado con el filtro le ayuda a navegar por los resultados de búsqueda de manera rápida y eficiente. Para obtener más información, consulte [Buscar recursos en AEM](search-assets.md).

![Ver el número aproximado de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda.](assets/asset_search_results_in_facets_filters.png)

*Figura:Ver el número aproximado de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda.*

## Comprender los resultados y el comportamiento de la búsqueda {#searchbehavior}

### Términos y resultados de búsqueda básicos {#searchbasics}

Puede ejecutar búsquedas de palabras clave desde el campo OmniSearch. La búsqueda de palabras clave no distingue entre mayúsculas y minúsculas y es una búsqueda de texto completo (en todos los campos de metadatos populares). Si se busca más de una palabra clave, el operador predeterminado entre las palabras clave es `AND` para la búsqueda predeterminada y es `OR` cuando los recursos están etiquetados de forma inteligente.

Los resultados se ordenan por relevancia, empezando por las coincidencias más cercanas. Para varias palabras clave, los resultados más relevantes son los recursos que contienen ambos términos en sus metadatos. Dentro de los metadatos, las palabras clave que aparecen como etiquetas inteligentes se clasifican más que las palabras clave que aparecen en otros campos de metadatos. AEM permite dar mayor peso a un término de búsqueda concreto. Además, es posible [aumentar la clasificación](#searchrank) de unos pocos recursos objetivo para términos de búsqueda específicos.

Para encontrar rápidamente los recursos relevantes, la interfaz enriquecida proporciona mecanismos de filtrado, clasificación y selección. Puede filtrar los resultados en función de varios criterios y ver el número de recursos buscados para varios filtros. De lo contrario, puede volver a ejecutar la búsqueda cambiando la consulta en el campo Omniture Search. Al cambiar los términos o filtros de búsqueda, los demás filtros permanecen aplicados para preservar el contexto de la búsqueda.

Cuando los resultados son muchos recursos, AEM muestra los primeros 100 en la vista de tarjeta y los 200 en la vista de lista. A medida que los usuarios se desplazan, se cargan más recursos. Esto sirve para mejorar el rendimiento.

>[!VIDEO](https://www.youtube.com/watch?v=LcrGPDLDf4o)

A veces, puede ver algunos recursos inesperados en los resultados de búsqueda. Para obtener más información, consulte Resultados [inesperados](#troubleshoot-unexpected-search-results-and-issues).

AEM puede buscar muchos formatos de archivo y los filtros de búsqueda se pueden personalizar para adaptarlos a sus necesidades comerciales. Póngase en contacto con el administrador para saber qué opciones de búsqueda están disponibles para el repositorio de DAM y qué restricciones tiene su cuenta.

### Resultados con y sin etiquetas inteligentes mejoradas {#withsmarttags}

De forma predeterminada, la búsqueda de AEM combina los términos de búsqueda con una cláusula AND. Por ejemplo: considere la búsqueda de palabras clave mujer en ejecución. De forma predeterminada, en los resultados de la búsqueda solo aparecen los recursos con palabras clave principales y las palabras clave en ejecución en los metadatos. El mismo comportamiento se mantiene cuando se utilizan caracteres especiales (puntos, subrayados o guiones) con las palabras clave. Las siguientes consultas de búsqueda devuelven los mismos resultados:

* `woman running`
* `woman.running`
* `woman-running`

Sin embargo, la consulta `woman -running` devuelve recursos sin incluir `running` en sus metadatos.
El uso de etiquetas inteligentes agrega una `OR` cláusula adicional para encontrar cualquiera de los términos de búsqueda como las etiquetas inteligentes aplicadas. Un recurso etiquetado con etiquetas inteligentes `woman` o `running` con etiquetas inteligentes también aparece en una consulta de búsqueda de este tipo. Los resultados de la búsqueda son una combinación de:

* Recursos con `woman` y `running` palabras clave en los metadatos (comportamiento predeterminado).

* Recursos con etiquetas inteligentes con cualquiera de las palabras clave (comportamiento de etiquetas inteligentes).

### Search suggestions as you type {#searchsuggestions}

Al empezar a escribir palabras clave, AEM sugiere las posibles palabras clave o frases de búsqueda. Las sugerencias se basan en los metadatos de los recursos existentes. AEM indexa todos los campos de metadatos para facilitar la búsqueda. Para proporcionar sugerencias de búsqueda, el sistema utiliza los valores de los siguientes campos de metadatos. Para proporcionar sugerencias de búsqueda, considere rellenar los campos siguientes con palabras clave apropiadas:

* Etiquetas de recursos. (mapas a `jcr:content/metadata/cq:tags`)
* Título del recurso. (mapas a `jcr:content/metadata/dc:title`)
* Descripción del recurso. (mapas a `jcr:content/metadata/dc:description`)
* Título en el repositorio de JCR. El valor puede asignarse al título del recurso. (mapas a `jcr:content/jcr:title`)
* Descripción en el repositorio JCR. El valor puede asignarse a la descripción del recurso. (mapas a `jcr:content/jcr:description`)

Para recibir sugerencias para más de una palabra clave de búsqueda, siga escribiendo todas las palabras clave sin seleccionar ninguna sugerencia para una sola palabra clave.

![Escriba varias palabras clave para ver las sugerencias que se ajustan a todas ellas](assets/search_suggestionsmanykeywords.gif)

*Figura:Escriba varias palabras clave para ver las sugerencias que se ajustan a todas ellas*

### Clasificación de búsqueda y aumento {#searchrank}

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. Coincidencias de `woman running` en los distintos campos de metadatos.
1. Coincidencias de `woman running` las etiquetas inteligentes.
1. Coincidencias de `woman` o de `running` en etiquetas inteligentes.

Puede mejorar la relevancia de las palabras clave para los recursos en particular a fin de mejorar las búsquedas basadas en las palabras clave. En otras palabras, las imágenes para las que promociona palabras clave específicas aparecen en la parte superior de los resultados de búsqueda cuando realiza una búsqueda en base a estas palabras clave.

1. En la interfaz de usuario de Assets, abra la página de propiedades del recurso. Haga clic en **[!UICONTROL Avanzadas]** y pulse o haga clic en **[!UICONTROL Agregar]** en **[!UICONTROL Elevar para las palabras clave de búsqueda]**.
1. En el cuadro **[!UICONTROL Buscar promoción]** , especifique una palabra clave para la que desee aumentar la búsqueda de la imagen y, a continuación, toque o haga clic en **[!UICONTROL Agregar]**. Puede especificar varias palabras clave de la misma manera.
1. Toque o haga clic en **[!UICONTROL Guardar y cerrar]**. El recurso que promocionó para esta palabra clave aparece entre los principales resultados de búsqueda.

Esto se puede utilizar en su beneficio al aumentar la clasificación de algunos recursos en los resultados de búsqueda de la palabra clave de objetivo. Consulte el siguiente vídeo de ejemplo. Para obtener información detallada, consulte [Búsqueda en AEM](https://helpx.adobe.com/experience-manager/kt/assets/using/search-feature-video-use.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Comprender cómo se clasifican los resultados de búsqueda y cómo se puede influir en la clasificación.*

## Advanced search {#scope}

AEM proporciona varios métodos, como filtros que se aplican a los recursos buscados, para ayudarle a localizar los recursos deseados con mayor rapidez. A continuación se describen algunos de los métodos más utilizados. A continuación se comparten algunos ejemplos [](#samples) ilustrados.

**Buscar archivos o carpetas**: En los resultados de la búsqueda, consulte archivos, carpetas o ambos. En el panel **[!UICONTROL Filtros]** , puede seleccionar la opción adecuada. Consulte la interfaz [de búsqueda](#searchui).

**Buscar recursos dentro de una carpeta**: Puede limitar la búsqueda a una carpeta específica. En el panel **[!UICONTROL Filtros]** , agregue la ruta de una carpeta. Solo puede seleccionar una carpeta a la vez.

![Limitar los resultados de búsqueda a una carpeta agregando una ruta de carpeta en el panel Filtros](assets/search_folder_select.gif)

*Figura:Limitar los resultados de búsqueda a una carpeta agregando una ruta de carpeta en el panel Filtros*

### Buscar imágenes similares {#visualsearch}

Para buscar imágenes que sean visualmente similares a una imagen seleccionada por el usuario, haga clic en la opción **[!UICONTROL Buscar similares]** en la vista de tarjeta de una imagen o en la barra de herramientas. AEM muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. Consulte [cómo configurar la búsqueda por similitudes](#configvisualsearch).

![Buscar imágenes similares con la opción en la vista de tarjeta](assets/search_find_similar.png)

*Figura:Buscar imágenes similares con la opción en la vista de tarjeta*

### Imágenes de Adobe Stock {#adobestock}

Desde la interfaz de usuario de AEM, los usuarios pueden buscar recursos [de](/help/assets/aem-assets-adobe-stock.md) Adobe Stock y obtener licencias para los recursos necesarios. Agregar `Location: Adobe Stock` en la barra de Omniture. También puede utilizar el panel Filtros para buscar todos los recursos con licencia o sin licencia o un recurso específico con el número de archivo de Adobe Stock.

### Recursos de Dynamic Media {#dmassets}

Puede filtrar imágenes de Dynamic Media seleccionando **[!UICONTROL Dynamic Media > Conjuntos]** en el panel **[!UICONTROL Filtros]**. Filtra y muestra recursos como conjuntos de imágenes, carruseles, conjuntos de medios mixtos y conjuntos de giros.

### Buscar con valores específicos en campos de metadatos {#gqlsearch}

Puede buscar recursos en función de los valores exactos de campos de metadatos específicos como, por ejemplo, título, descripción y autor. La función de búsqueda de texto completo de GQL captura solo aquellos recursos cuyo valor de metadatos coincida exactamente con la consulta de búsqueda. Los nombres de las propiedades (por ejemplo, autor, título, etc.) y los valores distinguen entre mayúsculas y minúsculas.

| Campo de metadatos | Valor y uso de faceta |
|---|---|
| Título | title:John |
| Creador | creador:John |
| Lugar de residencia | ubicación:NA |
| Descripción | description:&quot;Imagen de muestra&quot; |
| Herramienta Creador | creatortool:&quot;Adobe Photoshop CC 2015&quot; |
| Propietario del copyright | copyright:&quot;Adobe Systems&quot; |
| Colaborador | colaborador:John |
| Condiciones de uso | usageterms:&quot;CopyRights Reserved&quot; |
| Creado | creado:AAAA-MM-DDTHH |
| Caduca la fecha | expira:AAAA-MM-DDTHH |
| A tiempo | ontime:AAAA-MM-DDTHH |
| Tiempo de inactividad | offtime:AAAA-MM-DDTHH |
| Intervalo de tiempo (caduca dateontime, offtime) | facet field : límite inferior..upperbound |
| Ruta | /content/dam/&lt;nombre de carpeta> |
| Título del PDF | pdftitle:&quot;Documento de Adobe&quot; |
| Asunto | asunto: &quot;Formación&quot; |
| Etiquetas | etiquetas: &quot;Ubicación y viaje&quot; |
| Tipo | type:&quot;image\png&quot; |
| Anchura de la imagen | anchura:límite inferior..upperbound |
| Altura de la imagen | altura:límite inferior..upperbound |
| Person | persona:John |

Las propiedades path, limit, size y order by no pueden escribirse en OR con ninguna otra propiedad.

La palabra clave para una propiedad generada por el usuario es su etiqueta de campo en el editor de propiedades en minúsculas, con espacios eliminados.

Estos son algunos ejemplos de formatos de búsqueda para consultas complejas:

* Para mostrar todos los recursos con varios campos de facetas (por ejemplo: title=John Doe y la herramienta de creación = Adobe Photoshop): `tiltle:"John Doe" creatortool : Adobe*`
* Para mostrar todos los recursos cuando el valor de facetas no es una sola palabra sino una frase (por ejemplo: title=Scott Reynolds): `title:"Scott Reynolds"`
* Para mostrar recursos con varios valores de una sola propiedad (por ejemplo: title=Scott Reynolds o John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Para mostrar recursos con valores de propiedad que empiecen por una cadena específica (por ejemplo: el título es Scott Reynolds): `title:Scott*`
* Para mostrar recursos con valores de propiedad que finalizan con una cadena específica (por ejemplo: el título es Scott Reynolds): `title:*Reynolds`
* Para mostrar recursos con un valor de propiedad que contenga una cadena específica (por ejemplo: título = Sala de reuniones de Basilea): `title:*Meeting*`
* Para mostrar los recursos que contienen una cadena concreta y tienen un valor de propiedad específico (por ejemplo: buscar la cadena Adobe en recursos con título=John Doe): `*Adobe* title:"John Doe"`

## Buscar recursos de otras ofertas o interfaces de AEM {#beyondomnisearch}

Adobe Experience Manager (AEM) conecta el repositorio de DAM con varias otras soluciones de AEM para proporcionar un acceso más rápido a los recursos digitales y optimizar los flujos de trabajo creativos. Cualquier descubrimiento de recursos comienza con la exploración o búsqueda. El comportamiento de la búsqueda sigue siendo en gran medida el mismo en las distintas superficies y soluciones. Algunos métodos de búsqueda cambian a medida que la audiencia de destino, los casos de uso y la interfaz de usuario varían según las soluciones de AEM. Los métodos específicos están documentados para las soluciones individuales en los vínculos siguientes. Los consejos y comportamientos universalmente aplicables están documentados en este artículo.

### Buscar recursos desde el panel Vínculo de recursos de Adobe {#aal}

Con Adobe Asset Link, los profesionales creativos ahora pueden acceder al contenido almacenado en Recursos AEM sin tener que abandonar las aplicaciones compatibles de Adobe Creative Cloud. Los creativos pueden examinar, buscar, desproteger y proteger recursos sin problemas mediante el panel integrado en las aplicaciones de Creative Cloud: Photoshop, Illustrator e InDesign. El vínculo de recursos también permite a los usuarios buscar resultados visualmente similares. Los resultados de la visualización de la búsqueda visual se basan en los algoritmos de aprendizaje automático de Adobe Sensei y ayudan a los usuarios a encontrar imágenes estéticas similares. Consulte [Búsqueda y exploración de recursos](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) mediante Adobe Asset Link.

### Buscar recursos en la aplicación de escritorio de AEM {#desktopapp}

Los profesionales creativos utilizan la aplicación de escritorio para facilitar la búsqueda y la disponibilidad de Recursos AEM en su escritorio local (Win o Mac). Los elementos creativos pueden revelar fácilmente los recursos deseados en Mac Finder o el Explorador de Windows, abrirlos en aplicaciones de escritorio y cambiarlos localmente; los cambios se guardan de nuevo en AEM con una nueva versión creada en el repositorio. La aplicación admite búsquedas básicas mediante una o más palabras clave, * y ? comodines y operador AND. Consulte [exploración, búsqueda y vista previa de recursos](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) en la aplicación de escritorio.

### Search assets in Brand Portal {#brandportal}

Los usuarios de la línea de negocios y los especialistas en marketing utilizan Brand Portal para compartir de forma eficaz y segura los recursos digitales aprobados con sus equipos, socios y distribuidores internos ampliados. See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Buscar imágenes de Adobe Stock {#adobestock-1}

Desde la interfaz de usuario de AEM, los usuarios pueden buscar recursos de Adobe Stock y obtener licencias para los recursos necesarios. Agregar `Location: Adobe Stock` en el campo Omniture Search. También puede utilizar el panel **[!UICONTROL Filtros]** para buscar todos los recursos con licencia o sin licencia, o para buscar un recurso específico con el número de archivo de Adobe Stock. Consulte [Gestión de imágenes de Adobe Stock en AEM](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Buscar recursos de Dynamic Media {#dynamicmedia}

Puede filtrar imágenes de Dynamic Media seleccionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** en el panel **[!UICONTROL Filtros]**. Filtra y muestra recursos como conjuntos de imágenes, carruseles, conjuntos de medios mixtos y conjuntos de giros. Durante la creación de páginas web, los autores pueden buscar conjuntos desde el Buscador de contenido. Los filtros para conjuntos están disponibles en un menú emergente.

### Buscar recursos en Content Finder al crear páginas Web {#contentfinder}

Los autores pueden utilizar Content Finder para buscar en el repositorio de DAM los recursos relevantes y utilizar los recursos en las páginas web que crean. Los autores también pueden utilizar la funcionalidad Recursos conectados para buscar recursos disponibles en una implementación remota de AEM. A continuación, los autores pueden utilizar estos recursos en páginas web en una implementación local de AEM. See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Buscar colecciones {#collections}

La función de búsqueda de AEM admite la búsqueda de colecciones y la búsqueda de recursos dentro de una colección. Consulte [Buscar colecciones](/help/assets/managing-collections-touch-ui.md).

## Asset selector {#assetselector}

El selector de recursos le permite buscar, filtrar y examinar los recursos DAM de forma especial. El selector de recursos está disponible en `https://[aem-server]:[port]/aem/assetpicker.html`. Puede recuperar los metadatos de los recursos seleccionados mediante el selector de recursos. Puede iniciarla con parámetros de solicitud admitidos, como el tipo de recurso (imagen, vídeo, texto) y el modo de selección (selecciones únicas o múltiples). Estos parámetros establecen el contexto del selector de recursos para una instancia de búsqueda en particular y se mantienen intactos durante toda la selección.

El selector de recursos utiliza el mensaje Window.postMessage de HTML5 para enviar datos del recurso seleccionado al destinatario. El selector de recursos se basa en el vocabulario del selector de base de Granite. De forma predeterminada, el selector de recursos funciona en el modo Examinar.

Puede pasar los siguientes parámetros de solicitud en una URL para iniciar el selector de recursos en un contexto concreto:

| Nombre | Valores | Ejemplo | Función |
|---|---|---|---|
| sufijo de recurso (B) | Ruta de carpeta como sufijo de recurso en la dirección URL:[https://localhost:4502/aem/assetpicker.html/&lt;ruta_de_carpeta>](https://localhost:4502/aem/assetpicker.html) | Para iniciar el selector de recursos con una carpeta concreta seleccionada, por ejemplo con la carpeta `/content/dam/we-retail/en/activities` seleccionada, la URL debe tener el formato: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Si necesita que se seleccione una carpeta determinada al iniciar el selector de recursos, pasarla como sufijo de recurso. |
| modo | único, múltiple | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | En varios modos, puede seleccionar varios recursos simultáneamente mediante el selector de recursos. |
| mimetype | mimetype(s) (`/jcr:content/metadata/dc:format`) de un recurso (también se admite el comodín) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png)</li></ul> | Utilícelo para filtrar recursos en función de tipos MIME |
| el cuadro de diálogo | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Utilice estos parámetros para abrir el selector de recursos como cuadro de diálogo Granito. Esta opción solo se aplica cuando se inicia el selector de recursos mediante Campo de ruta de granito y se configura como URL de pickerSrc. |
| assettype (S) | imágenes, documentos, multimedia, archivos | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | Utilice esta opción para filtrar los tipos de recursos en función del valor pasado. |
| raíz | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities) | Utilice esta opción para especificar la carpeta raíz del selector de recursos. En este caso, el selector de recursos permite seleccionar solo recursos secundarios (directos/indirectos) en la carpeta raíz. |

Para acceder a la interfaz del selector de recursos, vaya a `https://[aem_server]:[port]/aem/assetpicker`. Vaya a la carpeta que desee y seleccione uno o varios recursos. También puede buscar el recurso deseado en el cuadro Omniture, aplicar el filtro según sea necesario y luego seleccionarlo.

![Examinar y seleccionar recursos en el selector de recursos](assets/assetpicker.png)

*Figura:Examinar y seleccionar recursos en el selector de recursos*

## Restricciones  {#limitations}

La capacidad de búsqueda en Recursos AEM tiene las siguientes limitaciones:

* No introduzca un espacio de interlineado en la consulta de búsqueda; de lo contrario, la búsqueda no funcionará.
* AEM puede seguir mostrando el término de búsqueda después de seleccionar las propiedades de un recurso de los resultados de búsqueda y, a continuación, cancelar la búsqueda. <!-- (CQ-4273540) -->
* Al buscar carpetas o archivos y carpetas, los resultados de la búsqueda no se pueden ordenar según ningún parámetro.
* Si presiona return sin escribir nada en la barra de Omniture, AEM devuelve una lista de sólo archivos y no carpetas. Si busca carpetas de forma específica sin utilizar una palabra clave, AEM no devuelve ningún resultado.
* Con la casilla de verificación [!UICONTROL Seleccionar todo] , solo puede seleccionar los primeros 100 recursos buscados en la vista de tarjeta y los primeros 200 recursos buscados en la vista de lista. Si desplaza y carga más recursos en la interfaz de usuario, puede seleccionar más mediante la opción [!UICONTROL Seleccionar todo] .

La búsqueda visual o la búsqueda por similitudes tienen las siguientes limitaciones:

* La búsqueda visual funciona mejor con repositorios más grandes. Aunque no se requiere un número mínimo de imágenes para obtener buenos resultados, la calidad de las coincidencias con unas pocas imágenes puede no ser tan buena como las coincidencias de un repositorio grande.
* No puede cambiar el modelo ni entrenar a AEM para encontrar imágenes similares. Por ejemplo, la adición o eliminación de etiquetas inteligentes a algunos recursos no cambia el modelo. Los recursos se excluyen de los resultados de búsqueda visualmente similares.

La funcionalidad de búsqueda puede tener limitaciones de rendimiento en los siguientes escenarios:

* La vista de tarjeta tiene un tiempo de carga más rápido que la vista de lista para mostrar los resultados de la búsqueda.

## Sugerencias de búsqueda {#tips}

* Cuando supervise el estado de revisión de los recursos, utilice la opción adecuada para encontrar los recursos aprobados o los que están pendientes de aprobación.
* Use el predicado de perspectivas para buscar recursos admitidos en función de las estadísticas de uso obtenidas de varias aplicaciones de Creative. Los datos de uso se agrupan en Puntuación de uso, Impresiones, Clics y Canales de medios, donde los recursos aparecen como categorías.
* Utilice la casilla de verificación **[!UICONTROL Seleccionar todo]** para seleccionar los recursos buscados. Selecciona los primeros 100 recursos en la vista de tarjeta y los primeros 200 en la vista de lista. Puede operar en la selección, por ejemplo, descargar los recursos seleccionados, actualizar las propiedades de metadatos de forma masiva para los recursos seleccionados o agregar los recursos seleccionados a una colección.
* Para buscar recursos que no contengan los metadatos obligatorios, consulte Metadatos [](#mandatorymetadata)obligatorios.
* La búsqueda utiliza todos los campos de metadatos. Una búsqueda genérica, como la búsqueda de 12, generalmente devuelve muchos resultados. Para obtener mejores resultados, utilice comillas dobles (no simples) o asegúrese de que el número esté contiguo a una palabra sin carácter especial (por ejemplo, *shoe12*).
* La búsqueda de texto completo admite operadores como -, ^, etc. Para buscar estas letras como literales de cadena, encierre la expresión de búsqueda entre comillas dobles. Por ejemplo, utilice &quot;Portátil - Belleza&quot; en lugar de Portátil - Belleza.
* Si los resultados de búsqueda son demasiados, limite el [ámbito de búsqueda](#scope) a cero en los recursos deseados. Funciona mejor cuando tiene alguna idea de cómo buscar mejor los recursos deseados, por ejemplo, un tipo de archivo específico, una ubicación específica, metadatos específicos, etc.

* **Etiquetado**: Las etiquetas le ayudan a categorizar los recursos que se pueden explorar y buscar de forma más eficaz. El etiquetado ayuda a propagar la taxonomía adecuada a otros usuarios y flujos de trabajo. AEM ofrece métodos para etiquetar automáticamente recursos mediante los servicios inteligentes de Adobe Sensei, que mejoran aún más el etiquetado de los recursos con el uso y la formación. Cuando se buscan recursos, las etiquetas inteligentes se incluyen si la función está activada en la cuenta. Funciona junto con la funcionalidad de búsqueda integrada de AEM. Consulte Comportamiento [de búsqueda](#searchbehavior). Para optimizar el orden en que se muestran los resultados de la búsqueda, puede [aumentar la clasificación](#searchrank) de la búsqueda de algunos recursos seleccionados.

* **Indexación**: En los resultados de búsqueda solo se devuelven los metadatos y recursos indexados. Para obtener una mejor cobertura y rendimiento, asegúrese de que la indexación sea correcta y siga las optimizaciones. Consulte [indización](#searchindex).

## Algunos ejemplos que ilustran la búsqueda {#samples}

Utilice comillas dobles alrededor de las palabras clave para encontrar recursos que contengan la frase exacta en el orden exacto según lo especificado por el usuario.

![Comportamiento de búsqueda con y sin comillas](assets/search_with_quotes.gif)

*Figura:Comportamiento de búsqueda con y sin comillas*

**Buscar con comodín** asterisco: Para ampliar la búsqueda, utilice un asterisco antes o después de la palabra de búsqueda para que coincida con cualquier número de caracteres. Por ejemplo, al buscar una ejecución sin un asterisco, no se devuelven recursos que contengan ninguna variación de la palabra (incluidos los metadatos). Un asterisco sustituye a cualquier número de caracteres. Por ejemplo,

* `run` devuelve recursos con la palabra clave de ejecución exacta
* `run*` devuelve recursos con ejecución, ejecución, ejecución, etc.
* `*run` devuelve outrun, reejecutar, etc.
* `*run*` devuelve todas las combinaciones posibles.

![Ilustración del uso de un comodín de asterisco en la búsqueda de recursos mediante un ejemplo](assets/search_with_asterisk_run.gif)

*Figura:Ilustración del uso de un comodín de asterisco en la búsqueda de recursos mediante un ejemplo*

**Buscar con comodín** de signo de interrogación: Para ampliar la búsqueda, utilice uno o varios &#39;?&#39; caracteres para que coincidan con el número exacto de caracteres. Por ejemplo, en la siguiente ilustración,

* `run???` consulta no coincide con ningún recurso.

* `run????` la consulta coincide con la palabra `running` con cuatro caracteres después `run`.

* `??run` la consulta coincide con la palabra `rerun` con dos caracteres antes `run`.

![Ilustración del uso del comodín del signo de interrogación en la búsqueda de recursos mediante un ejemplo](assets/search_with_questionmark_run.gif)

*Figura:Ilustración del uso del comodín del signo de interrogación en la búsqueda de recursos mediante un ejemplo*

**Excluir una palabra clave**: Utilice dash para buscar recursos que no contengan una palabra clave. Por ejemplo, `running -shoe` la consulta devuelve recursos que contienen `running`, pero no `shoe`. Del mismo modo, `camp -night` la consulta devuelve recursos que contienen `camp` pero no `night`. Tenga en cuenta que `camp-night` la consulta devuelve recursos que contienen tanto `camp` como `night`.

![Uso del guión para buscar recursos que no contengan una palabra clave excluida](assets/search_dash_exclude_keyword.gif)

*Figura:Uso del guión para buscar recursos que no contengan una palabra clave excluida*

## Tareas de configuración y administración relacionadas con la funcionalidad de búsqueda {#configadmin}

### Buscar configuraciones de índice {#searchindex}

La detección de recursos depende de la indexación del contenido de DAM, incluidos los metadatos. La detección de recursos más rápida y precisa depende de la indexación optimizada y de las configuraciones adecuadas. Consulte Índice [de](/help/assets/performance-tuning-guidelines.md#search-indexes)búsqueda, consultas de [roble e indexación](/help/sites-deploying/queries-and-indexing.md), y [optimizaciones](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Búsqueda visual o de similitudes {#configvisualsearch}

La búsqueda visual utiliza etiquetado inteligente y requiere AEM 6.5.2.0 o posterior. Después de configurar la funcionalidad de etiquetado inteligente, siga estos pasos.

1. En AEM CRXDE, en el `/oak:index/lucene` nodo, agregue las siguientes propiedades y valores y guarde los cambios.

   * `costPerEntry` propiedad de tipo `Double` con el valor `10`.

   * `costPerExecution` propiedad de tipo `Double` con el valor `2`.

   * `refresh` propiedad de tipo `Boolean` con el valor `true`.
   Esta configuración permite realizar búsquedas desde el índice apropiado.

1. Para crear un índice de Lucene, en CRXDE, en `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, cree un nodo denominado `imageFeatures` de tipo `nt-unstructured`. En `imageFeatures` nodo,

   * Agregue `name` propiedad de tipo `String` con el valor `jcr:content/metadata/imageFeatures/haystack0`.

   * Agregar `nodeScopeIndex` propiedad de tipo `Boolean` con el valor de `true`.

   * Agregar `propertyIndex` propiedad de tipo `Boolean` con el valor de `true`.

   * Agregue `useInSimilarity` propiedad de tipo `Boolean` con el valor `true`.
   Guarde los cambios.

1. Acceda `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` y agregue `similarityTags` propiedad de tipo `Boolean` con el valor de `true`.
1. Aplique etiquetas inteligentes a los recursos del repositorio de AEM. Consulte [cómo configurar etiquetas](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)inteligentes.
1. En CRXDE, en `/oak-index/damAssetLucene` nodo, establezca la `reindex` propiedad en `true`. Guarde los cambios.
1. (Opcional) Si tiene un formulario de búsqueda personalizado, copie el `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` nodo en `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Guarde todos los cambios.

Para obtener información relacionada, consulte [Comprensión de las etiquetas inteligentes en AEM](https://helpx.adobe.com/experience-manager/kt/assets/using/smart-tags-feature-video-understand.html) y [cómo gestionar las etiquetas](/help/assets/managing-smart-tags.md)inteligentes.

### Metadatos obligatorios {#mandatorymetadata}

Los usuarios comerciales, administradores o bibliotecarios de DAM pueden definir algunos metadatos como metadatos obligatorios que son indispensables para que funcionen los procesos empresariales. Por varios motivos, es posible que algunos recursos no tengan estos metadatos, como recursos heredados o recursos migrados de forma masiva. Los recursos con metadatos que faltan o no son válidos se detectan y generan informes en función de la propiedad de metadatos indizados. Para configurarlo, consulte Metadatos [](/help/assets/metadata-schemas.md#define-mandatory-metadata)obligatorios.

### Modificar facetas de búsqueda {#searchfacets}

Para mejorar la velocidad de detección, Recursos AEM ofrece facetas de búsqueda que permiten filtrar los resultados de búsqueda. El panel Filtros incluye algunas facetas estándar de forma predeterminada. Los administradores pueden personalizar el panel Filtros para modificar las facetas predeterminadas mediante los predicados integrados. AEM ofrece una buena colección de predicados integrados y un editor para personalizar las facetas. Consulte facetas [de búsqueda](/help/assets/search-facets.md).

### Extraer texto al cargar recursos {#extracttextupload}

Puede configurar AEM para que extraiga el texto de los recursos cuando los usuarios carguen recursos, como archivos PSD o PDF. AEM indexa el texto extraído y ayuda a los usuarios a buscar estos recursos en función del texto extraído. Consulte [Carga de recursos](/help/assets/managing-assets-touch-ui.md#uploading-assets).

### Predicados personalizados para filtrar los resultados de búsqueda {#custompredicates}

Los predicados se utilizan para crear facetas. Los administradores pueden personalizar las facetas de búsqueda en el panel Filtros mediante predicados preconfigurados. Estos predicados se pueden personalizar mediante superposiciones. Consulte [Creación de predicados](/help/assets/searchx.md)personalizados.

Puede buscar recursos digitales en función de una o varias de las siguientes propiedades. Los filtros que se aplican a algunas de estas propiedades están disponibles de forma predeterminada y algunos otros filtros se pueden crear personalizados para aplicarlos a otras propiedades.

| Campo de búsqueda | Valores de propiedades de búsqueda |
|---|---|
| Tipos MIME | Imágenes, Documentos, Multimedia, Archivos u Otros. |
| Última modificación | Hora, día, semana, mes o año. |
| Tamaño del archivo | Pequeño, Medio o Grande. |
| Estado de publicación | Publicado o sin publicar. |
| Estado aprobado | Aprobado o rechazado. |
| Orientación | Horizontal, Vertical o Cuadrado. |
| Estilo | Color o Blanco y negro. |
| Altura del vídeo | Especificado como valor mínimo y máximo. El valor se almacena únicamente en los metadatos de las representaciones de vídeo. |
| Anchura del vídeo | Especificado como valor mínimo y máximo. El valor se almacena únicamente en los metadatos de las representaciones de vídeo. |
| Formato de vídeo | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. El valor se almacena en los metadatos del vídeo de origen y en cualquier representación. |
| Códec de vídeo | x264. El valor se almacena únicamente en los metadatos de las representaciones de vídeo. |
| Velocidad de bits de vídeo | Especificado como valor mínimo y máximo. El valor se almacena únicamente en los metadatos de las representaciones de vídeo. |
| Códec de audio | Libvorbis, Lame MP3, AAC Encoding. El valor se almacena únicamente en los metadatos de las representaciones de vídeo. |
| Velocidad de bits de audio | Especificado como valor mínimo y máximo. El valor se almacena únicamente en los metadatos de las representaciones de vídeo. |

## Trabajar con resultados de búsqueda de recursos {#aftersearch}

Una vez que vea algunos recursos buscados que coinciden con sus criterios, puede realizar las siguientes tareas típicas con estos resultados de búsqueda o realizar las siguientes acciones:

* Ver propiedades de metadatos y otra información.
* Descargue uno o varios recursos.
* Utilice las acciones de escritorio para abrir estos recursos en la aplicación de escritorio.
* Cree colecciones inteligentes.

### Ordenar resultados de búsqueda {#sort}

La ordenación de los resultados de búsqueda ayuda a descubrir los recursos necesarios con mayor rapidez. La ordenación de los resultados de búsqueda funciona en la vista de lista y solo cuando se selecciona **[!UICONTROL [Archivos](#searchui)]**en el panel**[!UICONTROL  Filtros ]**. AEM Assets utiliza la ordenación del lado del servidor para ordenar rápidamente todos los recursos (aunque sean muchos) de una carpeta o los resultados de una consulta de búsqueda. La ordenación del lado del servidor proporciona resultados más rápidos y precisos que la ordenación del lado del cliente.

En la vista de lista, puede ordenar los resultados de la búsqueda del mismo modo que puede ordenar los recursos en cualquier carpeta. La ordenación funciona en estas columnas: nombre, título, estado, dimensiones, tamaño, clasificación, uso, (fecha) de creación, (fecha) de modificación, (fecha) de publicación, flujo de trabajo y desprotección.

Para ver las limitaciones de la funcionalidad de ordenación, consulte [Limitaciones](#limitations).

### Comprobar información detallada de un recurso {#checkinfo}

Puede comprobar la información detallada de los recursos buscados desde la página de resultados de la búsqueda.

Para ver todos los metadatos de un recurso, selecciónelo y haga clic en **[!UICONTROL las propiedades]** de la barra de herramientas.

Para comprobar los comentarios de un recurso o del historial de versiones de un recurso, haga clic en el recurso y abrirá una vista previa de gran tamaño. Abra la cronología en el carril izquierdo y seleccione **[!UICONTROL Comentarios]** o **[!UICONTROL Versiones]**. También puede ordenar la actividad de la cronología como comentarios o versiones en orden cronológico.

![Ordenar entradas de línea de tiempo para un recurso de búsqueda](assets/sort_timeline_search_results.gif)

*Figura:Ordenar entradas de línea de tiempo para un recurso de búsqueda*

### Descargar recursos buscados {#download}

Puede descargar los recursos buscados y sus representaciones del mismo modo que descarga los recursos normales de las carpetas. Seleccione uno o varios recursos en los resultados de búsqueda y haga clic en **[!UICONTROL Descargar]** en la barra de herramientas.

### Propiedades de metadatos de actualización masiva {#metadataupdates}

Es posible realizar actualizaciones masivas en los campos de metadatos comunes de varios recursos. En los resultados de la búsqueda, seleccione uno o varios recursos. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas y actualice los metadatos según sea necesario. Haga clic en **[!UICONTROL Guardar y cerrar]** cuando termine. Los metadatos existentes anteriormente en los campos actualizados se sobrescriben.

Para los recursos disponibles en una sola carpeta o colección, es más fácil [actualizar los metadatos de forma masiva](/help/assets/managing-multiple-assets.md) sin utilizar la funcionalidad de búsqueda. Para los recursos disponibles en varias carpetas o que cumplen un criterio común, es más rápido actualizar los metadatos de forma masiva mediante la búsqueda.

### Colecciones inteligentes {#collections-1}

Una colección es un conjunto ordenado de recursos que puede incluir recursos de distintas ubicaciones porque las colecciones solo contienen referencias a estos recursos. Las colecciones son de los dos tipos siguientes:

* Una lista de referencia estática de recursos, carpetas y otras colecciones.
* Lista dinámica (colección inteligente) que rellena los recursos de la colección en función de criterios de búsqueda.

Puede crear colecciones inteligentes basadas en los criterios de búsqueda. En el panel **[!UICONTROL Filtros]**, seleccione **[!UICONTROL Archivos]** y haga clic en **[!UICONTROL Guardar colección inteligente]**. Consulte [Gestión de colecciones](/help/assets/managing-collections-touch-ui.md).

## Solución de problemas y resultados de búsqueda inesperados {#troubleshoot-unexpected-search-results-and-issues}

| Error, problemas, síntomas | Motivo posible | Posible solución o comprensión del problema |
|---|---|---|
| Resultados incorrectos al buscar recursos con metadatos que faltan |  Al buscar recursos que no tienen los metadatos obligatorios, AEM puede mostrar algunos recursos que tienen metadatos válidos. Los resultados se basan en la propiedad de metadatos indexados. | Una vez actualizados los metadatos, es necesario volver a indexar para reflejar el estado correcto de los metadatos de los recursos. Consulte metadatos [](metadata-schemas.md#define-mandatory-metadata)obligatorios. |
| Demasiados resultados de búsqueda | Parámetro de búsqueda amplia. | Considere limitar el [alcance de la búsqueda](#scope). El uso de etiquetas inteligentes puede proporcionarle más resultados de búsqueda de los esperados. Consulte Comportamiento [de búsqueda con etiquetas](#withsmarttags)inteligentes. |
| Resultados de búsqueda no relacionados o parcialmente relacionados | El comportamiento de búsqueda cambia con el etiquetado inteligente. | Comprender [cómo cambia la búsqueda después del etiquetado](#withsmarttags)inteligente. |
| No hay sugerencias de autocompletar para los recursos | Los recursos recién cargados no se han indizado todavía. Los metadatos no están disponibles inmediatamente como sugerencias cuando comienza a escribir una palabra clave de búsqueda en la barra de Omniture. | Recursos AEM espera hasta la expiración de un período de tiempo de espera (una hora de forma predeterminada) antes de ejecutar un trabajo en segundo plano para indexar los metadatos de todos los recursos cargados o actualizados y, a continuación, agrega los metadatos a la lista de sugerencias. |
| No hay resultados de la búsqueda | <ul><li>No existen recursos que coincidan con la consulta.</li><li>Ha agregado un espacio en blanco antes de la consulta de búsqueda.</li><li>Un campo de metadatos no admitido contiene la palabra clave que busca.</li><li>Tiempo de activación y tiempo de inactividad se configura para el recurso y la búsqueda se realizó durante el tiempo de inactividad del recurso.</li></ul> | <ul><li>Buscar usando una palabra clave diferente. También puede utilizar el etiquetado (inteligente) para mejorar los resultados de la búsqueda.</li><li>Es una limitación [conocida](#limitations).</li><li>No todos los campos de metadatos se consideran para las búsquedas. Consulte [ámbito](#scope).</li><li>Busque más tarde o modifique los tiempos de activación y desactivación de los recursos necesarios.</li></ul> |
| El filtro de búsqueda o predicado no está disponible | <ul><li>El filtro de búsqueda no está configurado.</li><li>No está disponible para su inicio de sesión.</li><li>(Menos probable) Las opciones de búsqueda no están personalizadas en la implementación que esté utilizando.</li></ul> | <ul><li>Póngase en contacto con el administrador para comprobar si las personalizaciones de búsqueda están disponibles o no.</li><li>Póngase en contacto con el administrador para comprobar si su cuenta tiene los privilegios y permisos necesarios para utilizar la personalización.</li><li>Póngase en contacto con el administrador y compruebe las personalizaciones disponibles para la implementación de Recursos AEM que está utilizando.</li></ul> |
| Al buscar imágenes visualmente similares, falta una imagen esperada | <ul><li>La imagen no está disponible en AEM.</li><li>La imagen no está indizada. Normalmente, cuando se carga recientemente.</li><li>La imagen no está etiquetada de forma inteligente.</li></ul> | <ul><li>Agregue la imagen a Recursos AEM.</li><li>Póngase en contacto con el administrador para volver a indexar el repositorio. Además, asegúrese de que está utilizando el índice adecuado.</li><li>Póngase en contacto con el administrador para etiquetar los recursos relevantes de forma inteligente.</li></ul> |
| Al buscar imágenes visualmente similares, se muestra una imagen irrelevante | Comportamiento de búsqueda visual. | AEM muestra tantos recursos potencialmente relevantes como sea posible. Las imágenes menos relevantes, si las hay, se agregan a los resultados pero con una clasificación de búsqueda más baja. La calidad de las coincidencias y la relevancia de los recursos buscados disminuyen a medida que se desplaza hacia abajo por los resultados de la búsqueda. |
| Al seleccionar y operar en los resultados de búsqueda, no se aplican todos los recursos buscados | La opción [!UICONTROL Seleccionar todo] sólo selecciona los primeros 100 resultados de búsqueda en la vista de tarjeta y los primeros 200 resultados de búsqueda en la vista de lista. |  |

>[!MORELIKETHIS]
>
>* [Guía de implementación de búsquedas de AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configuración avanzada de predicados de búsqueda de etiquetas y varios valores](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/search-feature-video-use.html)
>* [Configurar la búsqueda de traducción inteligente](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

