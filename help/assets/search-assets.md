---
title: Buscar recursos digitales e imágenes en [!DNL Adobe Experience Manager]
description: Obtenga información sobre cómo encontrar los recursos necesarios en [!DNL Adobe Experience Manager] mediante el panel Filtros y cómo utilizar los recursos que aparecen en la búsqueda.
contentOwner: AG
mini-toc-levels: 1
feature: Búsqueda, metadatos
role: Profesional empresarial
translation-type: tm+mt
source-git-commit: fd283b840830bef613689f81cf753e226fb834d7
workflow-type: tm+mt
source-wordcount: '5577'
ht-degree: 5%

---


# Buscar recursos en [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] proporciona métodos de detección de recursos sólidos que le ayudan a alcanzar una mayor velocidad de contenido. Sus equipos pueden reducir el tiempo de salida al mercado con una experiencia de búsqueda inteligente y optimizada mediante la funcionalidad y los métodos personalizados integrados. La búsqueda de recursos es fundamental para el uso de un sistema de administración de recursos digitales, ya sea para su uso posterior por parte de los creativos, para la sólida administración de recursos por parte de los usuarios comerciales y los especialistas en marketing, o para la administración por parte de los administradores de DAM. Las búsquedas simples, avanzadas y personalizadas que puede realizar a través de la interfaz de usuario [!DNL Assets] u otras aplicaciones y superficies ayudan a cumplir estos casos de uso.

[!DNL Experience Manager Assets] admite los siguientes casos de uso y en este artículo se describen el uso, los conceptos, las configuraciones, las limitaciones y la resolución de problemas de estos casos de uso.

| Buscar recursos | Configuración y administración de la funcionalidad de búsqueda | Trabajar con resultados de búsqueda |
|---|---|---|
| [Búsquedas básicas](#searchbasics) | [Índice de búsqueda](#searchindex) | [Ordenar resultados](#sort) |
| [Explicación de la interfaz de usuario de búsqueda](#searchui) | [Búsqueda visual o de similitud](#configvisualsearch) | [Comprobar propiedades y metadatos de un recurso](#checkinfo) |
| [Sugerencias de búsqueda](#searchsuggestions) | [Metadatos obligatorios](#mandatorymetadata) | [Descargar](#download) |
| [Comprender los resultados y el comportamiento de la búsqueda](#searchbehavior) | [Modificar facetas de búsqueda](#searchfacets) | [Actualizaciones masivas de metadatos](#metadataupdates) |
| [Buscar clasificación y aumento](#searchrank) | [Extracción de texto](#extracttextupload) | [Colecciones inteligentes](#collections) |
| [Búsqueda avanzada: filtrado y ámbito de búsqueda](#scope) | [Predicados personalizados](#custompredicates) | [Comprender y solucionar problemas relacionados con resultados inesperados](#unexpected-results) |
| [Buscar desde otras soluciones y aplicaciones](#search-assets-other-surfaces):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[aplicación de escritorio de Experience Manager](#desktop-app)</li><li>[Imágenes de Adobe Stock](#adobe-stock)</li><li>[Recursos de Dynamic Media](#dynamic-media)</li></ul> |  |  |
| [Selector de recursos](#assetpicker) |  |  |
| [](#limitations) Limitaciones y  [sugerencias](#tips) |  |  |
| [Ejemplos ilustrados](#samples) |  |  |

Busque recursos utilizando el campo Omnisearch en la parte superior de la interfaz web [!DNL Experience Manager]. Vaya a **[!UICONTROL Assets]** > **[!UICONTROL Files]** en [!DNL Experience Manager], haga clic en ![search_icon](assets/do-not-localize/search_icon.png) en la barra superior, introduzca la palabra clave de búsqueda y seleccione `Return`. También puede utilizar el método abreviado de palabra clave `/` (barra diagonal) para abrir el campo Omnisearch . `Location:Assets` está preseleccionado para limitar las búsquedas a los recursos DAM. [!DNL Experience Manager] proporciona sugerencias cuando empieza a escribir una palabra clave de búsqueda.

Utilice el panel **[!UICONTROL Filtros]** para buscar recursos, carpetas, etiquetas y metadatos. Puede filtrar los resultados de la búsqueda en función de las distintas opciones (predicados), como, por ejemplo, tipo de archivo, tamaño de archivo, fecha de la última modificación, estado del recurso, datos de perspectivas y licencias de Adobe Stock. Puede personalizar el panel Filtros y agregar o eliminar predicados de búsqueda utilizando [facetas de búsqueda](/help/assets/search-facets.md). El filtro [!UICONTROL Tipo de archivo] del panel [!UICONTROL Filtros] tiene casillas de verificación de estado mixto. Por lo tanto, a menos que seleccione todos los predicados anidados (o formatos), las casillas de verificación de primer nivel se marcan parcialmente.

[!DNL Experience Manager] la capacidad de búsqueda admite la búsqueda de colecciones y la búsqueda de recursos dentro de una colección. Consulte [buscar colecciones](/help/assets/manage-collections.md).

## Comprender la interfaz de búsqueda {#searchui}

Familiarícese con la interfaz de búsqueda y las acciones disponibles.

![Comprender la interfaz de resultados de búsqueda de recursos Experience Manager](assets/aem_search_results.png)

*Figura: Comprender la interfaz de resultados de  [!DNL Experience Manager Assets] búsqueda.*

**A.** Guarde la búsqueda como una colección inteligente. **B.** Filtra o predica para reducir los resultados de búsqueda. **C.** Mostrar archivos, carpetas o ambos. **D.** Haga clic en Filtros para abrir o cerrar el carril izquierdo. **E.** La ubicación de búsqueda es DAM. **F.** Campo Omnisearch con palabra clave de búsqueda proporcionada por el usuario. **G.** Seleccione los resultados de búsqueda cargados. **H.** Número de resultados de búsqueda mostrados del total de resultados de búsqueda. **I.** Cierre la búsqueda. **J.** Cambie entre la vista de tarjeta y la vista de lista.

### Facetas de búsqueda dinámica {#dynamicfacets}

Puede descubrir los recursos que desee con mayor rapidez desde la página de resultados de la búsqueda, utilizando el número de resultados de búsqueda esperados actualizado dinámicamente en las facetas de búsqueda. El número esperado de recursos se actualiza incluso antes de aplicar el filtro de búsqueda. Ver el recuento esperado con el filtro le ayuda a navegar por los resultados de búsqueda de forma rápida y eficaz.

![Consulte el número aproximado de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda.](assets/asset_search_results_in_facets_filters.png)

*Figura: Consulte el número aproximado de recursos sin filtrar los resultados de búsqueda en las facetas de búsqueda.*

## Comprender los resultados y el comportamiento de la búsqueda {#searchbehavior}

### Términos y resultados de búsqueda básicos {#searchbasics}

Puede ejecutar búsquedas de palabras clave desde el campo OmniSearch . La búsqueda de palabras clave no distingue entre mayúsculas y minúsculas y es una búsqueda de texto completo (en los campos de metadatos populares). Si se utiliza más de una palabra clave, `AND` es el operador predeterminado entre las palabras clave.

Los resultados se ordenan por relevancia, empezando por las coincidencias más cercanas. Para varias palabras clave, los resultados más relevantes son los recursos que contienen ambos términos en sus metadatos. Dentro de los metadatos, las palabras clave que aparecen como etiquetas inteligentes están mejor clasificadas que las palabras clave que aparecen en otros campos de metadatos. [!DNL Experience Manager] permite dar mayor peso a un término de búsqueda particular. Además, es posible [aumentar la clasificación](#searchrank) de algunos recursos de destino para términos de búsqueda específicos.

Para encontrar rápidamente los recursos relevantes, la interfaz enriquecida proporciona mecanismos de filtrado, clasificación y selección. Puede filtrar los resultados según varios criterios y ver el número de recursos buscados para varios filtros. Como alternativa, puede volver a ejecutar la búsqueda cambiando la consulta en el campo Omnisearch . Al cambiar los términos o filtros de búsqueda, los demás filtros permanecen aplicados para preservar el contexto de la búsqueda.

Cuando los resultados son muchos recursos, [!DNL Experience Manager] muestra los primeros 100 en la vista de tarjeta y los 200 en la vista de lista. A medida que los usuarios se desplazan, se cargan más recursos. Esto es para mejorar el rendimiento. Vea una demostración en vídeo del [número de recursos mostrados](https://www.youtube.com/watch?v=LcrGPDLDf4o).

A veces, es posible que vea algunos recursos inesperados en los resultados de búsqueda. Para obtener más información, consulte [resultados inesperados](#unexpected-results).

[!DNL Experience Manager] puede buscar muchos formatos de archivo y los filtros de búsqueda se pueden personalizar para adaptarlos a sus necesidades comerciales. Póngase en contacto con su administrador para comprender qué opciones de búsqueda están disponibles para su repositorio de DAM y qué restricciones tiene su cuenta.

### Resultados con y sin etiquetas inteligentes mejoradas {#withsmarttags}

De forma predeterminada, la búsqueda [!DNL Experience Manager] combina los términos de búsqueda con una cláusula AND. Por ejemplo, considere la búsqueda de palabras clave mujer en ejecución. De forma predeterminada, solo los recursos con palabras clave de mujer y de ejecución en los metadatos aparecen en los resultados de búsqueda. Se conserva el mismo comportamiento cuando se utilizan caracteres especiales (puntos, guiones bajos o guiones) con las palabras clave. Las siguientes consultas de búsqueda devuelven los mismos resultados:

* `woman running`
* `woman.running`
* `woman-running`

Sin embargo, la consulta `woman -running` devuelve activos sin `running` en sus metadatos.
El uso de etiquetas inteligentes agrega una cláusula `OR` adicional para encontrar cualquiera de los términos de búsqueda como las etiquetas inteligentes aplicadas. En una consulta de búsqueda también aparece un recurso etiquetado con `woman` o `running` mediante etiquetas inteligentes. Así que los resultados de la búsqueda son una combinación de:

* Recursos con palabras clave `woman` y `running` en los metadatos (comportamiento predeterminado).

* Recursos inteligentes etiquetados con cualquiera de las palabras clave (comportamiento de etiquetas inteligentes).

### Buscar sugerencias mientras escribe {#searchsuggestions}

Cuando empieza a escribir palabras clave, [!DNL Experience Manager] sugiere las posibles palabras clave o frases de búsqueda. Las sugerencias se basan en los metadatos de los recursos existentes. [!DNL Experience Manager] indexa todos los campos de metadatos para ayudarle con la búsqueda. Para proporcionar sugerencias de búsqueda, el sistema utiliza los valores de los siguientes campos de metadatos. Para proporcionar sugerencias de búsqueda, considere rellenar los campos siguientes con palabras clave adecuadas:

* Etiquetas de recursos. (se asigna a `jcr:content/metadata/cq:tags`)
* Título del recurso. (se asigna a `jcr:content/metadata/dc:title`)
* Descripción del recurso. (se asigna a `jcr:content/metadata/dc:description`)
* Título en el repositorio JCR. El valor puede asignarse al título del recurso. (se asigna a `jcr:content/jcr:title`)
* Descripción en el repositorio JCR. El valor puede asignarse a la descripción del recurso. (se asigna a `jcr:content/jcr:description`)

Para recibir sugerencias para más de una palabra clave de búsqueda, siga escribiendo todas las palabras clave sin seleccionar ninguna sugerencia para una sola palabra clave.

![Escriba varias palabras clave para ver las sugerencias que se ajustan a todas](assets/search_suggestionsmanykeywords.gif)

*Figura: Escriba varias palabras clave para ver las sugerencias que se ajustan a todas ellas.*

### Clasificación de búsqueda y aumento {#searchrank}

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. Coincide con `woman running` en los distintos campos de metadatos.
1. Coincide con `woman running` en las etiquetas inteligentes.
1. Coincide con `woman` o `running` en las etiquetas inteligentes.

Puede mejorar la relevancia de las palabras clave para recursos concretos para ayudar a impulsar las búsquedas basadas en palabras clave. En otras palabras, las imágenes para las que promociona palabras clave específicas aparecen en la parte superior de los resultados de búsqueda cuando realiza una búsqueda basada en estas palabras clave.

1. En la interfaz de usuario [!DNL Assets], abra la página de propiedades del recurso. Haga clic en **[!UICONTROL Avanzado]** y en **[!UICONTROL Agregar]** en **[!UICONTROL Elevar para palabras clave de búsqueda]**.
1. En el cuadro **[!UICONTROL Buscar promoción]**, especifique una palabra clave para la que desee impulsar la búsqueda de la imagen y haga clic en **[!UICONTROL Agregar]**. Puede especificar varias palabras clave del mismo modo.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**. El recurso que promocionó para esta palabra clave aparece entre los principales resultados de búsqueda.

Puede utilizarla en su beneficio si aumenta la clasificación de algunos recursos en los resultados de búsqueda de la palabra clave de destino. Consulte el siguiente vídeo de ejemplo. Para obtener información detallada, consulte [buscar en [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Vídeo: Comprender cómo se clasifican los resultados de búsqueda y cómo se puede influir en la clasificación.*

## Búsqueda avanzada {#scope}

[!DNL Experience Manager] proporciona varios métodos, como filtros que se aplican a los recursos buscados, para ayudarle a localizar los recursos que desee con mayor rapidez. A continuación se describen algunos de los métodos más utilizados. A continuación se comparten algunos [ejemplos ilustrados](#samples).

**Buscar archivos o carpetas**: En los resultados de búsqueda, consulte archivos, carpetas o ambos. En el panel **[!UICONTROL Filters]**, puede seleccionar la opción adecuada. Consulte [interfaz de búsqueda](#searchui).

**Buscar recursos dentro de una carpeta**: Puede limitar la búsqueda a una carpeta específica. En el panel **[!UICONTROL Filters]**, agregue la ruta de una carpeta. Solo puede seleccionar una carpeta a la vez.

![Limitar los resultados de búsqueda a una carpeta añadiendo una ruta de carpeta en el panel Filtros](assets/search_folder_select.gif)

*Figura: Limite los resultados de búsqueda a una carpeta agregando una ruta de carpeta en el panel Filtros .*

### Buscar imágenes similares {#visualsearch}

Para buscar imágenes que sean visualmente similares a una imagen seleccionada por el usuario, haga clic en la opción **[!UICONTROL Buscar similares]** en la vista de tarjeta de una imagen o en la barra de herramientas. [!DNL Experience Manager] muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. Consulte [cómo configurar la búsqueda por similitudes](#configvisualsearch).

![Buscar imágenes similares con la opción en la vista de tarjeta](assets/search_find_similar.png)

*Figura: Busque imágenes similares con la opción en la vista de tarjeta.*

### Imágenes de Adobe Stock {#adobe-stock}

Desde la interfaz de usuario [!DNL Experience Manager], los usuarios pueden buscar [Adobe Stock assets](/help/assets/aem-assets-adobe-stock.md) y obtener una licencia para los recursos necesarios. Agregue `Location: Adobe Stock` en la barra Omnisearch. También puede utilizar el panel Filtros para buscar todos los recursos con licencia o sin licencia, o buscar un recurso específico mediante el número de archivo de Adobe Stock.

### Recursos Dynamic Media {#dmassets}

Puede filtrar imágenes de Dynamic Media seleccionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** en el panel **[!UICONTROL Filtros]**. Filtra y muestra recursos como conjuntos de imágenes, carruseles, conjuntos de medios mixtos y conjuntos de giros.

### Búsqueda GQL que utiliza valores específicos en campos de metadatos {#gql-search}

Puede buscar recursos en función de los valores exactos de los campos de metadatos, como el título, la descripción y el creador. La función de búsqueda de texto completo de GQL solo recupera los recursos cuyo valor de metadatos coincide exactamente con la consulta de búsqueda. Los nombres de las propiedades (Creador, Título, etc.) y los valores distinguen entre mayúsculas y minúsculas.

| Campo de metadatos | Valor y uso de faceta |
|---|---|
| Título | title:John |
| Creador | creador:John |
| Lugar de residencia | ubicación:NA |
| Descripción | description: &quot;Imagen de muestra&quot; |
| Herramienta Creador | creatortool: &quot;Adobe Photoshop CC 2015&quot; |
| Propietario del copyright | copyright:&quot;Adobe Systems&quot; |
| Colaborador | colaborador:John |
| Condiciones de uso | usageterms:&quot;CopyRights Reserved&quot; |
| Creado | created:AAAA-MM-DDTHH |
| Fecha de caducidad | caduca:AAAA-MM-DTHH |
| Tiempo de activación | ontime:AAAA-MM-DDTHH |
| Tiempo de inactividad | offtime:AAAA-MM-DDTHH |
| Intervalo de tiempo (caduca dateontime, offtime) | campo de faceta : límite inferior..Upperbound |
| Ruta | /content/dam/&lt;nombre de carpeta> |
| Título del PDF | pdftitle:&quot;Documento de Adobe&quot; |
| Asunto | asunto: &quot;Formación&quot; |
| Etiquetas | etiquetas: &quot;Ubicación Y Viaje&quot; |
| Tipo | tipo: &quot;image\png&quot; |
| Anchura de la imagen | ancho:límite inferior..Upperbound |
| Altura de la imagen | height:lowerbound..Upperbound |
| Person | person:John |

Las propiedades `path`, `limit`, `size` y `orderby` no se pueden combinar con el operador `OR` con ninguna otra propiedad.

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

La palabra clave de una propiedad generada por el usuario es su etiqueta de campo en el editor de propiedades en minúsculas, con espacios eliminados.

A continuación se muestran algunos ejemplos de formatos de búsqueda para consultas complejas:

* Para mostrar todos los recursos con varios campos de facetas (por ejemplo: title=John Doe y la herramienta de creación = Adobe Photoshop): `title:"John Doe" creatortool:Adobe*`
* Para mostrar todos los recursos cuando el valor de facetas no es una sola palabra sino una frase (por ejemplo: title=Scott Reynolds): `title:"Scott Reynolds"`
* Para mostrar recursos con varios valores de una sola propiedad (por ejemplo: title=Scott Reynolds o John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Para mostrar recursos con valores de propiedad que empiecen por una cadena específica (por ejemplo: el título es Scott Reynolds): `title:Scott*`
* Para mostrar los recursos con valores de propiedad que terminan con una cadena específica (por ejemplo: el título es Scott Reynolds): `title:*Reynolds`
* Para mostrar recursos con un valor de propiedad que contenga una cadena específica (por ejemplo: título = Sala de reuniones de Basilea): `title:*Meeting*`
* Para mostrar los recursos que contienen una cadena concreta y tienen un valor de propiedad específico (por ejemplo: busque Adobe de cadena en los recursos que tengan title=John Doe): `*Adobe* title:"John Doe"`

## Buscar recursos de otras [!DNL Experience Manager] ofertas o interfaces {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] conecta el repositorio de DAM con varias otras  [!DNL Experience Manager] soluciones para proporcionar un acceso más rápido a los recursos digitales y optimizar los flujos de trabajo creativos. Cualquier detección de recursos comienza con la exploración o la búsqueda. El comportamiento de búsqueda sigue siendo el mismo en las distintas superficies y soluciones. Algunos métodos de búsqueda cambian a medida que la audiencia de destino, los casos de uso y la interfaz de usuario varían en las soluciones [!DNL Experience Manager]. Los métodos específicos se documentan para las soluciones individuales en los vínculos siguientes. Los consejos y comportamientos universalmente aplicables están documentados en este artículo.

### Buscar recursos desde el panel Vínculo de recursos de Adobe {#aal}

Al utilizar Adobe Asset Link, los profesionales creativos ahora pueden acceder al contenido almacenado en [!DNL Experience Manager Assets], sin salir de las aplicaciones de Adobe Creative Cloud compatibles. Los creativos pueden examinar, buscar, extraer y registrar recursos sin problemas mediante el panel en la aplicación de las aplicaciones [!DNL Adobe Creative Cloud]: [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] y [!DNL Adobe InDesign]. Asset Link también permite a los usuarios buscar resultados visualmente similares. Los resultados de visualización de la búsqueda visual utilizan algoritmos de aprendizaje automático de Adobe Sensei para ayudar a los usuarios a encontrar imágenes estéticas similares. Consulte [Buscar y examinar recursos](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) mediante el vínculo de recursos de Adobe.

### Buscar recursos en la aplicación de escritorio [!DNL Experience Manager] {#desktop-app}

Los profesionales creativos utilizan la aplicación de escritorio para que el [!DNL Experience Manager Assets] sea fácil de buscar y esté disponible en su escritorio local (Win o Mac). Los elementos creativos pueden revelar fácilmente los recursos deseados en el Buscador de Mac o en el Explorador de Windows, abrirlos en aplicaciones de escritorio y cambiarlos localmente. Los cambios se guardan de nuevo en [!DNL Experience Manager] con una nueva versión creada en el repositorio. La aplicación admite búsquedas básicas mediante una o más palabras clave, `*` y `?` comodines y el operador `AND`. Consulte [examinar, buscar y previsualizar recursos](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) en la aplicación de escritorio.

### Buscar recursos en [!DNL Brand Portal] {#brand-portal}

Los usuarios y especialistas en marketing de la línea de negocios utilizan Brand Portal para compartir de forma eficaz y segura los recursos digitales aprobados con sus equipos internos, socios y distribuidores ampliados. Consulte [Buscar recursos en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Buscar [!DNL Adobe Stock] imágenes {#adobe-stock1}

Desde la interfaz de usuario [!DNL Experience Manager], los usuarios pueden buscar recursos de Adobe Stock y obtener licencias para los recursos necesarios. Agregue `Location: Adobe Stock` en el campo Omnisearch . También puede utilizar el panel **[!UICONTROL Filtros]** para encontrar todos los recursos con licencia o sin licencia, o buscar un recurso específico mediante el número de archivo de Adobe Stock. Consulte [administrar [!DNL Adobe Stock] imágenes en [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Buscar [!DNL Dynamic Media] activos {#dynamic-media}

Puede filtrar imágenes de Dynamic Media seleccionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** en el panel **[!UICONTROL Filtros]**. Filtra y muestra recursos como conjuntos de imágenes, carruseles, conjuntos de medios mixtos y conjuntos de giros. Durante la creación de páginas web, los autores pueden buscar conjuntos desde el Buscador de contenido. Los filtros para conjuntos están disponibles en un menú emergente.

### Buscar recursos en el Buscador de contenido al crear páginas web {#content-finder}

Los autores pueden utilizar el buscador de contenido para buscar en el repositorio de DAM los recursos relevantes y utilizar los recursos en las páginas web que crean. Los autores también pueden utilizar la funcionalidad Recursos conectados para buscar recursos disponibles en una implementación remota [!DNL Experience Manager]. Los autores pueden utilizar estos recursos en páginas web en una implementación local [!DNL Experience Manager]. Consulte [usar recursos remotos](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### Buscar colecciones {#collections}

[!DNL Experience Manager] la capacidad de búsqueda admite la búsqueda de colecciones y la búsqueda de recursos dentro de una colección. Consulte [buscar colecciones](/help/assets/manage-collections.md).

## Selector de recursos {#asset-picker}

>[!NOTE]
>
>El selector de recursos se llamaba [selector de recursos](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) en versiones anteriores de [!DNL Adobe Experience Manager].

El selector de recursos permite buscar, filtrar y examinar los recursos DAM de una forma especial. El selector de recursos está disponible en `https://[aem_server]:[port]/aem/assetpicker.html`. Puede recuperar los metadatos de los recursos que seleccione mediante el selector de recursos. Puede iniciarlo con parámetros de solicitud admitidos, como el tipo de recurso (imagen, vídeo, texto) y el modo de selección (selección única o múltiple). Estos parámetros establecen el contexto del selector de recursos para una instancia de búsqueda en particular y permanecen intactos durante toda la selección.

El selector de recursos utiliza el mensaje HTML5 `Window.postMessage` para enviar datos del recurso seleccionado al destinatario. Solo funciona en el modo de exploración y solo con la página de resultados de Omnisearch.

Pase los siguientes parámetros de solicitud en una dirección URL para iniciar el selector de recursos en un contexto determinado:

| Nombre | Valores | Ejemplo | Función |
|---|---|---|---|
| sufijo de recurso (B) | Ruta de carpeta como sufijo de recurso en la URL: [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | Para iniciar el selector de recursos con una carpeta concreta seleccionada, por ejemplo con la carpeta `/content/dam/we-retail/en/activities` seleccionada, la dirección URL debe tener el siguiente formato: `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | Si necesita seleccionar una carpeta concreta cuando se inicia el selector de recursos, pasarla como sufijo de recurso. |
| `mode` | único, múltiple | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | En el modo múltiple, puede seleccionar varios recursos simultáneamente mediante el selector de recursos. |
| `dialog` | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Utilice estos parámetros para abrir el selector de recursos como cuadro de diálogo de Granite. Esta opción solo es aplicable cuando se inicia el selector de recursos a través de Granite Path Field y se configura como pickerSrc URL. |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | Utilice esta opción para especificar la carpeta raíz del selector de recursos. En este caso, el selector de recursos permite seleccionar solo recursos secundarios (directos/indirectos) en la carpeta raíz. |
| `viewmode` | búsqueda |  | Para iniciar el selector de recursos en modo de búsqueda, con los parámetros `assettype` y `mimetype` . |
| `assettype` | Imágenes, documentos, multimedia, archivos. | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | Utilice la opción para filtrar los tipos de recursos según el valor proporcionado. |
| `mimetype` | Tipo MIME (`/jcr:content/metadata/dc:format`) de un recurso (también se admite el comodín). | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | Utilícelo para filtrar recursos según el tipo MIME. |

Para acceder a la interfaz del selector de recursos, vaya a `https://[aem_server]:[port]/aem/assetpicker`. Vaya a la carpeta deseada y seleccione uno o varios recursos. Como alternativa, busque el recurso deseado en el cuadro Omnisearch , aplique el filtro según sea necesario y, a continuación, selecciónelo.

![Busque y seleccione un recurso en el selector de recursos](assets/assetpicker.png)

*Figura: Busque y seleccione un recurso en el selector de recursos.*

## Restricciones     {#limitations}

La capacidad de búsqueda en [!DNL Experience Manager Assets] tiene las siguientes limitaciones:

* No introduzca un espacio inicial en la consulta de búsqueda; de lo contrario, la búsqueda no funcionará.
* [!DNL Experience Manager] puede seguir mostrando el término de búsqueda después de seleccionar las propiedades de un recurso en los resultados de búsqueda y luego cancelar la búsqueda.  <!-- (CQ-4273540) -->
* Al buscar carpetas o archivos y carpetas, los resultados de la búsqueda no se pueden ordenar según ningún parámetro.
* Si selecciona `Return` sin escribir en la barra de Omnisearch, [!DNL Experience Manager] devuelve una lista de sólo archivos y no carpetas. Si busca carpetas específicamente sin usar una palabra clave, [!DNL Experience Manager] no devuelve ningún resultado.
* Puede realizar búsquedas de texto completo en carpetas. Especifique un término de búsqueda para que funcione la búsqueda.

La búsqueda visual o la búsqueda por similitudes tienen las siguientes limitaciones:

* La búsqueda visual funciona mejor con un repositorio grande. Aunque no hay un número mínimo de imágenes necesarias para obtener buenos resultados, la calidad de las coincidencias con algunas imágenes no es tan buena como las coincidencias de un repositorio grande.
* No puede cambiar el modelo o entrenar [!DNL Experience Manager] para encontrar imágenes similares. Por ejemplo, agregar o quitar etiquetas inteligentes a algunos recursos no cambia el modelo. Los recursos se excluyen de los resultados de búsqueda visualmente similares.

La funcionalidad de búsqueda puede tener limitaciones de rendimiento en los siguientes casos:

* La vista de tarjeta tiene un tiempo de carga más rápido que la vista de lista para mostrar los resultados de la búsqueda.

## Sugerencias de búsqueda {#tips}

* Cuando supervise el estado de revisión de los activos, utilice la opción adecuada para encontrar qué activos están aprobados o qué activos están pendientes de aprobación.
* Utilice el predicado de perspectivas para buscar recursos compatibles en función de las estadísticas de uso que obtengan de varias aplicaciones de Creative. Los datos de uso se agrupan en Puntuación de uso, Impresiones, Clics y Canales de medios, donde los recursos aparecen en categorías.
* Utilice la casilla de verificación **[!UICONTROL Seleccionar todo]** para seleccionar los recursos buscados. [!DNL Experience Manager] inicialmente muestra 100 recursos en la vista de tarjeta y 200 en la vista de lista. Se cargan más recursos a medida que se desplaza por los resultados de la búsqueda. Puede seleccionar más recursos que los cargados. El recuento de los recursos seleccionados se muestra en la esquina superior derecha de la página de resultados de la búsqueda. Puede operar en la selección, por ejemplo, descargar los recursos seleccionados, actualizar las propiedades de metadatos de forma masiva para los recursos seleccionados o agregar los recursos seleccionados a una colección. Cuando se seleccionan más recursos de los que se muestran, se aplica una acción a todos los recursos seleccionados o un cuadro de diálogo muestra el número de recursos sobre los que se aplica. Para aplicar una acción a los recursos que no se cargaron, asegúrese de que todos los recursos estén seleccionados explícitamente.
* Para buscar recursos que no contengan los metadatos obligatorios, consulte [metadatos obligatorios](#mandatorymetadata).
* La búsqueda utiliza todos los campos de metadatos. Una búsqueda genérica, como la búsqueda de 12, generalmente devuelve muchos resultados. Para obtener mejores resultados, utilice comillas dobles (no simples) o asegúrese de que el número esté contiguo a una palabra sin un carácter especial (por ejemplo `shoe12`).
* La búsqueda de texto completo admite operadores como `-` y `^`. Para buscar estas letras como literales de cadena, escriba la expresión de búsqueda entre comillas dobles. Por ejemplo, utilice `"Notebook - Beauty"` en lugar de `Notebook - Beauty`.
* Si los resultados de búsqueda son demasiados, limite el [ámbito de búsqueda](#scope) a cero en los recursos deseados. Funciona mejor cuando tiene alguna idea de cómo buscar mejor los recursos deseados, por ejemplo, tipo de archivo específico, ubicación específica, metadatos específicos, etc.

* **Etiquetado**: Las etiquetas ayudan a categorizar los recursos que se pueden explorar y buscar de forma más eficaz. El etiquetado ayuda a propagar la taxonomía adecuada a otros usuarios y flujos de trabajo. [!DNL Experience Manager] ofrece métodos para etiquetar recursos automáticamente mediante los servicios artificialmente inteligentes de Adobe Sensei que siguen mejorando el etiquetado de sus recursos con uso y formación. Al buscar recursos, las etiquetas inteligentes se tienen en cuenta si la función está habilitada en la cuenta. Funciona junto con la funcionalidad de búsqueda integrada. Consulte [comportamiento de búsqueda](#searchbehavior). Para optimizar el orden en que se muestran los resultados de la búsqueda, puede [mejorar la clasificación de la búsqueda](#searchrank) de algunos recursos seleccionados.

* **Indexación**: En los resultados de búsqueda solo se devuelven los metadatos y recursos indexados. Para obtener una mejor cobertura y un mejor rendimiento, asegúrese de realizar una indexación adecuada y siga las prácticas recomendadas. Consulte [indexación](#searchindex).

* Para excluir recursos específicos de los resultados de búsqueda, utilice la propiedad `excludedPath` en el índice de Lucene.

## Algunos ejemplos que ilustran la búsqueda {#samples}

Utilice comillas dobles alrededor de las palabras clave para encontrar recursos que contengan la frase exacta en el orden exacto especificado por el usuario.

![Comportamiento de búsqueda con y sin comillas](assets/search_with_quotes.gif)

*Figura: Comportamiento de búsqueda con y sin comillas.*

**Buscar con comodín de asterisco**: Para ampliar la búsqueda, utilice un asterisco antes o después de la palabra de búsqueda para que coincida con cualquier número de caracteres. Por ejemplo, si se busca ejecutar sin un asterisco, no se devuelven recursos que contengan ninguna variación de la palabra (incluidos los metadatos). Un asterisco sustituye a cualquier número de caracteres. Por ejemplo,

* `run` devuelve activos con la palabra clave &quot;run&quot; exactamente
* `run*` devuelve recursos con  `running`,  `run`,  `runaway`, etc.
* `*run` devuelve recursos con  `outrun`,  `rerun`, etc.
* `*run*` devuelve todas las combinaciones posibles.

![Ilustración del uso de un comodín de asterisco en la búsqueda de recursos mediante un ejemplo](assets/search_with_asterisk_run.gif)

*Figura: Ilustración del uso de un comodín de asterisco en la búsqueda de recursos mediante un ejemplo.*

**Buscar con comodín** de signo de interrogación: Para ampliar la búsqueda, utilice uno o más &quot;?&quot; para que coincida con el número exacto de caracteres. Por ejemplo, en la siguiente ilustración,

* `run???` La consulta no coincide con ningún recurso.

* `run????` query coincide con la palabra  `running` con cuatro caracteres después de  `run`.

* `??run` La consulta coincide con la palabra  `rerun` con dos caracteres antes de  `run`.

![Ilustración del uso del comodín del signo de interrogación en la búsqueda de recursos mediante un ejemplo](assets/search_with_questionmark_run.gif)

*Figura: Ilustración del uso del comodín del signo de interrogación en la búsqueda de recursos mediante un ejemplo.*

**Excluir una palabra clave**: Utilice el guión para buscar recursos que no contengan una palabra clave. Por ejemplo, la consulta `running -shoe` devuelve recursos que contienen `running`, pero no `shoe`. Del mismo modo, la consulta `camp -night` devuelve recursos que contienen `camp` pero no `night`. La consulta `camp-night` devuelve recursos que contienen `camp` y `night`.

![Uso del guión para buscar recursos que no contienen una palabra clave excluida](assets/search_dash_exclude_keyword.gif)

*Figura: Uso del guión para buscar recursos que no contengan una palabra clave excluida.*

## Tareas de configuración y administración relacionadas con la funcionalidad de búsqueda {#configadmin}

### Configuraciones de índice de búsqueda {#searchindex}

La detección de recursos se basa en la indexación del contenido de DAM, incluidos los metadatos. La detección de recursos más rápida y precisa depende de la indexación optimizada y las configuraciones adecuadas. Consulte [índice de búsqueda](/help/assets/performance-tuning-guidelines.md#search-indexes), [consultas oak e indexación](/help/sites-deploying/queries-and-indexing.md) y [prácticas recomendadas](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

Para excluir recursos específicos de los resultados de búsqueda, utilice la propiedad `excludedPath` en el índice de Lucene.

### Búsqueda visual o de similitud {#configvisualsearch}

La búsqueda visual utiliza etiquetas inteligentes. Después de configurar la funcionalidad de etiquetado inteligente, siga estos pasos.

1. En [!DNL Experience Manager] CRXDE, en el nodo `/oak:index/lucene`, agregue las siguientes propiedades y valores y guarde los cambios.

   * `costPerEntry` propiedad de tipo  `Double` con el valor  `10`.
   * `costPerExecution` propiedad de tipo  `Double` con el valor  `2`.
   * `refresh` propiedad de tipo  `Boolean` con el valor  `true`.

   Esta configuración permite realizar búsquedas desde el índice adecuado.

1. Para crear el índice de Lucene, en CRXDE, en `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, cree el nodo `imageFeatures` de tipo `nt-unstructured`. En el nodo `imageFeatures`,

   * Agregue la propiedad `name` del tipo `String` con el valor `jcr:content/metadata/imageFeatures/haystack0`.
   * Agregue la propiedad `nodeScopeIndex` del tipo `Boolean` con el valor `true`.
   * Agregue la propiedad `propertyIndex` del tipo `Boolean` con el valor `true`.
   * Agregue la propiedad `useInSimilarity` del tipo `Boolean` con el valor `true`.

   Guarde los cambios.

1. Acceda a `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` y añada la propiedad `similarityTags` del tipo `Boolean` con el valor `true`.
1. Aplique etiquetas inteligentes a los recursos de su repositorio [!DNL Experience Manager]. Consulte [cómo configurar las etiquetas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html?lang=en#configuring).
1. En CRXDE, en el nodo `/oak-index/damAssetLucene`, establezca la propiedad `reindex` en `true`. Guarde los cambios.
1. (Opcional) Si tiene un formulario de búsqueda personalizado, copie el nodo `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` en `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Guarde los cambios.

Para obtener información relacionada, consulte [comprensión de las etiquetas inteligentes en Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) y [cómo administrar las etiquetas inteligentes](/help/assets/enhanced-smart-tags.md).

>[!CAUTION]
>
>Si la indexación de Lucene se realiza a partir de [!DNL Adobe Experience Manager], la búsqueda basada en etiquetas inteligentes no funciona como se espera.

### Metadatos obligatorios {#mandatorymetadata}

Los usuarios empresariales, administradores o bibliotecarios de DAM pueden definir algunos metadatos como metadatos obligatorios que son imprescindibles para que funcionen los procesos empresariales. Por varios motivos, es posible que a algunos recursos les falten estos metadatos, como recursos heredados o recursos migrados de forma masiva. Los recursos con metadatos que faltan o no son válidos se detectan y generan informes en función de la propiedad de metadatos indexados. Para configurarlo, consulte [metadatos obligatorios](/help/assets/metadata-schemas.md#define-mandatory-metadata).

### Modificar facetas de búsqueda {#searchfacets}

Para mejorar la velocidad de detección, [!DNL Experience Manager Assets] ofrece facetas de búsqueda mediante las cuales puede filtrar los resultados de búsqueda. El panel Filtros incluye algunas facetas estándar de forma predeterminada. Los administradores pueden personalizar el panel Filtros para modificar las facetas predeterminadas mediante los predicados integrados. [!DNL Experience Manager] proporciona una buena colección de predicados integrados y un editor para personalizar las facetas. Consulte [facetas de búsqueda](/help/assets/search-facets.md).

### Extraer texto al cargar recursos {#extracttextupload}

Puede configurar [!DNL Experience Manager] para extraer el texto de los recursos cuando los usuarios cargan recursos, como archivos PSD o PDF. [!DNL Experience Manager] indexa el texto extraído y ayuda a los usuarios a buscar en estos recursos en función del texto extraído. Consulte [carga de recursos](/help/assets/manage-assets.md#uploading-assets).

Si la extracción de texto consume demasiados recursos para la implementación, considere la posibilidad de [deshabilitar la extracción de texto](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html).

### Predicados personalizados para filtrar los resultados de búsqueda {#custompredicates}

Los predicados se utilizan para crear facetas. Los administradores pueden personalizar las facetas de búsqueda en el panel Filtros mediante predicados preconfigurados. Estos predicados se pueden personalizar mediante superposiciones. Consulte [crear predicados personalizados](/help/assets/searchx.md).

Puede buscar recursos digitales en función de una o varias de las siguientes propiedades. Los filtros que se aplican a algunas de estas propiedades están disponibles de forma predeterminada y se pueden crear algunos otros filtros personalizados para aplicarlos a las otras propiedades.

| Campo de búsqueda | Buscar valores de propiedades |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Tipos MIME | Imágenes, documentos, multimedia, archivos u otros. |
| Última modificación | Hora, día, semana, mes o año. |
| Tamaño del archivo | Pequeño, Medio o Grande. |
| Estado de publicación | Publicado o no publicado. |
| Estado aprobado | Aprobado o rechazado. |
| Orientación | Horizontal, Vertical o Cuadrado. |
| Estilo | Color o blanco y negro. |
| Altura del vídeo | Especificado como valor mínimo y máximo. El valor solo se almacena en los metadatos de representaciones de vídeo. |
| Anchura del vídeo | Especificado como valor mínimo y máximo. El valor solo se almacena en los metadatos de representaciones de vídeo. |
| Formato de vídeo | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. El valor se almacena en los metadatos del vídeo de origen y en cualquier representación. |
| Códec de vídeo | x264. El valor solo se almacena en los metadatos de representaciones de vídeo. |
| Velocidad de bits de vídeo | Especificado como valor mínimo y máximo. El valor solo se almacena en los metadatos de representaciones de vídeo. |
| Códec de audio | Libvorbis, Lame MP3, AAC Encoding. El valor solo se almacena en los metadatos de representaciones de vídeo. |
| Velocidad de bits de audio | Especificado como valor mínimo y máximo. El valor solo se almacena en los metadatos de representaciones de vídeo. |

## Trabajar con resultados de búsqueda de recursos {#aftersearch}

Puede hacer lo siguiente con los recursos que ha buscado en [!DNL Experience Manager]:

* Vea las propiedades de los metadatos y otra información.
* Descargue uno o varios recursos.
* Utilice las acciones de escritorio para abrir estos recursos en la aplicación de escritorio.
* Cree colecciones inteligentes.

### Ordenar resultados de búsqueda {#sort}

Ordene los resultados de búsqueda para descubrir los recursos necesarios más rápido. Puede ordenar los resultados de búsqueda en la vista de lista y solo cuando selecciona **[[!UICONTROL Archivos]](#searchui)** en el panel **[!UICONTROL Filtros]**. [!DNL Assets] utiliza la ordenación del lado del servidor para ordenar rápidamente todos los recursos (aunque sean muchos) de una carpeta o los resultados de una consulta de búsqueda. La ordenación del lado del servidor proporciona resultados más rápidos y precisos que la ordenación del lado del cliente.

En la vista de lista, puede ordenar los resultados de búsqueda del mismo modo que puede ordenar los recursos en cualquier carpeta. La ordenación funciona en estas columnas: Nombre, Título, Estado, Dimension, Tamaño, Clasificación, Uso, (Fecha) Creado, (Fecha) Modificado, (Fecha) Publicado, Flujo de trabajo y Desprotegido.

Para ver las limitaciones de la funcionalidad de ordenación, consulte [limitaciones](#limitations).

### Compruebe la información detallada de un recurso {#checkinfo}

Puede comprobar la información detallada de los recursos buscados desde la página de resultados de la búsqueda.

Para ver todos los metadatos de un recurso, seleccione el recurso y haga clic en **[!UICONTROL properties]** en la barra de herramientas.

Para comprobar los comentarios de un recurso o del historial de versiones de un recurso, haga clic en el recurso y abrirá una vista previa de gran tamaño. Abra la cronología en el carril izquierdo y seleccione **[!UICONTROL Comentarios]** o **[!UICONTROL Versiones]**. También puede ordenar la actividad de la cronología como comentarios o versiones en orden cronológico.

![Ordenar entradas de línea de tiempo para un recurso de búsqueda](assets/sort_timeline_search_results.gif)

*Figura: Ordene las entradas de la cronología de un recurso de búsqueda.*

### Descargar recursos buscados {#download}

Puede descargar los recursos buscados y sus representaciones del mismo modo que descarga los recursos habituales de las carpetas. Seleccione uno o varios recursos en los resultados de búsqueda y haga clic en **[!UICONTROL Descargar]** en la barra de herramientas.

### Propiedades de metadatos de actualización masiva {#metadataupdates}

Es posible realizar actualizaciones masivas en los campos de metadatos comunes de varios recursos. En los resultados de la búsqueda, seleccione uno o varios recursos. Haga clic en **[!UICONTROL Properties]** en la barra de herramientas y actualice los metadatos según sea necesario. Haga clic en **[!UICONTROL Guardar y cerrar]** cuando termine. Se sobrescriben los metadatos existentes anteriormente en los campos actualizados.

Para los recursos disponibles en una única carpeta o en una colección, es más fácil [actualizar los metadatos de forma masiva](/help/assets/metadata.md) sin utilizar la funcionalidad de búsqueda. Para los recursos disponibles en todas las carpetas o que coinciden con criterios comunes, es más rápido actualizar los metadatos de forma masiva mediante la búsqueda.

### Colecciones inteligentes {#smart-collections}

Una colección es un conjunto ordenado de recursos que pueden incluir recursos de distintas ubicaciones porque las colecciones solo contienen referencias a estos recursos. Las colecciones son de los dos tipos siguientes:

* Una lista de referencia estática de recursos, carpetas y otras colecciones.
* Lista dinámica (colección inteligente) que rellena los recursos de la colección en función de criterios de búsqueda.

Puede crear colecciones inteligentes basadas en los criterios de búsqueda. En el panel **[!UICONTROL Filtros]**, seleccione **[!UICONTROL Archivos]** y haga clic en **[!UICONTROL Guardar colección inteligente]**. Consulte [Gestión de colecciones](/help/assets/manage-collections.md).

## Resultados y problemas de búsqueda inesperados {#unexpected-results}

| Error, problemas, síntomas | Motivo posible | Posible solución o comprensión del problema |
|---|---|---|
| Resultados incorrectos al buscar recursos con metadatos ausentes. | Al buscar recursos que no tengan los metadatos obligatorios, [!DNL Experience Manager] puede mostrar algunos recursos que tengan metadatos válidos. Los resultados se basan en la propiedad de metadatos indexados. | Una vez actualizados los metadatos, es necesario volver a indexar para reflejar el estado correcto de los metadatos de los recursos. Consulte [metadatos obligatorios](metadata-schemas.md#define-mandatory-metadata). |
| Demasiados resultados de búsqueda. | Parámetro de búsqueda amplia. | Considere limitar el [ámbito de búsqueda](#scope). El uso de etiquetas inteligentes puede proporcionar más resultados de búsqueda de los esperados. Consulte [comportamiento de búsqueda con etiquetas inteligentes](#withsmarttags). |
| Resultados de búsqueda no relacionados o parcialmente relacionados. | El comportamiento de búsqueda cambia con el etiquetado inteligente. | Comprenda [cómo cambia la búsqueda después del etiquetado inteligente](#withsmarttags). |
| No hay sugerencias de autocompletar para los recursos. | Los recursos cargados recientemente aún no están indexados. Los metadatos no están disponibles inmediatamente como sugerencias cuando empieza a escribir una palabra clave de búsqueda en la barra Omnisearch. | [!DNL Experience Manager] espera hasta la caducidad de un tiempo de espera (una hora de forma predeterminada) antes de ejecutar un trabajo en segundo plano para indexar los metadatos de todos los recursos cargados o actualizados recientemente y, a continuación, agrega los metadatos a la lista de sugerencias. |
| No hay resultados de la búsqueda. | <ul><li>Los recursos que coinciden con la consulta no existen. </li><li> Se ha añadido un espacio en blanco antes de la consulta de búsqueda. </li><li> El campo de metadatos no compatibles contiene la palabra clave que buscó.</li><li> Búsqueda realizada durante el tiempo de inactividad de un recurso. </li></ul> | <ul><li>Buscar usando una palabra clave diferente. Alternativamente, utilice etiquetado inteligente o búsqueda por similitudes para mejorar los resultados de la búsqueda. </li><li>[Limitación conocida](#limitations).</li><li>Todos los campos de metadatos no se tienen en cuenta en las búsquedas. Consulte [ámbito](#scope).</li><li>Busque más tarde o modifique en tiempo real y fuera de tiempo los recursos necesarios.</li></ul> |
| Un filtro de búsqueda o un predicado no está disponible. | <ul><li>El filtro de búsqueda no está configurado.</li><li>No está disponible para su inicio de sesión.</li><li>(Menos probable) Las opciones de búsqueda no están personalizadas en la implementación que está utilizando.</li></ul> | <ul><li>Póngase en contacto con el administrador para comprobar si las personalizaciones de búsqueda están disponibles o no.</li><li>Póngase en contacto con el administrador para comprobar si su cuenta tiene los privilegios/permisos para utilizar la personalización.</li><li>Póngase en contacto con el administrador y compruebe las personalizaciones disponibles para la implementación [!DNL Assets] que está utilizando.</li></ul> |
| Al buscar imágenes visualmente similares, falta una imagen esperada. | <ul><li>La imagen no está disponible en [!DNL Experience Manager].</li><li>La imagen no está indexada. Normalmente, cuando se carga recientemente.</li><li>La imagen no está etiquetada de forma inteligente.</li></ul> | <ul><li>Agregue la imagen a [!DNL Assets].</li><li>Póngase en contacto con el administrador para volver a indexar el repositorio. Además, asegúrese de que está utilizando el índice adecuado.</li><li>Póngase en contacto con el administrador para etiquetar de forma inteligente los recursos relevantes.</li></ul> |
| Al buscar imágenes visualmente similares, se muestra una imagen irrelevante. | Comportamiento de búsqueda visual. | [!DNL Experience Manager] muestra tantos recursos potencialmente relevantes como sea posible. Las imágenes menos relevantes, si las hay, se añaden a los resultados, pero con una clasificación de búsqueda inferior. La calidad de las coincidencias y la relevancia de los recursos buscados disminuyen a medida que se desplaza hacia abajo por los resultados de la búsqueda. |
| Al seleccionar y operar en los resultados de búsqueda, no se utilizan todos los recursos buscados. | La opción [!UICONTROL Seleccionar todo] solo selecciona los primeros 100 resultados de búsqueda en la vista de tarjeta y los primeros 200 resultados de búsqueda en la vista de lista. |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] guía de implementación de búsqueda](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configuración avanzada para mejorar los resultados de búsqueda](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Configurar la búsqueda de traducción inteligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

