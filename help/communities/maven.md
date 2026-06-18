---
title: Uso de Maven para comunidades
description: Obtenga información acerca del JAR de la API de Adobe Experience Manager Uber para su uso en comunidades.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3df90511-e43e-442b-bf73-44c22c1886b7
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1c2c350e91fe9a0a67618ea4ec00d4a8b4e3f0ca
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Uso de Maven para comunidades {#using-maven-for-communities}

## Información general {#overview}

Esta sección de la documentación de las comunidades de Adobe Experience Manager (AEM) se suma a lo siguiente:

* [Generando proyectos de AEM usando Apache Maven](../../help/sites-developing/ht-projects-maven.md).

Solo hay un artefacto &quot;uber&quot; que reemplaza artefactos individuales:

* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

>[!NOTE]
>
>A partir de AEM 6.4, las API de Communities no se lanzan explícitamente. Todas las API de Communities ahora están incluidas en el propio Uber jar.
>
>Manténgase al día con la última versión de Communities.
>
>Consulte la sección [Últimas versiones](deploy-communities.md#latest-releases), donde podrá identificar la versión más reciente.

## Ejemplo de dependencia de Maven

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.7</version>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>Consulte el [repositorio jar de AEM Uber](https://mvnrepository.com/artifact/com.adobe.aem/uber-jar) donde podrá identificar el último artefacto jar de Uber.

<!--
There are now two "uber" artifacts that replace individual artifacts:

* AEM [Communities API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Communities API Jar Artifact {#communities-api-jar-artifact}

Following is an example of a GAV for the AEM Communities API jar:

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>

```

Ensure thet the version specified corresponds with the Communities package version installed for AEM Communities. To verify the installed version number:

1. Log in with adminstrative privileges.
1. Browse to [Package Manager](../../help/sites-administering/package-manager.md). For example, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Locate the package: `cq-socialcommunities-pkg-1.x.xxx`
1. Extract the version from the package name:
   * First version for AEM 6.3 is version 1.11.170.
   * Feature packs is versions 1.12.xxx.

>[!NOTE]
>
>It is recommended to keep up-to-date with the most recent Communities release.
>
>Visit the [Latest Releases](deploy-communities.md#latest-releases) section to identify the most recent version.

## Maven Dependency Example

The Communities API jar must be specified before the Uber API jar.

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
-->
