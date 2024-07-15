---
title: AEM Notas de la versión 2019 de Content and Commerce
description: Contenido de Adobe Experience Manager y notas de la versión de Commerce 2019.
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 6%

---

# Información general sobre la versión de Commerce integration framework GitHub

## Fecha de versión: noviembre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| CIF Conector de | 0,7,1 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Componentes principales | 0,6,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Tipo de archivo de | 0,6,2 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-november}

* Los autores pueden obtener una vista previa de las páginas de detalles y listas de productos con productos/categorías con una nueva opción &quot;Ver con producto/categoría&quot; en el editor de Sites.

* Los autores pueden etiquetar recursos por SKU del producto y buscar recursos específicos del producto por SKU.

* Se ha agregado compatibilidad con cupones en el carro de compras.

* Se ha agregado soporte de pago para Braintree AEM en la tienda Venia en la parte delantera.

### Qué se ha mejorado {#what-is-improved-november}

* Los selectores de categorías/productos se mejoraron para respetar la vista de tienda de Adobe Commerce especificada en una configuración de varias tiendas.

* Los componentes basados en React están disponibles como paquete npm. Esto permite a los desarrolladores utilizar el paquete de componentes de React como dependencia para un nuevo proyecto de React para permitir la personalización de componentes existentes o desarrollar nuevos componentes basados en React.

* La personalización de consultas de GraphQL está simplificada. CIF Esto permite a los desarrolladores personalizar los componentes principales de la con menos código.

## Fecha de versión: octubre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| CIF Conector de | 0,6,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Componentes principales | 0,5,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Tipo de archivo de | 0,5,0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-october}

* Plantillas totalmente legibles para la página de detalles del producto y la página de lista del producto. Los autores ahora pueden crear plantillas y arrastrar y soltar componentes de lista de productos y detalles de productos en estas plantillas. Además de añadir otros componentes, los autores ahora pueden cambiar el diseño de estas plantillas también, lo que les da una libertad ilimitada para crear experiencias increíbles que combinen contenido de marketing y comercio.

* CIF AEM Se han mejorado todos los componentes principales de la aplicación de creación fácil de usar para admitir el sistema de estilos [. ](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html) Se han proporcionado estilos de ejemplo para el componente de lista de productos.

* Componentes del lado del cliente basados en React para la administración de cuentas. Esta versión admite las siguientes funcionalidades: Inicio de sesión, Olvidé la contraseña y Crear una cuenta.

### Qué se ha mejorado {#what-is-improved-october}

* Los componentes de detalles de producto y lista de productos se han mejorado para mostrar datos ficticios a fin de proporcionar a los autores una vista previa del diseño cuando estos componentes se colocan en una plantilla o página.

* Los componentes Minicart y Checkout ahora utilizan los enlaces de React para mejorar la extensibilidad.

## Fecha de versión: septiembre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| CIF Conector de | 0,5,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Componentes principales | 0,4,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Tipo de archivo de | 0,4,0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-september}

* La función de varias plantillas permite a los autores enriquecer una página de detalles de producto o una página de lista de productos específica. Los autores pueden crear fácilmente una página de detalles de producto personalizada o una página de lista de productos y utilizar el selector de productos o categorías para asignar la página personalizada a un producto o categoría específicos.

* AEM Enlace de varios catálogos para permitir que los autores enlacen varios catálogos en la consola de producto de la. Los autores también pueden editar y ver las propiedades de enlace del catálogo después de crear el enlace.

* React-based client-side Checkout and Mini Cart con GraphQL para ofrecer un recorrido de compra básico completo.

* El componente Pago y envío incluye formularios de dirección, selección de pago y selección de métodos de envío.

### Qué se ha mejorado {#what-is-improved-september}

* Los componentes teaser y carrusel de productos admiten variantes de productos.

## Fecha de versión: agosto de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| CIF Conector de | 0,4,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Componentes principales | 0,3,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Tipo de archivo de | 0,3,0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-august}

* CIF CIF La incrustación de conector de en el tipo de archivo de se convierte en opcional para proporcionar a los desarrolladores más flexibilidad.

* CIF Componentes desacoplados del estilo CSS específico de &quot;Venia&quot; para permitir a los desarrolladores aplicar el estilo CSS de su elección.

* CIF AEM Función de varias tiendas y sitios para permitir el uso de componentes principales de la en varias estructuras de sitio y permitir que la implementación de cliente de GraphQL subyacente se conecte a diferentes vistas de tiendas y tiendas de Adobe Commerce.

* El almacenamiento en caché de GraphQL está habilitado para determinadas consultas de GraphQL a través de la GET HTTP para reducir el tiempo de respuesta.

* AEM La vista de descripción del producto está habilitada en la consola Productos de.

* Teaser de Commerce amplía el componente Teaser de WCM para permitir a los autores agregar también campos de CTA a una página de detalles de producto o a una página de lista de productos.

* AEM AEM Botón para permitir que los autores coloquen en una página de y enlacen a una página de producto, página de detalles del producto, página de lista del producto o un enlace externo.

### Qué se ha mejorado {#what-is-improved-august}

* La configuración de la tienda de Adobe Commerce AEM se movió de OSGi a la consola de producto de para que la configuración de la integración sea más fácil de crear.

## Fecha de versión: julio de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| CIF Conector de | 0,3,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Componentes principales | 0,2,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Tipo de archivo de | 0,2,0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-july}

* CIF AEM Primer tipo de archivo que proporciona a los desarrolladores varias opciones de implementación: 1.Implementar la tienda de Venia 2. Implementar andamiaje para un nuevo proyecto 3. CIF Uso de elementos de un proyecto existente

* Navegación por catálogo de varios niveles para admitir la navegación por categorías y subcategorías.

* Paginación en páginas de categoría para una mejor experiencia de usuario.

* Representación del atributo de precio en el lado del cliente en los componentes Detalle del producto y Lista del producto para admitir la representación de atributos dinámicos.

* Carrusel de productos del lado del servidor para mostrar una lista de los productos destacados en un estilo de carrusel.

* AEM Lista de categorías destacadas del lado del servidor para mostrar una lista de categorías en una página de la página de la.

### Qué se ha mejorado {#what-is-improved-july}

* La compatibilidad con Adobe Commerce 2.3.2 y las correcciones de errores relacionadas con las propiedades del producto se muestran en la consola del producto.

## Fecha de versión: junio de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| CIF Conector de | 0,2,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF Componentes principales | 0.1.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |

### Novedades {#what-is-new-june}

* AEM Tienda B2C con estilo Venia CSS con prioridad móvil, página de aterrizaje, navegación dinámica por el catálogo a través de páginas de productos y categorías, página de búsqueda de productos y funciones del carro de compras para iniciar y acelerar proyectos de comercio.

* CIF AEM Herramientas de creación y conector de datos (consola de producto, selector de productos y selector de categorías) para permitir a los autores crear experiencias en el área de la con contenido comercial.

* CIF Primera versión de componentes principales de la compatible con Adobe Commerce 2.3.1:
   * Detalles del producto
   * Lista de productos
   * Teaser de productos
   * Navegación
   * Búsqueda de productos
   * Carro de compras (REST)
