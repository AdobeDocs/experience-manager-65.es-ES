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
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---


# Creación y administración del contenido de la aplicación{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

La administración del contenido de la aplicación requiere un esfuerzo colectivo de [desarrolladores](#developer), [autores](#author) y [administradores](#administrator). Los autores manipulan las páginas, que a su vez se basan en plantillas y componentes generados por los desarrolladores de la aplicación.

Por último, los administradores publican estratégicamente el contenido actualizado de la aplicación.

>[!NOTE]
>
>**Requisitos previos**:
>
>En [Implementación y mantenimiento](/help/sites-deploying/deploy.md), los desarrolladores se familiarizaron con AEM sistema de componentes y plantillas.

## El icono Administrar contenido de página {#the-manage-page-content-tile}

>[!CAUTION]
>
>Si no utiliza una plantilla de aplicación lista para usar, para permitir que se publique contenido de aplicación nuevo en OTA, debe configurar un controlador de sincronización de contenido.
>
>Consulte [Mobile with Content Sync](/help/mobile/phonegap-contentsync.md) en la sección del programador para obtener más información.

Aquí, el contenido se puede crear, editar y eliminar en AEM Mobile de la misma manera que lo haría en AEM Sites.

El **mosaico Administrar contenido de página** muestra el número de páginas de contenido administrado y la última modificación para una carga útil concreta. Puede profundizar en el contenido para crear, copiar, mover, eliminar y actualizar páginas haciendo clic en cada registro del mosaico.

Una vez actualizado el contenido, los administradores pueden publicar una carga útil de actualización de contenido sobre el aire (OTA) para los clientes a través del mosaico **Administrar paquetes de contenido.**

![chlimage_1-161](assets/chlimage_1-161.png)

Seleccione uno de los paquetes de contenido de la lista para crear o editar contenido, como crear, editar o eliminar páginas, cambiar la navegación y el orden de las páginas, crear o actualizar contenido como copiar (texto) y medios.

Nota *todo es contenido*, lo que significa que los estilos de aplicación, la copia (texto), los medios, las páginas, la navegación y la segmentación de contenido pueden editarse y actualizarse sin necesidad de visitar una tienda de aplicaciones.

Para editar el contenido de AEM Mobile, *AEM autores *necesitarán una sólida comprensión de AEM interfaz de edición de contenido: [Creación de páginas en AEM.](/help/sites-authoring/qg-page-authoring.md)

## El icono Administrar paquetes de contenido {#the-manage-content-packages-tile}

Aquí, *Los administradores de AEM* pueden actualizar rápida y fácilmente sus aplicaciones para ofrecer experiencias atractivas y contenido actualizado con el fin de impulsar la participación de la marca y cumplir los objetivos comerciales, todo sin necesidad de un programador o un reenvío de App Store.

![chlimage_1-162](assets/chlimage_1-162.png)

Una vez que *AEM Authors* han agregado o modificado contenido a través del icono Administrar contenido, *Los administradores de AEM* pueden insertar estos cambios en los clientes con una actualización de los paquetes de contenido.

La acción Paquete de contenido permite que *AEM Author* cree y edite contenido de página mientras que el equipo de desarrollo realiza cambios en un diseño e implementación de aplicación host que incluyen navegación, estilo, lógica de servidor, plantillas y componentes y, a continuación, envía estos cambios a los clientes sin necesidad de volver a enviarlos a los distintos almacenes para su distribución.

**Para publicar contenido nuevo o actualizado**

Seleccione un paquete de contenido del mosaico, en este ejemplo el paquete inglés. Observe que un cuadro de diálogo de actualización de contenido lista la configuración *Sincronización de contenido* relevante. Si el contenido de la aplicación se ha modificado desde una actualización anterior, el estado mostrará *Pendiente*, como se muestra a continuación.

![chlimage_1-163](assets/chlimage_1-163.png)

A continuación, seleccione la acción **Escenario** en la parte superior derecha para crear la nueva actualización de contenido. Añada la información de actualización adecuada y pulse Listo.

![chlimage_1-164](assets/chlimage_1-164.png)

El controlador *Content Sync* crea los paquetes necesarios formando un delta (un paquete de *sólo* lo que ha cambiado). Una vez completado, este paquete de contenido de actualización se ha escalonado como se muestra a continuación.

El ensayo de una actualización de contenido permite realizar varias actualizaciones antes de publicarlas en OTA en dispositivos móviles.

>[!NOTE]
>
>El contenido escalonado se puede comprobar con la aplicación AEM Verificar antes de publicar.
>
>Consulte [Inicio rápido móvil para AEM Verify](/help/mobile/phonegap-mobile-quickstart.md) para obtener más detalles sobre AEM aplicación de verificación.

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

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un administrador y un desarrollador, consulte los siguientes recursos:

* [Desarrollo para Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Administración de contenido para Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
