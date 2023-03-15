---
title: Convenciones de nomenclatura
seo-title: Naming Conventions
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 21%

---

# Convenciones de nomenclatura{#naming-conventions}

Los nodos del repositorio están sujetos a las convenciones de nomenclatura de [Repositorio de contenido Java](/help/sites-developing/the-basics.md#java-content-repository). AEM Sin embargo, impone otras convenciones para el nombre de los nodos de la página.

## Convenciones de nomenclatura para páginas {#naming-conventions-for-pages}

Estas convenciones de nomenclatura se implementan en varios niveles:

* AEM JcrUtil: la implementación de la aplicación de la aplicación de la aplicación de la [Utilidades JCR](#jcr-utilities).
* PageManager: el [Administrador de páginas](#page-manager) proporciona métodos para operaciones a nivel de página.
* Según la interfaz de usuario utilizada:

   * [IU estándar con capacidad táctil](#standard-ui)
   * [IU clásica](#classic-ui)

### Utilidades JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) AEM es la implementación de la implementación de la implementación de JCR. De especial interés para validar nombres son las asignaciones de caracteres que controla y las siguientes validaciones:

* `isValidName`

   * Comprueba si el nombre no está vacío y contiene solo caracteres válidos.
   * Se puede utilizar para comprobar si un nombre propuesto es válido.

* `createValidName`

   * Esto crea una etiqueta válida a partir de una cadena arbitraria.
   * Se puede utilizar para crear un nombre a partir de un título.

### Administrador de páginas {#page-manager}

[PageManager](https://helpx.adobe.com/es/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) proporciona métodos para operaciones a nivel de página, basados en [JCRUtil](#jcr-utilities).

### IU estándar {#standard-ui}

La interfaz de usuario táctil estándar:

* Valida el nombre según las restricciones impuestas por PageManager cuando:

   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito

### IU clásica {#classic-ui}

La IU clásica impone restricciones más estrictas:

* Valida el nombre cuando un nombre de nodo explícito cuando:

   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito

* Caracteres válidos (solo estos caracteres son válidos cuando se crea una página desde la IU clásica) aunque `PageManagerImpl` permitirían caracteres adicionales):

   * De la &quot;a&quot; a la &quot;z&quot;
   * De la &quot;A&quot; a la &quot;Z&quot;
   * &quot;0&quot; a &quot;9&quot;
   * _ (guion bajo)
   * `-` (guion/signo menos)
