---
title: Interfaz de usuario de Recommendations para clientes
seo-title: User Interface Recommendations for Customers
description: Una lista de recomendaciones relacionadas con las interfaces de usuario clásicas y las optimizadas para dispositivos táctiles.
seo-description: A list of recommendations related to the classic and touch-optimized user interfaces.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
exl-id: 7b71119a-ff58-47c0-aeef-a705ed8c40e0
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 2%

---

# Interfaz de usuario de Recommendations para clientes{#user-interface-recommendations-for-customers}

Adobe Experience Manager incluye dos interfaces de usuario: la IU unificada del Experience Cloud (también conocida como IU táctil) y la IU clásica.

Este documento pretende guiar a los clientes para que elijan qué interfaz de usuario utilizar según su situación.

Términos de interés:

* **IU (o IU estándar)**
Interfaz de usuario moderna introducida en la versión 5.6.0 como vista previa tecnológica y ampliada en versiones posteriores. Se basa en la experiencia de usuario unificada para Adobe Experience Cloud, anteriormente conocida como IU táctil o IU táctil.

* **IU clásica**
Interfaz de usuario basada en la tecnología ExtJS introducida con CQ 5.1 en 2008.

* **Administrador del sitio**
Capacidades para administrar la jerarquía del sitio (mover, activar, gestionar referencias) y crear nuevas páginas.

* **Creación de páginas**
Capacidad para añadir o editar el contenido de una página.

* **Administrador de DAM/Assets**
Funciones para administrar recursos digitales (como imágenes, vídeos, documentos y descargas).

* **ContextHub**
Capacidades para agregar información sobre el visitante y utilizarla para varios fines. Proporciona una interfaz de usuario para simular a las personas que visitan el sitio. AEM A partir de la versión 6.2, ContextHub sustituyó a la tecnología anterior, Client Context.

## General {#general}

En los últimos años, el Adobe ha actualizado todas las soluciones de Adobe Experience Cloud con una interfaz de usuario unificada. Los usuarios de las soluciones de Experience Cloud disfrutan de una experiencia coherente con patrones comunes sobre cómo utilizar y utilizar las aplicaciones. Con cada versión, Adobe ha refinado su interfaz de usuario en función de los comentarios de los clientes que trabajan en las distintas soluciones.

La interfaz de usuario original para Adobe Experience Manager AEM (anteriormente conocida como CQ5), introducida en 2008 y utilizada por los clientes que ejecutan las versiones 5.0-5.6.1, está presente en la versión 6.5. Esto garantiza que los clientes puedan actualizar a la versión 6.5 y beneficiarse de una plataforma actualizada con nuevas funciones mientras siguen utilizando la misma interfaz de usuario.

El Adobe recomienda a los clientes que planifiquen el cambio a la nueva interfaz de usuario en 2018/19. Esto se puede hacer durante la actualización a 6.5 o en un proyecto independiente después de la actualización, que incluiría los ajustes necesarios en las personalizaciones y los cuadros de diálogo de componentes.

AEM La IU clásica ha quedado obsoleta con la versión 6.4 de y Adobe no tiene previsto realizar más mejoras en la IU clásica. Tenga en cuenta que la interfaz de usuario clásica será totalmente compatible mientras esté en desuso.

### Reglas y Recommendations {#rules-and-recommendations}

A continuación se muestra una lista de recomendaciones de Administración de productos para Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Mi proyecto...</th>
   <th>Recomendaciones</th>
  </tr>
  <tr>
   <td>Acaba de empezar a usar Adobe Experience Manager.</td>
   <td>Utilice la interfaz de usuario predeterminada.</td>
  </tr>
  <tr>
   <td><p>AEM Se ha usado durante un tiempo. - Sí.</p> <p>Ha utilizado la interfaz de usuario predeterminada del producto y ha desarrollado componentes personalizados para los sitios.<br /> </p> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la interfaz de usuario predeterminada para la administración de sitios, recursos, etc. etc.<br /> </li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de IU clásico. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</li>
    </ol> <p>A continuación, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de componentes para utilizar el formato de diálogo Coral 3. El Adobe recomienda utilizar la variable <a href="/help/sites-developing/modernization-tools.md">AEM Herramientas de modernización de</a> para actualizar los componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creado un sitio que utiliza el ClientContext con integraciones.<br /> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la interfaz de usuario predeterminada para la administración de sitios, recursos, etc. etc.</li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de IU clásico. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</li>
    </ol> <p>A continuación, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de componentes para utilizar el formato de diálogo Coral 3. El Adobe recomienda utilizar la variable <a href="/help/sites-developing/modernization-tools.md">AEM Herramientas de modernización de</a> para actualizar los componentes.</li>
     <li>Configure ContextHub (el reemplazo del ClientContext) y actualice las plantillas de página para utilizar ContextHub. Tenga en cuenta que ContextHub tiene un modo de compatibilidad que permite cargar almacenes de ClientContexts personalizados.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>AEM Ha usado CQ/durante muchos años.</p> <p>Ha ampliado la interfaz de usuario del producto (p. ej., el administrador del sitio) y ha creado componentes con numerosos cuadros de diálogo de edición.</p> </td>
   <td><p>Actualice a 6.5 y configure la IU clásica como la predeterminada para la creación de páginas para todos los usuarios. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</p> <p>A continuación, inicie un proyecto para aplicar la personalización y optimizar los cuadros de diálogo de componentes en formato Coral 3. Consulte <a href="#resources-to-help">Recursos de ayuda</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Preguntas más frecuentes {#faq}

Consulte el artículo de la Base de conocimiento, [Preguntas frecuentes sobre la creación de IU táctiles](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), para obtener más información; incluida la información acerca de la programación de desaprobación de la IU clásica.

### Selección de la IU {#selecting-your-ui}

Consulte [Selección de la IU](/help/sites-authoring/select-ui.md) para obtener información acerca de cómo configurar el sistema según sea necesario.

### Estado de IU táctil {#touch-enabled-ui-status}

AEM Para obtener más información sobre las mejoras realizadas en la IU táctil en la versión 6.5 de la, consulte [Novedades de la versión](/help/release-notes/release-notes.md#what-s-new) en las Notas de la versión.

Una descripción general completa consulte la [Estado de función de IU táctil](/help/release-notes/touch-ui-features-status.md) página

### Recursos de ayuda {#resources-to-help}

Para obtener información básica sobre la manipulación básica:

* [Creación de páginas](/help/sites-authoring/page-authoring.md).

Para obtener información detallada sobre el desarrollo:

* [Arquitectura de IU táctil](/help/sites-developing/touch-ui-concepts.md).
* Utilice el [AEM Herramientas de modernización de](/help/sites-developing/modernization-tools.md) para convertir los cuadros de diálogo de edición de componentes de la IU clásica a la IU táctil.

* [Estructura de la IU táctil](/help/sites-developing/touch-ui-structure.md).

* [Personalización de las consolas en la IU táctil](/help/sites-developing/customizing-consoles-touch.md) (incluye código de ejemplo).

* [Personalización de la creación de páginas en la IU táctil](/help/sites-developing/customizing-page-authoring-touch.md) (incluye código de ejemplo).

* [Documentación de Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).
