---
title: No se puede usar Experience Manager Forms con ciertas versiones de Oracle JDK
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: No se puede usar Experience Manager Forms con ciertas versiones de Oracle JDK
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
source-git-commit: 91b012f8024350effc19613bcecfc42dee4130d9
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 4%

---

# No se puede usar Experience Manager Forms con ciertas versiones de Oracle JDK {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

El problema se aplica a las siguientes versiones:

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## Problema   {#issue}

El usuario encuentra la siguiente excepción:
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## Motivo {#reason}

La excepción se produce cuando ejecuta Experience Manager Forms con Oracle JDK (Java Development Kit) versión buena o igual a las siguientes versiones:

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

Las versiones anteriores y posteriores de Java, incluyen nuevos límites de procesamiento XML en la JVM (máquina virtual Java) que hacen que ciertas operaciones específicas de Forms fallen.

## Solución alternativa {#workaround}

1. Detenga el servidor de Experience Manager Forms.
1. Configure el siguiente argumento JVM para su servidor de aplicaciones:

   `-Djdk.xml.xpathExprOpLimit=2000`

   Establece la propiedad del sistema en JVM en un valor razonablemente alto para que no se alcance el límite predeterminado.

1. Inicie el servidor de Experience Manager Forms.
