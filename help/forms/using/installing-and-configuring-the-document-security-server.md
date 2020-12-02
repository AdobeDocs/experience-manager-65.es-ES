---
title: Instalación y configuración del servidor de seguridad de documento
seo-title: Instalación y configuración del servidor de seguridad de documento
description: 'Utilice la seguridad de documento para distribuir de forma segura cualquier información que haya guardado en un formato compatible. Solo los usuarios autorizados pueden acceder a documentos protegidos. '
seo-description: 'Utilice la seguridad de documento para distribuir de forma segura cualquier información que haya guardado en un formato compatible. Solo los usuarios autorizados pueden acceder a documentos protegidos. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# Instalación y configuración del servidor de seguridad de documento {#installing-and-configuring-the-document-security-server}

Utilice la seguridad de documento para distribuir de forma segura cualquier información que haya guardado en un formato compatible. Solo los usuarios autorizados pueden acceder a documentos protegidos.

La seguridad de Adobe Experience Manager Forms documento garantiza que solo los usuarios autorizados puedan utilizar sus documentos. Con la seguridad de documento, puede distribuir con seguridad cualquier información que haya guardado en un formato compatible. Los formatos de archivo admitidos son Formato de Documento portátil Adobe (PDF) y archivos de Microsoft Word, Excel y PowerPoint.

Puede proteger documentos mediante políticas. La configuración de confidencialidad que especifique en una política determinará cómo puede un destinatario utilizar un documento al que aplique la política. Por ejemplo, puede especificar si los destinatarios pueden imprimir o copiar texto, editar texto o agregar firmas y comentarios a documentos protegidos.

Las directivas se almacenan en el servidor de seguridad de Documento; las políticas se aplican a los documentos a través de la aplicación cliente. Cuando se aplica una política a un documento, la configuración de confidencialidad especificada en la política protege la información que contiene el documento. Puede distribuir el documento protegido por una política a destinatarios autorizados por la política.

La seguridad de documento también proporciona clientes, visores e indexadores para proteger documentos, documentos protegidos por vistas y documentos protegidos por índices. Para obtener información detallada sobre la seguridad de documento, consulte [acerca de la seguridad de documento](/help/forms/using/admin-help/document-security.md).

## Topología de implementación {#deployment-topology}

La capacidad de seguridad de documento solo está disponible en AEM Forms en JEE. Se requiere una sola instancia de AEM Forms en JEE. También puede crear un clúster o conjunto de servidores de AEM Forms, si es necesario. La siguiente topología es una topología indicativa para ejecutar la capacidad de seguridad de documento. Para obtener información detallada sobre la topología, consulte [Topologías de arquitectura e implementación para AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

En el diagrama siguiente se muestra la arquitectura típica de Seguridad de Documento de AEM Forms:

![](do-not-localize/document-security-typical-environment.png)

## Instalación de AEM Forms en JEE {#installing-aem-forms-on-jee}

Realice los siguientes pasos para instalar y configurar AEM Forms en JEE:

1. Descargue el instalador de Forms AEM 6.5 en JEE desde el [sitio web de licencias de Adobe (LWS)](https://licensing.adobe.com/). Se requiere un contrato de mantenimiento y soporte válido para descargar el instalador.
1. Lea [AEM Forms en el documento de plataformas admitidas por JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) y asegúrese de tener el software, el hardware, los sistemas operativos, el servidor de aplicaciones, las bases de datos, los JDK y otras infraestructuras listas para instalar AEM Forms en JEE.
1. (Solo las instalaciones no llave en mano) Lea [Preparación para instalar AEM Forms single server](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) o [Preparación para instalar AEM Forms server cluster](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) y prepare su entorno para instalar y configurar AEM Forms en JEE.
1. Según el entorno y el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones para completar la instalación

   * [Instalación e implementación de AEM Forms en JEE con JBoss llave en mano](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Instalación e implementación de AEM Forms en JEE para JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Instalación e implementación de AEM Forms en JEE para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Instalación e implementación de AEM Forms en JEE para WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configuración de AEM Forms en JEE en el clúster de JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configuración de AEM Forms en JEE en el clúster de WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configuración de AEM Forms en JEE en el clúster de WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >En la pantalla de selección de módulos de AEM Forms en el administrador de configuración de JEE, seleccione la opción Seguridad de Documento. La opción Seguridad de Documento no requiere que se seleccione ningún otro módulo.

## Próximos pasos {#next-steps}

* [Configuración de las opciones de cliente y servidor](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Crear y administrar políticas](/help/forms/using/admin-help/creating-policies.md)
* [Crear y administrar conjuntos de políticas](/help/forms/using/admin-help/creating-policy-sets.md)
