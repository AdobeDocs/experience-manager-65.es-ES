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
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Invocación de AEM Forms mediante API {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms es un software empresarial basado en J2EE que consta de servicios que funcionan dentro de una infraestructura compartida. Las operaciones de servicio generalmente consumen o producen documentos. Con AEM Forms, puede combinar el flujo de trabajo de los formularios con formularios electrónicos, la seguridad de los documentos y la generación de documentos en un conjunto integrado y coherente de servicios. Se puede acceder a estos servicios desde dentro y fuera del cortafuegos.

Las aplicaciones cliente pueden invocar mediante programación servicios de AEM Forms mediante una API de Java, servicios Web, Remoting y REST. Mediante la consola de administración, puede configurar un servicio para que exponga un punto final que permita que los servicios de AEM Forms se invoquen mediante programación. De forma predeterminada, la mayoría de los servicios están preconfigurados para exponer los extremos de servicio Web, Java y Remoting.

Los requisitos comerciales determinan qué método de invocación se debe utilizar. Por ejemplo, con la API de Java, puede integrar la funcionalidad de AEM Forms en sus aplicaciones empresariales de Java, como Entidad de Java y Pronósticos de mensajes. Del mismo modo, puede integrar la funcionalidad de AEM Forms en proyectos .NET (u otros proyectos desarrollados con entornos de desarrollo que admitan estándares de servicio Web) mediante servicios Web.

Los servicios requieren un contenedor de servicios para ejecutarse, de forma similar a como los JavaBeans™ (EJB) empresariales requieren un contenedor J2EE. AEM Forms solo incluye una implementación de un contenedor de servicio. El contenedor de servicios es responsable de administrar la duración de un servicio, incluida su implementación y de garantizar que todas las solicitudes se envíen al servicio correcto. También administra documentos que un servicio consume o produce.

>[!NOTE]
>
>La programación con formularios AEM no incluye información sobre cómo invocar AEM Forms mediante carpetas vigiladas o correo electrónico.

