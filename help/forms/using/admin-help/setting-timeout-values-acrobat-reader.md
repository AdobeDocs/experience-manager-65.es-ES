---
title: Configuración de valores de tiempo de espera para utilizarlos con extensiones de Acrobat Reader DC
description: Obtenga información sobre cómo establecer valores de tiempo de espera para utilizarlos con extensiones de Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Configuración de valores de tiempo de espera para utilizarlos con extensiones de Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Cuando trabaje con muchos archivos de PDF en Extensiones de Acrobat Reader DC, asegúrese de que los siguientes valores de tiempo de espera estén correctamente configurados para evitar que los trabajos agoten el tiempo de espera y produzcan errores:

**Tiempo de espera de eliminación de documento**

Este valor se puede establecer en la consola de administración. Haga clic en Configuración > Configuración del sistema principal > Configuraciones y especifique un valor para Tiempo de espera de eliminación de documentos predeterminado.

AEM **Tiempo de espera de formularios de la versión de User Manager:** Este valor se puede establecer editando el archivo config.xml. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración y, a continuación, haga clic en Exportar. Abra el archivo config.xml exportado y edite las siguientes líneas:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Guarde y vuelva a importar el archivo config.xml en la consola de administración.

**Tiempo de espera de sesión del servidor de aplicaciones:** Este valor se puede establecer en el servidor de aplicaciones. Para obtener más información, consulte la documentación proporcionada con el servidor de aplicaciones.
