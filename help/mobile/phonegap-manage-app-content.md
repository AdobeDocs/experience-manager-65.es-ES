---
title: Creación y administración del contenido de la aplicación
seo-title: Creación y administración del contenido de la aplicación
description: La administración del contenido de la aplicación requiere un esfuerzo colectivo de los desarrolladores, autores de contenido y administradores.  Los autores manipulan las páginas, que a su vez se basan en plantillas y componentes generados por los desarrolladores de la aplicación.
seo-description: La administración del contenido de la aplicación requiere un esfuerzo colectivo de los desarrolladores, autores de contenido y administradores.  Los autores manipulan las páginas, que a su vez se basan en plantillas y componentes generados por los desarrolladores de la aplicación.
uuid: ca049bad-9be8-47aa-b010-298258feda26
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 5c8971ab-b07c-4131-b4cb-f34c52425014
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creación y administración del contenido de la aplicación{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

La administración del contenido de la aplicación requiere un esfuerzo colectivo de [los desarrolladores](#developer), [autores](#author) de contenido y [administradores](#administrator). Los autores manipulan las páginas, que a su vez se basan en plantillas y componentes generados por los desarrolladores de la aplicación.

Por último, los administradores publican estratégicamente el contenido actualizado de la aplicación.

>[!NOTE]
>
>**Requisitos previos**:
>
>Al [implementar y mantener](/help/sites-deploying/deploy.md), los desarrolladores se familiarizaron con el sistema de componentes y plantillas de AEM.

## Mosaico Administrar contenido de página {#the-manage-page-content-tile}

>[!CAUTION]
>
>Si no utiliza una plantilla de aplicación lista para usar, para permitir que se publique contenido de aplicación nuevo en OTA, debe configurar un controlador de sincronización de contenido.
>
>Consulte [Móvil con sincronización](/help/mobile/phonegap-contentsync.md) de contenido en la sección del desarrollador para obtener más información.

Aquí, el contenido se puede crear, editar y eliminar en AEM Mobile de la misma manera que lo haría en los sitios de AEM.

El mosaico **** Administrar contenido de página muestra el número de páginas de contenido administrado y la última modificación para una carga útil determinada. Puede profundizar en el contenido para crear, copiar, mover, eliminar y actualizar páginas haciendo clic en cada registro del mosaico.

Una vez actualizado el contenido, los administradores pueden publicar una carga útil de actualización de contenido sobre el aire (OTA) para los clientes a través del mosaico **Administrar paquetes de contenido.**

![chlimage_1-161](assets/chlimage_1-161.png)

Seleccione uno de los paquetes de contenido de la lista para crear o editar contenido, como crear, editar o eliminar páginas, cambiar la navegación y el orden de las páginas, crear o actualizar contenido como copiar (texto) y medios.

Tenga en cuenta que *todo es contenido*, lo que significa que los estilos de aplicación, la copia (texto), los medios, las páginas, la navegación y la segmentación de contenido se pueden editar y actualizar sin necesidad de visitar una tienda de aplicaciones.

Para editar el contenido de AEM Mobile, *los autores de AEM *necesitarán una sólida comprensión de la interfaz de edición de contenido de AEM: Creación [de páginas en AEM.](/help/sites-authoring/qg-page-authoring.md)

## Mosaico Administrar paquetes de contenido {#the-manage-content-packages-tile}

Aquí, los administradores *de* AEM pueden actualizar rápida y fácilmente sus aplicaciones para ofrecer experiencias atractivas y contenido actualizado que impulsen la participación de la marca y cumplan los objetivos empresariales sin necesidad de un desarrollador o un reenvío de la tienda de aplicaciones.

![chlimage_1-162](assets/chlimage_1-162.png)

Una vez que los autores *de* AEM han agregado o modificado contenido a través de Administrar mosaico de contenido, los administradores *de* AEM pueden insertar estos cambios en los clientes con una actualización de paquetes de contenido.

La acción Paquete de contenido permite que *AEM Author* cree y edite contenido de página mientras que el equipo de desarrollo realiza cambios en el diseño y la implementación de una aplicación host, incluida la navegación, el estilo, la lógica del servidor, las plantillas y los componentes y, a continuación, envía esos cambios a los clientes sin necesidad de volver a enviarlos a los distintos almacenes para su distribución.

**Para publicar contenido nuevo o actualizado**

Seleccione un paquete de contenido del mosaico, en este ejemplo el paquete inglés. Observe que un cuadro de diálogo de actualización de contenido enumera la configuración de sincronización *de* contenido relevante. Si el contenido de la aplicación se ha modificado desde una actualización anterior, el estado mostrará *Pendiente*, como se muestra a continuación.

![chlimage_1-163](assets/chlimage_1-163.png)

A continuación, seleccione la acción **Escenario** en la parte superior derecha para crear la nueva actualización de contenido. Agregue la información de actualización adecuada y pulse Listo.

![chlimage_1-164](assets/chlimage_1-164.png)

A continuación, el controlador de sincronización *de* contenido crea los paquetes necesarios formando un delta (un paquete de *solo* lo que ha cambiado). Una vez completado, este paquete de contenido de actualización se ha escalonado como se muestra a continuación.

El ensayo de una actualización de contenido permite realizar varias actualizaciones antes de publicarlas en OTA en dispositivos móviles.

>[!NOTE]
>
>El contenido escalonado se puede comprobar con la aplicación AEM Verify antes de publicar.
>
>Consulte Inicio rápido [móvil para AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) para obtener más información sobre la aplicación AEM Verify.

![chlimage_1-165](assets/chlimage_1-165.png)

Cuando esté listo para entregar contenido nuevo a los usuarios de la aplicación con OTA de sincronización de contenido, seleccione **Publicar** como se muestra a continuación.

![chlimage_1-166](assets/chlimage_1-166.png)

### Pasos siguientes {#the-next-steps}

Una vez que haya aprendido a crear y administrar el contenido de la aplicación en el panel de la aplicación, consulte los siguientes recursos para otras funciones de creación:

* [El icono Administrar aplicación](/help/mobile/phonegap-app-details-tile.md)
* [Edición de metadatos de la aplicación](/help/mobile/phonegap-editmetadata.md)
* [Definiciones de aplicaciones](/help/mobile/phonegap-app-definitions.md)
* [Creación de una aplicación nueva mediante el Asistente para crear aplicación](/help/mobile/phonegap-create-new-app.md)
* [Importar una aplicación híbrida existente](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Additional Resources {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los siguientes recursos:

* [Desarrollo para Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
