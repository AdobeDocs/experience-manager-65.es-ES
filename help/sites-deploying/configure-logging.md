---
title: Registro
description: Obtenga información sobre cómo configurar parámetros globales para el servicio de registro central, la configuración específica de los servicios individuales o cómo solicitar el registro de datos.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Registro{#logging}

AEM le ofrece la posibilidad de configurar lo siguiente:

* parámetros globales para el servicio de registro central
* registro de datos de solicitud; una configuración de registro especializada para solicitar información
* configuración específica para los servicios individuales; por ejemplo, un archivo de registro individual y formato para los mensajes de registro

Estos son todos [Configuraciones de OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>AEM El inicio de sesión en la se basa en los principios de Sling. Consulte [Registro de Sling](https://sling.apache.org/site/logging.html) para obtener más información.

## Registro global {#global-logging}

[Configuración de registro de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md) se utiliza para configurar el registrador raíz. AEM Esto define la configuración global para iniciar sesión en el sitio de trabajo de la siguiente manera

* el nivel de registro
* la ubicación del archivo de registro central
* el número de versiones que se van a conservar
* rotación de versiones; tamaño máximo o intervalo de tiempo
* el formato que se utilizará al escribir los mensajes de registro

>[!NOTE]
>
>Esta [Artículo de Knowledge Base](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) explica cómo girar los archivos request.log y access.log.

## Registradores y escritores para servicios individuales {#loggers-and-writers-for-individual-services}

AEM Además de la configuración del registro global, le permite configurar opciones específicas para un servicio individual:

* el nivel de registro específico
* la ubicación del archivo de registro individual
* el número de versiones que se van a conservar
* rotación de versiones; tamaño máximo o intervalo de tiempo
* el formato que se utilizará al escribir los mensajes de registro
* el registrador (el servicio OSGi que suministra los mensajes de registro)

Esto permite canalizar los mensajes de registro de un solo servicio a un archivo independiente. Esto puede resultar especialmente útil durante el desarrollo o las pruebas; por ejemplo, cuando necesita aumentar el nivel de registro para un servicio específico.

AEM Utiliza lo siguiente para escribir mensajes de registro en el archivo:

1. Un **Servicio OSGi** (logger) escribe un mensaje de registro.
1. A **Registrador de registros** toma este mensaje y le da formato según su especificación.
1. A **Escritor de registro** escribe todos estos mensajes en el archivo físico que ha definido.

Estos elementos están vinculados por los siguientes parámetros para los elementos correspondientes:

* **Registrador (Registrador)**

  Defina los servicios que generan los mensajes.

* **Archivo de registro (registrador de registros)**

  Defina el archivo físico para almacenar los mensajes de registro.

  Se utiliza para vincular un registrador con un registrador. El valor debe ser idéntico al mismo parámetro en la configuración de Escritor de registro para que se realice la conexión.

* **Archivo de registro (Escritor de registro)**

  Defina el archivo físico en el que se escribirán los mensajes de registro.

  Debe ser idéntico al mismo parámetro en la configuración de Escritor de registro; de lo contrario, no se realizará la coincidencia. Si no hay coincidencia, se creará un objeto Writer implícito con la configuración predeterminada (rotación diaria del registro).

### Registradores y escritores estándar {#standard-loggers-and-writers}

AEM Ciertos registradores y escritores están incluidos en una instalación estándar de la.

El primero es un caso especial, ya que controla tanto la `request.log` y `access.log` archivos:

* El registrador:

   * Registrador de datos de solicitud personalizable de Apache Sling

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Escribir mensajes sobre el contenido de la solicitud en `request.log`.

* Vínculos a:

   * Registrador de solicitudes de Apache Sling

     (org.apache.sling.engine.impl.log.RequestLogger)

   * Escribe los mensajes en `request.log` o `access.log`.

Se pueden personalizar si es necesario, aunque la configuración estándar es adecuada para la mayoría de las instalaciones.

Los otros pares siguen la configuración estándar:

* El registrador:

   * Configuración del registrador de Apache Sling

     (org.apache.sling.commons.log.LogManager.factory.config)

   * Escribe `Information` mensajes a `logs/error.log`.

* Vínculos al escritor:

   * Configuración del escritor de registro de Apache Sling

     (org.apache.sling.commons.log.LogManager.factory.writer)

* El registrador:

   * Configuración del registrador de Apache Sling (org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Escribe `Warning` mensajes a `../logs/error.log` para el servicio `org.apache.pdfbox`.

* No se vincula a un objeto Writer específico, por lo que se crea y utiliza un objeto Writer implícito con la configuración predeterminada (rotación diaria del registro).

### Crear sus propios registradores y escritores {#creating-your-own-loggers-and-writers}

Puede definir su propio par Registrador/Escritor:

1. Cree una instancia de la configuración de fábrica [Configuración del registrador de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique el Archivo de registro.
   1. Especifique el registrador.
   1. Configure los demás parámetros según sea necesario.

1. Cree una instancia de la configuración de fábrica [Configuración del escritor de registro de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Especifique el Archivo de registro: debe coincidir con el especificado para el registrador.
   1. Configure los demás parámetros según sea necesario.

>[!NOTE]
>
>En determinadas circunstancias, es posible que desee crear una [archivo de registro personalizado](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
