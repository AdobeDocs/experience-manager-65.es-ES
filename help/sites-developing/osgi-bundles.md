---
title: Paquetes OSGI
seo-title: OSGI Bundles
description: Sugerencias para administrar sus paquetes OSGi
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

Puede consultar las prácticas recomendadas para la numeración semántica en [https://semver.org/](https://semver.org/).

## No incruste más clases y tarros de los estrictamente necesarios en los paquetes OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Las bibliotecas comunes deben incluirse en paquetes separados. Esto les permitirá reutilizarlas en sus paquetes. Al ajustar un *JAR* en un paquete OSGI, asegúrese de comprobar las fuentes en línea para ver si alguien ya ha hecho esto antes. Algunos lugares comunes para encontrar contenedores de paquetes existentes son: Apache Felix, Apache Sling, Apache Gerónimo, Apache ServiceMix, Eclipse Bundle Recipes y el Repositorio de Paquetes de SpringSource Enterprise.

## Depende de las versiones de paquete más bajas necesarias {#depend-on-the-lowest-needed-bundle-versions}

Para las dependencias de tiempo de compilación en archivos POM, siempre depende de la versión más baja necesaria que expone la API necesaria. Esto permitirá una mayor compatibilidad con versiones anteriores y facilita las correcciones de versiones anteriores.

## Exportar un conjunto mínimo de paquetes de paquetes OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

En cuanto se ha exportado un paquete, se ha creado una API de la que dependen otros. Asegúrese de exportar lo menos posible y de que lo que se exporta es una API. Es mucho más fácil tomar un método o clase privado y hacerlo público que tomar algo que se exportó anteriormente y hacerlo privado.

Las implementaciones siempre deben colocarse en una *impl* paquete. De forma predeterminada, la variable *maven-bundle-plugin* exportará cualquier elemento del proyecto que no tenga un *impl* en su nombre.

## Definir siempre explícitamente una versión semántica para cada paquete exportado {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Esto permitirá a los consumidores de su API evolucionar junto con usted. Al hacerlo, siga siempre las prácticas recomendadas de versiones semánticas. Esto permitirá a los consumidores de su API saber qué tipos de cambios se esperan en una nueva versión.

## Incluir información de tipo de meto donde se exponga {#include-metatype-information-where-exposed}

Al especificar información significativa de los tipos de metadatos, hará que sus servicios y componentes sean más fáciles de entender en la consola Felix. Puede encontrar una lista de anotaciones y atributos de SCR en: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
