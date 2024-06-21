---
title: Pasar credenciales mediante encabezados WS-security
description: Obtenga información sobre cómo pasar credenciales mediante encabezados WS-security
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---

# Pasar credenciales mediante encabezados WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Al invocar un servicio de AEM Forms en JEE mediante servicios web, puede utilizar encabezados WS-Security para pasar la información de autenticación de cliente que AEM Forms requiere en JEE. SOAP WS-Security define las extensiones de la para implementar la autenticación del cliente, la confidencialidad del mensaje y la integridad del mensaje. Como resultado, puede invocar AEM Forms en servicios JEE cuando AEM Forms en JEE se implementa como servidor independiente o dentro de un entorno agrupado.

La forma de pasar encabezados WS-Security a AEM Forms SOAP en JEE depende de si está utilizando clases Java generadas por Axis o un ensamblado de cliente de .NET que consume la pila de la versión nativa de un servicio de la pila de la versión de la aplicación de la versión de Windows (JEE).

>[!NOTE]
>
>Como ejemplo de invocación de un servicio mediante encabezados WS-Security, en este tema se cifra un documento de PDF con una contraseña invocando el servicio Encryption.

Este documento abarca los siguientes temas:

* Pasar la autenticación de cliente mediante clases Java generadas por Axis

* Generando archivos de biblioteca de Axis necesarios para invocar el servicio Encryption

* Invocar el servicio Encryption mediante un encabezado WS-Security

* Pasar la autenticación de cliente mediante un ensamblado de cliente de .NET

* Invocar el servicio Encryption mediante un encabezado WS-Security


## Requisitos  {#requirements}

Para sacar el máximo partido a este documento, debe tener una comprensión sólida de AEM Forms en el software JEE.

>[!MORELIKETHIS]
>
>* [Pasar credenciales mediante encabezados WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)
