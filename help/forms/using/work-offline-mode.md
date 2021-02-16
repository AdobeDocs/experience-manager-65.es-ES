---
title: Trabajar en modo sin conexión
seo-title: Trabajar en modo sin conexión
description: Desconecte el dispositivo móvil fuera del rango de red de AEM Forms o en modo completamente sin conexión y trabaje en la aplicación de AEM Forms
seo-description: Desconecte el dispositivo móvil fuera del rango de red de AEM Forms o en modo completamente sin conexión y trabaje en la aplicación de AEM Forms
uuid: b900a0f8-90ce-486a-bde6-6cdf11bd2801
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9a3c6ab4-8bb9-40c7-8c56-59153b364887
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Trabajar en modo sin conexión {#working-in-the-offline-mode}

El modo sin conexión de la aplicación de AEM Forms le permite trabajar sin problemas incluso si la aplicación se desconecta. Puede abrir, actualizar y enviar un formulario sin necesidad de conectividad de red.

Tiene el inicio de trabajar en la aplicación de AEM Forms sincronizando la aplicación con el servidor de AEM Forms. Todos los formularios asignados se descargan en la aplicación. Para AEM Forms en JEE, las tareas se recuperan en la ficha tareas y los nombres de inicio se asocian a formularios y otros formularios en la ficha Forms. Para AEM Forms en OSGi, solo Forms se carga en la ficha Forms.

Para obtener más información sobre cómo sincronizar la aplicación, consulte [Sincronización de la aplicación](/help/forms/using/sync-app.md).

## Cómo hacer que Forms esté disponible sin conexión {#making-forms-available-offline}

Al sincronizar la aplicación con el servidor de AEM Forms, los formularios se descargan en el dispositivo móvil. Sin embargo, de forma predeterminada, los archivos adjuntos asociados al formulario no se descargan. Esto implica que si está en línea, puede realizar la vista de los archivos adjuntos. Sin embargo, para asegurarse de que puede realizar la vista de los datos adjuntos en el modo sin conexión, cambie la configuración predeterminada de la aplicación.

Para asegurarse de que los archivos adjuntos asociados se descargan con cada formulario, establezca Buscar archivos adjuntos en Activado. Para obtener más información, consulte [Actualización de la configuración general](/help/forms/using/update-general-settings.md).

Dado que la descarga de datos en el dispositivo móvil puede afectar al rendimiento del dispositivo, de forma predeterminada, el ajuste Buscar archivos adjuntos se establece en OFF. Los archivos adjuntos se recuperan en el dispositivo para cualquier tarea que se descargue del servidor después de actualizar la configuración a ON. En el modo sin conexión, un usuario puede trabajar en todas las tareas que se descarguen en el dispositivo después de configurar las opciones **Buscar archivos adjuntos** en Activado.

## Configuración del servicio sin conexión para la aplicación de AEM Forms {#configuring-offline-service-for-aem-forms-app-br}

El servicio sin conexión de la aplicación de AEM Forms identifica los recursos utilizados en un formulario. La aplicación de AEM Forms depende de este servicio para obtener información sobre las dependencias de formularios. Se requiere información sobre las dependencias del formulario para habilitar las funcionalidades sin conexión. El servicio sin conexión de la aplicación de AEM Forms almacena en caché las rutas o direcciones URL de los recursos utilizados en un formulario. La caché se actualiza en función de los cambios en el formulario y del período de validez configurado para el servicio sin conexión. El almacenamiento en caché de rutas o direcciones URL de los recursos utilizados en un formulario mejora el rendimiento en el servidor.

Para configurar el componente sin conexión del lado del servidor de la aplicación de AEM Forms:

1. En la instancia de autor, vaya a **Adobe Experience Manager** >**Herramientas** > **Forms** > **Configurar el servicio sin conexión de la aplicación Forms**.

   URL: `https://<server>:<port>/<context-path>/libs/fd/workspace-offline/gui/content/config.html`

1. En Configuración general, puede realizar lo siguiente:

   * **Borrar caché**: Borra la caché del lado del servidor de las dependencias del formulario.
   * **Restablecer configuración**: Restaura la configuración sin conexión de la aplicación de AEM Forms.
   * **Validez** de caché: Especifica el período de validez de la caché sin conexión del lado del servidor.
   * **Rutas** de observación de recursos: Especifica las rutas en las que el servicio sin conexión supervisa los cambios de recursos. Si se produce algún cambio en las rutas especificadas, se actualiza la caché sin conexión de todos los formularios dependientes. Por ejemplo, `/etc/clientlibs/fd,/content/dam/images`.

1. En la ficha **Caché de recursos manual**, especifique las dependencias de formularios que el servicio sin conexión no puede identificar. Puede especificar recursos como imágenes cargadas desde JavaScript. La aplicación de AEM Forms también descargará estos recursos para el modo sin conexión.
