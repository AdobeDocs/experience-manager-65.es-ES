---
title: Paquetes OSGI
seo-title: Paquetes OSGI
description: Sugerencias para administrar los paquetes OSGi
seo-description: Sugerencias para administrar los paquetes OSGi
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Paquetes OSGI{#osgi-bundles}

## Usar versiones semánticas {#use-semantic-versioning}

Puede consultar las prácticas recomendadas para la numeración semántica en [https://semver.org/](https://semver.org/).

## No incruste más clases y tarros de los que se necesitan estrictamente en los paquetes OSGi {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Las bibliotecas comunes deben incluirse en paquetes separados. Esto les permitirá reutilizarlos en sus paquetes. Cuando envuelva un *JAR* en un paquete OSGI, asegúrese de comprobar las fuentes en línea para ver si alguien ya lo ha hecho antes. Algunos lugares comunes para encontrar los contenedores existentes son: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes y SpringSource Enterprise Bundle Repository.

## Depende de las versiones de paquete más bajas necesarias {#depend-on-the-lowest-needed-bundle-versions}

Para las dependencias de tiempo de compilación en archivos POM, siempre depende de la versión más baja necesaria que expone la API necesaria. Esto permitirá una mayor compatibilidad con versiones anteriores y facilita las correcciones de las versiones anteriores.

## Exportar un conjunto mínimo de paquetes de paquetes OSGi {#export-a-minimal-set-of-packages-from-osgi-bundles}

Tan pronto como se exporta un paquete, creamos una API de la que otros pueden depender. Asegúrese de exportar lo menos posible y de que lo que se está exportando es una API. Es mucho más fácil tomar un método o clase privado y hacerla pública que tomar algo que se exportó anteriormente y hacerlo privado.

Las implementaciones deben colocarse siempre en un paquete *impl* independiente. De forma predeterminada, *maven-bundle-plugin* exportará cualquier elemento del proyecto que no tenga un *impl* en su nombre.

## Definir siempre explícitamente una versión semántica para cada paquete exportado {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Esto permitirá que los consumidores de su API evolucionen junto con usted. Cuando lo haga, siga siempre las optimizaciones semánticas de versiones. Esto permitirá a los consumidores de su API saber qué tipos de cambios se esperan en una nueva versión.

## Incluir información de tipo de milímetro cuando se exponga {#include-metatype-information-where-exposed}

Al especificar información significativa sobre los tipos de metadatos, sus servicios y componentes serán más fáciles de entender en la consola Felix. Puede encontrar una lista de anotaciones y atributos de SCR en: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
