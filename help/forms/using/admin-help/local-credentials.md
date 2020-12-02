---
title: Administración de credenciales locales
seo-title: Administración de credenciales locales
description: Obtenga información sobre cómo administrar las credenciales locales.
seo-description: Obtenga información sobre cómo administrar las credenciales locales.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Administración de credenciales locales {#managing-local-credentials}

Las credenciales locales son credenciales de clave privada alojadas en Administración de almacén de confianza. Una *credencial local* identifica dónde se almacena la credencial DES de un usuario. Mediante la administración de almacén de confianza, puede importar y administrar sus credenciales locales mediante, por ejemplo, archivos PFX existentes para que pueda importar, editar y eliminar las credenciales locales.

Los formularios AEM admiten credenciales RSA y DSA de hasta 4096 bits en formato PKCS12 estándar (archivos .pfx y .p12).

Puede importar y exportar cualquier número de credenciales. Si desea reemplazar una credencial caducada con el mismo alias, elimine la credencial y, a continuación, importe la nueva credencial con el mismo alias.

Para obtener información e instrucciones relacionadas con extensiones de Acrobat Reader DC, consulte [Configuración de credenciales para su uso con extensiones de Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importar una credencial {#import-a-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Haga clic en Importar. En Tipo de almacén de confianza, seleccione una de estas opciones:

   * **Credencial de firma de documento:** credencial utilizada para emitir una firma digital en un documento.
   * **Extensiones de Acrobat Reader DC Credential:** certificado digital específico de extensiones de Acrobat Reader DC que permite activar los derechos de uso de Adobe Reader en los documentos PDF producidos.
   * **Predeterminado:** indica que es la credencial predeterminada que se utiliza con las extensiones de Acrobat Reader DC.

   Para obtener información sobre cómo obtener una credencial, consulte [Preparación para instalar AEM formularios](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar de las credenciales en las extensiones de Acrobat Reader DC y en el servicio Signature. Este alias también se utiliza para acceder a las credenciales mediante programación mediante el SDK de formularios AEM.

   >[!NOTE]
   >
   >El nombre del alias se convierte automáticamente en mayúsculas para su visualización. El nombre del alias no distingue entre mayúsculas y minúsculas cuando se hace referencia a él en un proceso.

1. Haga clic en Examinar para buscar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

   Si aparece el mensaje de error &quot;Error al importar credenciales debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

## Exportar una credencial {#export-a-credential}

Las credenciales se exportan como archivos P12 en formato PKCS#12.

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Haga clic en el nombre de alias de la credencial que desee exportar y, a continuación, haga clic en Exportar.
1. En el cuadro Contraseña, escriba la contraseña. Esta contraseña es nueva y se utiliza para cifrar las credenciales exportadas.
1. Haga clic en Exportar, siga las instrucciones para exportar las credenciales y, a continuación, haga clic en Aceptar.

## Editar el alias o tipo de almacén de confianza de una credencial {#edit-a-credential-s-alias-or-trust-store-type}

Después de importar una credencial, puede editar su nombre de alias y el tipo de almacén de confianza.

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Haga clic en el nombre del alias de la credencial que desee editar.
1. Haga clic en Actualizar credenciales.
1. Edite el nombre del alias y el tipo de almacén de confianza según sea necesario y haga clic en Aceptar.

## Eliminar una credencial {#delete-a-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Seleccione las casillas de verificación de las credenciales que desea eliminar.
1. Haga clic en Eliminar y, a continuación, en Aceptar.

