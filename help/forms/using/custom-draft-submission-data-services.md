---
title: Personalizar los servicios de datos Borradores y envíos
seo-title: Customizing Draft and Submission data services
description: AEM Forms, de forma predeterminada, almacena los borradores de formularios adaptables y los formularios enviados en un nodo predeterminado en la instancia de publicación. Sin embargo, puede configurar los servicios de datos de borrador y envío de AEM Forms para personalizar el almacenamiento de formularios adaptables en Borradores y Enviados.
seo-description: AEM Forms, by default, stores draft and submitted adaptive forms in a default node on the Publish instance. However, you can configure the draft and submission data services of AEM Forms to customize the storage of draft and submitted adaptive forms.
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 100%

---

# Personalizar los servicios de datos Borradores y envíos {#customizing-draft-and-submission-data-services}

## Información general {#overview}

AEM Forms permite a los usuarios guardar un formulario adaptable como borrador. La funcionalidad Borrador proporciona a los usuarios la opción de mantener un formulario de trabajo en curso. Un usuario puede completar y enviar el formulario en cualquier momento desde cualquier dispositivo.

De forma predeterminada, AEM Forms almacena los datos de usuario asociados con el borrador y el envío en la instancia de publicación en el nodo `/content/forms/fp`.

Sin embargo, los componentes del portal de AEM Forms proporcionan servicios de datos que le permiten personalizar la implementación del almacenamiento de datos de usuario para borradores y envíos. Por ejemplo, puede almacenar los datos en un repositorio de datos implementado en su organización actualmente.

Para personalizar el almacenamiento de los datos de usuario, debe implementar los servicios [Borrador de datos](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) y [Datos de envío](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p).

## Requisitos previos {#prerequisites}

* Habilitar [componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* Crear una [página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* Habilitar [formularios adaptables para el portal de formularios](/help/forms/using/draft-submission-component.md)
* Más información sobre los [detalles de implementación del almacenamiento personalizado](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Servicio Datos de borrador {#draft-data-service}

Para personalizar el almacenamiento de los datos de borrador del usuario, debe proporcionar implementación para todos los métodos de la `DraftAFDataService` interfaz.

En el siguiente ejemplo de código de la interfaz se proporciona una descripción de los métodos y sus argumentos:

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## Servicio Envío de datos {#submission-data-service}

Para personalizar el almacenamiento de los datos de envío de los usuarios, debe proporcionar implementación para todos los métodos de la `SubmittedAFDataService` interfaz.

En el siguiente ejemplo de código de la interfaz se proporciona una descripción de los métodos y sus argumentos:

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```
