---
title: Instalación y configuración del servidor de seguridad de documentos
seo-title: Instalación y configuración del servidor de seguridad de documentos
description: 'Utilice la seguridad del documento para distribuir de forma segura cualquier información guardada en un formato compatible. Solo los usuarios autorizados pueden acceder a los documentos protegidos. '
seo-description: 'Utilice la seguridad del documento para distribuir de forma segura cualquier información guardada en un formato compatible. Solo los usuarios autorizados pueden acceder a los documentos protegidos. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
role: Admin
exl-id: 4a4bad4a-3e68-43cb-b55c-03b509a5d304
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Instalación y configuración del servidor de seguridad de documentos {#installing-and-configuring-the-document-security-server}

Utilice la seguridad del documento para distribuir de forma segura cualquier información guardada en un formato compatible. Solo los usuarios autorizados pueden acceder a los documentos protegidos.

Adobe Experience Manager Forms document security garantiza que solo los usuarios autorizados puedan utilizar sus documentos. Con la seguridad de los documentos, puede distribuir de forma segura cualquier información guardada en un formato compatible. Los formatos de archivo admitidos son Adobe Portable Document Format (PDF) y Microsoft Word, Excel y PowerPoint.

Puede proteger los documentos mediante políticas. La configuración de confidencialidad que especifique en una directiva determina cómo un destinatario puede utilizar un documento al que aplica la directiva. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, editar texto o agregar firmas y comentarios a documentos protegidos.

Las directivas se almacenan en el servidor de seguridad de documentos; las políticas se aplican a los documentos a través de la aplicación cliente. Cuando aplica una directiva a un documento, la configuración de confidencialidad especificada en la directiva protege la información que contiene el documento. Puede distribuir el documento protegido por políticas a los destinatarios autorizados por la directiva.

La seguridad de los documentos también proporciona a los clientes, espectadores e indexadores protección de documentos, visualización de documentos protegidos y documentos protegidos por índices. Para obtener información detallada sobre la seguridad del documento, consulte [acerca de la seguridad del documento](/help/forms/using/admin-help/document-security.md).

## Topología de implementación  {#deployment-topology}

La funcionalidad de seguridad de documentos solo está disponible en AEM Forms en JEE. Necesita una sola instancia de AEM Forms en JEE. También puede crear un clúster o una granja de servidores de AEM Forms, si es necesario. La siguiente topología es una topología indicativa para ejecutar la capacidad de seguridad del documento. Para obtener información detallada sobre la topología, consulte [Arquitectura y topologías de implementación para AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

En el diagrama siguiente se muestra la arquitectura típica de AEM Forms Document Security:

![](do-not-localize/document-security-typical-environment.png)

## Instalación de AEM Forms en JEE {#installing-aem-forms-on-jee}

Siga estos pasos para instalar y configurar AEM Forms en JEE:

1. Descargue el instalador de AEM 6.5 Forms en JEE desde el [sitio web de licencias de Adobe (LWS)](https://licensing.adobe.com/). Necesita un contrato de mantenimiento y soporte válido para descargar el instalador.
1. Lea el [documento de AEM Forms en plataformas compatibles con JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) y asegúrese de que el software, el hardware, los sistemas operativos, el servidor de aplicaciones, las bases de datos, los JDK y otras infraestructuras estén listos para instalar AEM Forms en JEE.
1. (Solo para instalaciones que no sean llave en mano) Lea [Preparándose para instalar el servidor único de AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) o [Preparándose para instalar el clúster de servidores de AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) y prepare su entorno para instalar y configurar AEM Forms en JEE.
1. Según el entorno y el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones para completar la instalación

   * [Instalación e implementación de AEM Forms en JEE con JBoss llave en mano](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Instalación e implementación de AEM Forms en JEE para JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Instalación e implementación de AEM Forms en JEE para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Instalación e implementación de AEM Forms en JEE para WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configuración de AEM Forms en JEE en el clúster JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configuración de AEM Forms en JEE en el clúster WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configuración de AEM Forms en JEE en el clúster WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >En la pantalla de selección de módulos de AEM Forms en el administrador de configuración de JEE, seleccione la opción Seguridad de documentos . La opción Seguridad de documento no requiere que se seleccione ningún otro módulo.

## Pasos siguientes {#next-steps}

* [Configuración de las opciones de cliente y servidor](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Crear y administrar políticas](/help/forms/using/admin-help/creating-policies.md)
* [Crear y administrar conjuntos de políticas](/help/forms/using/admin-help/creating-policy-sets.md)
