---
title: Convenciones de nomenclatura
seo-title: Convenciones de nomenclatura
description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java
seo-description: Los nodos del repositorio están sujetos a las convenciones de nomenclatura del Repositorio de contenidos de Java
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 19%

---


# Asignar nombres a las convenciones{#naming-conventions}

Los nodos del repositorio están sujetos a las convenciones de nombres del [Repositorio de contenido de Java](/help/sites-developing/the-basics.md#java-content-repository). Sin embargo, AEM impone otras convenciones para el nombre de los nodos de página.

## Convenciones de nombres para páginas {#naming-conventions-for-pages}

Estas convenciones de nombres se implementan en varios niveles:

* JcrUtil: la implementación AEM de las [utilidades JCR](#jcr-utilities).
* PageManager: el [Administrador de páginas](#page-manager) proporciona métodos para las operaciones de nivel de página.
* Según la IU que se utiliza:

   * [IU estándar con capacidad táctil](#standard-ui)
   * [IU clásica](#classic-ui)

### Utilidades JCR {#jcr-utilities}

[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) JcrUtiliza la implementación AEM de las utilidades JCR. De particular interés para validar nombres son las asignaciones de caracteres que controla y las siguientes validaciones:

* `isValidName`

   * Comprueba si el nombre no está vacío y solo contiene caracteres válidos.
   * Se puede utilizar para comprobar si un nombre propuesto es válido.

* `createValidName`

   * Esto crea una etiqueta válida a partir de una cadena arbitraria.
   * Se puede utilizar para crear un nombre a partir de un título.

### Administrador de páginas {#page-manager}

[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) PageManager proporciona métodos para las operaciones de nivel de página, según  [JCRUtil](#jcr-utilities).

### IU estándar {#standard-ui}

La IU estándar con capacidad táctil:

* Valida el nombre según las restricciones impuestas por PageManager cuando:

   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito

### IU clásica {#classic-ui}

La IU clásica impone restricciones más estrictas:

* Valida el nombre cuando se muestra un nombre de nodo explícito cuando:

   * se proporciona un título de página para la conversión en el nombre del nodo
   * se proporciona un nombre de nodo explícito

* Caracteres válidos (solo estos caracteres son válidos cuando se crea una página desde la IU clásica, aunque `PageManagerImpl` permita caracteres adicionales):

   * De la &quot;a&quot; a la &quot;z&quot;
   * De la &quot;A&quot; a la &quot;Z&quot;
   * &quot;0&quot; a &quot;9&quot;
   * _ (guion bajo)
   * `-` (guion/signo menos)

