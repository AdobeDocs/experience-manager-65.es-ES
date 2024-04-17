---
title: Superposiciones
description: Adobe Experience Manager utiliza el principio de las superposiciones para permitirle ampliar y personalizar las consolas y otras funcionalidades.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Superposiciones{#overlays}

Adobe Experience Manager AEM (), y antes de eso, CQ, ha utilizado durante mucho tiempo el principio de las superposiciones para permitirle ampliar y personalizar el [consolas](/help/sites-developing/customizing-consoles-touch.md) y otras funcionalidades (por ejemplo, [creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)).

Superposición es un término que se utiliza en muchos contextos. AEM En este contexto (ampliación de la funcionalidad), una superposición significa tomar la funcionalidad predefinida e imponer sus propias definiciones sobre ella (para personalizar la funcionalidad estándar).

En una instancia estándar, la funcionalidad predefinida se encuentra en `/libs` y se recomienda definir la superposición (personalizaciones) en `/apps` Rama. AEM utiliza una ruta de búsqueda para encontrar un recurso. Primero busca en el `/apps` y luego la `/libs` rama (la [se puede configurar la ruta de búsqueda](#configuring-the-search-paths)). Este mecanismo significa que la superposición (y las personalizaciones definidas) tienen prioridad.

AEM Desde la versión 6.0, se han realizado cambios en la implementación y el uso de las superposiciones:

* AEM.0 y posteriores: para [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)Superposiciones relacionadas con (es decir, la IU táctil)

   * Método

      * Reconstruya el adecuado `/libs` estructura bajo `/apps`.

        Esto no requiere una copia 1:1, el [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) se utiliza para hacer referencia a las definiciones originales que son necesarias. La fusión de recursos de Sling proporciona servicios para acceder y combinar recursos con mecanismos de diferencia.

      * En `/apps`, realice cualquier cambio.

   * Ventajas

      * Más robustas a los cambios en `/libs`.
      * Redefina solo lo que sea necesario.

* AEM Superposiciones y superposiciones que no son de Granite antes de la versión 6 0

   * Método

      * Copie el contenido de `/libs` hasta `/apps`

        Copie toda la subrama, incluidas las propiedades.

      * En `/apps`, realice cualquier cambio.

   * Desventajas

      * Aunque los cambios no se perderán cuando algo cambie en `/libs`, es posible que tenga que volver a crear ciertos cambios que se producen en la superposición en `/apps`.

>[!CAUTION]
>
>El [Fusión de recursos de Sling](/help/sites-developing/sling-resource-merger.md) y los métodos relacionados solo se pueden utilizar con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Esto significa que la creación de una superposición con una estructura de esqueleto solo es adecuada para la IU táctil estándar.
>
>Las superposiciones de otras áreas (incluida la IU clásica) implican copiar el nodo adecuado y toda la subestructura y, a continuación, realizar los cambios necesarios.

Las superposiciones son el método recomendado para muchos cambios, como [configuración de las consolas](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) o [creación de la categoría de selección en el explorador de recursos del panel lateral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (se utiliza al crear páginas). Se requieren como sigue:

* ***No hacer* realice cambios en la `/libs` ramificación **Cualquier cambio que realice podría perderse, ya que esta rama puede cambiar siempre que haga lo siguiente:

   * actualice en su instancia
   * aplicar una revisión
   * instalación de un paquete de funciones

* Concentran los cambios en una ubicación, lo que facilita el seguimiento, la migración, la copia de seguridad o la depuración de los cambios, según sea necesario.

## Configuración de las rutas de búsqueda {#configuring-the-search-paths}

En el caso de las superposiciones, el recurso enviado es un agregado de los recursos y las propiedades recuperados, según las rutas de búsqueda que se puedan definir:

* El recurso **Ruta de búsqueda de resolución** tal como se define en la [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para el **Apache Sling Resource Resolver Factory**.

   * El orden descendente de las rutas de búsqueda indica sus respectivas prioridades.
   * En una instalación estándar, los valores predeterminados principales son `/apps`, `/libs` - así que el contenido de `/apps` tiene una prioridad mayor que la de `/libs` (es decir, es *superposiciones* it).

* Dos usuarios del servicio necesitan acceso JCR:READ a la ubicación donde se almacenan los scripts. Estos usuarios son: components-search-service (utilizado por los componentes com.day.cq.wcm.core access/cache) y sling-scripting (utilizado por org.apache.sling.servlets.resolver para buscar servlets).
* La siguiente configuración también debe configurarse según dónde coloque los scripts (en este ejemplo, en /etc, /libs o /apps).

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* Finalmente, también se debe configurar el Servlet Resolver (en este ejemplo, para añadir /etc a)

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## Ejemplo de uso {#example-of-usage}

Algunos ejemplos se tratan cuando:

* [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md)
* [Personalización de la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md)
