---
title: Crear formularios de Adobe Campaign en AEM
seo-title: Crear formularios de Adobe Campaign en AEM
description: AEM permite crear y utilizar formularios que interactúan con Adobe Campaign en el sitio web
seo-description: AEM permite crear y utilizar formularios que interactúan con Adobe Campaign en el sitio web
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
translation-type: tm+mt
source-git-commit: 2451f4994a18b1566ea0efddbefcaa5bb8e41c99
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 75%

---


# Crear formularios de Adobe Campaign en AEM {#creating-adobe-campaign-forms-in-aem}

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

## Hacer que una plantilla esté disponible  {#making-a-template-available}

Antes de poder crear formularios específicos de Adobe Campaign, debe realizar las plantillas diferentes que hay en su aplicación de AEM.

Para ello, consulte la [documentación de plantillas](/help/sites-developing/templates.md#template-availability).

## Crear un formulario {#creating-a-form}

En primer lugar, compruebe la conexión entre el autor y las instancias de publicación y que Adobe Campaign funciona correctamente. Consulte [Integrar con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrar con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Asegúrese de que la propiedad **acMapping** en el nodo **jcr:content** de la página está establecida en **mapRecipient** o en **profile** al usar Adobe Campaign Classic o Adobe Campaign Standard, respectivamente.


1. En AEM, en Sitios, vaya a la ubicación donde desee creación de una nueva página.
1. Cree una página y seleccione **Adobe Campaign Classic Perfil** o **Adobe Campaign Standard Perfil** y haga clic en **Siguiente**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Si la plantilla deseada no está disponible, consulte [Disponibilidad de la plantilla](/help/sites-developing/templates.md#template-availability).

1. En el campo **Nombre**, añada el nombre de la página. Debe ser un nombre válido de JCR.
1. En el campo **Título**, especifique un título y haga clic en **Crear**.
1. Abra la página y seleccione **Abrir propiedades** y, en Servicios de nube, añada la configuración de Adobe Campaign y seleccione la marca de verificación para guardar los cambios.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. En la página, en el componente **Inicio del formulario**, seleccione el tipo de formulario: **Suscribirse, Cancelar la suscripción** o **Guardar perfil**. Solo puede tener un tipo por formulario. Puede [ editar el contenido del formulario](#editing-form-content).

## Editar el contenido del formulario {#editing-form-content}

Los dedicados a Adobe Campaign tienen componentes específicos. Estos componentes tienen una opción para permitir que se vincule cada campo del formulario a un campo de la base de datos de Adobe Campaign.

>[!NOTE]
>
>Si la plantilla deseada no está disponible, consulte [Disponibilidad de una plantilla](/help/sites-authoring/adobe-campaign.md).

En esta sección se detallan únicamente los vínculos específicos de Adobe Campaign. Para obtener más información sobre una descripción general más general de cómo utilizar formularios en Adobe Experience Manager, consulte [Componentes de Editmode](/help/sites-authoring/default-components-foundation.md).

1. Seleccione **Abrir propiedades** y en los servicios de nube añada la configuración de Adobe Campaign y seleccione la marca de verificación para guardar los cambios.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. En la página, en el componente **Inicio de formulario**, haga clic en el icono Configuración.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Haga clic en la ficha **Avanzado** y seleccione el tipo de formulario que es: **Suscribirse, Cancelar suscripción,** o **Guardar Perfil** y haga clic en **Aceptar.** Solo puede tener un tipo por formulario.

   * **Adobe Campaign: Guardar perfil**: permite crear o actualizar un destinatario en Adobe Campaign (valor predeterminado).
   * **Adobe Campaign: Suscribirse a servicios**: permite gestionar las suscripciones de un destinatario en Adobe Campaign.
   * **Adobe Campaign: Cancelar suscripción a los servicios**: permite cancelar las suscripciones de un destinatario en Adobe Campaign.

1. Debe tener un componente **Clave principal cifrada** en cada formulario. Este componente define qué parámetro de URL se utilizará para aceptar la clave principal cifrada de un perfil de Adobe Campaign. En Componentes, seleccione Adobe Campaign para que solo esos componentes estén visibles.
1. Arrastre el componente **Clave principal cifrada** al formulario (en cualquier lugar) y toque o haga clic en el icono **Configuración**. En la ficha **Adobe Campaign**, especifique un nombre para el parámetro de URL. Haga clic o pulse la marca de verificación para guardar los cambios.

   Los vínculos a este formulario que se crearon, necesitan utilizar este parámetro de URL y asignarle la clave principal cifrada de un perfil de Adobe Campaign. La clave principal cifrada debe estar correctamente codificada mediante una dirección URL (porcentaje).

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Añada componentes al formulario según sea necesario; por ejemplo, un campo de texto, un campo de fecha, un campo de casilla, un campo de opciones, y así sucesivamente. Consulte [Componentes del formulario de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) para obtener más información acerca de cada componente.
1. Haga clic en el icono de configuración para abrir el componente. Por ejemplo, en el componente **Campo de texto (Campaña)**, cambie el título y el texto.

   Haga clic en **Adobe Campaign** para asignar el campo de formulario a una variable de metadatos de Adobe Campaign. Cuando envíe el formulario, el campo asignado se actualizará en Adobe Campaign. Solo los campos con tipos coincidentes están disponibles en el selector de variables (por ejemplo, un conjunto de variables de cadena para los campos de texto).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Puede agregar o quitar campos que se muestran en la tabla de destinatario siguiendo las instrucciones que se indican a continuación: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Haga clic en **Publicar página**. La página se activa en el sitio. Puede verlo en la instancia de publicación de AEM. También puede [probar un formulario](#testing-a-form).

   >[!CAUTION]
   >
   >Debe proporcionar permiso de lectura al usuario anónimo del servicio de nube para usar formularios en la publicación. Sin embargo, recuerde tener en cuenta los problemas potenciales de seguridad al proporcionar permisos de lectura al usuario anónimo y asegúrese de atenuarlos; por ejemplo, puede configurar Dispatcher.

## Probar un formulario  {#testing-a-form}

Después de crear un formulario y editar el contenido, es posible que desee probar de forma manual que el formulario funciona correctamente.

>[!NOTE]
>
>Debe tener un componente **Clave principal cifrada** en cada formulario. En Componentes, seleccione Adobe Campaign para que solo esos componentes estén visibles.
>
>Aunque en este procedimiento escriba el número de EPK manualmente, en la práctica, los usuarios recibirán un vínculo a la página (para cancelar la suscripción, suscribirse o actualizar el perfil) en un boletín. De acuerdo con el usuario, la EPK se actualiza automáticamente.
>
>Para crear ese vínculo, utilice la variable **Identificador de recursos principal**(Adobe Campaign Standard) o **Identificador cifrado** (Adobe Campaign Classic) (por ejemplo, en un componente **Texto y personalización (Campaña)**), que se vincula a la página en Adobe Campaign.

Para hacer esto, debe obtener manualmente la EPK de un perfil de Adobe Campaign y añadirlo a la dirección URL:

1. Para obtener la clave principal de cifrado (EPK) de un perfil de Adobe Campaign:

   * En Adobe Campaign Standard: vaya a **Perfiles y Audiencias** > **Perfiles**, que lista los perfiles existentes. Asegúrese de que la tabla muestra el campo **Identificador de recursos principal** en una columna (esto se puede configurar haciendo clic o tocando **Configurar lista**). Copie el identificador del recurso principal del perfil deseado.
   * En Adobe Campaign Classic, vaya a **Perfiles y Destinatarios** > **Destinatarios**, que lista los perfiles existentes. Asegúrese de que la tabla muestra el campo **Identificador cifrado** en una columna (esto se puede configurar haciendo clic con el botón derecho en una entrada y seleccionando **Configurar lista...**). Copie el identificador cifrado del perfil deseado.

1. En AEM, abra la página de formulario en la instancia de publicación y anexe el EPK del paso 1 como parámetro de URL: utilice el mismo nombre que definió anteriormente en el componente EPK al crear el formulario (por ejemplo: `?epk=...`)
1. El formulario se puede utilizar para modificar los datos y las suscripciones asociados al perfil vinculado de Adobe Campaign. Después de modificar algunos campos y enviar el formulario, podrá comprobar en Adobe Campaign que se actualizaron los datos adecuados.

Los datos de la base de datos de Adobe Campaign se actualizan una vez que se valide un formulario.
