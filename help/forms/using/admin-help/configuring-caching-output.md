---
title: Configuración del almacenamiento en caché para Output
seo-title: Configuración del almacenamiento en caché para Output
description: El servicio Output almacena en caché los diseños de formulario, los fragmentos y las imágenes. Obtenga información sobre cómo configurar el almacenamiento en caché para la salida.
seo-description: El servicio Output almacena en caché los diseños de formulario, los fragmentos y las imágenes. Obtenga información sobre cómo configurar el almacenamiento en caché para la salida.
uuid: 00bffeb5-c9c4-4a46-98b5-e14ec9f4514e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5398abd-f62c-485d-9f4b-a316c0de2b6b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---


# Configuración del almacenamiento en caché para Output {#configuring-caching-for-output}

El servicio Output combina los datos de formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos.

La página Salida de la consola de administración contiene opciones que controlan la forma en que el servicio Output almacena en caché los elementos. Puede ajustar esta configuración para optimizar el rendimiento del servicio Output.

El servicio Output almacena en caché los siguientes elementos:

* **diseños de formulario:** El servicio Output almacena en caché los diseños de formulario que recupera desde el repositorio o desde orígenes HTTP. Este almacenamiento en caché mejora el rendimiento porque, para solicitudes de procesamiento posteriores, el servicio Output recupera el diseño de formulario de la caché en lugar de del repositorio.
* **fragmentos e imágenes:** el servicio Output puede almacenar en caché fragmentos e imágenes utilizados en diseños de formulario. Cuando el servicio Output almacena en caché estos objetos, mejora el rendimiento porque los fragmentos y las imágenes solo se leen desde el repositorio en la primera solicitud.

Output almacena la caché en dos ubicaciones:

* **en la memoria:** los elementos se almacenan en la memoria para un acceso rápido. La caché en memoria tiene un tamaño limitado y se elimina al reiniciar el servidor.
* **en disco:** los elementos se almacenan en el sistema de archivos del servidor. La caché de disco tiene una capacidad mayor que la caché en memoria y se conserva al reiniciar el servidor. La ubicación de la caché de disco depende del servidor de aplicaciones. Para obtener información sobre cómo cambiar la ubicación de la caché de disco, consulte [Especificar ubicaciones de archivos para Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Especificación del modo de caché {#specifying-the-cache-mode}

Output admite dos modos de almacenamiento en caché:

* incondicional
* uso del punto de comprobación de caché

Si cambia entre los modos de caché, reinicie el servicio Output para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte [Inicio o detenga los servicios asociados con los módulos de formularios de AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

El tiempo del punto de comprobación de la caché se restablece automáticamente al cambiar entre modos.

### Uso del almacenamiento en caché incondicional {#using-unconditional-caching}

En este modo, cuando el servicio Output recibe una solicitud, valida los recursos (diseño de formulario y cualquier recurso relacionado, como fragmentos e imágenes) que sean necesarios. El servicio Output compara la marca de tiempo de los recursos del repositorio con la marca de tiempo de los recursos de la caché. Si el recurso de la caché es anterior, el servicio Output lo actualiza.

Este modo de caché garantiza el uso de los recursos más recientes. Sin embargo, el rendimiento se ve afectado porque el servicio Output valida los elementos en caché con el repositorio con cada solicitud. Este modo de caché es adecuado para entornos de desarrollo y ensayo en los que los recursos se actualizan con frecuencia y el rendimiento no es un problema principal.

**Especificar almacenamiento en caché incondicional**

1. En la consola de administración, haga clic en Servicios > salida.
1. En Ajustes de control de caché de salida, seleccione Incondicionalmente y haga clic en Guardar.

### Usar el punto de comprobación de caché {#use-the-cache-check-point}

En este modo, el servicio Output solo comprueba en el repositorio si hay versiones más recientes de los recursos cuando la marca de tiempo del recurso en caché es anterior a la hora del punto de comprobación de la caché. La hora del último punto de comprobación de caché se muestra en la página Salida de la Consola de administración.

Utilice este modo de caché en entornos de producción de alto rendimiento en los que el rendimiento es un problema y los cambios en los recursos son poco frecuentes. Puede restablecer la hora del punto de comprobación de la caché cuando desee implementar los cambios realizados en los recursos del repositorio.

**Especificar el uso de un punto de comprobación de caché**

1. En la Consola de administración, haga clic en Servicios > salida.
1. En Ajustes de control de caché de salida, seleccione Solo si la última validación se realizó antes de la hora del punto de comprobación de caché y haga clic en Guardar.

**Restablecer el punto de comprobación de caché**

1. En la consola de administración, haga clic en Servicios > salida.
1. En Ajustes de control de caché de salida, haga clic en Punto de comprobación de caché.

### Restablecer el contenido de la caché {#reset-the-cache-contents}

Puede borrar el contenido de la caché en cualquier momento. Después de restablecer la caché, la primera solicitud para cada formulario es más lenta porque el servicio Output realiza una representación completa y crea nuevo contenido en la caché.

1. En la consola de administración, haga clic en Servicios > salida.
1. En Ajustes de control de caché de salida, haga clic en Restablecer caché.

## Configuración de la configuración de caché {#configuring-cache-settings}

Puede especificar la configuración que Output utiliza para el procesamiento en caché, que puede optimizar el rendimiento del entorno de formularios AEM.

Para acceder a esta configuración, en la consola de administración, haga clic en Servicios > salida.

>[!NOTE]
>
>Los requisitos de disco para la caché deben ser iguales al repositorio.

### Especificación de la configuración de caché global {#specifying-global-cache-settings}

La configuración del área **Configuración global de caché** afecta a todos los tipos de cachés. Si cambia cualquiera de estas opciones, reinicie el servicio Output para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte [Inicio o detenga los servicios asociados con los módulos de formularios de AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño máximo de Documento de caché (KB):** el tamaño máximo, en kilobytes, de un diseño de formulario u otro recurso que se puede almacenar en cualquier caché en memoria. Esta es una configuración global que se aplica a todas las memorias caché. Si el recurso es mayor que este valor, no se almacena en la memoria caché. El valor predeterminado es 1024 kilobytes. Esta configuración no afecta a la caché de disco.

**Caché de procesamiento de formularios habilitada:** de forma predeterminada, esta opción está seleccionada, lo que significa que los formularios procesados se almacenan en la caché para su posterior recuperación. Esta configuración tiene poco efecto en el rendimiento del servicio Output porque no almacena en caché documentos no interactivos. Esta opción tiene un efecto cuando se utiliza el servicio Output en documentos no interactivos procesados en el cliente.

### Almacenamiento en caché de diseños de formulario {#caching-form-designs}

Cuando el servicio Output recibe una solicitud de procesamiento, recupera el diseño de formulario del repositorio o de un origen HTTP y lo almacena en caché. Este almacenamiento en caché mejora el rendimiento porque, para solicitudes de procesamiento posteriores, el servicio Output recupera el diseño de formulario de la caché en lugar de del repositorio.

El servicio Output siempre almacena en caché los diseños de formulario en el disco. Si los diseños de formulario se almacenan en el servidor, dichos archivos se consideran la caché de disco. El servicio Output también almacena en caché los diseños de formulario en la memoria, según la configuración del área **Caché de plantilla de memoria**. Si cambia cualquiera de estas opciones, reinicie el servicio Output para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte [Inicio o detenga los servicios asociados con los módulos de formularios de AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño de caché de configuración de plantilla:** el número máximo de objetos de configuración de plantilla que se deben mantener en memoria. El valor predeterminado es 100. Se recomienda definir este valor bueno o igual al valor Tamaño de caché de plantilla. Esta configuración no afecta a la caché de disco.

**Tamaño de caché de plantilla:** el número máximo de objetos de contenido de plantilla que se van a conservar en memoria. El valor predeterminado es 100. Esta configuración no afecta a la caché de disco.

**Habilitado:** de forma predeterminada, esta casilla de verificación está seleccionada, lo que significa que las plantillas de formulario se almacenan en la memoria caché. Cuando esta opción no está seleccionada, las plantillas de formulario se almacenan en caché solo en disco.

### Almacenamiento en caché de fragmentos e imágenes {#caching-fragments-and-images}

El servicio Output almacena en caché fragmentos e imágenes que se utilizan en diseños de formulario en disco. Esto mejora el rendimiento porque los fragmentos y las imágenes solo se leen desde el repositorio en la primera solicitud. A continuación, en solicitudes posteriores, el servicio Output lee fragmentos e imágenes de la caché de disco. Los fragmentos y las imágenes solo se almacenan en caché en el disco y no en la memoria.

Puede utilizar los siguientes ajustes para controlar el almacenamiento en caché en disco de fragmentos e imágenes. Esta configuración se encuentra en el área **Configuración de caché de recursos de plantilla**:

**Almacenamiento en** caché de recursosSeleccione una de las siguientes opciones de la lista:

**Habilitado para fragmentos e imágenes:** el servicio Output almacena en caché fragmentos e imágenes. Ésta es la opción predeterminada.

**Habilitado para fragmentos:** el servicio Output almacena en caché fragmentos, pero no imágenes.

**Deshabilitado:** el servicio Output no almacena en caché fragmentos ni imágenes.

**Intervalo de limpieza (segundos):** especifica la frecuencia con la que el servicio Output elimina los antiguos archivos de caché no válidos. El servicio Output no elimina los archivos de caché válidos. Si cambia el intervalo de limpieza, reinicie el servicio Output para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte Inicio o detenga los servicios asociados con los módulos de formularios de AEM para obtener instrucciones.

## Consideraciones de clúster para cachés {#clustering-considerations-for-caches}

En un entorno agrupado, cada nodo mantiene su propia memoria y caché de disco. El contenido de la caché de cada nodo depende de qué formularios se han procesado en ese nodo.

La ubicación de la caché debe ser idéntica (el mismo disco y la misma ruta) en cada nodo del clúster. No coloque la caché en el almacenamiento compartido.

Si utiliza la página Salida en la consola de administración para cambiar la configuración de caché de un nodo concreto, la configuración de caché de otros nodos se actualiza cuando se envía una solicitud a ese nodo. Este comportamiento también se aplica al botón Restablecer caché. Si hace clic en el botón Restablecer caché para un nodo, la caché se elimina inmediatamente de ese nodo. La caché en otros nodos se borra cuando una solicitud se dirige a ese nodo.
