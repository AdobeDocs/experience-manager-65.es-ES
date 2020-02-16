---
title: Recomendaciones de interfaz de usuario para clientes
seo-title: Recomendaciones de interfaz de usuario para clientes
description: Una lista de recomendaciones relacionadas con las interfaces de usuario clásicas y táctiles.
seo-description: Una lista de recomendaciones relacionadas con las interfaces de usuario clásicas y táctiles.
uuid: 9ec2c9de-a79e-4f2c-a90f-b38ba9553e07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8f06d4b6-7d30-4ebc-9c6a-3bb8607a9be8
docset: aem65
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Recomendaciones de interfaz de usuario para clientes{#user-interface-recommendations-for-customers}

Adobe Experience Manager incluye dos IU: la IU unificada de Experience Cloud (también conocida como IU táctil) y la IU clásica.

Este documento tiene por objeto guiar a los clientes para que elijan qué IU utilizar en función de su situación.

Condiciones de interés:

* **Interfaz de usuario (o IU estándar)** Interfaz de usuario moderna que se introdujo en la versión 5.6.0 como vista previa de tecnología y se amplió en versiones posteriores. Se basa en la experiencia de usuario unificada de Adobe Experience Cloud, anteriormente conocida como IU táctil o IU táctil.

* **Interfaz de usuario** clásica basada en la tecnología ExtJS que se introdujo con CQ 5.1 en 2008.

* **Capacidades de administración** del sitio para administrar la jerarquía del sitio (mover, activar, referencias administradas) y crear nuevas páginas.

* **Funciones de creación** de páginas para agregar o editar el contenido de una página.

* **Funciones de administración** de DAM/Assets para administrar recursos digitales (incluidas imágenes, vídeo, documentos y descargas).

* **ContextHub** Capacidades para agregar información sobre el visitante y usarla para varios propósitos. Proporciona una interfaz de usuario para simular a las personas que visitan el sitio. A partir de AEM 6.2, ContextHub reemplazó a la tecnología anterior, Client Context.

## General {#general}

Durante los últimos años, Adobe ha actualizado todas las soluciones de Adobe Experience Cloud con una interfaz de usuario unificada. Los usuarios de las soluciones de Experience Cloud disfrutan de una experiencia uniforme con patrones comunes sobre cómo utilizar y utilizar las aplicaciones. Con cada versión, Adobe ha refinado su interfaz de usuario en función de los comentarios de los clientes que trabajan en las distintas soluciones.

La interfaz de usuario original de Adobe Experience Manager (anteriormente CQ5), introducida en 2008 y utilizada por los clientes que ejecutan las versiones 5.0-5.6.1, está presente en AEM 6.5. Esto garantiza que los clientes puedan actualizar a la versión 6.5 y beneficiarse de una plataforma actualizada con nuevas capacidades mientras siguen utilizando la misma interfaz de usuario.

Adobe recomienda a los clientes que planeen cambiar a la nueva interfaz de usuario en 2018/19. Esto puede realizarse durante la actualización a la versión 6.5 o en proyectos independientes después de la actualización, que incluirían los ajustes necesarios en los cuadros de diálogo de componentes y personalizaciones.

La interfaz de usuario clásica ya no se utiliza en AEM 6.4 y Adobe no tiene pensado realizar más mejoras en la IU clásica. Tenga en cuenta que la interfaz de usuario clásica será totalmente compatible mientras esté en desuso.

### Reglas y recomendaciones {#rules-and-recommendations}

A continuación se muestra una lista de recomendaciones de Administración de productos para Adobe Experience Manager 6.5:

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
   <td><p>Ha utilizado AEM durante un tiempo.</p> <p>Ha utilizado la interfaz de usuario del producto lista para usar y ha desarrollado componentes personalizados para los sitios.<br /> </p> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la IU predeterminada para la administración del sitio, los recursos, etc. etc.<br /> </li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de la IU clásica. See <a href="#selecting-your-ui">Selecting Your UI</a>.</li>
    </ol> <p>Luego, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de los componentes para utilizar el formato de cuadro de diálogo Coral 3. Adobe recomienda utilizar la herramienta <a href="/help/sites-developing/dialog-conversion.md">de conversión de</a> cuadro de diálogo para actualizar los componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creado un sitio que utiliza ClientContext con integraciones.<br /> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la IU predeterminada para la administración del sitio, los recursos, etc. etc.</li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de la IU clásica. See <a href="#selecting-your-ui">Selecting Your UI</a>.</li>
    </ol> <p>Luego, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de los componentes para utilizar el formato de cuadro de diálogo Coral 3. Adobe recomienda utilizar la herramienta <a href="/help/sites-developing/dialog-conversion.md">de conversión de</a> cuadro de diálogo para actualizar los componentes.</li>
     <li>Configure ContextHub (el reemplazo de ClientContext) y actualice las plantillas de página para utilizar ContextHub. Tenga en cuenta que ContextHub tiene un modo de compatibilidad que permite cargar almacenes personalizados de ClientContext.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Ha utilizado CQ/AEM durante muchos años.</p> <p>Ha ampliado la interfaz de usuario del producto (por ejemplo, administrador del sitio) y ha creado componentes con amplios diálogos de edición.</p> </td>
   <td><p>Actualice a 6.5 y configure la IU clásica como la predeterminada para la creación de páginas para todos los usuarios. See <a href="#selecting-your-ui">Selecting Your UI</a>.</p> <p>A continuación, inicie un proyecto para aplicar personalización y optimizar los cuadros de diálogo de componentes en formato Coral 3. Consulte <a href="#resources-to-help">Recursos para ayuda</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Preguntas más frecuentes {#faq}

Consulte el artículo de la Base de conocimiento, [Touch UI Authoring FAQ](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), para obtener más información; incluida cualquier información sobre la programación de desaprobación de la IU clásica.

### Selecting Your UI {#selecting-your-ui}

Consulte [Selección de la interfaz de usuario](/help/sites-authoring/select-ui.md) para obtener información sobre la configuración del sistema según sea necesario.

### Estado de IU táctil {#touch-enabled-ui-status}

Para obtener más información sobre las mejoras realizadas en la IU táctil en AEM 6.5, consulte [Novedades](/help/release-notes/release-notes.md#what-s-new) en las Notas de la versión.

Una descripción general completa consulte la página Estado [de la función de la interfaz de usuario](/help/release-notes/touch-ui-features-status.md) táctil

### Recursos para ayudar {#resources-to-help}

Para obtener información básica sobre la manipulación básica:

* [Creación de páginas](/help/sites-authoring/page-authoring.md).

Para obtener información detallada sobre el desarrollo:

* [Arquitectura](/help/sites-developing/touch-ui-concepts.md)de IU táctil.
* Utilice la herramienta [Conversión de](/help/sites-developing/dialog-conversion.md) cuadro de diálogo para convertir los cuadros de diálogo de edición de componentes de la IU clásica en la IU táctil.

* [Estructura de la IU](/help/sites-developing/touch-ui-structure.md)táctil.

* [Personalización de las consolas en la IU](/help/sites-developing/customizing-consoles-touch.md) táctil (incluye código de muestra).

* [Personalización de la creación de páginas en la IU](/help/sites-developing/customizing-page-authoring-touch.md) táctil (incluye código de muestra).

* [Sesión de AEM Gem sobre la personalización](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)táctil.
* [Documentación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)de la interfaz de usuario de Granite.

