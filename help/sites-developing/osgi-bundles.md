---
title: Paquetes OSGI
seo-title: OSGI Bundles
description: Sugerencias para administrar los paquetes OSGi
seo-description: Tips for managing your OSGi bundles
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Paquetes OSGI{#osgi-bundles}

## Uso de versiones semánticas {#use-semantic-versioning}

Las prácticas recomendadas acordadas para la numeración de versiones semánticas se encuentran en [https://semver.org/](https://semver.org/).

## No incruste más clases y tarros de los estrictamente necesarios en los paquetes OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Las bibliotecas comunes deben dividirse en paquetes independientes. Esto permite reutilizarlos en todos los paquetes. Al envolver un *JAR* en un paquete OSGI, asegúrese de comprobar las fuentes en línea para ver si alguien ya lo ha hecho antes. Algunos lugares comunes para encontrar envoltorios de paquetes existentes son: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Recetas de paquetes Eclipse y el Repositorio de paquetes Enterprise de SpringSource.

## Depender de las versiones de paquete más bajas necesarias {#depend-on-the-lowest-needed-bundle-versions}

Para las dependencias de tiempo de compilación en archivos POM, siempre dependen de la versión más baja necesaria que expone la API necesaria. Esto permitirá una mayor compatibilidad con versiones anteriores y facilita las correcciones de la compatibilidad con versiones anteriores.

## Exportación de un conjunto mínimo de paquetes desde paquetes OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Tan pronto como se ha exportado un paquete, hemos creado una API de la que otros pueden depender. Asegúrese de exportar lo menos posible y de que lo que se exporta es una API. Es mucho más fácil tomar un método/clase privado y hacerlo público que tomar algo que se exportó anteriormente y hacerlo privado.

Las implementaciones siempre deben colocarse en una carpeta independiente *impl* paquete. De forma predeterminada, la variable *maven-bundle-plugin* exportará cualquier elemento del proyecto que no tenga un *impl* en su nombre.

## Siempre defina explícitamente una versión semántica para cada paquete exportado {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Esto permitirá que los consumidores de su API evolucionen junto con usted. Al hacerlo, siga siempre las prácticas recomendadas de control semántico de versiones. Esto permitirá a los consumidores de su API saber qué tipos de cambios esperar en una nueva versión.

## Incluir información de tipos de metales donde se expone {#include-metatype-information-where-exposed}

Al especificar información significativa sobre el tipo de metal, hará que sus servicios y componentes sean más fáciles de entender en la consola Felix. Puede encontrar una lista de anotaciones y atributos de SCR en: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
