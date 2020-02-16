---
title: Crear formularios de Adobe Campaign en AEM
seo-title: Crear formularios de Adobe Campaign en AEM
description: AEM permite crear y utilizar formularios que interactúan con Adobe Campaign en el sitio web. Hay campos específicos que se pueden insertar en los formularios y asignar a la base de datos de Adobe Campaign.
seo-description: AEM permite crear y utilizar formularios que interactúan con Adobe Campaign en el sitio web. Hay campos específicos que se pueden insertar en los formularios y asignar a la base de datos de Adobe Campaign.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Crear formularios de Adobe Campaign en AEM{#creating-adobe-campaign-forms-in-aem}

AEM permite crear y utilizar formularios que interactúan con Adobe Campaign en el sitio web. Hay campos específicos que se pueden insertar en los formularios y asignar a la base de datos de Adobe Campaign.

Puede administrar nuevas suscripciones de contacto, cancelaciones de suscripciones y datos de perfiles de usuarios, a la vez que integra todos esos datos en la base de datos de Adobe Campaign.

Para utilizar los formularios de Adobe Campaign en AEM, tiene que seguir estos pasos que se describen en este documento:

1. Consiga que una plantilla esté disponible.
1. Cree un formulario.
1. Edite el contenido del formulario.

De forma predeterminada, existen tres tipos de formularios disponibles específicos de Adobe Campaign:

* Guardar un perfil
* Suscribirse a un servicio
* Cancelar la suscripción a un servicio

Estos formularios definen un parámetro de URL que acepte la clave principal cifrada de un perfil de Adobe Campaign. Según este parámetro de URL, el formulario actualiza los datos del perfil de Adobe Campaign asociado.

Aunque cree estos formularios de forma independiente, al usarlos se genera un vínculo personalizado a una página de formularios dentro del contenido del boletín, de modo que los destinatarios puedan abrir el vínculo y realizar los ajustes necesarios en los datos del perfil (para cancelar la suscripción, suscribirse o actualizar el perfil).

El formulario se actualiza automáticamente en función del usuario. Consulte [Editar el contenido de los formularios](#editing-form-content) para obtener más información.

## Hacer que una plantilla esté disponible {#making-a-template-available}

Antes de poder crear formularios específicos de Adobe Campaign, debe realizar las plantillas diferentes que hay en su aplicación de AEM.

To do this, see the [Templates documentation](/help/sites-developing/page-templates-static.md#templateavailability).

En primer lugar, compruebe la conexión entre el autor y las instancias de publicación y que Adobe Campaign funciona correctamente. Consulte [Integrar con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrar con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Asegúrese de que la propiedad **acMapping** en el nodo **jcr:content** de la página está establecida en **mapRecipient** o en **profile** al usar Adobe Campaign 6.1.x o Adobe Campaign Standard, respectivamente.


### Crear un formulario {#creating-a-form}

1. Empiece en siteadmin.
1. Desplácese por la estructura de árbol hasta llegar al lugar donde desea crear el formulario en la página web seleccionada.
1. **Seleccione** Nuevo **>** Nueva página... .
1. Select either **Adobe Campaign Profile (AC 6.1)** or **Adobe Campaign Profile (ACS)** template and enter the page properties.

   >[!NOTE]
   >
   >If the template is not available, refer to the [Making a template available](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) section.

1. Click **Create** to create the form.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   A continuación podrá [editar y configurar el contenido del formulario](#editing-form-content).

## Editar el contenido del formulario {#editing-form-content}

Los dedicados a Adobe Campaign tienen componentes específicos. Estos componentes tienen una opción para permitir que se vincule cada campo del formulario a un campo de la base de datos de Adobe Campaign.

>[!NOTE]
>
>If the desired template is not available, see [Making a template available](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

En esta sección se detallan únicamente los vínculos específicos de Adobe Campaign. For more information on a more general overview of how to use forms in Adobe Experience Manager, see [Editmode components](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Desplácese hasta el formulario que quiera editar.
1. **En el cuadro de herramientas, seleccione** Página **> Propiedades** de la página... a continuación, vaya a la ficha Servicios **de** nube de la ventana emergente.
1. Add the Adobe Campaign service by clicking **Add service**, and then selecting the configuration that corresponds to your Adobe Campaign instance in the service&#39;s drop down list. Se realiza esta configuración al configurar la conexión entre instancias. For more information, see [Connecting AEM to Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Si es necesario, desbloquee la configuración haciendo clic en el icono del candado para poder añadir el servicio de Adobe Campaign.

1. Access the form&#39;s general parameters using the **Edit** button found at the start of the form. The **Form** tab allows you to select a thank you page to which the user will be redirected after having validated the form.

   The **Advanced** form allows you to select the type of form. The **Post Options** field gives you the choice between three types of Adobe Campaign forms:

   * **Adobe Campaign: Guardar perfil**: permite crear o actualizar un destinatario en Adobe Campaign (valor predeterminado).
   * **Adobe Campaign: Suscribirse a servicios**: permite gestionar las suscripciones de un destinatario en Adobe Campaign.
   * **Adobe Campaign: Cancelar suscripción a los servicios**: permite cancelar las suscripciones de un destinatario en Adobe Campaign.
   The **Action Configuration** field lets you specify whether or not you would like to create the recipient profile in the Adobe Campaign database if it does not yet exist. To do this, check the **Create user if not existing** option.

1. Añada los componentes seleccionados; para ello, arrástrelos del cuadro de herramientas y situándolos en el formulario. Para obtener más información sobre los componentes específicos que están disponibles en Adobe Campaign, consulte [Componentes de formulario de Adobe](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configure los campos añadidos al hacer doble clic en ellos. The **Adobe Campaign** tab lets you link the field to a field in the Adobe Campaign recipient table. También puede especificar si el campo forma parte de la clave de reconciliación, la cual permite reconocer a los destinatarios que ya se encuentran en la base de datos de Adobe Campaign.

   >[!CAUTION]
   >
   >The **Element Name** must be different for each form field. Cambiar si es necesario.
   >
   >Each form must contain an **Encrypted Primary Key** component in order to correctly manage recipients in the Adobe Campaign database.

1. Activate the page by selecting **Page** > **Activate Page** in the toolbox. La página se activa en el sitio. Puede verlo en la instancia de publicación de AEM. Los datos de la base de datos de Adobe Campaign se actualizan una vez que se valide un formulario.

## Probar un formulario {#testing-a-form}

Después de crear un formulario y editar el contenido, es posible que desee probar de forma manual que el formulario funciona correctamente.

>[!NOTE]
>
>You must have an **Encryted Primary Key** component on each form. En Componentes, seleccione Adobe Campaign para que solo esos componentes estén visibles.
>
>Aunque en este procedimiento escriba el número de EPK manualmente, en la práctica, los usuarios recibirán un vínculo a la página (para cancelar la suscripción, suscribirse o actualizar el perfil) en un boletín. De acuerdo con el usuario, la EPK se actualiza automáticamente.
>
>To create that link, you use the variable **Main resource identifier**(Adobe Campaign Standard) or **Encrypted identifier** (Adobe Campaign 6.1) (for example, in a **Text &amp; Personalization (Campaign)** component), which links to the epk in Adobe Campaign.

Para hacer esto, debe obtener manualmente la EPK de un perfil de Adobe Campaign y añadirlo a la dirección URL:

1. Para obtener la clave principal de cifrado (EPK) de un perfil de Adobe Campaign:

   * In Adobe Campaign Standard - Navigate to **Profiles and Audiences** > **Profiles**, which lists the existing profiles. Make sure the table displays the **Main Resource Identifier** field in a column (This can be configured by clicking/tapping **Configure list**). Copie el identificador del recurso principal del perfil deseado.
   * In Adobe Campaign 6.11, go to **Profiles and Targets** >  **Recipients**, which lists the existing profiles. Make sure the table displays the **Encrypted identifier** field in a column (This can be configured by right-clicking on an entry and selecting **Configure list...**). Copie el identificador cifrado del perfil deseado.

1. In AEM, open the form page on the publish instance and append the EPK from step 1 as a URL parameter: use the same name that you previously defined in the EPK component when authoring the form (for example: `?epk=...`)
1. El formulario se puede utilizar para modificar los datos y las suscripciones asociados al perfil vinculado de Adobe Campaign. Después de modificar algunos campos y enviar el formulario, podrá comprobar en Adobe Campaign que se actualizaron los datos adecuados.

Los datos de la base de datos de Adobe Campaign se actualizan una vez que se valide un formulario.
