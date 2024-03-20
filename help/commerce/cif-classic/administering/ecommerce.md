---
title: Marco de integración de eCommerce
description: AEM eCommerce ayuda a los especialistas en marketing a ofrecer experiencias de compra personalizadas y de marca en puntos de contacto web, móviles y sociales.
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 2%

---

# eCommerce{#ecommerce}

* [Conceptos ](/help/commerce/cif-classic/administering/concepts.md)
* [Administración (genérica)](/help/commerce/cif-classic/administering/generic.md)

Adobe proporciona dos versiones del Commerce integration framework:

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF local de la zona de trabajo</p> </th>
   <th><p>CIF Nube de</p> </th>
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
     <li>Adobe Commerce</li>
     <li>Java y JavaScript</li>
     <li>No hay datos de comercio almacenados en el repositorio JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>AEM Páginas procesadas del lado del servidor de</p> </td>
   <td>Aplicación de página mixta (procesamiento híbrido)</td>
  </tr>
  <tr>
   <td><p>Catálogo de productos</p> </td>
   <td>
    <ul>
     <li>AEM Importador de productos, editor, almacenamiento en caché en la</li>
     <li>AEM Catálogos normales con páginas de proxy o de la red de distribución de contenido</li>
    </ul> </td>
   <td>
    <ul>
     <li>No hay importación de productos</li>
     <li>Plantillas genéricas</li>
     <li>Datos a petición mediante conector</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Escalabilidad</p> </td>
   <td>
    <ul>
     <li>Puede admitir hasta unos pocos millones de productos (depende del caso de uso)</li>
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
   <td>Sí, esquema de Adobe Commerce GraphQL</td>
  </tr>
  <tr>
   <td>Disponibilidad</td>
   <td><p>Sí. COMMERCE CLOUD AEM de SAP (extensión actualizada para admitir la versión 6.4 y la versión 5 de Hybris (predeterminada)), que mantiene la compatibilidad con la versión 4 de Hybris).</p> <p>Commerce Cloud AEM de Salesforce (conector de código abierto para admitir la versión 6.4 de)</p> </td>
   <td>Sí a través de código abierto mediante GitHub. Adobe Commerce (compatible con 2.3.2 (predeterminado) y con 2.3.1).</td>
  </tr>
  <tr>
   <td>Cuándo se usa</td>
   <td>Casos de uso limitados: por ejemplo, escenarios en los que puede ser necesario importar catálogos estáticos pequeños</td>
   <td>Solución preferida en la mayoría de los casos de uso</td>
  </tr>
 </tbody>
</table>

El comercio electrónico, junto con la gestión de la información de los productos (PIM), gestiona las actividades de un sitio web centrado en la venta de productos a través de una tienda en línea:

* Creación, vida útil y obsolescencia de un producto
* Gestión de precios
* Administración de transacciones
* Gestión de catálogos completos
* Registros de almacenamiento activos y centralizados
* Interfaces web

AEM eCommerce ayuda a los especialistas en marketing a ofrecer experiencias de compra personalizadas y de marca en puntos de contacto web, móviles y sociales. AEM El entorno de creación de segmentos le permite personalizar páginas y componentes en función del contexto del visitante de destino y de las estrategias de comercialización; por ejemplo:

* Páginas de producto
* Componentes del carro de compras
* Componentes de extracción

La implementación permite el acceso en tiempo real a la información del producto. Esto se puede utilizar para aplicar lo siguiente:

* Integridad de la información del producto
* Precio
* Inventario de existencias
* Variaciones en el estado de un carro de compras

>[!NOTE]
>
>Para utilizar el marco de integración con proveedores de comercio electrónico externos, primero debe instalar los paquetes necesarios. Para obtener más información, consulte [Implementar eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>Para obtener información sobre la ampliación de las capacidades de comercio electrónico, consulte [Desarrollo del comercio electrónico](/help/commerce/cif-classic/developing/ecommerce.md).

## Características principales {#main-features}

AEM eCommerce proporciona lo siguiente:

* Un número de **AEM componentes listos para usar de la interfaz de usuario de la interfaz de usuario de** para ilustrar lo que se puede lograr con su proyecto:

   * Visualización del producto
   * Carro de compras
   * Fecha de salida
   * Productos vistos recientemente
   * Cupones
   * y otros

  ![ejemplo de componentes de geometrixx](/help/sites-administering/assets/chlimage_1-130.png)

  >[!NOTE]
  >
  >AEM AEM El marco de trabajo de integración proporcionado por el usuario también le permite crear componentes de integración adicionales para las capacidades de comercio electrónico independientemente de su motor de comercio electrónico específico.

* **Buscar** - usando:

   * AEM la búsqueda de la
   * la búsqueda del sistema de comercio electrónico
   * una búsqueda de terceros
   * o una combinación de los mismos.

  ![ejemplo de búsqueda](/help/sites-administering/assets/chlimage_1-131.png)

* AEM Utiliza la capacidad de para **presentar el contenido en varios canales**, ya sea una ventana completa del navegador o un dispositivo móvil. Esto ofrece el contenido en el formato que necesitan los visitantes.

  ![ejemplo de vista móvil](/help/sites-administering/assets/chlimage_1-132.png)

* La capacidad de **desarrolle su propia implementación de integración basada en [AEM Marco de eCommerce de](#the-framework)**.

  Las dos implementaciones disponibles actualmente se crean sobre la misma base, además de la API general (el marco de trabajo). La implementación de una nueva integración solo implica implementar las funciones que su integración necesita. Cualquier implementación nueva puede utilizar los componentes front-end, ya que utilizan interfaces (por lo que son independientes de la implementación).

* La posibilidad de desarrollar **comercio basado en la experiencia y en los datos de los compradores y la actividad**. Esto permite realizar muchos escenarios:

   * Un ejemplo podría ser proporcionar reducciones en los costes de envío cuando el pedido total supera una cantidad específica.
   * Otra opción podría permitirle proporcionar ofertas estacionales que utilicen datos de perfil (por ejemplo, ubicación). A continuación, se pueden resaltar, nuevamente en función de otros factores cuando sea necesario.

  En el ejemplo siguiente, se muestra un teaser porque el contenido del carro de compras es inferior a 75 $:

  ![carro de compras con contexto de cliente](/help/sites-administering/assets/chlimage_1-133.png)

  Esto se puede cambiar cuando el contenido del carro de compras supera los 75 $:

  ![carro de compras con contexto de cliente después del cambio](/help/sites-administering/assets/chlimage_1-134.png)

* Y otras características que incluyen:

   * Contenido del carro de compras conservado entre sesiones
   * Historial completo de pedidos
   * Actualización rápida del catálogo

## El marco {#the-framework}

El [Conceptos](/help/commerce/cif-classic/administering/concepts.md) La sección trata el marco de trabajo con más detalle, pero la siguiente sección proporciona una vista de alto nivel y alta velocidad del marco de trabajo:

### ¿Qué? {#what}

* El marco de integración proporciona la API, una serie de componentes para ilustrar la funcionalidad y varias extensiones para proporcionar ejemplos de métodos de conexión.
* El marco proporciona la estructura básica necesaria para la ejecución de un proyecto.
* El marco de trabajo es extensible.
* El marco de trabajo no proporciona un sitio listo para usar y listo para usar. Siempre se necesita una cierta cantidad de trabajo de desarrollo para adaptar el marco a sus especificaciones.

### ¿Por qué? {#why}

* Proporcionar los mecanismos básicos necesarios para realizar rápidamente un sitio de comercio electrónico personalizado.
* Los consejos proporcionan la flexibilidad necesaria para desarrollar un sitio de comercio electrónico en la vida real.
* Ilustrar las prácticas recomendadas.
