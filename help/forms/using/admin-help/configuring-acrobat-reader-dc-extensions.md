---
title: Configuración de extensiones de Acrobat Reader DC para la captura de datos
seo-title: Configuring Acrobat Reader DC extensions for data capture
description: Obtenga información sobre cómo configurar extensiones de Acrobat Reader DC para la captura de datos.
seo-description: Learn how to configure Acrobat Reader DC extensions for data capture.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Configuración de extensiones de Acrobat Reader DC para la captura de datos {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Si los usuarios de la instalación de los formularios AEM utilizan la funcionalidad de captura de datos de Content Services (obsoleto), se recomienda crear una función con acceso de solo lectura para estos usuarios.

***nota **: Adobe® Content Services ES (obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, monitorear y optimizar procesos centrados en el ser humano. La compatibilidad con los servicios de contenido (obsoletos) finaliza el 31/12/2014. Consulte [Documento de ciclo de vida del producto de Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).*

La captura de datos requiere que asigne una función de usuario para acceder a SampleReaderExtensionsCredential. Puede asignar la función de administrador de confianza estándar, pero tenga en cuenta que esta función proporciona a los usuarios generales que no son administradores los potentes privilegios de administrador que controlan la configuración de confianza de PKI y administran las credenciales de PKI, lo que podría comprometer la seguridad de la instalación de los formularios AEM en un entorno de producción. Se recomienda que el administrador del sistema de AEM forms cree una función que conceda solo acceso de solo lectura al Almacén de confianza y asigne esta nueva función a los usuarios que no sean administradores y que utilicen la captura de datos.

## Crear una función para los usuarios de la captura de datos {#create-a-role-for-data-capture-users}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nueva función.
1. Introduzca el nombre de la función (por ejemplo, Usuario de captura de datos) y la descripción en los campos correspondientes y, a continuación, haga clic en Siguiente.
1. En la pantalla Permisos de rol, haga clic en Buscar permisos y, a continuación, seleccione Leído de Credencial en la lista de permisos disponibles.
1. Haga clic en Aceptar y, a continuación, en Finalizar.

## Asignación de la función de captura de datos {#assign-the-data-capture-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Buscar.
1. Haga clic en la función de usuario de captura de datos que ha creado.
1. En la ficha Usuarios/grupos de funciones , haga clic en Buscar usuarios/grupos.
1. En la pantalla Buscar usuarios y grupos, haga clic en Buscar, seleccione los usuarios que necesitan la función de usuario de captura de datos y, a continuación, haga clic en Aceptar.
1. En la pantalla Editar función, haga clic en Guardar.
