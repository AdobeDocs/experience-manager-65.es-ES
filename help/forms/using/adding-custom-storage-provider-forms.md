---
title: Almacenamiento personalizado para borradores y componentes de envíos
seo-title: Almacenamiento personalizado para borradores y componentes de envíos
description: Consulte cómo personalizar el almacenamiento de datos de usuario para borradores y envíos.
seo-description: Consulte cómo personalizar el almacenamiento de datos de usuario para borradores y envíos.
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Almacenamiento personalizado para borradores y componentes de envíos {#custom-storage-for-drafts-and-submissions-component}

## Información general {#overview}

AEM Forms permite guardar un formulario como borrador. La funcionalidad de borrador le permite mantener un formulario de trabajo en curso, que puede completar y enviar posteriormente desde cualquier dispositivo.

De forma predeterminada, AEM Forms almacena los datos de usuario asociados con el borrador y el envío de un formulario en el `/content/forms/fp` nodo de la instancia de Publish. Además, los componentes del portal de AEM Forms proporcionan servicios de datos, que puede utilizar para personalizar la implementación del almacenamiento de datos de usuario para borradores y envíos. Por ejemplo, puede almacenar datos de usuario en un almacén de datos.

## Requisitos previos  {#prerequisites}

* Habilitar componentes [del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* Creación de una página de portal de [formularios](/help/forms/using/creating-form-portal-page.md)
* Habilitar formularios [adaptables para el portal de formularios](/help/forms/using/draft-submission-component.md)
* Conozca los detalles [de implementación del almacenamiento personalizado](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Servicio de borradores de datos {#draft-data-service}

Para personalizar el almacenamiento de datos de usuario para borradores, debe implementar todos los métodos de la `DraftDataService` interfaz. El siguiente código de muestra describe los métodos y argumentos.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

## Servicio de envío de datos {#submission-data-service}

Para personalizar el almacenamiento de datos de usuario para envíos, debe implementar todos los métodos de la `SubmitDataService` interfaz. El siguiente código de muestra describe los métodos y argumentos.

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

Forms Portal utiliza el concepto de identificador único universal (UUID) para generar un ID único para cada borrador y formulario enviado. También puede generar una ID única propia. Puede implementar la interfaz FPKeyGeneratorService, anular sus métodos y desarrollar una lógica personalizada para generar una ID única personalizada para cada borrador y formulario enviado. Además, establezca la clasificación de servicio de la implementación de generación de ID personalizada más alta que 0. Garantiza que se utilice la implementación personalizada en lugar de la implementación predeterminada.

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

Puede utilizar la anotación siguiente para aumentar la clasificación del servicio para el ID personalizado generado con el código anterior:

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

Para utilizar la anotación anterior, importa lo siguiente a su proyecto:

```
import org.apache.felix.scr.annotations.Properties;
 import org.apache.felix.scr.annotations.Property;
```

