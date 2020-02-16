---
title: Arquitectura del contenido
seo-title: Arquitectura del contenido
description: 'Sugerencias para diseñar el contenido (sugerencia: todo es contenido)'
seo-description: 'Sugerencias para la arquitectura del contenido en Adobe Experience Manager (AEM). (sugerencia: todo es contenido)'
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Arquitectura del contenido{#content-architecture}

## Seguir el modelo de David {#follow-david-s-model}

El Modelo de David fue escrito por David Nuescheler hace años, pero las ideas se hacen realidad hoy en día. Los principios principales del Modelo de David son los siguientes:

* Los datos son los primeros, estructurarlos más tarde. Tal vez.
* Impulse la jerarquía de contenido, no permita que esto suceda.
* Los espacios de trabajo son para `clone()`, `merge()`y `update()`.
* Cuidado con los hermanos del mismo nombre.
* Las referencias se consideran perjudiciales.
* Los archivos son archivos.
*  Las identificaciones son malas.

El Modelo de David se puede encontrar en la wiki de Jackrabbit en [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Todo es contenido {#everything-is-content}

Todo debe almacenarse en el repositorio en lugar de depender de fuentes de datos de terceros independientes, como las bases de datos. Esto se aplica a contenido creado, datos binarios como imágenes, código, configuraciones, etc. Esto nos permite utilizar un conjunto de API para administrar todo el contenido y administrar la promoción de este contenido mediante la replicación. También obtenemos una única fuente de backup, registro, etc.

### Usar el principio de diseño &quot;modelo de contenido primero&quot; {#use-the-content-model-first-design-principle}

Al crear una nueva función, comience siempre diseñando primero la estructura de contenido JCR y, a continuación, consulte la lectura y escritura del contenido con los servlets de Sling predeterminados. Esto le permitirá asegurarse de que la implementación funciona bien con los mecanismos de control de acceso predeterminados y evitar la generación de servlets innecesarios de estilo CRUD.

### Sea RESTful {#be-restful}

Los servlets deben definirse en función de resourceTypes en lugar de rutas. Esto permite utilizar los controles de acceso JCR, atenerse a los principios REST y utilizar la resolución de recursos y recursos que se nos proporcionan en la solicitud. Esto también nos permite cambiar las secuencias de comandos que procesan las direcciones URL en el servidor sin necesidad de cambiar ninguna dirección URL del lado del cliente, al tiempo que se ocultan los detalles de implementación del lado del servidor del cliente para mayor seguridad.

### Evite definir nuevos tipos de nodos {#avoid-defining-new-node-types}

Los tipos de nodo funcionan a un nivel bajo en la capa de infraestructura y la mayoría de los requisitos se pueden cumplir mediante un tipo de nodo sling:resourceType asignado a nt:unstructure, oak:Unstructure, sling:Folder o cq:Page. Los tipos de nodos equivalen a un esquema en el repositorio y cambiar los tipos de nodos puede resultar muy caro en el futuro.

### Adherirse a las convenciones de nombres en el JCR {#adhere-to-naming-conventions-in-the-jcr}

El cumplimiento de las convenciones de nombres aumentará la coherencia en la base de código, reduciendo la tasa de incidencia de defectos y aumentando la velocidad de los desarrolladores que trabajan en el sistema. Adobe utiliza las siguientes convenciones para desarrollar AEM:

* Nombres de nodos

   * Todas las minúsculas
   * Separación de palabras con guiones

* Nombres de propiedades

   * Carcasa de camello, comenzando con una letra minúscula

* Componentes (JSP/HTML)

   * Todas las minúsculas
   * Separación de palabras con guiones

