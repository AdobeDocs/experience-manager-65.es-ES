---
title: Creación de Adobe Campaign Forms AEM en
description: AEM La permite crear y utilizar formularios que interactúen con Adobe Campaign en el sitio web. Se pueden insertar campos específicos en los formularios y asignarlos a la base de datos de Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Creación de Adobe Campaign Forms AEM en{#creating-adobe-campaign-forms-in-aem}

AEM La permite crear y utilizar formularios que interactúen con Adobe Campaign en el sitio web. Se pueden insertar campos específicos en los formularios y asignarlos a la base de datos de Adobe Campaign.

Puede administrar nuevas suscripciones de contacto, bajas de suscripción y datos de perfil de usuario, todo ello a la vez que integra sus datos en la base de datos de Adobe Campaign.

Para utilizar formularios Adobe Campaign AEM Forms en la, debe seguir estos pasos, que se describen en este documento:

1. Hacer que una plantilla esté disponible.
1. Cree un formulario.
1. Editar contenido del formulario.

Hay tres tipos de formularios disponibles de forma predeterminada, específicos de Adobe Campaign:

* Guardar un perfil
* Suscripción a un servicio
* Cancelar la suscripción a un servicio

Estos formularios definen un parámetro de URL que acepta la clave principal cifrada de un perfil de Adobe Campaign. En función de este parámetro de URL, el formulario actualiza los datos del perfil de Adobe Campaign asociado.

Aunque estos formularios se crean de forma independiente, en un caso de uso habitual, se genera un vínculo personalizado a una página de formulario dentro del contenido del boletín informativo para que los destinatarios puedan abrir el vínculo y realizar ajustes en los datos de perfil (ya sea cancelar la suscripción, suscribirse o actualizar el perfil).

El formulario se actualiza automáticamente en función del usuario. Consulte [Edición del contenido del formulario](#editing-form-content) para obtener más información.

## Disponibilidad de una plantilla {#making-a-template-available}

Antes de poder crear formularios específicos de Adobe Campaign AEM, debe hacer que las distintas plantillas estén disponibles en la aplicación.

Para ello, consulte las [Documentación de plantillas](/help/sites-developing/page-templates-static.md#templateavailability).

En primer lugar, compruebe la conexión entre las instancias de autor y publicación, y Adobe Campaign está funcionando. Consulte [Integración con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integración con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Asegúrese de que la **acMapping** propiedad en la página **jcr:contenido** El nodo está configurado en **mapRecipient** o **perfil** al usar Adobe Campaign 6.1.x o Adobe Campaign Standard, respectivamente
>

### Creación de un formulario {#creating-a-form}

1. Comience en siteadmin.
1. Desplácese por la estructura de árbol para llegar al lugar en el que desee crear el formulario en el sitio web seleccionado.
1. Seleccionar **Nuevo** > **Nueva página...**.
1. Seleccione una de las opciones **Perfil de Adobe Campaign (AC 6.1)** o **Perfil de Adobe Campaign (ACS)** y escriba las propiedades de la página.

   >[!NOTE]
   >
   >Si la plantilla no está disponible, consulte la [Disponibilidad de una plantilla](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) sección.

1. Clic **Crear** para crear el formulario.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Puede hacer lo siguiente [editar y configurar el contenido del formulario](#editing-form-content).

## Edición del contenido del formulario {#editing-form-content}

Forms dedicado a Adobe Campaign tiene componentes específicos. Estos componentes tienen una opción para permitirle vincular cada campo del formulario a un campo de la base de datos de Adobe Campaign.

>[!NOTE]
>
>Si la plantilla deseada no está disponible, consulte [Disponibilidad de una plantilla](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Esta sección solo detalla los vínculos específicos a Adobe Campaign. Para obtener más información sobre una descripción general más general del uso de los formularios en Adobe Experience Manager, consulte [Componentes del modo de edición](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Desplácese hasta el formulario que desee editar.
1. En el cuadro de herramientas, seleccione **Página** > **Propiedades de página...** a continuación, vaya a **Cloud Service** de la ventana emergente.
1. Agregue el servicio Adobe Campaign haciendo clic en **Añadir servicio** y, a continuación, en la lista desplegable del servicio, seleccione la configuración que corresponda a la instancia de Adobe Campaign. Esta configuración se realiza al configurar la conexión entre las instancias. Para obtener más información, consulte [AEM Conexión de la a Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Si es necesario, desbloquee la configuración haciendo clic en el icono de candado para poder agregar el servicio de Adobe Campaign.

1. Acceda a los parámetros generales del formulario con la variable **Editar** se encuentra al principio del formulario. El **Form** Esta pestaña le permite seleccionar una página de agradecimiento a la que se redirigirá al usuario después de validar el formulario.

   El **Avanzadas** form permite seleccionar el tipo de formulario. El **Opciones de publicación** Este campo permite elegir entre tres tipos de formularios Adobe Campaign:

   * **Adobe Campaign: Guardar perfil**: permite crear o actualizar un destinatario en Adobe Campaign (valor predeterminado).
   * **Adobe Campaign: Suscribirse a servicios**: permite administrar las suscripciones de un destinatario en Adobe Campaign.
   * **Adobe Campaign: Cancelar suscripción a los servicios**: permite cancelar las suscripciones de un destinatario en Adobe Campaign.

   El **Configuración de acción** Este campo permite especificar si desea crear o no el perfil de destinatario en la base de datos de Adobe Campaign si aún no existe. Para ello, marque la **Crear usuario si no existe** opción.

1. Añada los componentes seleccionados arrastrándolos desde el cuadro de herramientas y soltándolos en el formulario. Para obtener más información sobre los componentes específicos de Adobe Campaign disponibles, consulte [Componentes de formulario de Adobe](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configure los campos agregados haciendo doble clic en ellos. El **Adobe Campaign** Esta pestaña permite vincular el campo a un campo de la tabla de destinatarios de Adobe Campaign. También puede especificar si el campo forma parte de la clave de reconciliación que permite reconocer a los destinatarios que ya están presentes en la base de datos de Adobe Campaign.

   >[!CAUTION]
   >
   >El **Nombre de elemento** debe ser diferente para cada campo de formulario. Cámbielo si es necesario.
   >
   >Cada formulario debe contener un **Clave principal cifrada** para administrar correctamente los destinatarios en la base de datos de Adobe Campaign.

1. Active la página seleccionando **Página** > **Activar página** en la caja de herramientas. La página se activa en el sitio. AEM Para verlo, vaya a la instancia de publicación de la publicación de la. Los datos de la base de datos de Adobe Campaign se actualizan una vez validado un formulario.

## Prueba de un formulario {#testing-a-form}

Después de crear un formulario y editar su contenido, es posible que desee probar manualmente que el formulario funciona según lo esperado.

>[!NOTE]
>
>Debe tener un **Clave principal cifrada** en cada formulario. En Componentes, seleccione Adobe Campaign para que solo estén visibles esos componentes.
>
>Aunque en este procedimiento introduzca el número epk manualmente, en la práctica los usuarios obtendrían un vínculo a esta página (ya sea para cancelar la suscripción, suscribirse o actualizar su perfil) dentro de un boletín informativo. El epk se actualiza automáticamente en función del usuario.
>
>Para crear ese vínculo, se utiliza la variable **Identificador del recurso principal**(Adobe Campaign Standard) o **Identificador cifrado** (Adobe Campaign 6.1) (por ejemplo, en un **Texto y personalización (Campaign)** ), que se vincula al epk de Adobe Campaign.

Para ello, debe obtener manualmente el EPK de un perfil de Adobe Campaign y anexarlo a la dirección URL:

1. Para obtener la clave principal cifrada (EPK) de un perfil de Adobe Campaign:

   * En Adobe Campaign Standard: Vaya a **Perfiles y audiencias** > **Perfiles**, que enumera los perfiles existentes. Asegúrese de que la tabla muestra el **Identificador de medio principal** en una columna (esto se puede configurar haciendo clic o pulsando ). **Configurar lista**). Copie el identificador de recurso principal del perfil deseado.
   * En Adobe Campaign 6.11, vaya a **Perfiles y objetivos** >  **Destinatarios**, que enumera los perfiles existentes. Asegúrese de que la tabla muestra el **Identificador cifrado** en una columna (esto se puede configurar haciendo clic con el botón derecho en una entrada y seleccionando **Configurar lista...**). Copie el identificador cifrado del perfil deseado.

1. AEM En, abra la página del formulario en la instancia de publicación y añada el EPK del paso 1 como parámetro de URL: utilice el mismo nombre que definió anteriormente en el componente EPK al crear el formulario (por ejemplo: `?epk=...`)
1. Ahora el formulario se puede utilizar para modificar los datos y las suscripciones asociados al perfil de Adobe Campaign vinculado. Después de modificar algunos campos y enviar el formulario, puede comprobar dentro de Adobe Campaign que se han actualizado los datos correspondientes.

Los datos de la base de datos de Adobe Campaign se actualizan una vez validado un formulario.
