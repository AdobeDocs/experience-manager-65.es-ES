---
title: Configuración de credenciales para usarlas con extensiones de Acrobat Reader DC
description: Obtenga información sobre cómo configurar credenciales para utilizarlas con extensiones de Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Configuración de credenciales para usarlas con extensiones de Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Para aplicar derechos de uso a documentos de PDF AEM, configure formularios de con una credencial válida para las extensiones de Acrobat Reader DC. AEM Es posible que se haya configurado una credencial durante la instalación de los formularios de. Si no configuró la credencial de las extensiones de Acrobat Reader DC al ejecutar el Administrador de configuración o si necesita importar una credencial nueva o de reemplazo, puede hacerlo mediante las páginas Administración del almacén de confianza.

Si utiliza una credencial de evaluación, reemplácela por una credencial de producción al pasar al entorno de producción. Para actualizar una credencial caducada o de evaluaciones, primero elimine la credencial antigua de extensiones de Acrobat Reader DC.

Para obtener información sobre cómo obtener una credencial, consulte [AEM Preparación para la instalación de formularios (un solo servidor)](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

El almacén de confianza puede contener más de una credencial de extensiones de Acrobat Reader DC. Designe una de esas credenciales como credencial predeterminada de las extensiones de Reader. La credencial predeterminada se utiliza cuando un usuario de Workbench no puede determinar qué credencial utilizar durante la creación del proceso. Estas reglas se aplican a las credenciales predeterminadas:

* Si importa una credencial de extensiones de Acrobat Reader DC y el almacén de confianza no contiene otras credenciales de extensiones de Acrobat Reader DC, se establece como predeterminada.
* Si importa una credencial de extensiones de Acrobat Reader DC con la opción predeterminada seleccionada, el tipo predeterminado se elimina de una credencial predeterminada existente. La credencial importada se convierte en la predeterminada.
* No puede eliminar una credencial de extensiones de Acrobat Reader DC predeterminada. Para eliminar la credencial predeterminada, primero establezca otra credencial como predeterminada. Una excepción a esta regla es que si solo hay una credencial, puede eliminarla aunque sea la predeterminada.
* No puede actualizar una credencial predeterminada de extensiones de Acrobat Reader DC.

>[!NOTE]
>
>También puede importar y eliminar credenciales mediante programación. (Consulte [AEM Programar con formularios de](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es).)

## Importar una credencial de extensiones de Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione Credenciales de extensiones de Acrobat Reader DC.
1. (Opcional) Para indicar que esta credencial es la credencial predeterminada que se utiliza con las extensiones de Acrobat Reader DC, seleccione Predeterminada.
1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar de la credencial en las extensiones de Acrobat Reader DC. AEM Este alias también se utiliza para acceder a las credenciales mediante programación a través del SDK de formularios de la aplicación de la plataforma de datos de.

   >[!NOTE]
   >
   >El nombre del alias se convierte automáticamente a mayúsculas para su visualización. El nombre del alias no distingue entre mayúsculas y minúsculas cuando se hace referencia a él en un proceso.

1. Haga clic en Elegir archivo para buscar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

   Si aparece el mensaje de error &quot;No se pudieron importar las credenciales debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

## Eliminar una credencial de extensiones de Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Seleccione la credencial y haga clic en Eliminar.

## Reemplazar una credencial de extensiones de Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Tome nota del alias de la credencial existente, selecciónela y haga clic en Eliminar.
1. Importe la nueva credencial con el mismo nombre de alias.
