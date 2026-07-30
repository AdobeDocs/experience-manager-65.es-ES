---
title: Notas de la versión 2019 de AEM Content and Commerce
description: Contenido de Adobe Experience Manager y notas de la versión de Commerce 2019.
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 10%

---

# Información general sobre la versión de Commerce integration framework GitHub

## Fecha de versión: noviembre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 0.7.1 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0.6.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquetipo de CIF | 0.6.2 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-november}

* Los autores pueden obtener una vista previa de las páginas de detalles y listas de productos con productos/categorías con una nueva opción &quot;Ver con producto/categoría&quot; en el editor de Sites.

* Los autores pueden etiquetar recursos por SKU del producto y buscar recursos específicos del producto por SKU.

* Se ha agregado compatibilidad con cupones en el carro de compras.

* Se agregó compatibilidad con pagos de Braintree en la tienda Venia de AEM.

### Qué se ha mejorado {#what-is-improved-november}

* Los selectores de categorías/productos se mejoraron para respetar la vista de tienda de Adobe Commerce especificada en una configuración de varias tiendas.

* Los componentes basados en React están disponibles como paquete npm. Esto permite a los desarrolladores utilizar el paquete de componentes de React como dependencia para un nuevo proyecto de React para permitir la personalización de componentes existentes o desarrollar nuevos componentes basados en React.

* La personalización de consultas de GraphQL está simplificada. Esto permite a los desarrolladores personalizar los componentes principales de CIF con menos código.

## Fecha de versión: octubre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 0.6.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0.5.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquetipo de CIF | 0.5.0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-october}

* Plantillas totalmente legibles para la página de detalles del producto y la página de lista del producto. Los autores ahora pueden crear plantillas y arrastrar y soltar componentes de lista de productos y detalles de productos en estas plantillas. Además de añadir otros componentes, los autores ahora pueden cambiar el diseño de estas plantillas también, lo que les da una libertad ilimitada para crear experiencias increíbles que combinen contenido de marketing y comercio.

* Todos los componentes principales de CIF descriptivos se han mejorado para admitir [el sistema de estilos de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html?lang=es). Se han proporcionado estilos de ejemplo para el componente de lista de productos.

* Componentes del lado del cliente basados en React para la administración de cuentas. Esta versión admite las siguientes funcionalidades: Inicio de sesión, Olvidé la contraseña y Crear una cuenta.

### Qué se ha mejorado {#what-is-improved-october}

* Los componentes de detalles de producto y lista de productos se han mejorado para mostrar datos ficticios a fin de proporcionar a los autores una vista previa del diseño cuando estos componentes se colocan en una plantilla o página.

* Los componentes Minicart y Checkout ahora utilizan los enlaces de React para mejorar la extensibilidad.

## Fecha de versión: septiembre de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 0.5.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0.4.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquetipo de CIF | 0.4.0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-september}

* La función de varias plantillas permite a los autores enriquecer una página de detalles de producto o una página de lista de productos específica. Los autores pueden crear fácilmente una página de detalles de producto personalizada o una página de lista de productos y utilizar el selector de productos o categorías para asignar la página personalizada a un producto o categoría específicos.

* Enlace de varios catálogos para permitir a los autores enlazar varios catálogos en la consola de productos de AEM. Los autores también pueden editar y ver las propiedades de enlace del catálogo después de crear el enlace.

* React-based client-side Checkout and Mini Cart con GraphQL para ofrecer un recorrido de compra básico completo.

* El componente Pago y envío incluye formularios de dirección, selección de pago y selección de métodos de envío.

### Qué se ha mejorado {#what-is-improved-september}

* Los componentes teaser y carrusel de productos admiten variantes de productos.

## Fecha de versión: agosto de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 0.4.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0.3.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquetipo de CIF | 0.3.0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-august}

* La incrustación del conector de CIF en el tipo de archivo de CIF se convierte en opcional para proporcionar a los desarrolladores más flexibilidad.

* Los componentes de CIF se separan del estilo CSS específico de &quot;Venia&quot; para permitir a los desarrolladores aplicar el estilo CSS de su elección.

* Función de varias tiendas/sitios para permitir el uso de los componentes principales de CIF en varias estructuras de sitio de AEM y permitir que la implementación de cliente de GraphQL subyacente se conecte a diferentes vistas de tiendas/tiendas de Adobe Commerce.

* El almacenamiento en caché de GraphQL está habilitado para determinadas consultas de GraphQL a través de HTTP GET para reducir el tiempo de respuesta.

* La vista de descripción del producto está habilitada en la consola Productos de AEM.

* Teaser de Commerce amplía el componente Teaser de WCM para permitir a los autores agregar también campos de CTA a una página de detalles de producto o a una página de lista de productos.

* Botón para permitir que los autores coloquen en una página de AEM y enlacen a una página de AEM, una página de detalles del producto, una página de lista de productos o un enlace externo.

### Qué se ha mejorado {#what-is-improved-august}

* La configuración de la tienda Adobe Commerce se movió de OSGi a la consola de producto de AEM para que la configuración de la integración sea más fácil de crear.

## Fecha de versión: julio de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 0.3.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0.2.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |
| Arquetipo de CIF | 0.2.0 | [Notas de la versión](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novedades {#what-is-new-july}

* Primer tipo de archivo de CIF que proporciona a los desarrolladores varias opciones de implementación: 1.Implementar AEM Venia tienda 2. Implementar andamiaje para un nuevo proyecto 3. Uso de elementos CIF en un proyecto existente

* Navegación por catálogo de varios niveles para admitir la navegación por categorías y subcategorías.

* Paginación en páginas de categoría para una mejor experiencia de usuario.

* Representación del atributo de precio en el lado del cliente en los componentes Detalle del producto y Lista del producto para admitir la representación de atributos dinámicos.

* Carrusel de productos del lado del servidor para mostrar una lista de los productos destacados en un estilo de carrusel.

* Lista de categorías destacadas del lado del servidor para mostrar una lista de categorías en una página de AEM.

### Qué se ha mejorado {#what-is-improved-july}

* La compatibilidad con Adobe Commerce 2.3.2 y las correcciones de errores relacionadas con las propiedades del producto se muestran en la consola del producto.

## Fecha de versión: junio de 2019

| GitHub | Versión | Notas de la versión detalladas |
|:-------|:-----:|---------------------:|
| Conector de CIF | 0.2.0 | [Notas de la versión](https://github.com/adobe/commerce-cif-connector/releases) |
| Componentes principales de CIF | 0.1.0 | [Notas de la versión](https://github.com/adobe/aem-core-cif-components/releases) |

### Novedades {#what-is-new-june}

* Tienda AEM B2C con estilo Venia CSS con prioridad móvil, página de aterrizaje, navegación dinámica por el catálogo a través de páginas de productos y categorías, página de búsqueda de productos y funciones del carro de compras para iniciar y acelerar proyectos de comercio.

* Conector de CIF y herramientas de creación (consola de producto, selector de productos y selector de categorías) para permitir a los autores crear experiencias en AEM con contenido comercial.

* Primera versión de los componentes principales de CIF compatibles con Adobe Commerce 2.3.1:
  * Detalles del producto
  * Lista de productos
  * Teaser del producto
  * Navegación
  * Búsqueda de productos
  * Carro de compras (REST)
