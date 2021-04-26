---
title: Notas de la versión de contenido y comercio de AEM 2021
description: Notas de la versión de contenido y comercio de AEM 2021
translation-type: tm+mt
source-git-commit: c2fb9af056fa4be13cfd7e60e8a44485e8712c0b
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 10%

---

# Información general sobre la versión de Commerce Integration Framework GitHub

## Fecha de versión: Noviembre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 0,7,1 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0,6,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Tipo de archivo del CIF | 0,6,2 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-november}

* Los autores pueden obtener una vista previa de las páginas de lista de productos y de los detalles de los productos con una nueva opción &quot;Ver con producto/categoría&quot; en el editor de sitios.

* Los autores pueden etiquetar recursos por SKU de producto y buscar recursos específicos de producto por SKU.

* Se ha añadido o eliminado la compatibilidad con cupones en el carro de compras.

* Se agregó soporte de pago para Braintree en AEM tienda Venia.

### Mejoras {#what-is-improved-november}

* Selector de categoría/producto mejorado para respetar la vista especificada del almacén de Magento en una configuración de varias tiendas.

* Componentes basados en React disponibles como paquete npm. Esto permite a los desarrolladores utilizar el paquete React Components como dependencia de un nuevo proyecto React para permitir la personalización de componentes existentes o desarrollar nuevos componentes basados en React.

* Se ha simplificado la personalización de consultas de GraphQL. Esto permite a los desarrolladores personalizar los componentes principales del CIF con menos código.

## Fecha de versión: Octubre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 0,6,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0,5,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Tipo de archivo del CIF | 0,5,0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-october}

* Plantillas totalmente autorizables para la página de detalles del producto y la página de lista de productos. Los autores ahora pueden crear nuevas plantillas y arrastrar y soltar los componentes de lista de productos y detalles de productos en estas plantillas. Además de añadir otros componentes, los autores también pueden cambiar el diseño de estas plantillas, lo que les ofrece libertad ilimitada para crear experiencias increíbles que combinan contenido comercial y de marketing.

* Todos los componentes principales del CIF compatibles con el autor se han mejorado para admitir [AEM Style System](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html). Se han proporcionado estilos de ejemplo para el componente de lista de productos.

* Componentes basados en React del lado del cliente para la administración de cuentas. Esta versión es compatible con las siguientes funcionalidades: Inicio de sesión, contraseña olvidada y creación de cuenta.

### Mejoras {#what-is-improved-october}

* Los componentes detalle del producto y de la lista de productos se han mejorado para mostrar datos ficticios y proporcionar a los autores una vista previa del diseño cuando estos componentes se colocan en una plantilla o página.

* Los componentes Minicart y Checkout ahora utilizan enlaces React para mejorar la extensibilidad.

## Fecha de versión: Septiembre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 0,5,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0,4,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Tipo de archivo del CIF | 0,4,0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-september}

* Función de varias plantillas para permitir a los autores enriquecer una página de detalles del producto o una página de lista de productos específicos. Los autores pueden crear fácilmente una página de detalles del producto o una página de lista de productos personalizados y utilizar el selector de productos o categorías para asignar la página personalizada a un producto o categorías específicos.

* Enlace de varios catálogos para permitir a los autores enlazar varios catálogos en la consola del producto de AEM. Los autores también pueden editar y ver las propiedades de enlace del catálogo después de crear el enlace.

* React-based client-side Checkout and Mini Cart usando GraphQL para soportar un completo recorrido básico de compras.

* El componente Cierre de compra incluye formularios de direcciones, selección de pagos y selección de métodos de envío.

### Mejoras {#what-is-improved-september}

* Los componentes teaser de productos y carrusel de productos admiten variantes de producto.

## Fecha de versión: Agosto de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 0,4,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0,3,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Tipo de archivo del CIF | 0,3,0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-august}

* La incrustación del conector CIF en el tipo de archivo CIF se ha hecho opcional para proporcionar a los desarrolladores más flexibilidad.

* Componentes del CIF disociados del estilo CSS específico de &quot;Venia&quot; para permitir a los desarrolladores aplicar el estilo CSS de su elección.

* Característica de varias tiendas/sitios para permitir el uso de los componentes principales del CIF en varias estructuras AEM sitio y permitir que la implementación de cliente de GraphQL subyacente se conecte a diferentes vistas de tiendas/almacenes de Magento.

* El almacenamiento en caché de GraphQL está habilitado para ciertas consultas de GraphQL a través de la GET HTTP para reducir el tiempo de respuesta.

* Vista de descripción del producto habilitada en AEM consola Productos.

* El teaser de comercio amplía el componente teaser de WCM para permitir que los autores también agreguen campos de llamada a acción a una página de detalles del producto o a una página de lista de productos.

* Botón para permitir que los autores coloquen en una página AEM y vinculen a una página AEM, a una página de detalles del producto, a una página de lista de productos o a un vínculo externo.

### Mejoras {#what-is-improved-august}

* La configuración del almacén de Magento se ha trasladado de OSGi a AEM consola de producto para que la configuración de la integración sea más fácil de usar para el autor.

## Fecha de versión: Julio de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 0,3,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0,2,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Tipo de archivo del CIF | 0,2,0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-july}

* Primer tipo de archivo CIF para proporcionar a los desarrolladores varias opciones de implementación: 1. Implementar AEM tienda de Venia 2. Implementar scaffolding para un nuevo proyecto 3. Uso de elementos CIF en un proyecto existente

* Navegación de catálogo de varios niveles para admitir la navegación a través de categorías y subcategorías.

* Paginación en páginas de categoría para mejorar el usuario.

* Renderización del atributo de precio en el lado del cliente en los componentes Product Detail y Product List para admitir la renderización de atributos dinámicos.

* Carrusel de productos del lado del servidor para mostrar la lista de productos destacados en un estilo de carrusel.

* Lista de categorías destacadas del lado del servidor para mostrar la lista de categorías en una página AEM.

### Mejoras {#what-is-improved-july}

* La compatibilidad con el Magento 2.3.2 y las correcciones de errores relacionadas con las propiedades del producto se muestran en la consola del producto.

## Fecha de versión: Junio de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector del CIF | 0,2,0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0,1,0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |

### Novedades {#what-is-new-june}

* AEM tienda B2C con estilo CSS Venia, página de aterrizaje, navegación dinámica por catálogo a través de páginas de productos y categorías, página de búsqueda de productos y capacidades del carro de compras para iniciar y acelerar proyectos de comercio.

* El conector del CIF y las herramientas de creación (consola de producto, selector de productos y selector de categorías) permiten a los autores crear experiencias en AEM con contenido comercial.

* Primera versión de los componentes principales de CIF compatibles con el Magento 2.3.1:
   * Detalles del producto
   * Lista de productos
   * Teaser de productos
   * Navegación
   * Búsqueda de productos
   * Carro de compras (REST)

