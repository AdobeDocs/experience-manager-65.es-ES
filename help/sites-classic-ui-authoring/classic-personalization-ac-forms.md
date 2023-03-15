---
title: Crear formularios de Adobe Campaign en AEM
seo-title: Creating Adobe Campaign Forms in AEM
description: AEM permite crear y utilizar formularios que interactúan con Adobe Campaign en el sitio web. Hay campos específicos que se pueden insertar en los formularios y asignar a la base de datos de Adobe Campaign.
seo-description: AEM lets you create and use forms that interact with Adobe Campaign on your website. Specific fields can be inserted into your forms and mapped to the Adobe Campaign database.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 62%

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

Para ello, consulte las [Documentación de plantillas](/help/sites-developing/page-templates-static.md#templateavailability).

En primer lugar, compruebe la conexión entre el autor y las instancias de publicación y que Adobe Campaign funciona correctamente. Consulte [Integrar con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrar con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Asegúrese de que la propiedad **acMapping** en el nodo **jcr:content** de la página está establecida en **mapRecipient** o en **profile** al usar Adobe Campaign 6.1.x o Adobe Campaign Standard, respectivamente.

### Crear un formulario {#creating-a-form}

1. Empiece en siteadmin.
1. Desplácese por la estructura de árbol hasta llegar al lugar donde desea crear el formulario en la página web seleccionada.
1. Seleccionar **Nuevo** > **Nueva página...**.
1. Seleccione una de las opciones **Perfil de Adobe Campaign (AC 6.1)** o **Perfil de Adobe Campaign (ACS)** y escriba las propiedades de la página.

   >[!NOTE]
   >
   >Si la plantilla no está disponible, consulte la [Disponibilidad de una plantilla](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) sección.

1. Clic **Crear** para crear el formulario.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   A continuación podrá [editar y configurar el contenido del formulario](#editing-form-content).

## Editar el contenido del formulario {#editing-form-content}

Los dedicados a Adobe Campaign tienen componentes específicos. Estos componentes tienen una opción para permitir que se vincule cada campo del formulario a un campo de la base de datos de Adobe Campaign.

>[!NOTE]
>
>Si la plantilla deseada no está disponible, consulte [Disponibilidad de una plantilla](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

En esta sección se detallan únicamente los vínculos específicos de Adobe Campaign. Para obtener más información sobre una descripción general más general del uso de los formularios en Adobe Experience Manager, consulte [Componentes del modo de edición](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Desplácese hasta el formulario que quiera editar.
1. En el cuadro de herramientas, seleccione **Página** > **Propiedades de página...** a continuación, vaya a **Cloud Services** de la ventana emergente.
1. Agregue el servicio Adobe Campaign haciendo clic en **Añadir servicio** y, a continuación, en la lista desplegable del servicio, seleccione la configuración que corresponda a la instancia de Adobe Campaign. Se realiza esta configuración al configurar la conexión entre instancias. Para obtener más información, consulte [AEM Conexión de la a Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Si es necesario, desbloquee la configuración haciendo clic en el icono del candado para poder añadir el servicio de Adobe Campaign.

1. Acceda a los parámetros generales del formulario con la variable **Editar** se encuentra al principio del formulario. El **Form** le permite seleccionar una página de agradecimiento a la que se redirigirá al usuario después de validar el formulario.

   El **Avanzadas** permite seleccionar el tipo de formulario. El **Opciones de publicación** Este campo permite elegir entre tres tipos de formularios Adobe Campaign:

   * **Adobe Campaign: Guardar perfil**: permite crear o actualizar un destinatario en Adobe Campaign (valor predeterminado).
   * **Adobe Campaign: Suscribirse a servicios**: permite gestionar las suscripciones de un destinatario en Adobe Campaign.
   * **Adobe Campaign: Cancelar suscripción a los servicios**: permite cancelar las suscripciones de un destinatario en Adobe Campaign.

   El **Configuración de acción** Este campo permite especificar si desea crear o no el perfil de destinatario en la base de datos de Adobe Campaign si aún no existe. Para ello, marque la **Crear usuario si no existe** opción.

1. Añada los componentes seleccionados; para ello, arrástrelos del cuadro de herramientas y situándolos en el formulario. Para obtener más información sobre los componentes específicos que están disponibles en Adobe Campaign, consulte [Componentes de formulario de Adobe](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configure los campos añadidos al hacer doble clic en ellos. El **Adobe Campaign** Esta pestaña permite vincular el campo a un campo de la tabla de destinatarios de Adobe Campaign. También puede especificar si el campo forma parte de la clave de reconciliación, la cual permite reconocer a los destinatarios que ya se encuentran en la base de datos de Adobe Campaign.

   >[!CAUTION]
   >
   >El **Nombre de elemento** debe ser diferente para cada campo de formulario. Cambiar si es necesario.
   >
   >Cada formulario debe contener un **Clave principal cifrada** para administrar correctamente los destinatarios en la base de datos de Adobe Campaign.

1. Active la página seleccionando **Página** > **Activar página** en la caja de herramientas. La página se activa en el sitio. Puede verlo en la instancia de publicación de AEM. Los datos de la base de datos de Adobe Campaign se actualizan una vez que se valide un formulario.

## Probar un formulario {#testing-a-form}

Después de crear un formulario y editar el contenido, es posible que desee probar de forma manual que el formulario funciona correctamente.

>[!NOTE]
>
>Debe tener un **Clave principal cifrada** en cada formulario. En Componentes, seleccione Adobe Campaign para que solo esos componentes estén visibles.
>
>Aunque en este procedimiento escriba el número de EPK manualmente, en la práctica, los usuarios recibirán un vínculo a la página (para cancelar la suscripción, suscribirse o actualizar el perfil) en un boletín. De acuerdo con el usuario, la EPK se actualiza automáticamente.
>
>Para crear ese vínculo, se utiliza la variable **Identificador del recurso principal**(Adobe Campaign Standard) o **Identificador cifrado** (Adobe Campaign 6.1) (por ejemplo, en un **Texto y personalización (Campaign)** ), que se vincula al epk de Adobe Campaign.

Para hacer esto, debe obtener manualmente la EPK de un perfil de Adobe Campaign y añadirlo a la dirección URL:

1. Para obtener la clave principal de cifrado (EPK) de un perfil de Adobe Campaign:

   * En Adobe Campaign Standard: Vaya a **Perfiles y audiencias** > **Perfiles**, que enumera los perfiles existentes. Asegúrese de que la tabla muestra el **Identificador de medio principal** en una columna (esto se puede configurar haciendo clic o pulsando ). **Configurar lista**). Copie el identificador del recurso principal del perfil deseado.
   * En Adobe Campaign 6.11, vaya a **Perfiles y objetivos** >  **Destinatarios**, que enumera los perfiles existentes. Asegúrese de que la tabla muestra el **Identificador cifrado** en una columna (esto se puede configurar haciendo clic con el botón derecho en una entrada y seleccionando **Configurar lista...**). Copie el identificador cifrado del perfil deseado.

1. AEM En, abra la página del formulario en la instancia de publicación y añada el EPK del paso 1 como parámetro de URL: utilice el mismo nombre que definió anteriormente en el componente EPK al crear el formulario (por ejemplo: `?epk=...`)
1. El formulario se puede utilizar para modificar los datos y las suscripciones asociados al perfil vinculado de Adobe Campaign. Después de modificar algunos campos y enviar el formulario, podrá comprobar en Adobe Campaign que se actualizaron los datos adecuados.

Los datos de la base de datos de Adobe Campaign se actualizan una vez que se valide un formulario.
