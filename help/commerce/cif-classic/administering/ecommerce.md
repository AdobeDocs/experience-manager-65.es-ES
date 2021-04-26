---
title: eCommerce
description: AEM comercio electrónico ayuda a los especialistas en marketing a ofrecer experiencias de compra personalizadas y con marca en puntos de contacto web, móviles y sociales.
topic-tags: e-commerce
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# eCommerce{#ecommerce}

* [Conceptos ](/help/commerce/cif-classic/administering/concepts.md)
* [Administración (genérica)](/help/commerce/cif-classic/administering/generic.md)

Adobe proporciona dos versiones de Commerce Integration Framework:

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF local</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>Versiones de AEM compatibles</p> </td>
   <td><p>AEM local o AMS 6.x</p> </td>
   <td>AEM AMS 6.4 y 6.5</td>
  </tr>
  <tr>
   <td><p>Back-end</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>Integración monolítica, asignación previa a la compilación (plantilla)</li>
     <li>Repositorio JCR</li>
    </ul> </td>
   <td>
    <ul>
     <li>Magento</li>
     <li>Java y Javascript</li>
     <li>No hay datos de comercio almacenados en el repositorio JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>AEM páginas procesadas del lado del servidor</p> </td>
   <td>Aplicación de página mixta (renderización híbrida)</td>
  </tr>
  <tr>
   <td><p>Catálogo de productos</p> </td>
   <td>
    <ul>
     <li>Importador de productos, editor, almacenamiento en caché en AEM</li>
     <li>Catálogos regulares con páginas AEM o proxy</li>
    </ul> </td>
   <td>
    <ul>
     <li>Sin importación de productos</li>
     <li>Plantillas genéricas</li>
     <li>Datos bajo demanda mediante conector</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Escalabilidad</p> </td>
   <td>
    <ul>
     <li>Pueden admitir hasta unos pocos millones de productos (depende del caso de uso)</li>
     <li>Almacenamiento en caché en Dispatcher</li>
    </ul> </td>
   <td>
    <ul>
     <li>Sin limitación de volumen</li>
     <li>Almacenamiento en caché en Dispatcher o CDN</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelo de datos estandarizado</td>
   <td>No</td>
   <td>Sí, esquema de Magento GraphQL</td>
  </tr>
  <tr>
   <td>Disponibilidad</td>
   <td><p>Sí. Commerce Cloud de SAP (la extensión se ha actualizado para admitir AEM 6.4 e Hybris 5 (predeterminado) y mantiene la compatibilidad con Hybris 4</p> <p>Commerce Cloud de Salesforce (conector de código abierto compatible con AEM 6.4)</p> </td>
   <td>Sí, a través de código abierto a través de GitHub. Magento Commerce (admite Magento 2.3.2 (predeterminado) y compatible con Magento 2.3.1).</td>
  </tr>
  <tr>
   <td>Cuándo se utiliza</td>
   <td>Casos de uso limitados: Por ejemplo, escenarios en los que sea necesario importar catálogos estáticos pequeños</td>
   <td>Solución preferida en la mayoría de los casos de uso</td>
  </tr>
 </tbody>
</table>

El comercio electrónico, junto con la gestión de información de productos (PIM), gestiona las actividades de un sitio web centrado en la venta de productos a través de una tienda en línea:

* Creación, duración y obsolescencia de un producto
* Gestión de precios
* Administración de transacciones
* Administración de catálogos completos
* Registros de almacenamiento activo y centralizado
* Interfaces web

AEM comercio electrónico ayuda a los especialistas en marketing a ofrecer experiencias de compra personalizadas y con marca en puntos de contacto web, móviles y sociales. El entorno de creación de AEM le permite personalizar páginas y componentes en función del contexto del visitante objetivo y las estrategias de comercialización; por ejemplo:

* Páginas de producto
* Componentes del carro de compras
* Componentes de cierre de compra

La implementación permite el acceso en tiempo real a la información del producto. Esto se puede utilizar para hacer cumplir:

* Integridad de la información del producto
* Precio
* Inventario de existencias
* Variaciones en el estado de un carro de compras

>[!NOTE]
>
>Para utilizar el marco de integración con proveedores de comercio electrónico externos, primero debe instalar los paquetes necesarios. Para obtener más información, consulte [Implementación de eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>Para obtener información sobre la ampliación de las capacidades de comercio electrónico, consulte [Desarrollo del comercio electrónico](/help/commerce/cif-classic/developing/ecommerce.md).

## Funciones principales {#main-features}

AEM comercio electrónico proporciona:

* Varios **componentes de AEM listos para usar** para ilustrar lo que se puede lograr para el proyecto:

   * Visualización del producto
   * Carro de compras
   * Extracción
   * Productos vistos recientemente
   * Cupones
   * y otros

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >El marco de integración proporcionado por AEM también le permite crear componentes de AEM adicionales para las funciones de comercio independientes del motor de comercio electrónico específico.

* **Buscar** : mediante:

   * la búsqueda AEM
   * la búsqueda del sistema de comercio electrónico
   * una búsqueda de terceros (como Search&amp;Promote)
   * o una combinación de ellos.

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* Utiliza la capacidad AEM para **presentar el contenido en varios canales**, ya sea en la ventana completa del explorador o en el dispositivo móvil. Esto ofrece el contenido en el formato que necesitan los visitantes.

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* La capacidad de **desarrollar su propia implementación de integración basada en el [AEM marco de comercio electrónico](#the-framework)**.

   Las dos implementaciones disponibles actualmente se crean sobre la misma base, además de la API general (el marco de trabajo). La implementación de una nueva integración solo implica implementar las funciones que necesita la integración. Las nuevas implementaciones pueden utilizar los componentes front-end, ya que utilizan interfaces (por lo que son independientes de la implementación).

* La posibilidad de desarrollar **comercio basado en la experiencia basado en los datos y la actividad del comprador**. Esto le permite dar cuenta de muchos escenarios:

   * Un ejemplo podría ser proporcionar reducciones en los costos de envío cuando el pedido total exceda una cantidad específica.
   * Otro puede permitirle proporcionar ofertas de temporada que utilicen datos de perfil (por ejemplo, ubicación). A continuación, se pueden resaltar, dependiendo de nuevo de otros factores cuando sea necesario.

   En el ejemplo siguiente, se muestra un teaser, ya que el contenido del carro de compras es inferior a 75 $:

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   Esto se puede cambiar cuando el contenido del carro de compras supera los 75 $:

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* Y otras características, entre ellas:

   * Contenido del carro de compras retenido entre sesiones
   * Historial de pedidos completo
   * Actualización del catálogo exprés

## El marco {#the-framework}

La sección [Conceptos](/help/commerce/cif-classic/administering/concepts.md) cubre el marco de trabajo con más detalle, pero lo siguiente proporciona una vista de alto nivel y alta velocidad del marco de trabajo:

### ¿Qué? {#what}

* El marco de integración proporciona la API, una serie de componentes para ilustrar la funcionalidad y varias extensiones para proporcionar ejemplos de métodos de conexión.
* El marco proporciona la estructura básica necesaria para la ejecución de un proyecto.
* El marco es extensible.
* El marco de trabajo no proporciona un sitio listo para usar. Siempre se necesita una cierta cantidad de trabajo de desarrollo para adaptar el marco a sus especificaciones.

### ¿Por qué? {#why}

* Proporcionar los mecanismos básicos necesarios para realizar rápidamente un sitio de comercio electrónico personalizado.
* Tp proporciona la flexibilidad necesaria para desarrollar un sitio de comercio electrónico en la vida real.
* Ilustración de las prácticas recomendadas.
