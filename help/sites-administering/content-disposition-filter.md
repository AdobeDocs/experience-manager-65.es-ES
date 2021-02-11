---
title: Filtro de disposición de contenido
seo-title: Filtro de disposición de contenido
description: Aprenda a utilizar el filtro de disposición de contenido para evitar ataques XSS.
seo-description: Aprenda a utilizar el filtro de disposición de contenido para evitar ataques XSS.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
translation-type: tm+mt
source-git-commit: bb50e530f0d015c0e7d06650157e3e3994082483
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Filtro de disposición de contenido{#content-disposition-filter}

El filtro de disposición de contenido es una función de seguridad contra los ataques XSS en archivos SVG.

Una vez instalado, el filtro bloquea el acceso a todos los recursos. Por ejemplo, no se pudo realizar la vista de un PDF en línea. Esta sección describe cómo configurar el filtro según sus necesidades.

## Configurar el filtro de disposición de contenido {#configure-content-disposition-filter}

Puede vista del [Filtro de disposición de contenido de Apache Sling en GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Las opciones de Filtro de disposición del contenido proporcionan la siguiente funcionalidad:

* Rutas de disposición del contenido: una lista de rutas donde se aplicará el filtro seguida de una lista de tipos MIME para excluir en esa ruta. Esta ruta debe ser una ruta absoluta y puede contener un comodín (&#39;&amp;ast;&#39;) al final, para que todas las rutas de recursos coincidan con el prefijo de ruta dado. Por ejemplo: /content/&amp;ast;:image/jpeg,image/svg+xml &quot; aplicará el filtro a todos los nodos de /content excepto las imágenes jpg y svg

* Rutas de recursos excluidas: Una lista de recursos excluidos, cada ruta de recursos debe proporcionarse como ruta absoluta y completa. No se admiten caracteres comodín/coincidencia de prefijos.

* Habilitar para todas las rutas de recursos: este indicador controla si se habilita este filtro para todas las rutas, excepto para las rutas excluidas definidas por Rutas de recursos excluidas. Si se establece en &#39;true&#39;, se ignora la ruta de disposición del contenido. Independientemente de la configuración, solo se cubren las rutas de recursos que contienen una propiedad denominada &#39;jcr:data&#39; o &#39;jcr:content/jcr:data&#39;.
