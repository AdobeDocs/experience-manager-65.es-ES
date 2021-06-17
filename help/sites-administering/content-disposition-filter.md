---
title: Filtro Disposición de contenido
seo-title: Filtro Disposición de contenido
description: Aprenda a utilizar el Filtro de disposición de contenido para evitar ataques XSS.
seo-description: Aprenda a utilizar el Filtro de disposición de contenido para evitar ataques XSS.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Filtro Disposición de contenido {#content-disposition-filter}

El filtro de disposición de contenido es una función de seguridad contra los ataques XSS en archivos SVG.

Una vez instalado, el filtro bloquea el acceso a todos los recursos. Por ejemplo, no se pudo ver un PDF en línea. En esta sección se describe cómo configurar el filtro según sus necesidades.

## Configurar el filtro de disposición de contenido {#configure-content-disposition-filter}

Puede ver el [Filtro de disposición de contenido de Apache Sling en GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Las opciones del Filtro de disposición de contenido proporcionan las siguientes funciones:

* **Rutas de disposición de contenido:** una lista de rutas en las que se aplicará el filtro seguida de una lista de tipos de mime que se excluirán en esa ruta. Esta ruta debe ser una ruta absoluta y puede contener un comodín (`*`) al final, para que coincida cada ruta de recurso con el prefijo de ruta dado. Por ejemplo: `/content/*:image/jpeg,image/svg+xml` aplicará el filtro a todos los nodos de `/content?` excepto a las imágenes jpg y svg

* **Rutas de recurso excluidas:** una lista de recursos excluidos, cada ruta de recurso debe proporcionarse como ruta absoluta y completa. No se admiten caracteres comodín/coincidentes de prefijo.

* **Habilitar para todas las rutas de recursos:**  este indicador controla si se habilita este filtro para todas las rutas, excepto para las rutas excluidas definidas por Rutas de recursos excluidas. Si se establece en &quot;true&quot;, se ignorarán las rutas de disposición del contenido. Independientemente de la configuración, solo se cubren las rutas de recursos que contienen una propiedad denominada `jcr:data` o `jcr:content/jcr:data`.
