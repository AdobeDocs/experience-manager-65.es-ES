---
title: Creación y administración de contenido de aplicación
description: La administración del contenido de la aplicación requiere un esfuerzo colectivo por parte de los desarrolladores, los autores de contenido y los administradores. Los autores manipulan las páginas, que se basan en plantillas y componentes generados por desarrolladores de aplicaciones.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Creación y administración de contenido de aplicación{#creating-and-managing-app-content}

{{ue-over-mobile}}

La administración del contenido de la aplicación requiere un esfuerzo colectivo por parte de [desarrolladores](#developer), [autores](#author) y [administradores](#administrator). Los autores manipulan las páginas, que se basan en plantillas y componentes generados por desarrolladores de aplicaciones.

Por último, los administradores publican de forma estratégica el contenido actualizado de la aplicación.

>[!NOTE]
>
>**Requisito previo**:
>
>En [Implementación y mantenimiento](/help/sites-deploying/deploy.md), los desarrolladores se familiarizaron con los componentes y las plantillas del sistema en Adobe Experience Manager AEM ().

## El mosaico Administrar contenido de la página {#the-manage-page-content-tile}

>[!CAUTION]
>
>Si no utiliza una plantilla de aplicación predeterminada, para habilitar la publicación de contenido nuevo de la aplicación en OTA, debe configurar un controlador de sincronización de contenido.
>
>Consulte [Dispositivo móvil con sincronización de contenido](/help/mobile/phonegap-contentsync.md) en la sección del Desarrollador para obtener más información.

En este caso, el contenido se puede crear, editar y eliminar en AEM Mobile de la misma manera que lo haría en AEM Sites.

El mosaico **Administrar contenido de la página** muestra el número de páginas de contenido administrado y modificadas por última vez para una carga en particular. Puede explorar el contenido para crear, copiar, mover, eliminar y actualizar páginas haciendo clic en cada registro del mosaico.

Una vez actualizado el contenido, los administradores pueden publicar una carga útil de actualización de contenido por correo electrónico (OTA) para los clientes a través del mosaico **Administrar paquetes de contenido.**

![chlimage_1-161](assets/chlimage_1-161.png)

Seleccione uno de los paquetes de contenido enumerados para crear o editar contenido, como crear, editar o eliminar páginas, cambiar la navegación y el orden de las páginas, crear o actualizar contenido como copiar (texto) y medios.

Nota *todo es contenido*, lo que significa que los estilos de aplicación, la copia (texto), los medios, las páginas, la navegación y la segmentación del contenido se pueden editar y actualizar en formato OTA, sin tener que ir a una tienda de aplicaciones.

Para editar el contenido de AEM Mobile AEM AEM AEM, los autores de **necesitarán tener una comprensión sólida de la interfaz de edición de contenido de: [Creación de páginas en el.](/help/sites-authoring/qg-page-authoring.md)

## El Mosaico Administrar Paquetes De Contenido {#the-manage-content-packages-tile}

AEM En este caso, *Los administradores* pueden actualizar sus aplicaciones de forma rápida y sencilla para ofrecer experiencias atractivas y contenido actualizado que promuevan la participación de la marca y cumplan con los objetivos comerciales, todo sin necesidad de que los desarrolladores o las tiendas de aplicaciones vuelvan a enviarlas.

![chlimage_1-162](assets/chlimage_1-162.png)

AEM AEM Una vez que *autores* hayan agregado o modificado contenido a través del mosaico Administrar contenido, *Los administradores* pueden insertar esos cambios en los clientes con una actualización de paquetes de contenido.

AEM La acción Paquete de contenido permite al *Autor de* crear y editar el contenido de la página mientras el equipo de desarrollo realiza cambios en el diseño y la implementación de una aplicación host, incluidos la navegación, el estilo, la lógica del lado del servidor, las plantillas y los componentes, y luego enviar esos cambios fuera de OTA a los clientes sin necesidad de volver a enviarlos a las distintas tiendas para su distribución.

**Para publicar contenido nuevo o actualizado**

Seleccione un paquete de contenido del mosaico; en este ejemplo, el paquete en inglés. Observe que un cuadro de diálogo de actualización de contenido enumera la configuración *Sincronización de contenido* relevante. Si el contenido de la aplicación se ha modificado desde una actualización anterior, el estado se mostrará *Pendiente*, como se muestra a continuación.

![chlimage_1-163](assets/chlimage_1-163.png)

A continuación, seleccione la acción **Stage** en la parte superior derecha para crear la actualización de contenido. Añada la información de actualización adecuada y pulse Listo.

![chlimage_1-164](assets/chlimage_1-164.png)

A continuación, el controlador *Content Sync* crea los paquetes necesarios formando un delta (un paquete de *solamente* lo que ha cambiado). Una vez finalizado, este paquete de contenido de actualización se ha preparado como se muestra a continuación.

El ensayo de una actualización de contenido permite realizar varias actualizaciones antes de publicarlas en OTA para dispositivos móviles.

>[!NOTE]
>
>AEM El contenido ensayado se puede comprobar mediante la aplicación Verificar el antes de publicar.
>
>AEM AEM Consulte [Inicio rápido móvil para la verificación de datos](/help/mobile/phonegap-mobile-quickstart.md) para obtener más información sobre la aplicación de verificación de datos en el teléfono móvil.

![chlimage_1-165](assets/chlimage_1-165.png)

Cuando esté listo para entregar contenido nuevo a los usuarios de su aplicación con Content Sync OTA, seleccione **Publish** como se muestra a continuación.

![chlimage_1-166](assets/chlimage_1-166.png)

### Pasos siguientes {#the-next-steps}

Una vez que haya aprendido a crear y administrar contenido de aplicación en el panel de aplicaciones, consulte los siguientes recursos para otras funciones de creación:

* [El mosaico Administrar aplicación](/help/mobile/phonegap-app-details-tile.md)
* [Edición de metadatos de aplicación](/help/mobile/phonegap-editmetadata.md)
* [Definiciones de aplicación](/help/mobile/phonegap-app-definitions.md)
* [Crear una aplicación nueva mediante el Asistente para crear aplicación](/help/mobile/phonegap-create-new-app.md)
* [Importar una aplicación híbrida existente](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los recursos siguientes:

* [Desarrollo para Adobe PhoneGap AEM Enterprise con](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap AEM Enterprise con el servicio de administración de](/help/mobile/administer-phonegap.md)
