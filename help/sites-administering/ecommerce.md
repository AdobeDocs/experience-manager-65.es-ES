---
title: eCommerce
seo-title: eCommerce
description: AEM eCommerce ayuda a los especialistas en marketing a ofrecer experiencias de compra personalizadas y con marca en puntos de contacto web, móviles y sociales.
seo-description: AEM eCommerce ayuda a los especialistas en marketing a ofrecer experiencias de compra personalizadas y con marca en puntos de contacto web, móviles y sociales.
uuid: 75818c60-1cf1-4a91-94ce-d722563b661c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: e972ee05-f0cb-40ca-9ae2-34395791c709
docset: aem65
translation-type: tm+mt
source-git-commit: 46610888fd61900c52b197e73a8a5850dc9c4c35

---


# eCommerce{#ecommerce}

* [Conceptos](/help/sites-administering/concepts.md)
* [Administración (genérica)](/help/sites-administering/generic.md)

Adobe proporciona dos versiones de Commerce Integration Framework:

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF on-prem</p> </th>
   <th><p>Nube CIF</p> </th>
  </tr>
  <tr>
   <td><p>Versiones de AEM compatibles</p> </td>
   <td><p>AEM on-prem o AMS 6.x</p> </td>
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
     <li>Java y JavaScript</li>
     <li>No hay datos de comercio almacenados en el repositorio JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>Páginas procesadas en el servidor de AEM</p> </td>
   <td>Aplicación de página mixta (procesamiento híbrido)</td>
  </tr>
  <tr>
   <td><p>Catálogo de productos</p> </td>
   <td>
    <ul>
     <li>Importador de productos, editor y almacenamiento en caché en AEM</li>
     <li>Catálogos regulares con páginas de AEM o proxy</li>
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
     <li>Puede soportar hasta unos pocos millones de productos (depende del caso de uso)</li>
     <li>Almacenamiento en caché de Dispatcher</li>
    </ul> </td>
   <td>
    <ul>
     <li>Sin limitación de volumen</li>
     <li>Almacenamiento en caché de Dispatcher o CDN</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelo de datos estandarizado</td>
   <td>No</td>
   <td>Sí, esquema Magento GraphQL</td>
  </tr>
  <tr>
   <td>Disponibilidad</td>
   <td><p>Sí. SAP Commerce Cloud (Extension actualizada para admitir AEM 6.4 e Hybris 5 (predeterminado) y mantiene la compatibilidad con Hybris 4</p> <p>Salesforce Commerce Cloud (conector de código abierto para admitir AEM 6.4)</p> </td>
   <td>Sí, vía código abierto vía GitHub. Magento Commerce (Compatible con Magento 2.3.2 (predeterminado) y compatible con Magento 2.3.1).</td>
  </tr>
  <tr>
   <td>Cuándo usar</td>
   <td>Casos de uso limitados: Por ejemplo, escenarios en los que es posible que sea necesario importar catálogos estáticos pequeños</td>
   <td>Solución preferida en la mayoría de los casos de uso</td>
  </tr>
 </tbody>
</table>

El comercio electrónico, junto con la Administración de información de productos (PIM), gestiona las actividades de un sitio web centrado en la venta de productos a través de una tienda en línea:

* Creación, duración y obsolescencia de un producto
* Gestión de precios
* Administración de transacciones
* Administración de catálogos completos
* Registros de almacenamiento activo y centralizado
* Interfaces Web

AEM eCommerce ayuda a los especialistas en marketing a ofrecer experiencias de compra personalizadas y con marca en puntos de contacto web, móviles y sociales. El entorno de creación de AEM le permite personalizar páginas y componentes en función del contexto del visitante objetivo y las estrategias de comercialización; por ejemplo:

* Páginas de producto
* Componentes del carro de compras
* Componentes de cierre de compra

La implementación permite el acceso en tiempo real a la información del producto. Se puede utilizar para aplicar:

* Integridad de la información del producto
* Precios
* Inventario de existencias
* Variaciones en el estado de un carro de compras

>[!NOTE]
>
>Para utilizar el marco de integración con proveedores de comercio electrónico externos, primero debe instalar los paquetes necesarios. Para obtener más información, consulte [Implementación de comercio electrónico](/help/sites-deploying/ecommerce.md).
>
>Para obtener información sobre la ampliación de las capacidades de comercio electrónico, consulte [Desarrollo de comercio electrónico](/help/sites-developing/ecommerce.md).

## Funciones principales {#main-features}

AEM eCommerce proporciona:

* Varios componentes **de AEM** integrados para ilustrar lo que se puede lograr con el proyecto:

   * Pantalla del producto
   * Carro de compras
   * Cierre de compra
   * Productos vistos recientemente
   * Cupones
   * y otros
   ![](assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >El marco de integración proporcionado por AEM también le permite crear componentes de AEM adicionales para las capacidades comerciales, independientemente del motor de comercio electrónico específico.

* **Buscar** : mediante:

   * la búsqueda de AEM
   * la búsqueda del sistema de comercio electrónico
   * una búsqueda de terceros (como Search&amp;Promote)
   * o una combinación de ellos.
   ![](assets/chlimage_1-131.png)

* Utiliza la capacidad de AEM para **presentar el contenido en varios canales**, ya sea en la ventana completa del navegador o en el dispositivo móvil. Esto ofrece el contenido en el formato que necesitan los visitantes.

   ![](assets/chlimage_1-132.png)

* La capacidad de **desarrollar su propia implementación de integración basada en el marco[de comercio electrónico de](#the-framework)**AEM.

   Las dos implementaciones disponibles actualmente se crean sobre la misma base, además de la API general (el marco de trabajo). Implementar una nueva integración solo implica implementar las funciones que necesita la integración. Cualquier implementación nueva puede utilizar componentes front-end, ya que utilizan interfaces (por lo tanto son independientes de la implementación).

* La posibilidad de desarrollar el comercio basado en la **experiencia y en la actividad** del comprador. Esto le permite comprender muchos escenarios:

   * Un ejemplo podría ser proporcionar reducciones en los costos de envío cuando el pedido total exceda una cantidad específica.
   * Otro puede permitirle proporcionar ofertas de temporada que utilicen datos de perfil (por ejemplo, ubicación). A continuación, se pueden resaltar, dependiendo de nuevo de otros factores cuando sea necesario.
   En el ejemplo siguiente se muestra un teaser, ya que el contenido del carro de compras es menor de $75:

   ![](assets/chlimage_1-133.png)

   Esto se puede cambiar cuando el contenido del carro de compras exceda los $75:

   ![](assets/chlimage_1-134.png)

* Y otras características, incluyendo:

   * Contenido del carro de compras retenido en las sesiones
   * Historial de pedidos completo
   * Actualización de catálogo Express

## El marco {#the-framework}

La sección [Conceptos](/help/sites-administering/concepts.md) cubre el marco en forma más detallada, pero la siguiente proporciona una vista de alto nivel y alta velocidad del marco:

### ¿Qué? {#what}

* El marco de integración proporciona la API, una serie de componentes para ilustrar la funcionalidad y varias extensiones para proporcionar ejemplos de métodos de conexión.
* El marco proporciona la estructura básica necesaria para la ejecución de un proyecto.
* El marco es extensible.
* El marco no proporciona un sitio listo para usar. Siempre se necesita una cierta cantidad de trabajo de desarrollo para adaptar el marco a sus especificaciones.

### ¿Por qué? {#why}

* Proporcionar los mecanismos básicos necesarios para realizar rápidamente un sitio de comercio electrónico personalizado.
* Tp proporciona la flexibilidad necesaria para desarrollar un sitio de comercio electrónico en la vida real.
* Ilustrar prácticas recomendadas.