---
title: Uso de Maven para comunidades
seo-title: Uso de Maven para comunidades
description: AEM Communities API jar y AEM Uber API jar
seo-description: AEM Communities API jar y AEM Uber API jar
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Uso de Maven para comunidades {#using-maven-for-communities}

## Información general {#overview}

Esta sección de la documentación de AEM Communities se suma a:

* [Creación de proyectos AEM con Apache Maven](../../help/sites-developing/ht-projects-maven.md).

Ahora hay dos artefactos &quot;uber&quot; que reemplazan a artefactos individuales:

* Archivo de API de [Comunidades AEM](#communities-api-jar-artifact)
* Frasco [de API de AEM Uber](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Artificio Jar API de Communities {#communities-api-jar-artifact}

A continuación se muestra un ejemplo de GAV para el tarro de la API de AEM Communities:

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

Asegúrese de que la versión especificada corresponde a la versión del paquete Communities instalada para AEM Communities. Para verificar el número de versión instalada:

1. Inicie sesión con privilegios administrativos.
1. Vaya al Administrador [de paquetes](../../help/sites-administering/package-manager.md). Por ejemplo, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Busque el paquete: `cq-socialcommunities-pkg-1.x.xxx`
1. Extraiga la versión del nombre del paquete:
   * La primera versión de AEM 6.3 es la versión 1.11.170.
   * Los paquetes de funciones serán las versiones 1.12.xxx.

>[!NOTE]
>
>Se recomienda mantenerse al día con la última versión de Comunidades.
>
>Visite la sección [Últimas versiones](deploy-communities.md#latest-releases) para identificar la versión más reciente.

## Ejemplo de dependencia de Maven {#maven-dependency-example}

El jar de API de Communities debe especificarse antes del jar de la API de Uber.

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
