---
title: Introducción a la API de Java QuickStart
seo-title: Introducing Java API QuickStart
description: Introducción a la API de Java QuickStart
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Developer
exl-id: 1d4062ef-fb24-4527-b899-896ce757beda
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Introducción al inicio rápido de la API de Java {#introducing-java-api-quickstart}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Adobe Inicio rápido de la API de AEM Forms puede ayudarle a acelerar sus esfuerzos para desarrollar programas que interactúen con los servicios de AEM Forms. *Inicio rápido* son programas completos que puede copiar y pegar en sus propios proyectos y usar como punto de partida. Puede ejecutar un Inicio rápido para ver cómo se comporta y modificarlo según sus necesidades.

Las operaciones de AEM Forms se pueden realizar mediante la API con establecimiento inflexible de tipos de AEM Forms y el modo de conexión se debe establecer en SOAP.

El inicio rápido de la API con establecimiento inflexible de tipos de Java proporciona una lista de los archivos JAR necesarios para ejecutar la aplicación Java. La mayoría de los inicios rápidos de Java son aplicaciones de consola que se ejecutan dentro de `main`. Sin embargo, el inicio rápido de la API con establecimiento inflexible de tipos de Forms Java se implementa como servlet de Java que se ejecuta dentro de una aplicación web.

La lista de archivos JAR se encuentra en una sección de comentarios ubicada al principio del inicio rápido. Por ejemplo, el siguiente comentario se encuentra en un Output quick start y es una lista de archivos JAR típica que se encuentra en cada Java Quick Start.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## Inicio rápido de varios servicios {#multiple-services-quick-start}

Los inicios más rápidos se encuentran en *Programación con AEM Forms en JEE* invoque un servicio específico para realizar una operación. Sin embargo, algunos Quick Starts invocan varios servicios de AEM Forms para realizar un flujo de trabajo determinado. La siguiente lista proporciona inicios rápidos de Java que invocan más de un servicio de AEM Forms:

[Inicio rápido (modo SOAP): Pasar un documento ubicado en el repositorio de AEM Forms al servicio de salida mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (invoca el servicio Repository y Output )

[Inicio rápido (modo SOAP): Creación de un documento de PDF basado en fragmentos mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) (invoca el servicio Assembler y Output )

[Inicio rápido (modo SOAP): Creación de documentos de PDF con datos XML enviados mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (invoca el servicio Forms, Output y Document Management)

[Inicio rápido (modo SOAP): Pasar documentos al servicio de Forms mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (invoca el servicio Forms y Document Management)

[Inicio rápido (modo SOAP): Firma digital de un formulario basado en XFA mediante la API de Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (invoca el servicio Forms y Signature)

[Inicio rápido (modo SOAP): Administración de funciones y permisos mediante la API de Java](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) (invoca DirectoryManager y el servicio AuthorizationManager )

[Inicio rápido (modo SOAP): Pasar documentos al servicio de salida mediante la API de Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) (invoque el servicio Output y Document Management)

>[!NOTE]
>
>Inicio rápido ubicado en Programación con AEM Forms se basa en que AEM Forms se implementa en JBoss® Application Server y en el sistema operativo Microsoft® Windows®. Sin embargo, si está utilizando otro sistema operativo, como UNIX®, reemplace las rutas específicas de Windows por rutas compatibles con el sistema operativo aplicable. Del mismo modo, si utiliza otro servidor de aplicaciones J2EE, asegúrese de especificar propiedades de conexión válidas. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>La mayoría de los servicios web Quick Starts se escriben en C# y utilizan el marco .NET. Sin embargo, puede crear una lógica de aplicación de cliente que pueda invocar los servicios de AEM Forms en cualquier entorno de desarrollo que admita los estándares SOAP. (Consulte [Invocación de AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
