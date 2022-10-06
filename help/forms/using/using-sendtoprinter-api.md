---
title: Uso de la API sendToPrinter
seo-title: Using the sendToPrinter API
description: Uso del servicio sendToPrinter para enviar un documento a la impresora.
seo-description: Using the sendToPrinter service to send a document to printer.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 14%

---

# Uso de la API sendToPrinter {#using-the-sendtoprinter-api}

## Información general {#overview}

En AEM Forms, puede utilizar el servicio SendToPrinter para enviar un documento a la impresora. El servicio SendToPrinter es compatible con los siguientes mecanismos de acceso de impresión:

* **Impresora accesible directamente** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Impresora accesible indirecto** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   Cuando envíe un documento a una impresora, especifique uno de estos protocolos de impresión:

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**: El servicio Output es compatible con el protocolo de impresión del Sistema de archivos de Internet común (CIFS).

## Uso del servicio SendToPrinter {#using-sendtoprinter-service}

La tabla siguiente enumera:

* información sobre el nombre de impresora o printServer que se utilizará para varios protocolos.
* valor o excepción que devuelve una impresora para varias combinaciones de URI de servidor de impresora y Nombre de la impresora

| Protocolo (mecanismo de acceso) | URI del servidor de impresión (PrinterSpec.printServer) | Nombre de la impresora (PrinterSpec.PrinterName) | Resultado |
|--- |--- |--- |--- |
| SharedPrinter | Cualquiera | Vacío | Excepción: El argumento requerido sPrinterName no puede estar vacío. |
| SharedPrinter | Cualquiera | No válido | Una excepción indica que no se puede encontrar la impresora. |
| SharedPrinter | Cualquiera | Válido | Trabajo de impresión correcto. |
| LPD | Vacío | Cualquiera | una excepción que indica que el argumento requerido sPrintServerUri no puede estar vacío. |
| LPD | No válido | Vacío | una excepción que indica que el argumento requerido sPrinterName no puede estar vacío. |
| LPD | No válido | No vacío | excepción que indica que sPrintServerUri no se encuentra. |
| LPD | Válido | No válido | una excepción que indica que no se puede encontrar la impresora. |
| LPD | Válido | Válido | Un trabajo de impresión correcto. |
| CUPS | Vacío | Cualquiera | una excepción que indica que el argumento requerido sPrintServerUri no puede estar vacío. |
| CUPS | No válido | Cualquiera | una excepción que indica que no se puede encontrar la impresora. |
| CUPS | Válido | Cualquiera | Trabajo de impresión correcto. |
| DirectIP | Vacío | Cualquiera | una excepción que indica que el argumento requerido sPrintServerUri no puede estar vacío. |
| DirectIP | No válido | Cualquiera | una excepción que indica que no se puede encontrar la impresora. |
| DirectIP | Válido | Cualquiera | Trabajo de impresión correcto. |
| CIFS | Válido | Vacío | Trabajo de impresión correcto. |
| CIFS | No válido | Cualquiera | error desconocido al imprimir con CIFS. |
| CIFS | Vacío | Cualquiera | una excepción que indica que el argumento requerido sPrintServerUri no puede estar vacío. |

## Compatibilidad con autenticación {#authentication-support}

La autenticación solo es compatible para la impresión CIFS. Para autenticarse, proporcione el nombre de usuario/contraseña/dominio en PrinterSpec. Puede cifrar una contraseña utilizando AEM servicio de asistencia técnica de Granite Cyprto siguiendo estos pasos:

1. Vaya a https://&lt;server>:&lt;port>/system/console.

1. Vaya a **[!UICONTROL Principal]** > **[!UICONTROL Compatibilidad con Crypto]**.

1. Introduzca texto sin formato y haga clic en **[!UICONTROL Protect]**.
