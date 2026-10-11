---
title: Configurar extensiones de Acrobat Reader DC para capturar datos
description: Obtenga información sobre cómo configurar extensiones de Acrobat Reader DC para capturar datos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 621ad6f8-3769-57bb-838c-1d26cfb18d50
    internal-label: Reader Extensions
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%
---
# Configurar extensiones de Acrobat Reader DC para capturar datos {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Si los usuarios de la instalación de formularios AEM Forms utilizan la funcionalidad de captura de datos de Content Services (Obsoleto), se recomienda crear una función con acceso de solo lectura para estos usuarios.

***Nota &#x200B;**: Adobe® LiveCycle® Content Services ES (Obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, supervisar y optimizar procesos centrados en las personas. La compatibilidad con los servicios de contenido (obsoleto) finaliza el 31/12/2014. Ver [documento del ciclo de vida del producto Adobe](https://helpx.adobe.com/es/support/programs/eol-matrix.html).*

La captura de datos requiere que asigne una función de usuario para acceder a SampleReaderExtensionsCredential. Puede asignar la función estándar Administrador de confianza. Sin embargo, tenga en cuenta que esta función proporciona a los usuarios no administradores privilegios generales de administrador que controlan la configuración de confianza de PKI y administran las credenciales de PKI, lo que podría poner en peligro la seguridad de la instalación de los formularios AEM Forms en un entorno de producción. Se recomienda que el administrador del sistema de AEM Forms cree una función que conceda acceso de solo lectura al Almacén de confianza y asigne esta nueva función a usuarios que no sean administradores y que utilicen la captura de datos.

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
