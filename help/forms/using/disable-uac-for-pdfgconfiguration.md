---
title: Deshabilitar UAC para la configuración de PDFG aplicable tanto a JEE como a OSGI
description: Obtenga información sobre cómo deshabilitar UAC para la configuración de PDFG para corregir la conversión de Word a PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 62%

---

# No se pueden convertir archivos de Word o Excel a PDF en Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problema {#issue}

Cuando el usuario intenta convertir archivos de Word o Excel a PDF en Microsoft® Windows Server, se encuentra el siguiente error:

*Mensaje de error del convertidor principal:*
*ALC-PDG-015-003-El sistema no puede abrir el archivo de entrada. Vuelva a enviar el archivo o póngase en contacto con el administrador del sistema.*


## Solución {#solution}

Haga lo siguiente:

1. Para acceder a la Utilidad de configuración del sistema, vaya a **[!UICONTROL Inicio > Ejecutar]** y, a continuación, escriba **[!UICONTROL MSCONFIG]**.
1. Haga clic en la pestaña **[!UICONTROL Herramientas]**, desplácese hacia abajo y seleccione **[!UICONTROL Cambiar configuración de UAC]**. Clic **[!UICONTROL Launch]** para poder ejecutar el comando en una nueva ventana.
1. Ajuste el control deslizante al nivel No notificar nunca. Cuando termine, cierre la ventana de comandos y la de Configuración del sistema.
1. Compruebe que la configuración del registro para UAC está establecida en 0 (cero). Siga estos pasos para comprobarlo:

   1. Microsoft® recomienda realizar una copia de seguridad del registro antes de modificarlo. Para ver los pasos detallados, consulte [Realizar una copia de seguridad y restaurar el registro en Windows](https://support.microsoft.com/es-es/help/322756).
   1. Abra el editor del registro de Windows de Microsoft®. Para abrir el editor del registro, vaya a Inicio > Ejecutar, escriba regedit y haga clic en Aceptar.
   1. Navegue hasta `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Asegúrese de que el valor de EnableLUA está establecido en 0 (cero).
   1. Asegúrese de que el valor de **EnableLUA** esté establecido en 0 (cero). Si el valor no es 0, cambie el valor a 0. Cierre el editor del registro.

1. Reinicie el equipo.

## Aplicable a {#appliesto}

Esta solución se aplica a AEM Forms en el servidor JEE y a AEM Forms en el servidor OSGi.
