---
title: Registro
seo-title: Registro
description: Obtenga información sobre cómo configurar parámetros globales para el servicio de registro central, ajustes específicos para los servicios individuales o cómo solicitar el registro de datos.
seo-description: Obtenga información sobre cómo configurar parámetros globales para el servicio de registro central, ajustes específicos para los servicios individuales o cómo solicitar el registro de datos.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# Registro{#logging}

AEM le ofrece la posibilidad de configurar:

* parámetros globales para el servicio de registro central
* solicitar el registro de datos; una configuración de registro especializada para información de solicitud
* ajustes específicos para los servicios individuales; por ejemplo, un archivo de registro y un formato individuales para los mensajes de registro

Todas estas son [configuraciones de OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>El inicio de sesión en AEM se basa en los principios de Sling. Consulte [Sling Logging](https://sling.apache.org/site/logging.html) para obtener más información.

## Registro global {#global-logging}

[La ](/help/sites-deploying/osgi-configuration-settings.md) configuración de registro de Apache Sling se utiliza para configurar el registrador raíz. Esto define la configuración global para iniciar sesión en AEM:

* el nivel de registro
* la ubicación del archivo de registro central
* el número de versiones que deben conservarse
* rotación de versiones; bien un tamaño máximo o un intervalo de tiempo
* el formato que se utilizará al escribir los mensajes de registro

>[!NOTE]
>
>Este [artículo de la Base de conocimiento](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) explica cómo rotar los archivos request.log y access.log.

## Registradores y escritores para servicios individuales {#loggers-and-writers-for-individual-services}

Además de la configuración de registro global, AEM permite configurar opciones específicas para un servicio individual:

* el nivel de registro específico
* la ubicación del archivo de registro individual
* el número de versiones que deben conservarse
* rotación de versiones; bien el tamaño máximo o el intervalo de tiempo
* el formato que se utilizará al escribir los mensajes de registro
* el registrador (el servicio OSGi que proporciona los mensajes de registro)

Esto le permite canalizar mensajes de registro para un solo servicio en un archivo independiente. Esto puede resultar especialmente útil durante el desarrollo o los ensayos; por ejemplo, cuando necesita un nivel de registro mayor para un servicio específico.

AEM utiliza lo siguiente para escribir mensajes de registro en el archivo:

1. Un **servicio OSGi** (registrador) escribe un mensaje de registro.
1. Un **Registrador de registros** toma este mensaje y lo da formato según su especificación.
1. Un **Escritor de registro** escribe todos estos mensajes en el archivo físico que ha definido.

Estos elementos están vinculados por los siguientes parámetros para los elementos adecuados:

* **Registrador (registrador)**

   Defina los servicios que generan los mensajes.

* **Archivo de registro (registrador)**

   Defina el archivo físico para almacenar los mensajes de registro.

   Se utiliza para vincular un Registrador de registros con un Escritor de registros. El valor debe ser idéntico al mismo parámetro en la configuración de Logging Writer para la conexión que se va a realizar.

* **Archivo de registro (escritor de registro)**

   Defina el archivo físico en el que se escribirán los mensajes de registro.

   Debe ser idéntico al mismo parámetro en la configuración del Escritor de registros o no se producirá la coincidencia. Si no hay coincidencia, se creará un Writer implícito con la configuración predeterminada (rotación diaria del registro).

### Registradores y escritores estándar {#standard-loggers-and-writers}

Algunos Registradores y Escritores están incluidos en una instalación AEM estándar.

El primero es un caso especial, ya que controla los archivos `request.log` y `access.log`:

* El registrador:

   * Registrador de datos de solicitud personalizable de Apache Sling

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Escriba mensajes sobre el contenido de la solicitud en `request.log`.

* Vínculos a:

   * Registrador de solicitudes de Apache Sling

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Escribe los mensajes en `request.log` o `access.log`.

Se pueden personalizar si es necesario, aunque la configuración estándar es adecuada para la mayoría de las instalaciones.

Los otros pares siguen la configuración estándar:

* El registrador:

   * Configuración del registrador de Apache Sling

      (org.apache.sling.commons.log.LogManager.factory.config)

   * Escribe `Information` mensajes en `logs/error.log`.

* Enlaces al escritor:

   * Configuración del Escritor de registro de Apache Sling

      (org.apache.sling.commons.log.LogManager.factory.writer)

* El registrador:

   * Configuración del registrador de Apache Sling
(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Escribe `Warning` mensajes en `../logs/error.log` para el servicio `org.apache.pdfbox`.

* No vincula a un escritor específico, por lo que creará y utilizará un Writer implícito con la configuración predeterminada (rotación diaria del registro).

### Creación de sus propios registradores y escritores {#creating-your-own-loggers-and-writers}

Puede definir su propio par Logger / Writer:

1. Cree una nueva instancia de la configuración de fábrica [Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique el archivo de registro.
   1. Especifique el Registrador.
   1. Configure los demás parámetros según sea necesario.

1. Cree una nueva instancia de la Configuración de fábrica [Apache Sling Logging Writer Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique el archivo de registro: debe coincidir con el especificado para el registrador.
   1. Configure los demás parámetros según sea necesario.

>[!NOTE]
>
>En determinadas circunstancias, es posible que desee crear un [archivo de registro personalizado](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

