---
title: Invocación de AEM Forms mediante API
seo-title: Invocación de AEM Forms mediante API
description: Invocación de AEM Forms mediante API
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# Invocación de AEM Forms mediante API {#invoking-aem-forms-using-apis}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Adobe Experience Manager Forms es un software empresarial basado en J2EE que consta de servicios que funcionan dentro de una infraestructura compartida. Las operaciones de servicio suelen consumir o producir documentos. Con AEM Forms, puede combinar el flujo de trabajo de los formularios con formularios electrónicos, la seguridad de los documentos y la generación de documentos en un conjunto integrado y coherente de servicios. Se puede acceder a estos servicios desde dentro y fuera del cortafuegos.

Las aplicaciones cliente pueden invocar mediante programación los servicios de AEM Forms mediante una API de Java, servicios web, Remoting y REST. Mediante la consola de administración, puede configurar un servicio para que exponga un punto final que permita que los servicios de AEM Forms se invoquen mediante programación. De forma predeterminada, la mayoría de los servicios están preconfigurados para exponer los extremos Remoting, Java y del servicio web.

Los requisitos empresariales determinan qué método de invocación utilizar. Por ejemplo, con la API de Java, puede integrar la funcionalidad de AEM Forms en las aplicaciones empresariales de Java, como Java Entity y Message Bans. Del mismo modo, puede integrar la funcionalidad de AEM Forms en proyectos .NET (u otros proyectos desarrollados con entornos de desarrollo compatibles con estándares de servicio web) mediante servicios web.

Los servicios requieren un contenedor de servicios para ejecutarse, de forma similar a como Enterprise JavaBeans™ (EJB) requiere un contenedor J2EE. AEM Forms solo incluye una implementación de un contenedor de servicios. El contenedor de servicio es responsable de administrar la duración de un servicio, incluida su implementación y de garantizar que todas las solicitudes se envíen al servicio correcto. También administra documentos que un servicio consume o produce.

>[!NOTE]
>
>La programación con formularios AEM no incluye información sobre cómo invocar AEM Forms mediante carpetas vigiladas o correo electrónico.

