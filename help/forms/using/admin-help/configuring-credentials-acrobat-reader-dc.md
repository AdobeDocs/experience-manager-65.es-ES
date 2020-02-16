---
title: Configuración de credenciales para su uso con extensiones de Acrobat Reader DC
seo-title: Configuración de credenciales para su uso con extensiones de Acrobat Reader DC
description: Obtenga información sobre cómo configurar las credenciales para usarlas con extensiones de Acrobat Reader DC.
seo-description: Obtenga información sobre cómo configurar las credenciales para usarlas con extensiones de Acrobat Reader DC.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de credenciales para su uso con extensiones de Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Para aplicar derechos de uso a documentos PDF, configure formularios AEM con una credencial válida para extensiones de Acrobat Reader DC. Es posible que se haya configurado una credencial durante la instalación de formularios AEM. Si no configuró las credenciales de extensiones de Acrobat Reader DC al ejecutar Configuration Manager o si necesita importar una credencial nueva o de reemplazo, puede hacerlo mediante las páginas de administración de almacén de confianza.

Si está utilizando una credencial de evaluación, reemplácela por una credencial de producción cuando se desplace al entorno de producción. Para actualizar una credencial de evaluación o caducada, primero elimine las credenciales antiguas de extensiones de Acrobat Reader DC.

Para obtener más información sobre la obtención de credenciales, consulte [Preparación de la instalación de formularios AEM (un solo servidor)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

El almacén de confianza puede contener más de una credencial de extensiones de Acrobat Reader DC. Debe designar una de estas credenciales como la credencial predeterminada de Reader Extensions. La credencial predeterminada se utiliza cuando un usuario de Workbench no puede determinar qué credenciales usar durante la creación del proceso. Estas reglas se aplican a las credenciales predeterminadas:

* Si importa una credencial de extensiones de Acrobat Reader DC y el almacén de confianza no contiene otras credenciales de extensiones de Acrobat Reader DC, se establece como predeterminada.
* Si importa una credencial de extensiones de Acrobat Reader DC con la opción Predeterminado seleccionada, el tipo predeterminado se elimina de una credencial predeterminada existente. La credencial importada se convierte en el valor predeterminado.
* No puede eliminar una credencial de extensiones de Acrobat Reader DC predeterminada. Para eliminar la credencial predeterminada, defina primero otra credencial como predeterminada. Una excepción a esta regla es que si solo hay una credencial, puede eliminarla aunque sea la predeterminada.
* No se puede actualizar una credencial de extensiones de Acrobat Reader DC predeterminada.

>[!NOTE]
>
>También puede importar y eliminar credenciales mediante programación. (Consulte [Programación con formularios](https://www.adobe.com/go/learn_aemforms_programming_63)AEM).

## Importación de credenciales de extensiones de Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione Credenciales de extensiones de Acrobat Reader DC.
1. (Opcional) Para indicar que esta credencial es la credencial predeterminada que se utiliza con las extensiones de Acrobat Reader DC, seleccione Predeterminado.
1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar de las credenciales en las extensiones de Acrobat Reader DC. Este alias también se utiliza para acceder a las credenciales mediante programación mediante el SDK de formularios AEM.

   >[!NOTE]
   >
   >El nombre del alias se convierte automáticamente en mayúsculas para su visualización. El nombre del alias no distingue entre mayúsculas y minúsculas cuando se hace referencia a él en un proceso.

1. Haga clic en Elegir archivo para localizar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

   Si aparece el mensaje de error &quot;Error al importar credenciales debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

## Eliminación de credenciales de extensiones de Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Seleccione la credencial y haga clic en Eliminar.

## Reemplazar una credencial de extensiones de Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Tenga en cuenta el alias de la credencial existente, selecciónelo y haga clic en Eliminar.
1. Importe la nueva credencial utilizando exactamente el mismo nombre de alias.

