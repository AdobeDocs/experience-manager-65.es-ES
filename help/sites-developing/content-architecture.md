---
title: Arquitectura de contenido
seo-title: Content Architecture
description: 'Sugerencias para diseñar el contenido (sugerencia: todo es contenido)'
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Arquitectura de contenido{#content-architecture}

## Sigue el modelo de David {#follow-david-s-model}

El Modelo de David fue escrito por David Nuescheler hace años, pero las ideas hoy son ciertas. Los principios principales del Modelo de David son los siguientes:

* Los datos van primero, la estructura después. Tal vez.
* Impulse la jerarquía de contenido, no permita que suceda.
* Los espacios de trabajo son para `clone()`, `merge()`y `update()`.
* Cuidado con los hermanos del mismo nombre.
* Las referencias se consideran perjudiciales.
* Los archivos son archivos.
* Las identificaciones son malas.

El Modelo de David se puede encontrar en la wiki de Jackrabbit en [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Todo es contenido {#everything-is-content}

Todo debe almacenarse en el repositorio en lugar de depender de fuentes de datos de terceros independientes, como las bases de datos. Esto se aplica al contenido creado, a los datos binarios como imágenes, código, configuraciones, etc. Esto nos permite utilizar un conjunto de API para administrar todo el contenido y administrar la promoción de este contenido mediante la replicación. También obtenemos una única fuente de backup, registro, etc.

### Utilice el principio de diseño &quot;modelo de contenido primero&quot; {#use-the-content-model-first-design-principle}

Al crear una nueva función, empiece siempre por diseñar primero la estructura de contenido JCR y, a continuación, consulte la lectura y escritura de su contenido utilizando los servlets Sling predeterminados. Esto le permitirá asegurarse de que la implementación funciona bien con los mecanismos de control de acceso predeterminados y le permitirá evitar la generación de servlets de estilo CRUD innecesarios.

### Be RESTful {#be-restful}

Los servlets deben definirse en función de resourceTypes en lugar de rutas. Esto permite utilizar los controles de acceso JCR, adherirse a los principios de REST y utilizar la resolución de recursos y recursos que se nos proporcionan en la solicitud. Esto también nos permite cambiar las secuencias de comandos que procesan direcciones URL en el servidor sin necesidad de cambiar ninguna dirección URL del lado del cliente, mientras que oculta los detalles de implementación del lado del servidor del cliente para mayor seguridad.

### Evitar definir nuevos tipos de nodos {#avoid-defining-new-node-types}

Los tipos de nodos funcionan a un nivel bajo en la capa de infraestructura y la mayoría de los requisitos se pueden cumplir utilizando un tipo de nodo sling:resourceType asignado a un tipo de nodo nt:unstructured, oak:Unstructured, sling:Folder o cq:Page. Los tipos de nodos equivalen a esquema en el repositorio y cambiar los tipos de nodos puede ser muy caro en el futuro.

### Adherirse a las convenciones de nomenclatura en el JCR {#adhere-to-naming-conventions-in-the-jcr}

El cumplimiento de las convenciones de nomenclatura aumentará la coherencia de la base de código, reduciendo la tasa de incidencia de defectos y aumentando la velocidad de los desarrolladores que trabajan en el sistema. El Adobe utiliza las siguientes convenciones para desarrollar AEM:

* Nombres de nodo

   * Todas las minúsculas
   * Separación de palabras mediante guiones

* Nombres de propiedades

   * Maleta de camello, comenzando por una letra en minúscula

* Componentes (JSP/HTML)

   * Todas las minúsculas
   * Separación de palabras mediante guiones
