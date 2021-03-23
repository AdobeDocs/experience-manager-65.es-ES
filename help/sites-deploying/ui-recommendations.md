---
title: Interfaz de usuario de Recommendations para clientes
seo-title: Interfaz de usuario de Recommendations para clientes
description: Una lista de recomendaciones relacionadas con las interfaces de usuario clásica y táctil.
seo-description: Una lista de recomendaciones relacionadas con las interfaces de usuario clásica y táctil.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---


# Interfaz de usuario de Recommendations para clientes{#user-interface-recommendations-for-customers}

Adobe Experience Manager incluye dos IU: la IU de Experience Cloud unificada (también conocida como IU táctil) y la IU clásica.

El objetivo de este documento es guiar a los clientes para que elijan qué IU utilizar en función de su situación.

Condiciones de interés:

* **IU (o IU estándar)**
Interfaz de usuario moderna que se introdujo en la versión 5.6.0 como vista previa de tecnología y que se amplió en versiones posteriores. Se basa en la experiencia de usuario unificada de Adobe Experience Cloud, anteriormente conocida como IU táctil o IU táctil.

* **Interfaz**
UIUser clásica basada en la tecnología ExtJS que se introdujo con CQ 5.1 en 2008.

* **Site**
AdminCapabilities para administrar la jerarquía del sitio (mover, activar, administrar referencias) y crear nuevas páginas.

* **Creación**
de páginasCapacidades para añadir/editar el contenido de una página.

* **DAM/Assets**
AdminCapacidades para administrar recursos digitales (incluidas imágenes, vídeo, documentos y descargas).

* ****
ContextHubCapabilities para agregar información sobre el visitante y utilizarla con distintos fines. Proporciona una interfaz de usuario para simular a las personas que visitan el sitio. A partir de AEM 6.2, ContextHub reemplazó a la tecnología anterior, Client Context.

## General {#general}

Durante los últimos años, Adobe ha actualizado todas las soluciones de Adobe Experience Cloud con una interfaz de usuario unificada. Los usuarios de las soluciones de Experience Cloud disfrutan de una experiencia coherente con patrones comunes sobre cómo utilizar y utilizar las aplicaciones. Con cada versión, Adobe ha refinado su interfaz de usuario basándose en los comentarios de los clientes que trabajan en las distintas soluciones.

La interfaz de usuario original para Adobe Experience Manager (anteriormente conocida como CQ5), introducida en 2008 y utilizada por los clientes que ejecutan las versiones 5.0-5.6.1, está presente en AEM 6.5. Esto garantiza que los clientes puedan actualizar a 6.5 y se beneficien de una plataforma actualizada con nuevas funciones, mientras siguen utilizando la misma interfaz de usuario.

Adobe recomienda a los clientes que planifiquen cambiar a la nueva interfaz de usuario en 2018/19. Esto se puede hacer durante la actualización a la versión 6.5 o en proyectos separados después de la actualización, que incluirían los ajustes necesarios en los cuadros de diálogo de personalizaciones y componentes.

La IU clásica quedó obsoleta con AEM 6.4 y Adobe no tiene previsto realizar más mejoras en la IU clásica. Tenga en cuenta que la interfaz de usuario clásica será totalmente compatible mientras esté en desuso.

### Reglas y Recommendations {#rules-and-recommendations}

A continuación se muestra una lista de recomendaciones de la administración de productos para Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Mi proyecto...</th>
   <th>Recomendaciones</th>
  </tr>
  <tr>
   <td>Está empezando a utilizar Adobe Experience Manager.</td>
   <td>Utilice la IU predeterminada.</td>
  </tr>
  <tr>
   <td><p>Ha usado AEM durante un tiempo.</p> <p>Ha utilizado la interfaz de usuario del producto lista para usar y ha desarrollado componentes personalizados para los sitios.<br /> </p> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la IU predeterminada para la administración del sitio, los recursos, . etc.<br /> </li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de la IU clásica. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</li>
    </ol> <p>A continuación, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de componentes para utilizar el formato de cuadro de diálogo Coral 3 . Adobe recomienda utilizar las <a href="/help/sites-developing/modernization-tools.md">AEM Herramientas de modernización</a> para actualizar los componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creado un sitio que utiliza el ClientContext con integraciones.<br /> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la IU predeterminada para la administración del sitio, los recursos, . etc.</li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de la IU clásica. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</li>
    </ol> <p>A continuación, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de componentes para utilizar el formato de cuadro de diálogo Coral 3 . Adobe recomienda utilizar las <a href="/help/sites-developing/modernization-tools.md">AEM Herramientas de modernización</a> para actualizar los componentes.</li>
     <li>Configure ContextHub (que sustituye al ClientContext) y actualice las plantillas de página para que utilicen ContextHub. Tenga en cuenta que ContextHub tiene un modo de compatibilidad que permite cargar almacenes de ClientContexts personalizados.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Ha utilizado CQ/AEM durante muchos años.</p> <p>Ha ampliado la interfaz de usuario del producto (por ejemplo, el administrador del sitio) y ha creado componentes con amplios cuadros de diálogo de edición.</p> </td>
   <td><p>Actualice a la versión 6.5 y configure la IU clásica como la predeterminada para la creación de páginas para todos los usuarios. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</p> <p>A continuación, inicie un proyecto para aplicar la personalización y optimizar los cuadros de diálogo de componentes en formato Coral 3. Consulte <a href="#resources-to-help">Recursos para ayudar</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Preguntas más frecuentes {#faq}

Consulte el artículo de la Base de conocimiento, [Touch UI Authoring FAQ](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), para obtener más información; se incluye información sobre la programación de desuso de la IU clásica.

### Selección de la IU {#selecting-your-ui}

Consulte [Selección de la IU](/help/sites-authoring/select-ui.md) para obtener información sobre cómo configurar el sistema según sea necesario.

### Estado de IU táctil {#touch-enabled-ui-status}

Para obtener más información sobre las mejoras realizadas en la IU táctil en la versión AEM 6.5, consulte [Novedades](/help/release-notes/release-notes.md#what-s-new) en las Notas de la versión.

Una descripción general completa puede ver la página [Estado de las funciones de la interfaz de usuario táctil](/help/release-notes/touch-ui-features-status.md)

### Recursos para ayudar {#resources-to-help}

Para información básica sobre la manipulación:

* [Creación de páginas](/help/sites-authoring/page-authoring.md).

Para obtener información detallada sobre el desarrollo:

* [Arquitectura de IU táctil](/help/sites-developing/touch-ui-concepts.md).
* Utilice las [AEM Herramientas de modernización](/help/sites-developing/modernization-tools.md) para convertir los cuadros de diálogo de edición de componentes de la IU clásica a la IU táctil.

* [Estructura de la IU táctil](/help/sites-developing/touch-ui-structure.md).

* [Personalización de las consolas en la IU táctil](/help/sites-developing/customizing-consoles-touch.md)  (incluye código de muestra).

* [Personalización de la creación de páginas en la IU táctil](/help/sites-developing/customizing-page-authoring-touch.md)  (incluye código de muestra).

* [AEM sesión de Gem en la personalización](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html) táctil.
* [Documentación de Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

