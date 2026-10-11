---
title: Pasar credenciales mediante encabezados WS-security
description: Obtenga información sobre cómo pasar credenciales mediante encabezados WS-security
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%
---
# Pasar credenciales mediante encabezados WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Al invocar un servicio de AEM Forms en JEE mediante servicios web, puede utilizar encabezados WS-Security para pasar la información de autenticación de cliente que AEM Forms requiere en JEE. WS-Security define las extensiones de SOAP para implementar la autenticación de clientes, la confidencialidad de mensajes y la integridad de mensajes. Como resultado, puede invocar AEM Forms en servicios JEE cuando AEM Forms en JEE se implementa como servidor independiente o dentro de un entorno agrupado.

La forma de pasar encabezados WS-Security a AEM Forms en JEE depende de si utiliza clases Java generadas por Axis o un ensamblado de cliente de .NET que consuma la pila nativa de SOAP de un servicio.

>[!NOTE]
>
>Como ejemplo de invocación de un servicio mediante encabezados WS-Security, en este tema se cifra un documento de PDF con una contraseña invocando el servicio Encryption.

Este documento abarca los siguientes temas:

* Pasar la autenticación de cliente mediante clases Java generadas por Axis

* Generando archivos de biblioteca de Axis necesarios para invocar el servicio Encryption

* Invocar el servicio Encryption mediante un encabezado WS-Security

* Pasar la autenticación de cliente mediante un ensamblado de cliente de .NET

* Invocar el servicio Encryption mediante un encabezado WS-Security


## Requisitos {#requirements}

Para sacar el máximo partido a este documento, debe tener una comprensión sólida de AEM Forms en el software JEE.

>[!MORELIKETHIS]
>
>* [Pasar credenciales mediante encabezados WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)
