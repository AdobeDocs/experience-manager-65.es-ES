---
title: Configurar credenciales para usarlas con extensiones de Acrobat Reader DC
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
ht-degree: 5%

---

# Configurar credenciales para usarlas con extensiones de Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Para aplicar derechos de uso a documentos de PDF AEM, configure formularios de con una credencial válida para extensiones de Acrobat Reader DC. AEM Es posible que se haya configurado una credencial durante la instalación de los formularios de. Si no configuró las credenciales de las extensiones de Acrobat Reader DC mientras ejecutaba el Administrador de configuración o si necesita importar una credencial nueva o de reemplazo, puede hacerlo mediante las páginas Administración de almacén de confianza.

Si utiliza una credencial de evaluación, reemplácela por una credencial de producción al pasar al entorno de producción. Para actualizar una credencial caducada o de evaluaciones, primero elimine la credencial antigua de extensiones de Acrobat Reader DC.

Para obtener información sobre cómo obtener una credencial, consulte [AEM Preparación para la instalación de formularios (un solo servidor)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_es).

El almacén de confianza puede contener más de una credencial de extensiones de Acrobat Reader DC. Debe designar una de esas credenciales como la credencial predeterminada de Extensiones de Reader. La credencial predeterminada se utiliza cuando un usuario de Workbench no puede determinar qué credencial utilizar durante la creación del proceso. Estas reglas se aplican a las credenciales predeterminadas:

* Si importa una credencial de extensiones de Acrobat Reader DC y el Almacén de confianza no contiene otras credenciales de extensiones de Acrobat Reader DC, se establece como predeterminada.
* Si importa una credencial de extensiones de Acrobat Reader DC con la opción Predeterminado seleccionada, el tipo predeterminado se elimina de una credencial predeterminada existente. La credencial importada se convierte en la predeterminada.
* No puede eliminar una credencial de extensiones de Acrobat Reader DC predeterminada. Para eliminar la credencial predeterminada, primero establezca otra credencial como predeterminada. Una excepción a esta regla es que si solo hay una credencial, puede eliminarla aunque sea la predeterminada.
* No puede actualizar una credencial de extensiones de Acrobat Reader DC predeterminada.

>[!NOTE]
>
>También puede importar y eliminar credenciales mediante programación. (Consulte [AEM Programar con formularios de](https://www.adobe.com/go/learn_aemforms_programming_63).)

## Importar una credencial de extensiones de Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione Credenciales de extensiones de Acrobat Reader DC.
1. (Opcional) Para indicar que esta credencial es la credencial predeterminada que se utiliza con las extensiones de Acrobat Reader DC, seleccione Predeterminada.
1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar de las credenciales en las extensiones de Acrobat Reader DC. AEM Este alias también se utiliza para acceder a las credenciales mediante programación a través del SDK de formularios de la aplicación de la plataforma de datos de.

   >[!NOTE]
   >
   >El nombre del alias se convierte automáticamente a mayúsculas para su visualización. El nombre del alias no distingue entre mayúsculas y minúsculas cuando se hace referencia a él en un proceso.

1. Haga clic en Elegir archivo para buscar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

   Si aparece el mensaje de error &quot;No se pudieron importar las credenciales debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

## Eliminar una credencial de extensiones de Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Seleccione la credencial y haga clic en Eliminar.

## Reemplazar una credencial de extensiones de Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Tome nota del alias de la credencial existente, selecciónela y haga clic en Eliminar.
1. Importe la nueva credencial con el mismo nombre de alias.
