---
title: Superposiciones
seo-title: Superposiciones
description: AEM utiliza el principio de superposiciones para permitirle ampliar y personalizar las consolas y otras funciones
seo-description: AEM utiliza el principio de superposiciones para permitirle ampliar y personalizar las consolas y otras funciones
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Superposiciones{#overlays}

AEM (y antes de eso, CQ) ha utilizado desde hace tiempo el principio de las superposiciones para permitirle ampliar y personalizar las [consolas](/help/sites-developing/customizing-consoles-touch.md) y otras funciones (por ejemplo, la creación de [páginas](/help/sites-developing/customizing-page-authoring-touch.md)).

Overlay es un término que se puede utilizar en muchos contextos. En este contexto (ampliar AEM), una superposición significa tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella (para personalizar la funcionalidad estándar).

En una instancia estándar, la funcionalidad predefinida se mantiene en `/libs` y se recomienda definir la superposición (personalizaciones) en la `/apps` rama. AEM utiliza una ruta de búsqueda para encontrar un recurso, buscando primero la rama y luego la `/apps` rama `/libs` (la ruta de [búsqueda se puede configurar](#configuring-the-search-paths)). Este mecanismo significa que la superposición (y las personalizaciones definidas allí) tendrán prioridad.

Desde AEM 6.0, se han realizado cambios en la forma en que se implementan y utilizan las superposiciones:

* A partir de AEM 6.0: para superposiciones relacionadas con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)(es decir, la IU táctil)

   * Método

      * Reconstruya la `/libs` estructura adecuada en `/apps`.

         Esto no requiere una copia 1:1, la fusión [de recursos de](/help/sites-developing/sling-resource-merger.md) Sling se utiliza para hacer referencia cruzada a las definiciones originales que son necesarias. La fusión de recursos Sling proporciona servicios para acceder a los recursos y combinarlos mediante mecanismos de diferenciación (diferenciación).

      * Realice los cambios en `/apps`.
   * Ventajas

      * Más robusto para los cambios en `/libs`.
      * Solo redefinir lo que realmente se requiere.


* Superposiciones y superposiciones sin granito anteriores a AEM 6.0

   * Método

      * Copiar el contenido de `/libs` a `/apps`

         Debe copiar toda la subrama, incluidas las propiedades.

      * Realice los cambios en `/apps`.
   * Desventajas

      * Aunque los cambios no se perderán cuando algo cambie en `/libs`, es posible que tenga que volver a crear ciertos cambios que se producen en la superposición en `/apps`.


>[!CAUTION]
>
>La fusión [de recursos de](/help/sites-developing/sling-resource-merger.md) Sling y los métodos relacionados solo pueden utilizarse con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Esto significa que la creación de una superposición con una estructura de esqueleto solo es adecuada para la IU estándar con capacidad táctil.
>
>Las superposiciones para otras áreas (incluida la IU clásica) implican copiar el nodo apropiado y toda la subestructura, y luego realizar los cambios necesarios.

Las superposiciones son el método recomendado para realizar muchos cambios, como [configurar las consolas](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) o [crear la categoría de selección en el navegador de recursos del panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) lateral (se utiliza al crear páginas). Se requieren como:

* No ***debe *realizar cambios en la`/libs`rama **. Es posible que se pierdan los cambios que realice, ya que esta rama puede cambiar cada vez que:

   * actualizar en su instancia
   * aplicar una revisión
   * instalar un paquete de funciones

* Concentran los cambios en un solo lugar; facilitando el seguimiento, la migración, la copia de seguridad y/o la depuración de los cambios según sea necesario.

## Configuración de las rutas de búsqueda {#configuring-the-search-paths}

Para las superposiciones, el recurso enviado es un agregado de los recursos y las propiedades recuperados, según las rutas de búsqueda que se puedan definir:

* El recurso **Resolver Ruta** de búsqueda según se define en la configuración [de](/help/sites-deploying/configuring-osgi.md) OSGi para la Fábrica **de resolución de recursos de Sling de** Apache.

   * El orden descendente de las rutas de búsqueda indica sus prioridades respectivas.
   * En una instalación estándar, los valores predeterminados principales son `/apps`, `/libs` por lo que el contenido de `/apps` tiene una prioridad mayor que el de `/libs` (es decir, *lo superpone* ).

* Dos usuarios de servicios necesitan acceso JCR:READ a la ubicación donde se almacenan las secuencias de comandos. Estos usuarios son: components-search-service (utilizado por los com.day.cq.wcm.coreto componentes access/cache) y sling-scripting (utilizado por org.apache.sling.servlets.resolver para encontrar servlets).
* La siguiente configuración también debe configurarse según dónde coloque los scripts (en este ejemplo en /etc, /libs o /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Finalmente, debe configurarse también el Resolver Servlet (en este ejemplo para agregar también /etc)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Ejemplo de uso {#example-of-usage}

Algunos ejemplos se tratan cuando:

* [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md)
* [Personalización de la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)

