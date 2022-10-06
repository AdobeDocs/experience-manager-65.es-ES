---
title: Configuración de credenciales para usarlas con extensiones de Acrobat Reader DC
seo-title: Configuring credentials for use with Acrobat Reader DC extensions
description: Obtenga información sobre cómo configurar credenciales para usarlas con extensiones de Acrobat Reader DC.
seo-description: Learn how to configure credentials for use with Acrobat Reader DC extensions.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# Configuración de credenciales para usarlas con extensiones de Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Para aplicar derechos de uso a documentos de PDF, configure AEM formularios con una credencial válida para extensiones de Acrobat Reader DC. Es posible que se haya configurado una credencial durante la instalación de AEM formularios. Si no configuró las credenciales de las extensiones de Acrobat Reader DC mientras ejecuta Configuration Manager o si necesita importar una credencial nueva o de reemplazo, puede hacerlo usando las páginas Administración de almacén de confianza .

Si está utilizando una credencial de evaluación, sustitúyala por una credencial de producción al pasar al entorno de producción. Para actualizar una credencial de caducada o de evaluaciones, primero elimine la credencial de extensiones de Acrobat Reader DC antigua.

Para obtener información sobre cómo obtener una credencial, consulte [Preparación para instalar AEM formularios (un solo servidor)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

El almacén de confianza puede contener más de una credencial de extensiones de Acrobat Reader DC. Debe designar una de esas credenciales como credencial predeterminada de Extensiones de Reader. La credencial predeterminada se utiliza cuando un usuario de Workbench no puede determinar qué credencial utilizar durante la creación del proceso. Estas reglas se aplican a las credenciales predeterminadas:

* Si importa una credencial de extensiones de Acrobat Reader DC y el almacén de confianza no contiene otras credenciales de extensiones de Acrobat Reader DC, se establece como predeterminado.
* Si importa una credencial de extensiones de Acrobat Reader DC con la opción Predeterminado seleccionada, se eliminará el tipo predeterminado de una credencial predeterminada existente. La credencial importada se convierte en el valor predeterminado.
* No puede eliminar una credencial de extensiones de Acrobat Reader DC predeterminada. Para eliminar la credencial predeterminada, establezca primero otra credencial como la predeterminada. Una excepción a esta regla es que si solo hay una credencial, puede eliminarla aunque sea la predeterminada.
* No puede actualizar una credencial de extensiones de Acrobat Reader DC predeterminada.

>[!NOTE]
>
>También puede importar y eliminar credenciales mediante programación. (Consulte [Programación con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)

## Importar credenciales de extensiones de Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione Credencial de extensiones de Acrobat Reader DC.
1. (Opcional) Para indicar que esta credencial es la credencial predeterminada que se utiliza con las extensiones de Acrobat Reader DC, seleccione Predeterminado.
1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar para las credenciales de las extensiones de Acrobat Reader DC. Este alias también se utiliza para acceder a las credenciales mediante programación mediante el SDK de AEM forms.

   >[!NOTE]
   >
   >El nombre del alias se convierte automáticamente en mayúsculas para que se muestre. El nombre del alias no distingue entre mayúsculas y minúsculas cuando se hace referencia a él en un proceso.

1. Haga clic en Elegir archivo para localizar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

   Si aparece el mensaje de error &quot;No se pudo importar la credencial debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

## Eliminación de credenciales de extensiones de Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Seleccione la credencial y haga clic en Eliminar.

## Reemplazar una credencial de extensiones de Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Tome nota del alias de la credencial existente, selecciónelo y haga clic en Eliminar.
1. Importe la nueva credencial utilizando exactamente el mismo nombre de alias.
