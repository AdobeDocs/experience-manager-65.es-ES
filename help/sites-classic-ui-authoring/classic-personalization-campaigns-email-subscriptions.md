---
title: Administración de suscripciones
seo-title: Administración de suscripciones
description: Se puede solicitar a los usuarios que se suscriban a las listas de correo del proveedor de servicios de correo electrónico, mediante el componente Formulario que se usa en la página web de AEM. Para preparar una página de AEM con un componente de formulario de registro configurado para la suscripción a las listas de correo del servicio de correo electrónico, deberá aplicar la configuración de servicio correspondiente a la página de AEM que visitará el posible suscriptor.
seo-description: Se puede solicitar a los usuarios que se suscriban a las listas de correo del proveedor de servicios de correo electrónico, mediante el componente Formulario que se usa en la página web de AEM. Para preparar una página de AEM con un componente de formulario de registro configurado para la suscripción a las listas de correo del servicio de correo electrónico, deberá aplicar la configuración de servicio correspondiente a la página de AEM que visitará el posible suscriptor.
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 74%

---


# Administración de suscripciones{#managing-subscriptions}

>[!NOTE]
>
>Adobe no planea seguir mejorando esta capacidad (Administración de posibles clientes y Listas).
>Se recomienda aprovechar [Adobe Campaign y su integración AEM](/help/sites-administering/campaign.md).

Se puede solicitar a los usuarios que se suscriban a **listas de correo electrónico** con la ayuda del componente **Formulario** utilizado en una página Web AEM. Para preparar una página de AEM con un componente de formulario de registro configurado para la suscripción a las listas de correo del servicio de correo electrónico, deberá aplicar la configuración de servicio correspondiente a la página de AEM que visitará el posible suscriptor.

## Aplicar la configuración del servicio de correo electrónico a una página {#applying-email-service-configuration-to-a-page}

Para configurar una página de AEM:

1. Desplácese a la ficha **Sitios web**.
1. Seleccione la página que debe configurarse para el servicio. Haga clic con el botón derecho en la página y seleccione **Propiedades**.

1. Seleccione **Cloud Services** y luego **Añadir servicio**. Seleccione una configuración de la lista de configuraciones disponibles.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Haga clic en **Aceptar**.

## Crear un formulario de registro en una página de AEM para suscribirse o cancelar la suscripción a las listas {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

Para crear un formulario de registro y configurarlo para las suscripciones a las listas de correo del proveedor de servicios de correo electrónico:

1. Abra la página de AEM que visitará el usuario.
1. Aplique la configuración del proveedor de servicio de correo electrónico a la página.

1. Añada el componente **Formulario** a la página arrastrándolo desde la barra de tareas. Si el componente no estuviera disponible, cambie al modo de diseño y habilite el grupo **Formularios**.
1. Haga clic en **Editar** en la barra **Inicio de formulario** y vaya a la ficha **Avanzado**.
1. En el menú desplegable **Formulario**, seleccione **Servicio de correo electrónico: Cree un suscriptor** y añádalo a la lista.
1. En la parte inferior del cuadro de diálogo, abra la lista desplegable **Configuración de la acción**, que le permite seleccionar una o varias listas de suscripción.
1. En la lista **Selección**, seleccione la lista a la que quiere que se suscriban los usuarios. Puede añadir varias listas; para ello, utilice el botón del signo más (+) (**Añadir elemento**).

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >El cuadro de diálogo puede variar en función del proveedor de servicios de correo electrónico.

1. En la ficha **Formulario**, seleccione la página de agradecimiento que desea que vean los usuarios tras enviar el formulario (si se deja en blanco, el formulario se vuelve a mostrar después del envío). Haga clic en **Aceptar**. Un componente de **id. de correo electrónico** aparecerá en el formulario, lo que le permite crear un formulario en el que los usuarios pueden enviar sus direcciones de correo electrónico para suscribirse o cancelar la suscripción a una lista de distribución de correo.
1. Añada el componente de botón **Enviar** de la sección **Formulario** de la barra de tareas.

   El formulario está listo. Publique la página configurada en los pasos anteriores, junto con la página de **agradecimiento**, en la instancia de publicación. Los suscriptores potenciales que visiten la página pueden rellenar el formulario y suscribirse a la lista indicada en la configuración.

   >[!NOTE]
   >
   >Para que la suscripción del formulario funcione correctamente, [deben exportarse las claves de cifrado del autor e importarse en la instancia de publicación](#exporting-keys-from-author-and-importing-on-publish).

## Exportar las claves de creación e importación en la publicación  {#exporting-keys-from-author-and-importing-on-publish}

Para la que suscripción y la cancelación de suscripciones del servicio de correo electrónico funcionen mediante el formulario de registro en la instancia de publicación, deberá realizar los pasos siguientes:

1. En la instancia de creación, desplácese al Administrador de paquetes.
1. Cree un paquete nuevo. Establezca el filtro como `/etc/key`.
1. Cree y descargue el paquete.
1. Desplácese al Administrador de paquetes en la instancia de publicación y cargue este paquete.
1. Desplácese a la consola OSGi de publicación y reinicie el paquete denominado **Adobe Granite Crypto Support**.

## Cancelar la suscripción de usuarios de las listas  {#unsubscribing-users-from-lists}

Para cancelar la suscripción de usuarios de las listas:

1. Abra las propiedades de página de la página de AEM que contenga el formulario de registro para cancelar la suscripción de un posible cliente.
1. Aplique la configuración de servicio a la página.
1. Cree un formulario de registro en la página.
1. Mientras configura el componente, seleccione la acción **Servicio de correo electrónico**: **Cancelar la suscripción del usuario de la lista.**
1. Desde el menú desplegable, seleccione la lista apropiada de la que debe eliminarse el usuario al cancelar la suscripción.

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. Exporte las claves de creación a la publicación.

## Configurar correos electrónicos de respuesta automática para el servicio de correo electrónico  {#configuring-auto-responder-emails-for-email-service}

Para configurar un correo electrónico de respuesta automática para un suscriptor:

1. Abra las propiedades de página de la página de AEM que contenga el formulario de registro para configurar la respuesta automática de un posible cliente.
1. Aplique la configuración de ExactTarget a la página.

1. Añada el componente **Formulario** a la página arrastrándolo desde la barra de tareas. Si el componente no estuviera disponible, cambie al modo de diseño y habilite el grupo **Formularios**.
1. Haga clic en **Editar** en la barra **Inicio de formulario** y vaya a la ficha **Avanzado**.
1. En el menú desplegable **Formulario**, seleccione **Servicio de correo electrónico: Enviar correo electrónico de respuesta automática.**
1. **Seleccione un correo electrónico**  (es el correo que se envía como correo electrónico de respuesta automática).

1. **Seleccione Clasificación**  (esta clasificación se utiliza para enviar el correo electrónico).
1. Seleccione la página **Gracias** (la página a la que se dirige a los usuarios una vez que envían el formulario).

   En la ficha **Formulario**, seleccione la página de agradecimiento a la que desea que se dirijan los usuarios después de enviar el formulario. (Si se deja en blanco, el formulario se vuelve a mostrar al enviar). Haga clic en **Aceptar**.

1. Exporte las claves de creación a la publicación.
1. Añada el componente de botón **Enviar** de la sección **Formulario** de la barra de tareas.

   El formulario de registro está listo. Publique la página configurada en los pasos anteriores, junto con la página de **agradecimiento**, en la instancia de publicación. Los suscriptores potenciales que visiten la página pueden rellenar el formulario y, al enviarlo, recibirán un correo electrónico de respuesta automática según el id. de correo electrónico especificado en el formulario.

   >[!NOTE]
   >
   >Para que la suscripción del formulario de registro funcione correctamente, [deben exportarse las claves de cifrado del autor e importarse en la instancia de publicación](#exporting-keys-from-author-and-importing-on-publish).

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)

