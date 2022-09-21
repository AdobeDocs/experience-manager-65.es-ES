---
title: Deshabilitar UAC para la configuración PDFG aplicable tanto a JEE como a OSGI
description: Pasos para desactivar UAC para la configuración de PDFG
source-git-commit: f6dcb488c64dad2d65facc0e8e1d6685b7375a08
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# No se puede convertir el archivo de Word o Excel al PDF en Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problema   {#issue}

Cuando el usuario intenta convertir archivos de Word o Excel a PDF en Microsoft Windows Server, se encuentra el siguiente error:

*Mensaje de error del convertidor principal: ALC-PDG-015-003-El sistema no puede abrir el archivo de entrada. Vuelva a enviar el archivo o póngase en contacto con el administrador del sistema.*


## Solución {#solution}

Siga estos pasos para resolver el problema:
1. Para acceder a la Utilidad de configuración del sistema, vaya a **[!UICONTROL Inicio > Ejecutar]** y, a continuación, introduzca **[!UICONTROL MSCONFIG]**.
1. Haga clic en el **[!UICONTROL Herramientas]** desplácese hacia abajo y seleccione **[!UICONTROL Cambiar configuración de UAC]**. Haga clic en **[!UICONTROL Launch]** para ejecutar el comando en una nueva ventana.
1. Ajuste el control deslizante al nivel No notificar nunca. Cuando termine, cierre la ventana de comandos y cierre la ventana Configuración del sistema.
1. Compruebe que la configuración del Registro para UAC está establecida en 0 (cero). Siga estos pasos para verificar:

   1. Microsoft® recomienda realizar una copia de seguridad del registro antes de modificarlo. Para ver los pasos detallados, consulte [Cómo realizar una copia de seguridad y restaurar el Registro en Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra el editor del Registro de Windows de Microsoft®. Para abrir el editor del Registro, vaya a Inicio > Ejecutar, escriba regedit y haga clic en Aceptar.
   1. Vaya a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Asegúrese de que el valor de EnableLUA está establecido en 0 (cero).
   1. Garantizar el valor de **EnableLUA** se establece en 0 (cero). Si el valor no es 0, cambie el valor a 0. Cierre el Editor del Registro.

1. Reinicie el equipo.

## Se aplica a {#appliesto}

Esta solución se aplica a lo siguiente:
* AEM Forms en el servidor JEE
* AEM Forms en el servidor OSGi