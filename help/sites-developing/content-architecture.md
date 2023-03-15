---
title: Arquitectura de contenido
seo-title: Content Architecture
description: 'Sugerencias para crear el contenido (sugerencia: todo es contenido)'
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

## Seguir el modelo de David {#follow-david-s-model}

El modelo de David fue escrito por David Nuescheler hace años, pero las ideas son ciertas hoy en día. Los principios principales del modelo de David son los siguientes:

* Los datos van primero, la estructura después. Tal vez.
* Impulse la jerarquía de contenido, no permita que ocurra.
* Los espacios de trabajo son para `clone()`, `merge()`, y `update()`.
* Tenga cuidado con los hermanos del mismo nombre.
* Las referencias se consideran perjudiciales.
* Los archivos son archivos son archivos.
* Los identificadores son malvados.

David’s Model se encuentra en la wiki de Jackrabbit en [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Todo está contenido {#everything-is-content}

Todo debe almacenarse en el repositorio en lugar de depender de fuentes de datos de terceros independientes, como bases de datos. Esto se aplica al contenido creado, a los datos binarios como imágenes, código, configuraciones, etc. Esto nos permite utilizar un conjunto de API para administrar todo el contenido y administrar la promoción de este contenido a través de la replicación. También obtenemos una única fuente de copia de seguridad, registro, etc.

### Utilice el principio de diseño &quot;el modelo de contenido primero&quot; {#use-the-content-model-first-design-principle}

Al crear una nueva función, comience siempre por diseñar primero la estructura de contenido JCR y, a continuación, busque leer y escribir el contenido utilizando los servlets predeterminados de Sling. Esto le permitirá asegurarse de que la implementación funciona correctamente con los mecanismos de control de acceso predeterminados y le permitirá evitar generar servlets innecesarios de estilo CRUD.

### Ser RESTful {#be-restful}

Los servlets deben definirse en función de resourceTypes en lugar de rutas. Esto permite utilizar controles de acceso JCR, adherirse a los principios de REST y utilizar el solucionador de recursos y recursos que se nos proporciona en la solicitud. Esto también nos permite cambiar las secuencias de comandos que representan las direcciones URL en el servidor sin necesidad de cambiar ninguna dirección URL del lado del cliente, mientras ocultamos los detalles de implementación del lado del servidor del cliente para mayor seguridad.

### Evite definir nuevos tipos de nodo {#avoid-defining-new-node-types}

Los tipos de nodo funcionan en un nivel bajo en la capa de infraestructura y la mayoría de los requisitos se pueden cumplir mediante un tipo de nodo sling:resourceType asignado a un tipo de nodo nt:unstructured, oak:Unstructured, sling:Folder o cq:Page. Los tipos de nodo equivalen al esquema en el repositorio y cambiar los tipos de nodo puede resultar muy caro en el futuro.

### Respetar las convenciones de nomenclatura en JCR. {#adhere-to-naming-conventions-in-the-jcr}

El cumplimiento de las convenciones de nomenclatura añadirá coherencia a la base de código, reduciendo la tasa de incidencia de defectos y aumentando la velocidad de los desarrolladores que trabajan en el sistema. El Adobe AEM utiliza las siguientes convenciones para desarrollar la:

* Nombres de nodo

   * Todas las minúsculas
   * Separación de palabras mediante guiones

* Nombres de propiedades

   * Mayúsculas y minúsculas, a partir de una letra minúscula

* Componentes (JSP/HTML)

   * Todas las minúsculas
   * Separación de palabras mediante guiones
