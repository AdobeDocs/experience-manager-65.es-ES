---
title: Interfaz de usuario de Recommendations para clientes
seo-title: Interfaz de usuario de Recommendations para clientes
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
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---


# Interfaz de usuario de Recommendations para clientes{#user-interface-recommendations-for-customers}

Adobe Experience Manager incluye dos IU: la IU de Experience Cloud unificada (también conocida como IU táctil) y la IU clásica.

Este documento está diseñado para guiar a los clientes a elegir qué IU utilizar en función de su situación.

Condiciones de interés:

* **Interfaz de usuario (o IU estándar)**
Interfaz de usuario moderna que se introdujo en la versión 5.6.0 como previsualización tecnológica y se amplió en versiones posteriores. Se basa en la experiencia de usuario unificada del Adobe Experience Cloud, anteriormente conocida como IU táctil o IU táctil.

* **Interfaz clásica**
UIUser basada en la tecnología ExtJS que se introdujo con CQ 5.1 en 2008.

* **Administración**
del sitioCapacidades para administrar la jerarquía del sitio (mover, activar, administrar referencias) y crear nuevas páginas.

* **Creación**
de páginasCapacidades para agregar o editar el contenido de una página.

* **Administración**
de DAM/AssetsCapacidades para administrar recursos digitales (incluidas imágenes, vídeo, documentos y descargas).

* ****
ContextHubCapabilities para acumulada información sobre el visitante y usarla para varios fines. Proporciona una interfaz de usuario para simular a las personas que visitan el sitio. A partir de AEM 6.2, ContextHub reemplazó a la tecnología anterior, Client Context.

## General {#general}

Durante los últimos años, Adobe ha actualizado todas las soluciones de Adobe Experience Cloud con una interfaz de usuario unificada. Los usuarios de las soluciones Experience Cloud disfrutan de una experiencia consistente con patrones comunes sobre cómo utilizar y utilizar las aplicaciones. Con cada versión, Adobe ha perfeccionado su interfaz de usuario en función de los comentarios de los clientes que trabajan en las distintas soluciones.

La interfaz de usuario original para Adobe Experience Manager (anteriormente conocida como CQ5), introducida en 2008 y utilizada por los clientes que ejecutan las versiones 5.0-5.6.1, está presente en AEM 6.5. Esto garantiza que los clientes puedan actualizar a la versión 6.5 y beneficiarse de una plataforma actualizada con nuevas capacidades mientras siguen utilizando la misma interfaz de usuario.

Adobe recomienda a los clientes que planeen cambiar a la nueva interfaz de usuario en 2018/19. Esto puede realizarse durante la actualización a la versión 6.5 o en proyectos independientes después de la actualización, que incluirían los ajustes necesarios en los cuadros de diálogo de componentes y personalizaciones.

La IU clásica quedó obsoleta con AEM 6.4 y Adobe no tiene pensado realizar más mejoras en la IU clásica. Tenga en cuenta que la interfaz de usuario clásica será totalmente compatible mientras esté en desuso.

### Reglas y Recommendations {#rules-and-recommendations}

A continuación se muestra una lista de las recomendaciones de Administración de productos para Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Mi proyecto...</th>
   <th>Recomendaciones</th>
  </tr>
  <tr>
   <td>Está empezando a usar Adobe Experience Manager.</td>
   <td>Utilice la IU predeterminada.</td>
  </tr>
  <tr>
   <td><p>Ha usado AEM por un tiempo.</p> <p>Ha utilizado la interfaz de usuario del producto lista para usar y ha desarrollado componentes personalizados para los sitios.<br /> </p> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la IU predeterminada para la administración del sitio, los recursos, etc. etc.<br /> </li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de la IU clásica. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</li>
    </ol> <p>Luego, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de los componentes para utilizar el formato de cuadro de diálogo Coral 3. Adobe recomienda utilizar la <a href="/help/sites-developing/dialog-conversion.md">Herramienta de conversión de cuadro de diálogo</a> para actualizar los componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creado un sitio que utiliza el ClientContext con integraciones.<br /> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la IU predeterminada para la administración del sitio, los recursos, etc. etc.</li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de la IU clásica. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</li>
    </ol> <p>Luego, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de los componentes para utilizar el formato de cuadro de diálogo Coral 3. Adobe recomienda utilizar la <a href="/help/sites-developing/dialog-conversion.md">Herramienta de conversión de cuadro de diálogo</a> para actualizar los componentes.</li>
     <li>Configure ContextHub (el reemplazo del ClientContext) y actualice las plantillas de página para utilizar ContextHub. Tenga en cuenta que ContextHub tiene un modo de compatibilidad que permite cargar almacenes de ClientContexts personalizados.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Ha utilizado CQ/AEM durante muchos años.</p> <p>Ha ampliado la interfaz de usuario del producto (por ejemplo, administrador del sitio) y ha creado componentes con amplios diálogos de edición.</p> </td>
   <td><p>Actualice a 6.5 y configure la IU clásica como la predeterminada para la creación de páginas para todos los usuarios. Consulte <a href="#selecting-your-ui">Selección de la IU</a>.</p> <p>A continuación, inicio un proyecto para aplicar personalización y optimizar los cuadros de diálogo de componentes en formato Coral 3. Consulte <a href="#resources-to-help">Recursos para ayudar</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Preguntas más frecuentes {#faq}

Consulte el artículo de la Base de conocimiento, [Touch UI Authoring FAQ](https://helpx.adobe.com/experience-manager/kb/index/touchui_faq.html), para obtener más información; incluida cualquier información sobre la programación de desaprobación de la IU clásica.

### Selección de la IU {#selecting-your-ui}

Consulte [Selección de la IU](/help/sites-authoring/select-ui.md) para obtener información sobre cómo configurar el sistema según sea necesario.

### Estado de IU táctil {#touch-enabled-ui-status}

Para obtener más información sobre las mejoras realizadas en la IU táctil en la AEM 6.5, consulte [Novedades](/help/release-notes/release-notes.md#what-s-new) en las Notas de la versión.

Una descripción general completa consulte la página [Estado de la función de IU táctil](/help/release-notes/touch-ui-features-status.md)

### Recursos para ayudar {#resources-to-help}

Para obtener información básica sobre la manipulación básica:

* [Creación de páginas](/help/sites-authoring/page-authoring.md).

Para obtener información detallada sobre el desarrollo:

* [Arquitectura](/help/sites-developing/touch-ui-concepts.md) de IU táctil.
* Utilice la [herramienta Conversión de cuadro de diálogo](/help/sites-developing/dialog-conversion.md) para convertir el componente Editar cuadros de diálogo de la IU clásica a la IU táctil.

* [Estructura de la IU](/help/sites-developing/touch-ui-structure.md) táctil.

* [Personalización de las consolas en la IU](/help/sites-developing/customizing-consoles-touch.md)  táctil (incluye código de muestra).

* [Personalización de la creación de páginas en la IU](/help/sites-developing/customizing-page-authoring-touch.md)  táctil (incluye código de muestra).

* [AEM sesión de Gem en la personalización](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html) táctil.
* [Documentación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) de la interfaz de usuario de Granite.

