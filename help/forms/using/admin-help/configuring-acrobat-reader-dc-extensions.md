---
title: Configuración de extensiones de Acrobat Reader DC para capturar datos
description: Obtenga información sobre cómo configurar extensiones de Acrobat Reader DC para capturar datos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Configuración de extensiones de Acrobat Reader DC para capturar datos {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

AEM Si los usuarios de la instalación de los formularios en la que está el usuario utilizan la funcionalidad de captura de datos de Content Services (Obsoleto), se recomienda crear una función con acceso de solo lectura para estos usuarios.

***Nota &#x200B;**: Adobe ® Servicios de contenido de LiveCycle® ES (obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, supervisar y optimizar procesos centrados en las personas. La compatibilidad con los servicios de contenido (obsoleto) finaliza el 31/12/2014. Ver [documento de ciclo de vida del producto de Adobe](https://helpx.adobe.com/es/support/programs/eol-matrix.html).*

La captura de datos requiere que asigne una función de usuario para acceder a SampleReaderExtensionsCredential. Puede asignar la función estándar Administrador de confianza. AEM Sin embargo, tenga en cuenta que esta función otorga a los usuarios no administrativos privilegios de administrador generales que controlan la configuración de confianza de PKI y administran las credenciales de PKI, lo que podría poner en peligro la seguridad de la instalación de los formularios de la en un entorno de producción. AEM Se recomienda que el administrador del sistema de formularios de cree una función que conceda solo acceso de solo lectura al Almacén de confianza y asigne esta nueva función a usuarios que no sean administradores y que utilicen la captura de datos.

## Cree una función para los usuarios de captura de datos {#create-a-role-for-data-capture-users}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nueva función.
1. Introduzca el nombre de la función (por ejemplo, Usuario de captura de datos) y la descripción en los campos correspondientes y, a continuación, haga clic en Siguiente.
1. En la pantalla Permisos de funciones, haga clic en Buscar permisos y, a continuación, seleccione Lectura de credencial en la lista de permisos disponibles.
1. Haga clic en Aceptar y luego en Finalizar.

## Asignar la función de captura de datos {#assign-the-data-capture-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Buscar.
1. Haga clic en la función de usuario de captura de datos que ha creado.
1. En la ficha Usuarios/grupos de roles, haga clic en Buscar usuarios/grupos.
1. En la pantalla Buscar usuarios y grupos, haga clic en Buscar, seleccione los usuarios que necesitan la función de usuario de captura de datos y, a continuación, haga clic en Aceptar.
1. En la pantalla Editar rol, haga clic en Guardar.
