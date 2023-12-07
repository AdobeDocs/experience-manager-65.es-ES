---
title: Administrar certificados
description: Obtenga información sobre cómo importar y exportar un certificado y editar su configuración de confianza.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 8%

---

# Administrar certificados {#managing-certificates}

Con la administración de almacén de confianza, puede importar, editar y eliminar certificados en los que confía en el servidor para validar firmas digitales y autenticación de certificados. Puede importar y exportar cualquier número de certificados. Una vez importado un certificado, puede editar la configuración de confianza y el tipo de almacén de confianza. Tenga en cuenta las siguientes opciones al combinar tipos de almacén de confianza:

* **Confianza para autenticación de certificado con CA:** Para validar CRL, seleccione también Confiar en la identidad.
* **Confianza para la autenticación de certificados con ICA:** Seleccione sólo Confiar en la identidad. No se debe confiar en ICA para la autenticación mediante certificado. Si confía en el ICA para la autenticación de certificados, el ICA se convierte en una CA para la generación de rutas. Si el ICA es de confianza tanto para la autenticación como para la identidad del certificado, se omite el certificado del proveedor de CA porque el ICA se convierte en la CA.
* **Confianza del servidor OCSP con HTTP:** Si el servidor encuestado OSCP reside en una ubicación HTTP, también debe seleccionar Confiar en conexiones SSL. Si el encuestado de OSCP requiere validación de CRL, asegúrese de seleccionar también Confiar en la identidad.
* **Raíz de Adobe:** No seleccione Conexiones SSL ni Tipos de almacén de confianza del servidor OCSP. La raíz de Adobe no es de confianza para Conexiones SSL y Servidor OCSP. El Adobe no emite certificados OCSP y SSL. La raíz de Adobe es de confianza implícita con un alias name=&quot;ADOBEROOT&quot;.

Solo se admiten certificados X509v3. Este tipo de certificado se puede proporcionar en un archivo binario con codificación DER (archivo .cer) o en un archivo de texto que contenga una versión codificada en Base64 del mismo certificado con codificación DER (incluidos los certificados X509 en formato de correo mejorado de privacidad (PEM)).

Los certificados necesarios para completar una verificación de firma deben estar en el mismo almacén (HSM o base de datos).

También puede importar y eliminar certificados mediante la API de Administrador de confianza. Para obtener más información, consulte &quot;Importación de certificados mediante la API de Trust Manager&quot; y &quot;Eliminación de certificados mediante la API de Trust Manager&quot; en [AEM Programar con formularios de](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importar un certificado {#import-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de almacén de confianza > Certificados]**.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione una de estas opciones:

   * **Confianza para conexiones SSL:** AEM Especifica que los formularios pueden utilizar certificados para conectarse a sistemas externos mediante SSL.
   * **Confiar en la firma del certificado:** Especifica que los certificados son de confianza en las operaciones de firma de documentos para certificar firmas digitales de autor.
   * **Confiar en la firma:** Especifica que los certificados son de confianza en las operaciones de firma de documentos para firmas digitales que no son de autor.
   * **Confianza para autenticación de certificado:** AEM Especifica los formularios que utilizan certificados para autenticar a los usuarios mediante la autenticación mediante certificado o tarjeta inteligente.
   * **Confianza para el servidor OCSP:** AEM Especifica que los formularios de la pueden utilizar certificados para conectarse a los respondedores de OCSP externos
   * **Confianza para identidad:** Especifica que los certificados se pueden usar para confiar en información distinta de los tipos especificados anteriormente.

   >[!NOTE]
   >
   >El almacén de confianza confía implícitamente en un certificado raíz de Adobe para la autenticación de certificados, la firma, la firma de certificado y la identidad.

1. En el cuadro Alias, escriba el identificador del certificado.
1. Clic **[!UICONTROL Examinar]** para localizar el certificado y haga clic en **[!UICONTROL OK]**.

## Exportar un certificado {#export-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de almacén de confianza > Certificados]**.
1. Haga clic en el nombre del alias del certificado que desea exportar. El **[!UICONTROL Detalles del certificado]** se muestra la página.
1. Clic **[!UICONTROL Exportar]**, siga las instrucciones para exportar el certificado y haga clic en **[!UICONTROL OK]**.

## Editar la configuración de confianza y el tipo de almacén de confianza de un certificado {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de almacén de confianza > Certificados]**.
1. Haga clic en el nombre de alias del certificado que desea editar.
1. Clic **[!UICONTROL Actualizar certificado]**.
1. Para cambiar el Nombre de alias del certificado, escriba un nombre nuevo en el cuadro Alias.
1. Para actualizar el tipo de almacén de confianza para el certificado, seleccione el tipo de almacén de confianza adecuado.
1. Para actualizar las restricciones de directiva, en el cuadro Directivas de certificado, escriba la información de directiva y haga clic en **[!UICONTROL OK]**.

## Eliminar un certificado {#delete-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de almacén de confianza > Certificados]**.
1. Seleccione las casillas de verificación de los certificados que desea eliminar y haga clic en **[!UICONTROL Eliminar]** y haga clic en **[!UICONTROL OK]**.
