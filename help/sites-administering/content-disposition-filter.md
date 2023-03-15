---
title: Filtro de disposición de contenido
seo-title: Content Disposition Filter
description: Aprenda a utilizar el filtro de disposición de contenido para evitar ataques XSS.
seo-description: Learn how to use the Content Disposition Filter to prevent XSS attacks.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Filtro de disposición de contenido {#content-disposition-filter}

El filtro de disposición de contenido es una función de seguridad contra ataques XSS a archivos de SVG.

Una vez instalado, el filtro bloquea el acceso a todos los recursos. Por ejemplo, no puede ver un PDF en línea. En esta sección se describe cómo configurar el filtro según sus necesidades.

## Configurar el filtro de disposición de contenido {#configure-content-disposition-filter}

Puede ver el [Filtro de disposición de contenido de Apache Sling en GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Las opciones del Filtro de disposición de contenido proporcionan las siguientes funciones:

* **Rutas de disposición de contenido:** una lista de rutas a las que se aplicará el filtro seguida de una lista de tipos MIME que se excluirán de esa ruta. Esta ruta debe ser una ruta absoluta y puede contener un comodín (`*`) al final, para hacer coincidir cada ruta de recurso con el prefijo de ruta dado. Por ejemplo: `/content/*:image/jpeg,image/svg+xml` aplicará el filtro a cada nodo en `/content?` excepto imágenes jpg y svg

* **Rutas de recursos excluidas:** En una lista de recursos excluidos, cada ruta de recurso debe darse como ruta absoluta y completa. No se admiten coincidencias de prefijos ni comodines.

* **Habilitar Para Todas Las Rutas De Recursos:** este indicador controla si se activa este filtro para todas las rutas, excepto para las rutas excluidas definidas por Rutas de recursos excluidas. Si se establece en &quot;true&quot;, se ignoran las rutas de disposición de contenido. Independientemente de la configuración, solo se tratan las rutas de recurso que contienen una propiedad denominada `jcr:data` o `jcr:content/jcr:data`.
