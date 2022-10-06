---
title: Superposiciones
seo-title: Overlays
description: AEM utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funciones
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Superposiciones{#overlays}

AEM (y antes de eso, CQ) ha utilizado durante mucho tiempo el principio de superposiciones para permitirle ampliar y personalizar el [consolas](/help/sites-developing/customizing-consoles-touch.md) y otras funciones (por ejemplo, [creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)).

La superposición es un término que se puede utilizar en muchos contextos. En este contexto (ampliación de AEM), una superposición implica tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella (para personalizar la funcionalidad estándar).

En una instancia estándar, la funcionalidad predefinida se mantiene en `/libs` y se recomienda definir la superposición (personalizaciones) en la variable `/apps` rama. AEM utiliza una ruta de búsqueda para encontrar un recurso, buscando primero el `/apps` y luego la `/libs` sucursal (la variable [la ruta de búsqueda se puede configurar](#configuring-the-search-paths)). Este mecanismo significa que la superposición (y las personalizaciones definidas allí) tendrán prioridad.

Desde AEM 6.0, se han realizado cambios en la forma en que se implementan y usan las superposiciones:

* AEM 6.0 en adelante: para [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Superposiciones relacionadas (es decir, la IU táctil)

   * Método

      * Reconstruya el `/libs` estructura `/apps`.

         Esto no requiere una copia 1:1, la variable [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) se utiliza para hacer referencia cruzada a las definiciones originales que son necesarias. La fusión de recursos de Sling proporciona servicios para acceder y fusionar recursos mediante mecanismos de diferenciación (diferenciación).

      * Realice cualquier cambio en `/apps`.
   * Ventajas

      * Más robusto en `/libs`.
      * Solo redefina lo que realmente se requiere.


* Superposiciones y superposiciones no de Granite anteriores a AEM 6.0

   * Método

      * Copiar el contenido de `/libs` a `/apps`

         Debe copiar toda la subrama, incluidas las propiedades.

      * Realice cualquier cambio en `/apps`.
   * Desventajas

      * Aunque los cambios no se perderán cuando algo cambie en `/libs`, es posible que tenga que volver a crear ciertos cambios que se producen en la superposición en `/apps`.


>[!CAUTION]
>
>La variable [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) y los métodos relacionados solo se pueden usar con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Esto significa que la creación de una superposición con una estructura de esqueletos solo es adecuada para la IU estándar con capacidad táctil.
>
>Las superposiciones de otras áreas (incluida la IU clásica) implican copiar el nodo apropiado y toda la subestructura y, a continuación, realizar los cambios necesarios.

Las superposiciones son el método recomendado para muchos cambios, como [configuración de las consolas](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) o [creación de la categoría de selección en el navegador de recursos del panel lateral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (se utiliza al crear páginas). Son necesarias como:

* You ***no debe* realice cambios en `/libs` Rama **Cualquier cambio que realice puede perderse, ya que esta rama puede cambiar siempre que:

   * actualizar en su instancia
   * aplicar una corrección
   * instalar un paquete de características

* Concentran los cambios en un solo lugar; facilitando el seguimiento, la migración, la copia de seguridad o la depuración de los cambios según sea necesario.

## Configuración de las rutas de búsqueda {#configuring-the-search-paths}

Para las superposiciones, el recurso enviado es un agregado de los recursos y propiedades recuperados, según las rutas de búsqueda que se puedan definir:

* El recurso **Ruta de búsqueda de resolución** tal como se define en la variable [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para el **Fábrica de resolución de recursos de Apache Sling**.

   * El orden descendente de las rutas de búsqueda indica sus prioridades respectivas.
   * En una instalación estándar, los valores predeterminados principales son `/apps`, `/libs` - así que el contenido de `/apps` tiene una prioridad mayor que la de `/libs` (es decir, que *superposiciones* ).

* Dos usuarios de servicio necesitan acceso JCR:READ a la ubicación donde se almacenan los scripts. Estos usuarios son: components-search-service (utilizado por los com.day.cq.wcm.coreto access/cache components) y sling-scripting (utilizado por org.apache.sling.servlets.resolver para encontrar servlets).
* La siguiente configuración también debe configurarse según el lugar donde coloque los scripts (en este ejemplo en /etc, /libs o /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Finalmente, Servlet Resolver también debe estar configurado (en este ejemplo para agregar /etc también)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Ejemplo de uso {#example-of-usage}

Algunos ejemplos se tratan cuando:

* [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md)
* [Personalización de la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)
