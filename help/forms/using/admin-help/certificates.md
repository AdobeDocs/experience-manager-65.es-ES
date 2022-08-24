---
title: Administración de certificados
seo-title: Managing certificates
description: Obtenga información sobre cómo importar y exportar un certificado y editar su configuración de confianza.
seo-description: Learn how to import and export a certificate and edit its trust settings.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Administración de certificados {#managing-certificates}

Con la Administración de almacén de confianza, puede importar, editar y eliminar certificados en los que confía en el servidor para validar firmas digitales y autenticación de certificados. Puede importar y exportar cualquier número de certificados. Una vez importado un certificado, puede editar la configuración de confianza y el tipo de almacén de confianza. Tenga en cuenta las siguientes opciones al combinar tipos de almacén de confianza:

* **Confianza para la autenticación de certificados con CA:** Para la validación de CRL, seleccione también Confiar en la identidad.
* **Confianza para la autenticación de certificados con ICA:** Seleccione solo Confiar en la identidad. No se debe confiar en un ICA para la autenticación de certificado. Si confía en el ICA para la autenticación de certificados, el ICA se convierte en una CA para la construcción de rutas. Si el ICA es de confianza tanto para la autenticación de certificado como para la identidad, el certificado de proveedor de CA se ignora porque el ICA se convierte en la CA.
* **Confianza para el servidor OCSP con HTTP:** Si el servidor encuestado OSCP reside en una ubicación HTTP, también debe seleccionar Confiar en las Conexiones SSL. Si el encuestado OSCP requiere la validación de CRL, asegúrese de seleccionar también Confiar en la identidad.
* **Raíz de Adobe:** No seleccione Conexiones SSL ni Tipos de almacén de confianza del servidor OCSP. La raíz de Adobe no es de confianza para conexiones SSL y el servidor OCSP. Adobe no emite certificados OCSP y SSL. La raíz de Adobe es de confianza implícita en un alias name=&quot;ADOBEROOT&quot;.

Solo se admiten certificados X509v3. Este tipo de certificado se puede proporcionar en un archivo binario con codificación DER (archivo .cer) o en un archivo de texto que contenga una versión con codificación Base64 del mismo certificado con codificación DER (incluidos los certificados X509 en formato Privacy Enhanced Mail (PEM)).

Los certificados necesarios para completar una verificación de firma deben estar en el mismo almacén (HSM o base de datos).

También puede importar y eliminar certificados mediante la API del administrador de confianza. Para obtener más información, consulte &quot;Importación de certificados mediante la API de Trust Manager&quot; y &quot;Eliminación de certificados mediante la API de Trust Manager&quot; en [Programación con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importar un certificado {#import-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración del almacén de confianza > Certificados]**.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione una de estas opciones:

   * **Confianza para conexiones SSL:** Especifica que AEM formularios pueden utilizar certificados para conectarse a sistemas externos a través de SSL.
   * **Confianza para certificar firma:** Especifica que los certificados son de confianza en las operaciones de firma de documentos para certificar firmas digitales de autor.
   * **Confianza en la firma:** Especifica que los certificados son de confianza en las operaciones de firma de documentos para firmas digitales que no sean de autor.
   * **Confianza para la autenticación de certificados:** Especifica AEM los formularios utilizan certificados para autenticar usuarios mediante autenticación de certificado o tarjeta inteligente.
   * **Confianza para el servidor OCSP:** Especifica que AEM formularios pueden utilizar certificados para conectarse a respondedores OCSP externos
   * **Confianza en la identidad:** Especifica que los certificados se pueden utilizar para confiar en información que no sea de los tipos especificados anteriormente.

   >[!NOTE]
   >
   >El almacén de confianza confía implícitamente en un certificado raíz de Adobe para la autenticación, la firma, la firma de certificado y la identidad.

1. En el cuadro Alias, escriba el identificador del certificado.
1. Haga clic en **[!UICONTROL Examinar]** para localizar el certificado y, a continuación, haga clic en **[!UICONTROL OK]**.

## Exportar un certificado {#export-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración del almacén de confianza > Certificados]**.
1. Haga clic en el nombre de alias del certificado que desea exportar. La variable **[!UICONTROL Detalles del certificado]** se muestra.
1. Haga clic en **[!UICONTROL Exportar]**, siga las instrucciones para exportar el certificado y, a continuación, haga clic en **[!UICONTROL OK]**.

## Editar la configuración de confianza de un certificado y el tipo de almacén de confianza {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración del almacén de confianza > Certificados]**.
1. Haga clic en el nombre del alias del certificado que desea editar.
1. Haga clic en **[!UICONTROL Actualizar certificado]**.
1. Para cambiar el nombre de alias del certificado, escriba un nuevo nombre en el cuadro Alias.
1. Para actualizar el tipo de almacén de confianza para el certificado, seleccione el tipo de almacén de confianza correspondiente.
1. Para actualizar las restricciones de directiva, en el cuadro Directivas de certificado, escriba la información de directiva y haga clic en **[!UICONTROL OK]**.

## Eliminar un certificado {#delete-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración del almacén de confianza > Certificados]**.
1. Seleccione las casillas de verificación de los certificados que desea eliminar y haga clic en **[!UICONTROL Eliminar]** y, a continuación, haga clic en **[!UICONTROL OK]**.
