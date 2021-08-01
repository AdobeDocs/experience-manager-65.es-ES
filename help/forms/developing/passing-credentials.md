---
title: ¿Cómo pasar credenciales utilizando encabezados WS-security?
description: Obtenga información sobre cómo pasar credenciales mediante encabezados WS-security
source-git-commit: 9b118ef4f852e3df1e717bb27b9be272caeb0456
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Pasar credenciales mediante encabezados WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Al invocar un AEM Forms en un servicio JEE mediante servicios web, puede utilizar encabezados WS-Security para pasar la información de autenticación de cliente requerida por AEM Forms en JEE. WS-Security define extensiones SOAP para implementar la autenticación de cliente, la confidencialidad de los mensajes y la integridad de los mensajes. Como resultado, puede invocar AEM Forms en servicios JEE cuando AEM Forms en JEE se implementa como servidor independiente o dentro de un entorno agrupado.

La forma de pasar encabezados WS-Security a AEM Forms en JEE depende de si está utilizando clases Java generadas por ejes o un ensamblado cliente .NET que consume la pila SOAP nativa de un servicio.

>[!NOTE]
>
>Como ejemplo de invocación de un servicio mediante encabezados WS-Security, este tema cifra un documento PDF con una contraseña invocando el servicio Encryption.

Este documento cubre los siguientes temas:

* Pasar la autenticación de cliente mediante clases Java generadas por el eje

* Generación de archivos de biblioteca de Eje necesarios para invocar el servicio de cifrado

* Invocación del servicio de cifrado mediante un encabezado WS-Security

* Pasar la autenticación de cliente mediante un ensamblado de cliente .NET

* Invocación del servicio de cifrado mediante un encabezado WS-Security


## Requisitos {#requirements}

Para aprovechar al máximo este documento, necesita tener una comprensión sólida del software AEM Forms en JEE.

>[!MORELIKETHIS]
>
>* [Pasar credenciales mediante encabezados WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)


