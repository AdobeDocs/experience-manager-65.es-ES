---
title: Creación de Adobe Campaign Forms en Adobe Experience Manager
description: Adobe Experience Manager permite crear y utilizar formularios que interactúen con Adobe Campaign en el sitio web
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# Creación de Adobe Campaign Forms AEM en {#creating-adobe-campaign-forms-in-aem}

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

Para ello, consulte las [Documentación de plantillas](/help/sites-developing/templates.md#template-availability).

## Creación de un formulario {#creating-a-form}

En primer lugar, compruebe la conexión entre las instancias de autor y publicación, y Adobe Campaign está funcionando. Consulte [Integración con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integración con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Asegúrese de que la **acMapping** propiedad en la página **jcr:contenido** El nodo está configurado en **mapRecipient** o **perfil** al usar Adobe Campaign Classic o Adobe Campaign Standard, respectivamente
>

1. AEM En, en Sitios, desplácese hasta donde desee crear una página.
1. Cree una página y seleccione **Perfil de Adobe Campaign Classic** o **Perfil de Adobe Campaign Standard** y haga clic en **Siguiente**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Si la plantilla deseada no está disponible, consulte [Disponibilidad de plantillas](/help/sites-developing/templates.md#template-availability).

1. En el **Nombre** , añada el nombre de la página. Debe ser un nombre JCR válido.
1. En el **Título** , introduzca un título y haga clic en **Crear**.
1. Abra la página y seleccione **Abrir propiedades** y en Cloud Service, añada la configuración de Adobe Campaign y seleccione la marca de verificación para guardar los cambios.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. En la página, en la variable **Inicio de formulario** , seleccione el tipo de formulario que es: **Suscribirse, Cancelar suscripción,** o **Guardar perfil**. Solo puede tener un tipo por formulario. Ahora puede [editar el contenido del formulario](#editing-form-content).

## Edición del contenido del formulario {#editing-form-content}

Forms dedicado a Adobe Campaign tiene componentes específicos. Estos componentes tienen una opción para permitirle vincular cada campo del formulario a un campo de la base de datos de Adobe Campaign.

>[!NOTE]
>
>Si la plantilla deseada no está disponible, consulte [Disponibilidad de una plantilla](/help/sites-authoring/adobe-campaign.md).

Esta sección solo detalla los vínculos específicos a Adobe Campaign. Para obtener más información sobre una descripción general más general del uso de los formularios en Adobe Experience Manager, consulte [Componentes del modo de edición](/help/sites-authoring/default-components-foundation.md).

1. Seleccionar **Abrir propiedades** y en Cloud Service, añada la configuración de Adobe Campaign y seleccione la marca de verificación para guardar los cambios.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. En la página, en la variable **Inicio de formulario** , haga clic en el icono Configuración.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Haga clic en **Avanzadas** y seleccione el tipo de formulario que es: **Suscribirse, Cancelar suscripción,** o **Guardar perfil** y haga clic en **OK.** Solo puede tener un tipo por formulario.

   * **Adobe Campaign: Guardar perfil**: permite crear o actualizar un destinatario en Adobe Campaign (valor predeterminado).
   * **Adobe Campaign: Suscribirse a servicios**: permite administrar las suscripciones de un destinatario en Adobe Campaign.
   * **Adobe Campaign: Cancelar suscripción a los servicios**: permite cancelar las suscripciones de un destinatario en Adobe Campaign.

1. Debe tener un **Clave principal cifrada** en cada formulario. Este componente define qué parámetro de URL se utiliza para aceptar la clave principal cifrada de un perfil de Adobe Campaign. En Componentes, seleccione Adobe Campaign para que solo estén visibles esos componentes.
1. Arrastre el componente **Clave principal cifrada** Vaya al formulario (en cualquier lugar) y toque o haga clic en **Configuración** icono. En el **Adobe Campaign** pestaña, especifique cualquier nombre para el parámetro de URL. Toque o haga clic en la marca de verificación para guardar los cambios.

   Los vínculos generados para este formulario deben utilizar este parámetro de URL y asignarle la clave principal cifrada de un perfil de Adobe Campaign. La clave principal cifrada debe tener la codificación URL (porcentaje) correcta.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Agregue componentes al formulario según sea necesario, como un campo de texto, un campo de fecha, un campo de casilla de verificación, un campo de opción, etc. Consulte [Componentes de formulario Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) para obtener más información sobre cada componente.
1. Haga clic en el icono Configuración para abrir el componente. Por ejemplo, en **Campo de texto (Campaign)** componente, cambie el título y el texto.

   Clic **Adobe Campaign** para asignar el campo de formulario a una variable de metadatos de Adobe Campaign. Al enviar el formulario, el campo asignado se actualiza en Adobe Campaign. En el selector de variables solo están disponibles los campos con tipos coincidentes (por ejemplo, las variables de cadena para los campos de texto).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Puede añadir o quitar campos que se muestran en la tabla de destinatarios siguiendo las instrucciones aquí: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Clic **Publicar página**. La página se activa en el sitio. AEM Para verlo, vaya a la instancia de publicación de la publicación de la. También puede [prueba de un formulario](#testing-a-form).

   >[!CAUTION]
   >
   >Debe proporcionar permisos de lectura al usuario anónimo en el servicio en la nube para utilizar formularios al publicar. Sin embargo, tenga en cuenta los posibles problemas de seguridad al proporcionar permisos de lectura al usuario anónimo y asegúrese de mitigarlo, por ejemplo, configurando Dispatcher.

## Prueba de un formulario {#testing-a-form}

Después de crear un formulario y editar su contenido, es posible que desee probar manualmente que el formulario funciona según lo esperado.

>[!NOTE]
>
>Debe tener un **Clave principal cifrada** en cada formulario. En Componentes, seleccione Adobe Campaign para que solo estén visibles esos componentes.
>
>Aunque en este procedimiento introduzca el número epk manualmente, en la práctica los usuarios obtendrían un vínculo a esta página (ya sea para cancelar la suscripción, suscribirse o actualizar su perfil) dentro de un boletín informativo. El epk se actualiza automáticamente en función del usuario.
>
>Para crear ese vínculo, se utiliza la variable **Identificador del recurso principal**(Adobe Campaign Standard) o **Identificador cifrado** (Adobe Campaign Classic) (por ejemplo, en un **Texto y personalización (Campaign)** ), que se vincula al epk de Adobe Campaign.

Para ello, debe obtener manualmente el EPK de un perfil de Adobe Campaign y anexarlo a la dirección URL:

1. Para obtener la clave principal cifrada (EPK) de un perfil de Adobe Campaign:

   * En Adobe Campaign Standard: Vaya a **Perfiles y audiencias** > **Perfiles**, que enumera los perfiles existentes. Asegúrese de que la tabla muestra el **Identificador de medio principal** en una columna (esto se puede configurar haciendo clic o pulsando ). **Configurar lista**). Copie el identificador de recurso principal del perfil deseado.
   * En Adobe Campaign Classic, vaya a **Perfiles y objetivos** >  **Destinatarios**, que enumera los perfiles existentes. Asegúrese de que la tabla muestra el **Identificador cifrado** en una columna (esto se puede configurar haciendo clic con el botón derecho en una entrada y seleccionando **Configurar lista...**). Copie el identificador cifrado del perfil deseado.

1. AEM En, abra la página del formulario en la instancia de publicación y añada el EPK del paso 1 como parámetro de URL: utilice el mismo nombre que definió anteriormente en el componente EPK al crear el formulario (por ejemplo: `?epk=...`)
1. Ahora el formulario se puede utilizar para modificar los datos y las suscripciones asociados al perfil de Adobe Campaign vinculado. Después de modificar algunos campos y enviar el formulario, puede comprobar dentro de Adobe Campaign que se han actualizado los datos correspondientes.

Los datos de la base de datos de Adobe Campaign se actualizan una vez validado un formulario.
