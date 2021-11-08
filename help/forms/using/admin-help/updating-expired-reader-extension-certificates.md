---
title: Actualización de certificados de servicio de extensión de Reader caducados
description: 'Reader documentos extendidos no funcionan, actualizar certificados '
source-git-commit: 5f2fc6a32f67cfed3bc4b09b63bcf9689659a99d
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 0%

---


# Actualización de certificados de servicio de extensión de Reader caducados {#Updating-expired-Reader-Extension-service-certificates}

Los clientes de Adobe Experience Manager Forms (AEM Forms) con licencias de Adobe Managed Services o On-Premise Enterprise Base tienen derecho a utilizar el servicio de extensión de Reader. El servicio permite a una organización compartir fácilmente documentos de PDF interactivos mediante la ampliación de la funcionalidad de Adobe Reader con derechos de uso adicionales. El servicio agrega derechos de uso a un documento de PDF y activa funciones que normalmente no están disponibles cuando se abre un documento de PDF con Adobe Acrobat Reader DC, como agregar comentarios a un documento, rellenar formularios y guardar el documento. Los usuarios de terceros no requieren software ni complementos adicionales para trabajar con documentos habilitados para derechos. Los documentos del PDF que tienen derechos de uso añadidos se denominan documentos con derechos activados. Un usuario que abre un documento PDF con derechos activados en Adobe Reader puede realizar las operaciones habilitadas para ese documento.

Adobe aprovecha una PKI (infraestructura de claves públicas) para emitir certificados digitales para su uso en licencias y habilitación de funciones. Adobe ha estado emitiendo certificados bajo la autoridad de certificación &quot;Adobe Root CA&quot;, está programado que caduque el 7 de enero de 2023. Esto llevará a la caducidad de todos los certificados emitidos bajo esta autoridad de certificación. Una vez caducado el certificado, todas las funciones que dependen de él ya no funcionan. Por ejemplo, un documento de PDF ampliado que permite agregar comentarios mediante Adobe Acrobat Reader deja de funcionar para los clientes a partir del 7 de enero de 2023. Para resolver el problema, el administrador del servicio Reader Extension, utilizando certificados antiguos, debe obtener y volver a aplicar los nuevos certificados emitidos por el nuevo Adobe Root CA G2 a sus documentos PDF (el lector debe extender los documentos PDF con nuevos certificados).

La caducidad de los certificados afecta tanto a AEM Forms en JEE como a AEM Forms en las pilas OSGi. Ambas pilas tienen un conjunto diferente de instrucciones. En función de la pila, elija una de las siguientes rutas:

* Actualización de certificados para una AEM Forms en un entorno JEE
* Actualización de certificados para una AEM Forms en un entorno OSGi

>[!NOTE]
>
>El documento utiliza certificados de términos y credenciales intercambiables.

## Requisitos previos {#Pre-requisites}

La actualización de los certificados requiere el uso de acciones disponibles en la consola del administrador de AEM Forms y en las API de extensión del Reader proporcionadas por AEM Forms. El documento está pensado para usuarios y administradores que conozcan el uso de las API de Forms de Adobe Experience Manager. Antes de comenzar, asegúrese de que:

* el usuario tiene derechos de administrador en el entorno de AEM Forms subyacente.
* el usuario ha configurado la variable [entorno de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) y tiene acceso a él.
* obtenga los certificados.

### Obtener los certificados {#obtain-the-certificates}

La credencial de derechos se entrega como certificado digital que contiene la clave pública, la clave privada y la contraseña utilizada para acceder a la credencial.

Si su organización compra una versión de producción de Extensiones de Reader, la credencial de derechos de producción la entrega el sitio web de licencias de Adobe (LWS). Una credencial de derechos de producción es única para su organización y puede habilitar los derechos de uso específicos que necesita.

Si obtuvo Extensiones de Reader a través de un socio o proveedor de software que integró Extensiones de Reader en su software, la credencial de Derechos la proporciona ese socio que, a su vez, recibe esta credencial de Adobe.

>[!NOTE]
>
>La credencial de derechos no se puede usar para la firma o afirmación de identidad de documentos típicos. Para estas aplicaciones, puede utilizar un certificado de autofirma o adquirir un certificado de identidad de una entidad emisora de certificados (CA).

Están disponibles los siguientes tipos de credenciales de derechos:

**Evaluación de clientes**: Credencial con un breve periodo de validez que se proporciona a los clientes que desean evaluar las extensiones de Reader. Los derechos de uso aplicados a documentos que utilizan esta credencial caducan cuando caduca la credencial. Este tipo de credenciales solo es válido durante dos o tres meses.

**Producción**: Una credencial con un periodo de validez prolongado que se proporciona a los clientes que compraron el producto completo. Las credenciales de producción son únicas para cada cliente, pero se pueden instalar en varios sistemas.

Si ya ha utilizado certificados para ampliar archivos de PDF del lector, descargue un certificado de producción de [Sitio web de licencias de Adobe (LWS)](https://licensing.adobe.com/).

## Actualización y aplicación de certificados para una AEM Forms en un entorno JEE {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

La actualización y aplicación de nuevos certificados en AEM Forms en la pila JEE requiere la importación de nuevas credenciales, la eliminación de los derechos de uso de documentos de PDF existentes y la aplicación de derechos de uso. Puede usar Admin Console para importar credenciales y API de extensión de Reader de AEM Forms para eliminar y aplicar derechos de uso.

### Importar y configurar credenciales

Puede utilizar las páginas Administración de almacén de confianza para importar una credencial nueva o de reemplazo. El almacén de confianza puede contener más de una credencial de extensiones de Reader. Debe designar una de esas credenciales como credencial predeterminada de Extensiones de Reader. La credencial predeterminada se utiliza cuando un usuario de Workbench no puede determinar qué credencial utilizar durante la creación del proceso. Estas reglas se aplican a las credenciales predeterminadas:

* Si importa una credencial de Extensiones de Reader y el almacén de confianza no contiene otras credenciales de Extensiones de Reader, se establece como predeterminado.
* Si importa una credencial de Extensiones de Reader con la opción Predeterminado seleccionada, se eliminará el tipo predeterminado de una credencial predeterminada existente. La credencial importada se convierte en el valor predeterminado.
* No puede eliminar una credencial predeterminada de Extensiones de Reader. Para eliminar la credencial predeterminada, establezca primero otra credencial como la predeterminada. Una excepción a esta regla es que si solo hay una credencial, puede eliminarla aunque sea la predeterminada.
* No se puede actualizar una credencial de Extensiones de Reader predeterminada.

Para importar las credenciales:

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione Credencial de extensiones de Acrobat Reader DC.
1. (Opcional) Para indicar que esta credencial es la credencial predeterminada que se utiliza con las extensiones de Acrobat Reader DC, seleccione Predeterminado.
1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar para las credenciales de las extensiones de Acrobat Reader DC. Este alias también se utiliza para acceder a las credenciales mediante programación mediante el SDK de AEM forms.
1. Haga clic en Elegir archivo para localizar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

Si aparece el mensaje de error &quot;No se pudo importar la credencial debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

También puede importar y eliminar credenciales mediante programación. (Consulte [Programación con formularios AEM](../../developing/credentials.md).)

### Eliminación de los derechos de uso de documentos PDF con derechos activados

Elimine los derechos de uso de los documentos de PDF habilitados para derechos existentes antes de aplicar los derechos de uso con las credenciales más recientes. AEM Forms en JEE proporciona API para eliminar los derechos de uso. Para obtener instrucciones detalladas, consulte [Eliminación de derechos de uso de documentos de PDF](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

Para eliminar los derechos de uso de AEM Forms en procesos JEE desarrollados en Workbench, consulte [Ayuda de Workbench](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### Aplicación de los derechos de uso a los documentos del PDF

Después de importar nuevas credenciales y eliminar los derechos de uso de documentos de PDF habilitados para derechos existentes, aplique derechos de uso a documentos de PDF mediante las nuevas credenciales. Puede aplicar derechos de uso a documentos de PDF mediante la API de cliente Java y el servicio web de Acrobat Reader DC Extensions.  Para obtener más información, consulte [Aplicación de derechos de uso a documentos de PDF](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## Actualización y aplicación de certificados para una AEM Forms en un entorno OSGi {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

La actualización y aplicación de nuevos certificados en AEM Forms en la pila OSGi requiere la importación de nuevas credenciales, la eliminación de los derechos de uso de documentos de PDF existentes y la aplicación de derechos de uso. Puede usar Admin Console para importar credenciales y API de extensión de Reader de AEM Forms para eliminar y aplicar derechos de uso.

### Importar credenciales {#Import-credentials}

En un AEM Forms en un entorno OSGi, una credencial de extensión de Reader está asociada al usuario del servicio fd. Antes de agregar credenciales para el almacén de claves fd-user, realice los siguientes pasos para crear un almacén de claves:

1. Inicie sesión en la instancia de AEM Author como administrador.
1. Vaya a Herramientas > Seguridad > Usuarios.
1. Desplácese hacia abajo por la lista de usuarios hasta que encuentre la cuenta de usuario del servicio de disponibilidad.
1. Haga clic en el usuario del fd-servicio.
1. Haga clic en la ficha almacén de claves.
1. Haga clic en Crear KeyStore.
1. Establezca la contraseña de acceso de KeyStore y guarde la configuración para crear la contraseña de KeyStore.

Después de crear el almacén de claves, agregue credenciales al usuario del servicio de fd.

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

El siguiente comando enumera los detalles del archivo pfx. Antes de ejecutar el comando, vaya al directorio que contiene el archivo .pfx.

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

Por ejemplo keytool -v -list -storetype pkcs12 -keystore 1005566.pfx donde 1005566.pfx es el nombre de mi archivo pfx

### Eliminación de los derechos de uso de documentos PDF con derechos activados

Elimine los derechos de uso de los documentos de PDF habilitados para derechos existentes antes de aplicar los derechos de uso con las credenciales más recientes. Puede eliminar los derechos de uso de un documento invocando la API removeUsageRights desde docAssuranceServiceAPI. Para obtener información detallada, consulte [Eliminar derechos de uso](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) documento.

### Aplicación de los derechos de uso a los documentos del PDF

Para aplicar derechos de uso en un AEM Forms en un entorno OSGi, cree un servicio OSGi personalizado a los derechos de uso de los documentos. También puede crear un servlet con un método de POST para devolver al usuario el PDF ampliado del lector. Para obtener instrucciones detalladas, consulte [Aplicación de extensiones de Reader](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## Preguntas frecuentes

**¿Con quién debo ponerme en contacto si tengo más preguntas?**

Puede ponerse en contacto con [Compatibilidad con Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) o levante un ticket de soporte.

**¿Qué sucede si no actualizo mi certificado antes del 7 de enero de 2023?**

Al intentar abrir un PDF de documentos Reader ampliado con certificados antiguos, los usuarios experimentan un mensaje de error y ya no pueden acceder a las funciones ampliadas por el lector. Un error de ejemplo es .

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**¿Hay algún cambio en el nombre de la nueva descripción?**

Los nuevos certificados de extensión de Reader mencionan G3-P24 como nombre de programa en la descripción. En los certificados anteriores, en la descripción se mencionó el nombre del programa P24.