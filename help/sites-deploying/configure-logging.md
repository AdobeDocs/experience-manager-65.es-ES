---
title: Registro
seo-title: Registro
description: Obtenga información sobre cómo configurar los parámetros globales para el servicio de registro central, la configuración específica para los servicios individuales o cómo solicitar el registro de datos.
seo-description: Obtenga información sobre cómo configurar los parámetros globales para el servicio de registro central, la configuración específica para los servicios individuales o cómo solicitar el registro de datos.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Registro{#logging}

AEM le ofrece la posibilidad de configurar:

* parámetros globales para el servicio de registro central
* registro de datos de solicitud; una configuración de registro especializada para información de solicitud
* ajustes específicos para los servicios individuales; por ejemplo, un archivo de registro y un formato individuales para los mensajes de registro

Todas ellas son [configuraciones de OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>El inicio de sesión en AEM se basa en los principios de Sling. Consulte [Registro de Sling](https://sling.apache.org/site/logging.html) para obtener más información.

## Registro global {#global-logging}

[Apache Sling Logging ](/help/sites-deploying/osgi-configuration-settings.md) Configurationse utiliza para configurar el registrador raíz. Esto define la configuración global para iniciar sesión en AEM:

* el nivel de registro
* la ubicación del archivo de registro central
* el número de versiones que deben conservarse
* rotación de versiones; bien el tamaño máximo o bien un intervalo de tiempo
* el formato que se utilizará al escribir los mensajes de registro

>[!NOTE]
>
>Este [artículo de la Base de conocimiento](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) explica cómo girar los archivos request.log y access.log.

## Registros y escritores para servicios individuales {#loggers-and-writers-for-individual-services}

Además de la configuración de registro global, AEM le permite configurar opciones específicas para un servicio individual:

* el nivel de registro específico
* la ubicación del archivo de registro individual
* el número de versiones que deben conservarse
* rotación de versiones; bien el tamaño máximo o el intervalo de tiempo
* el formato que se utilizará al escribir los mensajes de registro
* el registrador (el servicio OSGi que proporciona los mensajes de registro)

Esto le permite canal los mensajes de registro de un único servicio en un archivo independiente. Esto puede resultar especialmente útil durante el desarrollo o la realización de pruebas; por ejemplo, cuando necesita un nivel de registro mayor para un servicio específico.

AEM utiliza lo siguiente para escribir los mensajes de registro en el archivo:

1. Un **servicio OSGi** (registrador) escribe un mensaje de registro.
1. Un **Logging Logger** toma este mensaje y lo formatea según sus especificaciones.
1. Un **Escritor de registro** escribe todos estos mensajes en el archivo físico que ha definido.

Estos elementos están vinculados por los siguientes parámetros para los elementos apropiados:

* **Registrador (registrador)**

   Defina los servicios que generan los mensajes.

* **Archivo de registro (registrador)**

   Defina el archivo físico para almacenar los mensajes de registro.

   Se utiliza para vincular un registrador con un grabador de registros. El valor debe ser idéntico al mismo parámetro en la configuración del Escritor de registros para la conexión que se va a realizar.

* **Archivo de registro (escritor de registro)**

   Defina el archivo físico en el que se escribirán los mensajes de registro.

   Debe ser idéntico al mismo parámetro en la configuración del Escritor de registro, o no se realizará la coincidencia. Si no hay coincidencia, se creará un Writer implícito con la configuración predeterminada (rotación diaria del registro).

### Registros y escritores estándar {#standard-loggers-and-writers}

Ciertos registradores y escritores se incluyen en una instalación AEM estándar.

El primero es un caso especial ya que controla los archivos `request.log` y `access.log`:

* El Registrador:

   * Registrador De Datos De Solicitud Personalizable Apache Sling

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Escriba mensajes sobre el contenido de la solicitud en `request.log`.

* Vínculos a:

   * Registrador de solicitudes Apache Sling

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Escribe los mensajes en `request.log` o `access.log`.

Se pueden personalizar si es necesario, aunque la configuración estándar es adecuada para la mayoría de las instalaciones.

Los otros pares siguen la configuración estándar:

* El Registrador:

   * Configuración del registrador de Apache Sling

      (org.apache.sling.commons.log.LogManager.Factory.config)

   * Escribe `Information` mensajes en `logs/error.log`.

* Vínculos al escritor:

   * Configuración del escritor de registro de Apache Sling

      (org.apache.sling.commons.log.LogManager.Factory.writer)

* El Registrador:

   * Configuración del registrador de Apache Sling
(org.apache.sling.commons.log.LogManager.Factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Escribe `Warning` mensajes en `../logs/error.log` para el servicio `org.apache.pdfbox`.

* No se vincula a un escritor específico, por lo que creará y utilizará un escritor implícito con la configuración predeterminada (rotación diaria del registro).

### Creación de sus propios registros y escritores {#creating-your-own-loggers-and-writers}

Puede definir su propio par Logger/Writer:

1. Cree una nueva instancia de Configuración de fábrica [Configuración del registrador de registros de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique el archivo de registro.
   1. Especifique el registrador.
   1. Configure los demás parámetros según sea necesario.

1. Cree una nueva instancia de la Configuración de fábrica [Configuración de Apache Sling Logging Writer](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique el archivo de registro: debe coincidir con el especificado para el registrador.
   1. Configure los demás parámetros según sea necesario.

>[!NOTE]
>
>En determinadas circunstancias, es posible que desee crear un [archivo de registro personalizado](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

