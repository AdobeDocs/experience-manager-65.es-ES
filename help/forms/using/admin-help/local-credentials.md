---
title: Administración de credenciales locales
seo-title: Managing local credentials
description: Obtenga información sobre cómo administrar las credenciales locales.
seo-description: Learn how to manage local credentials.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Administración de credenciales locales {#managing-local-credentials}

Las credenciales locales son credenciales de clave privada alojadas en Administración de almacén de confianza. A *credencial local* identifica dónde se almacena la credencial DES de un usuario. Mediante la administración de almacenes de confianza, puede importar y administrar sus credenciales locales utilizando, por ejemplo, archivos PFX existentes para que pueda importar, editar y eliminar credenciales locales.

AEM formularios admite credenciales RSA y DSA de hasta 4096 bits en formato estándar PKCS12 (archivos .pfx y .p12).

Puede importar y exportar cualquier número de credenciales. Si desea reemplazar una credencial caducada con el mismo alias, elimine la credencial y, a continuación, importe la nueva credencial con el mismo alias.

Para obtener información e instrucciones relacionadas con las extensiones de Acrobat Reader DC, consulte [Configuración de credenciales para usarlas con extensiones de Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importar una credencial {#import-a-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Haga clic en Importar. En Tipo de almacén de confianza, seleccione una de estas opciones:

   * **Credencial de firma de documento:** Credencial que se utiliza para emitir una firma digital en un documento.
   * **Credencial de extensiones de Acrobat Reader DC:** Certificado digital específico de extensiones de Acrobat Reader DC que permite activar los derechos de uso de Adobe Reader en los documentos de PDF producidos.
   * **Predeterminado:** Indica que esta es la credencial predeterminada para usar con extensiones de Acrobat Reader DC.

   Para obtener información sobre cómo obtener una credencial, consulte [Preparación para la instalación de AEM formularios](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar para las credenciales de las extensiones de Acrobat Reader DC y el servicio de firma. Este alias también se utiliza para acceder a las credenciales mediante programación mediante el SDK de AEM forms.

   >[!NOTE]
   >
   >El nombre del alias se convierte automáticamente en mayúsculas para que se muestre. El nombre del alias no distingue entre mayúsculas y minúsculas cuando se hace referencia a él en un proceso.

1. Haga clic en Examinar para localizar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

   Si aparece el mensaje de error &quot;No se pudo importar la credencial debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

## Exportar una credencial {#export-a-credential}

Las credenciales se exportan como archivos P12 en formato PKCS#12.

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Haga clic en el nombre de alias de la credencial que desea exportar y, a continuación, haga clic en Exportar.
1. En el cuadro Contraseña, escriba la contraseña. Esta contraseña es nueva y se utiliza para cifrar las credenciales exportadas.
1. Haga clic en Exportar, siga las instrucciones para exportar las credenciales y, a continuación, haga clic en Aceptar.

## Edición del alias o tipo de almacén de confianza de una credencial {#edit-a-credential-s-alias-or-trust-store-type}

Una vez importadas las credenciales, puede editar su nombre de alias y el tipo de almacén de confianza.

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Haga clic en el nombre de alias de la credencial que desee editar.
1. Haga clic en Actualizar credencial.
1. Edite el nombre del alias y el tipo de almacén de confianza según sea necesario y haga clic en Aceptar.

## Eliminar una credencial {#delete-a-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Seleccione las casillas de verificación de las credenciales que desea eliminar.
1. Haga clic en Eliminar y, a continuación, en Aceptar.
