---
title: Creación de Adobe Campaign Forms en AEM
description: AEM permite crear y utilizar formularios que interactúan con Adobe Campaign en el sitio web. Se pueden insertar campos específicos en los formularios y asignarlos a la base de datos de Adobe Campaign.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Creación de Adobe Campaign Forms en AEM{#creating-adobe-campaign-forms-in-aem}

AEM permite crear y utilizar formularios que interactúan con Adobe Campaign en el sitio web. Se pueden insertar campos específicos en los formularios y asignarlos a la base de datos de Adobe Campaign.

Puede administrar nuevas suscripciones de contacto, bajas de suscripción y datos de perfil de usuario, todo mientras integra sus datos en la base de datos de Adobe Campaign.

Para utilizar Adobe Campaign forms en AEM, debe seguir estos pasos, descritos en este documento:

1. Haga que una plantilla esté disponible.
1. Cree un formulario.
1. Edite el contenido del formulario.

Hay tres tipos de formularios disponibles de forma predeterminada, específicos de Adobe Campaign:

* Guardar un perfil
* Suscripción a un servicio
* Cancelar suscripción a un servicio

Estos formularios definen un parámetro de URL que acepta la clave principal cifrada de un perfil de Adobe Campaign. En función de este parámetro de URL, el formulario actualiza los datos del perfil de Adobe Campaign asociado.

Aunque cree estos formularios de forma independiente, en un caso de uso típico, genere un vínculo personalizado a una página de formulario dentro del contenido del boletín, de modo que los destinatarios puedan abrir el vínculo y realizar ajustes en sus datos de perfil (ya sea cancelar la suscripción, suscribirse o actualizar su perfil).

El formulario se actualiza automáticamente en función del usuario. Consulte [Edición del contenido del formulario](#editing-form-content) para obtener más información.

## Disponibilidad de una plantilla {#making-a-template-available}

Antes de poder crear formularios específicos de Adobe Campaign, debe estar disponible en la aplicación AEM.

Para ello, consulte la [Documentación de plantillas](/help/sites-developing/page-templates-static.md#templateavailability).

En primer lugar, compruebe la conexión entre las instancias de autor y publicación y que Adobe Campaign funciona. Consulte [Integración con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integración con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Asegúrese de que la variable **acMapping** en la **jcr:content** el nodo está configurado en **mapRecipient** o **perfil** al usar Adobe Campaign 6.1.x o Adobe Campaign Standard, respectivamente

### Creación de un formulario {#creating-a-form}

1. Inicie en siteadmin.
1. Desplácese por la estructura de árbol para llegar al lugar en el que desea crear el formulario en el sitio web elegido.
1. Select **Nuevo** > **Nueva página...**.
1. Seleccione: **Perfil de Adobe Campaign (AC 6.1)** o **Perfil de Adobe Campaign (ACS)** e introduzca las propiedades de la página.

   >[!NOTE]
   >
   >Si la plantilla no está disponible, consulte la [Disponibilidad de una plantilla](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) para obtener más información.

1. Haga clic en **Crear** para crear el formulario.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Entonces puede [editar y configurar el contenido del formulario](#editing-form-content).

## Edición del contenido del formulario {#editing-form-content}

Forms dedicado a Adobe Campaign tiene componentes específicos. Estos componentes tienen una opción para permitirle vincular cada campo del formulario a un campo de la base de datos de Adobe Campaign.

>[!NOTE]
>
>Si la plantilla deseada no está disponible, consulte [Disponibilidad de una plantilla](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Esta sección solo detalla los vínculos específicos a Adobe Campaign. Para obtener más información sobre cómo utilizar los formularios en Adobe Experience Manager, consulte [Componentes de Editmode](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Desplácese hasta el formulario que quiera editar.
1. En el cuadro de herramientas, seleccione **Página** > **Propiedades de página...** a continuación, vaya a la **Cloud Services** de la ventana emergente.
1. Para añadir el servicio Adobe Campaign, haga clic en **Añadir servicio** y, a continuación, seleccione la configuración que corresponde a su instancia de Adobe Campaign en la lista desplegable del servicio. Esta configuración se realiza al configurar la conexión entre las instancias. Para obtener más información, consulte [Conexión de AEM a Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Si es necesario, desbloquee la configuración haciendo clic en el icono de cerrojo para poder añadir el servicio de Adobe Campaign.

1. Acceda a los parámetros generales del formulario utilizando la variable **Editar** se encuentra al principio del formulario. La variable **Formulario** permite seleccionar una página de agradecimiento a la que se redirigirá al usuario después de haber validado el formulario.

   La variable **Avanzadas** permite seleccionar el tipo de formulario. La variable **Opciones de publicación** permite elegir entre tres tipos de formularios Adobe Campaign:

   * **Adobe Campaign: Guardar perfil**: permite crear o actualizar un destinatario en Adobe Campaign (valor predeterminado).
   * **Adobe Campaign: Suscripción a servicios**: permite administrar las suscripciones de un destinatario en Adobe Campaign.
   * **Adobe Campaign: Cancelar suscripción a los servicios**: permite cancelar las suscripciones de un destinatario en Adobe Campaign.

   La variable **Configuración de la acción** El campo permite especificar si desea crear o no el perfil de destinatario en la base de datos de Adobe Campaign si aún no existe. Para ello, marque la casilla **Crear usuario si no existe** .

1. Añada los componentes seleccionados arrastrándolos desde el cuadro de herramientas y soltándolos en el formulario. Para obtener más información sobre los componentes específicos de Adobe Campaign disponibles, consulte [Componentes de formulario de Adobe](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configure los campos añadidos haciendo doble clic en ellos. La variable **Adobe Campaign** permite vincular el campo a un campo de la tabla de destinatarios de Adobe Campaign. También puede especificar si el campo forma parte de la clave de reconciliación, lo que permite reconocer los destinatarios que ya están presentes en la base de datos de Adobe Campaign.

   >[!CAUTION]
   >
   >La variable **Nombre del elemento** debe ser diferente para cada campo de formulario. Cambie si es necesario.
   >
   >Cada formulario debe contener un **Clave principal cifrada** para administrar correctamente los destinatarios en la base de datos de Adobe Campaign.

1. Activar la página seleccionando **Página** > **Activar página** en el cuadro de herramientas. La página se activa en el sitio. Puede verlo en la instancia de publicación de AEM. Los datos de la base de datos de Adobe Campaign se actualizan una vez que se valida un formulario.

## Prueba de un formulario {#testing-a-form}

Después de crear un formulario y editar su contenido, es posible que desee probar manualmente que el formulario funciona como se espera.

>[!NOTE]
>
>Debe tener un **Clave principal cifrada** en cada formulario. En Componentes, seleccione Adobe Campaign para que solo esos componentes estén visibles.
>
>Aunque en este procedimiento introduce el número de EPK manualmente, en la práctica, los usuarios recibirán un vínculo a esta página (ya sea para cancelar la suscripción, suscribirse o actualizar su perfil) dentro de un boletín informativo. En función del usuario, la EPK se actualiza automáticamente.
>
>Para crear ese vínculo, utilice la variable **Identificador del recurso principal**(Adobe Campaign Standard) o **Identificador cifrado** (Adobe Campaign 6.1) (por ejemplo, en un **Texto y personalización (Campaign)** ), que se vincula a la EPK en Adobe Campaign.

Para ello, debe obtener manualmente la EPK de un perfil de Adobe Campaign y añadirlo a la URL:

1. Para obtener la clave principal cifrada (EPK) de un perfil de Adobe Campaign:

   * En Adobe Campaign Standard: Vaya a **Perfiles y audiencias** > **Perfiles**, que enumera los perfiles existentes. Asegúrese de que la tabla muestra la variable **Identificador de recurso principal** campo en una columna (esto puede configurarse tocando o haciendo clic en **Configurar lista**). Copie el identificador del recurso principal del perfil deseado.
   * En Adobe Campaign 6.11, vaya a **Perfiles y objetivos** >  **Destinatarios**, que enumera los perfiles existentes. Asegúrese de que la tabla muestra la variable **Identificador cifrado** en una columna (esto se puede configurar haciendo clic con el botón derecho en una entrada y seleccionando **Configurar lista...**). Copie el identificador cifrado del perfil deseado.

1. En AEM, abra la página del formulario en la instancia de publicación y añada la EPK del paso 1 como parámetro de URL: utilice el mismo nombre que definió anteriormente en el componente EPK al crear el formulario (por ejemplo: `?epk=...`)
1. El formulario ahora se puede utilizar para modificar los datos y las suscripciones asociados al perfil de Adobe Campaign vinculado. Después de modificar algunos campos y enviar el formulario, puede comprobar dentro de Adobe Campaign que se han actualizado los datos adecuados.

Los datos de la base de datos de Adobe Campaign se actualizan una vez que se valida un formulario.
