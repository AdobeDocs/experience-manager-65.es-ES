---
title: Configuración de extensiones de Acrobat Reader DC para la captura de datos
seo-title: Configuración de extensiones de Acrobat Reader DC para la captura de datos
description: Obtenga información sobre cómo configurar extensiones de Acrobat Reader DC para la captura de datos.
seo-description: Obtenga información sobre cómo configurar extensiones de Acrobat Reader DC para la captura de datos.
uuid: af6b3c72-601e-4f54-8343-a323eeee5906
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8f8367fe-a8e9-46ee-a980-1633be02932d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Configuración de extensiones de Acrobat Reader DC para la captura de datos {#configuring-acrobat-reader-dc-extensions-for-data-capture}

Si los usuarios de la instalación de formularios AEM utilizan la funcionalidad de captura de datos de Content Services (obsoleto), se recomienda crear una función con acceso de solo lectura para estos usuarios.

***nota **: Adobe® LiveCycle® Content Services ES (obsoleto) es un sistema gestor de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, monitorear y optimizar procesos centrados en el ser humano. La compatibilidad con Content Services (obsoleto) finaliza el 31/12/2014. Consulte [documento del ciclo vital del producto de Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Para obtener información sobre la configuración de Content Services (obsoleto), consulte [Administración de Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).*

La captura de datos requiere que asigne una función de usuario para acceder a SampleReaderExtensionsCredential. Puede asignar la función de administrador de confianza estándar, pero tenga en cuenta que esta función proporciona a los usuarios generales que no son administradores los potentes privilegios de administrador que controlan la configuración de confianza de PKI y administran las credenciales de PKI, lo que podría comprometer la seguridad de la instalación de los formularios AEM en un entorno de producción. Se recomienda que el administrador del sistema de formularios AEM cree una función que conceda solo acceso de solo lectura al almacén de confianza y asigne esta nueva función a los usuarios que no sean administradores y que utilicen la captura de datos.

## Crear una función para los usuarios de captura de datos {#create-a-role-for-data-capture-users}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nueva función.
1. Introduzca el nombre de la función (por ejemplo, Usuario de captura de datos) y la descripción en los campos correspondientes y, a continuación, haga clic en Siguiente.
1. En la pantalla Permisos de roles, haga clic en Buscar permisos y, a continuación, seleccione Leído de credenciales en la lista de permisos disponibles.
1. Haga clic en Aceptar y, a continuación, en Finalizar.

## Asignar la función de captura de datos {#assign-the-data-capture-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Buscar.
1. Haga clic en la función de usuario de captura de datos que ha creado.
1. En la ficha Usuarios/grupos de roles, haga clic en Buscar usuarios/grupos.
1. En la pantalla Buscar usuarios y grupos, haga clic en Buscar, seleccione los usuarios que requieren la función de usuario de captura de datos y, a continuación, haga clic en Aceptar.
1. En la pantalla Editar función, haga clic en Guardar.

