---
title: Habilitar conversiones de archivos con varios subprocesos
description: Obtenga información sobre cómo habilitar las conversiones de archivos con varios subprocesos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 4a55f87d3b8aa9944f0b32760aa645c42efd93e8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%
---
# Habilitar conversiones de archivos con varios subprocesos {#enabling-multi-threaded-file-conversions}

PDF Generator puede ejecutar varias conversiones de archivos simultáneamente para mejorar el rendimiento de las conversiones. Elija el modo de conversión aplicable:

| Modo de conversión | Aplicaciones que admiten conversiones simultáneas | Modelo de cuenta de usuario |
|---|---|---|
| Modo multiusuario | OpenOffice | Una cuenta de usuario independiente ejecuta cada instancia de OpenOffice. |
| Modo de un solo usuario | Microsoft® Word y Microsoft® Excel | Una cuenta de usuario ejecuta varias instancias de Word y Excel. Las conversiones de PowerPoint permanecen serializadas. |

Antes de habilitar cualquiera de los dos modos, complete la [configuración previa a la instalación de PDF Generator](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations) para las aplicaciones y el sistema operativo que utilice. Para ver las versiones de aplicaciones compatibles, consulte [Soporte de software para PDF Generator](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator).

## Modo multiusuario {#multi-user-mode}

En el modo multiusuario, PDF Generator inicia cada instancia de OpenOffice en una cuenta de usuario independiente. Configure suficientes cuentas de usuario administrativo válidas para la cantidad de conversiones simultáneas que necesita. En un clúster, configure las mismas cuentas en cada nodo.

En Windows, asegúrese de que los usuarios de PDF Generator tengan el privilegio [Reemplazar un token de nivel de proceso](/help/forms/using/install-configure-document-services.md#grant-the-replace-a-process-level-token-privilege) y complete la configuración de Control de cuentas de usuario aplicable que se describe en [Configurar servicios de documentos](/help/forms/using/install-configure-document-services.md#disable-user-account-control-uac).

### Conversiones de OpenOffice {#openoffice-conversions}

Configure una cuenta de usuario de PDF Generator para cada instancia de OpenOffice que se pueda ejecutar simultáneamente. Instale OpenOffice en una ubicación a la que todos los usuarios configurados puedan acceder y descarte los cuadros de diálogo de activación iniciales de OpenOffice para cada usuario.

Para sistemas basados en UNIX, complete los requisitos de instalación de OpenOffice y permisos de usuario en [Configurar servicios de documentos](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations).

## Modo de un solo usuario en Windows {#single-user-mode-on-windows}

El modo de un solo usuario permite que PDF Generator ejecute conversiones simultáneas en una cuenta de usuario configurada.

En este modo, varias instancias de Microsoft® Word (DOC y DOCX) y Excel (XLS y XLSX) se ejecutan bajo el mismo usuario. Microsoft® PowerPoint (PPT y PPTX) no admite el modo de usuario único. PDF Generator inicia sólo una instancia de PowerPoint a la vez, por lo que las conversiones de PowerPoint se serializan.

Para habilitar el modo de un solo usuario para las conversiones de Word y Excel:

1. En la consola de administración, vaya a **Inicio > Servicios > Aplicaciones y servicios > Administración de servicios**.
1. Filtre por **PDF Generator** y seleccione **GeneratePDFService**.
1. En la ficha **Configuración**, configure las siguientes opciones:

   * Establezca **Habilitar modo de usuario único para PDFMaker** en **true**.
   * Establezca **Tamaño de grupo de PDFMaker** en el número máximo de instancias de Word que pueden ejecutar conversiones simultáneamente.
   * Establezca **Habilitar modo de usuario único para Native2PDF** en **true**.
   * Establezca **Native2PDF Pool Size** en el número máximo de instancias de Excel que pueden ejecutar conversiones simultáneamente.

1. Reinicie el servidor de AEM Forms.
