---
title: Creación de experiencias comerciales
description: Experiencias comerciales en trabajo
exl-id: 2db51bd7-8fc7-4ae8-8d6f-e5035fbe954d
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Creación de experiencias comerciales {#authoring-commerce-experiences}

## Información general {#overview}

El complemento CIF amplía AEM creación con capacidades específicas del comercio. Esto permite a los autores crear y administrar de forma eficaz experiencias relacionadas con el comercio al obtener acceso a los datos del producto y al contenido sin abandonar el contexto.

## Pickers {#pickers}

Los selectores de producto y categoría son cuadros de diálogo de interfaz de usuario modales que ofrecen una forma cómoda para que los autores de AEM encuentren y seleccionen productos o categorías cuando sea necesario. Los componentes principales, la asociación de contenido y las plantillas de producto son las áreas típicas con configuraciones que requieren datos del catálogo de productos. Los seleccionadores admiten diversas opciones de configuración, como selección múltiple, selección de variaciones y selección previa de valores.

### Selector de productos {#product-picker}

Este selector ofrece explorar la estructura del catálogo o la búsqueda de texto completo para encontrar el producto. Los productos con variación ofrecen un icono de carpeta en la columna &quot;Tipo&quot;. Al hacer clic en el icono de carpeta, se abren las variaciones del producto seleccionado.

![Selector de producto](/help/commerce/cif/assets/authoring/product-picker.png)

Al hacer clic en la categoría principal, el autor volverá al nivel de producto.

![Selector de producto](/help/commerce/cif/assets/authoring/product-picker-variation.png)

**Ejemplo de teaser de productos**

![Componente teaser sin selección](/help/commerce/cif/assets/authoring/teaser_component_without_selection.png)

El cuadro de diálogo de configuración de este componente requiere un producto. CIF utiliza el SKU como identificador de producto. Los autores pueden entrar al sku a mano o hacer clic en el icono de la carpeta para abrir el selector de productos. Después de seleccionar y cerrar el selector, el cuadro de diálogo del componente muestra el nombre del producto seleccionado

![Componente teaser con selección](/help/commerce/cif/assets/authoring/teaser_component_with_selection.png)

### Selector de categoría {#category-picker}

Este selector ofrece explorar la estructura del catálogo para encontrar la categoría.

![Selector de categoría](/help/commerce/cif/assets/authoring/category-picker.png)

**Ejemplo de carrusel de categoría**

![Componente de carrusel sin selección](/help/commerce/cif/assets/authoring/carousel_component_without_selection.png)

El cuadro de diálogo de configuración de este componente requiere 1 : n categorías. CIF utiliza el UID/ID como identificador de categoría. Los autores pueden introducir el UID manualmente o hacer clic en el icono de la carpeta para abrir el selector de categorías. Después de seleccionar y cerrar el selector, el cuadro de diálogo del componente muestra el nombre de la categoría seleccionada.

![Componente de carrusel con selección](/help/commerce/cif/assets/authoring/carousel_component_with_selection.png)

## Editor universal {#universal-editor}

El editor universal se ha ampliado con funciones para acceder a los datos de productos en tiempo real y al contenido de productos asociado.

### Acceso a los datos del producto {#access-product-data}

La pestaña &quot;Recursos&quot; del panel lateral del editor ofrece acceso a los datos del producto seleccionando el tipo &quot;Productos&quot;. Los datos se recuperan en vivo desde el extremo de comercio configurado. El filtro es una búsqueda de texto completo en el extremo de comercio para encontrar productos específicos.

![Panel lateral de datos del producto](/help/commerce/cif/assets/authoring/products-side-panel.png)

Análogo a los recursos, los productos se pueden añadir en una página (que crea un componente teaser de productos como predeterminado) o en componentes (Actualmente se admiten teaser de productos y carrusel de productos).

### Adición de vínculos en campos de texto mediante RTE {#rte}

Las páginas del catálogo de productos CIF son páginas virtuales que se procesan sobre la marcha. Por lo tanto, no es posible incrustar hipervínculos como para páginas de AEM normales. CIF agrega una nueva acción &quot;Vínculos comerciales&quot; a RTE (Editor de texto enriquecido). Esta acción funciona exactamente igual que la acción &quot;Hipervínculo&quot; normal, pero permite a los autores seleccionar un producto o una categoría mediante los selectores.

![RTE](/help/commerce/cif/assets/authoring/RTE.png)

    >[!NOTE]
    >
    >Si se seleccionan la categoría y el producto, se toma el producto.

Esto crea un vínculo de marcador de posición que se sustituye por un vínculo real cuando se representa la página.

### Acceso al contenido de producto asociado {#associated-content}

Si el Editor universal reconoce los productos de 1:n en una página, el panel lateral mostrará automáticamente la pestaña &quot;Contenido de comercio asociado&quot;. Esta pestaña permite a los autores acceder rápidamente AEM contenido que se ha etiquetado con el producto (consulte [enriquecer los datos del producto con contenido de AEM asociado](./enrich-product-associated-content.md) para obtener más información). Esta pestaña ofrece menús desplegables para filtrar por tipo de contenido y productos específicos si hay varios productos en la página. El uso del contenido funciona exactamente igual que el uso del contenido de la pestaña &quot;Recursos&quot;.

![Panel lateral de datos del producto](/help/commerce/cif/assets/authoring/associated-commerce-content-tab.png)

### Vista previa de datos de producto escalonados {#staged-data}

El modo Deformación de tiempo en el editor permite a los autores previsualizar y examinar una experiencia AEM con datos del catálogo de productos clasificados en función de la fecha Deformación de tiempo.

![Deformación de tiempo  ](/help/commerce/cif/assets/authoring/timewarp.png)

Los componentes muestran un indicador visual si la fecha utilizada está escalonada.

![Indicador escalonado](/help/commerce/cif/assets/authoring/staged-indicator.png)

## Omnisearch {#omnisearch}

El uso de Omnisearch es una forma sencilla de que los profesionales encuentren AEM contenido y datos del catálogo de productos mediante la búsqueda de texto completo. Omnisearch ejecutará la búsqueda de texto completo en AEM y el back-end de comercio para encontrar objetos de catálogo de productos en el backend de comercio y en el contenido de AEM. AEM resultados también incluyen contenido que se etiquetó con datos de producto/categoría.

![Omnisearch](/help/commerce/cif/assets/authoring/omnisearch.png)

El resultado se agrupa por tipo.

    >[!NOTE]
    >
    >La búsqueda de texto completo en Omnisearch no admite fragmentos de contenido asociados. Utilice el SKU o el UID para buscar fragmentos de contenido asociados.
