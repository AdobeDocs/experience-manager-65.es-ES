---
title: Configuración del almacenamiento en caché para salida
seo-title: Configuring caching for Output
description: El servicio Output almacena en caché los diseños de formulario, los fragmentos y las imágenes. Aprenda a configurar el almacenamiento en caché para la salida.
seo-description: The Output service caches the form designs, fragments and images. Learn how to configure the caching for output.
uuid: 00bffeb5-c9c4-4a46-98b5-e14ec9f4514e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5398abd-f62c-485d-9f4b-a316c0de2b6b
exl-id: 1015f5c9-6ab8-4656-a5c8-40f82b9938b9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---

# Configuración del almacenamiento en caché para salida  {#configuring-caching-for-output}

El servicio Output combina los datos de formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos.

La página Salida de la consola de administración contiene ajustes que controlan la forma en que el servicio Salida almacena en caché los elementos. Puede ajustar esta configuración para optimizar el rendimiento del servicio de salida.

El servicio Output almacena en caché los siguientes elementos:

* **diseños de formulario:** El servicio Output almacena en caché los diseños de formulario que recupera del repositorio o de los orígenes HTTP. Este almacenamiento en caché mejora el rendimiento porque para las solicitudes de procesamiento posteriores, el servicio Output recupera el diseño de formulario de la caché en lugar de del repositorio.
* **fragmentos e imágenes:** El servicio Output puede almacenar en caché fragmentos e imágenes utilizados en los diseños de formulario. Cuando el servicio Output almacena en caché estos objetos, mejora el rendimiento porque los fragmentos y las imágenes solo se leen desde el repositorio en la primera solicitud.

Output almacena la caché en dos ubicaciones:

* **en memoria:** Los elementos se almacenan en la memoria para un acceso rápido. La caché en memoria tiene un tamaño limitado y se elimina al reiniciar el servidor.
* **en disco:** Los elementos se almacenan en el sistema de archivos del servidor. La caché de disco tiene una capacidad mayor que la caché en memoria y se conserva al reiniciar el servidor. La ubicación de la caché de disco depende del servidor de aplicaciones. Para obtener información sobre cómo cambiar la ubicación de la caché de disco, consulte [Especificar ubicaciones de archivos para la salida](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Especificación del modo de caché {#specifying-the-cache-mode}

La salida admite dos modos de almacenamiento en caché:

* incondicional
* uso del punto de comprobación de caché

Si cambia entre modos de caché, reinicie el servicio Output para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte [Iniciar o detener los servicios asociados con AEM módulos de formularios](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

El tiempo del punto de comprobación de la caché se restablece automáticamente al cambiar entre modos.

### Uso del almacenamiento en caché incondicional {#using-unconditional-caching}

En este modo, cuando el servicio Output recibe una solicitud, valida los recursos (diseño de formulario y recursos relacionados, como fragmentos e imágenes) necesarios. El servicio Output compara la marca de tiempo de los recursos del repositorio con la marca de tiempo de los recursos de la caché. Si el recurso de la caché es anterior, el servicio Output lo actualiza.

Este modo de caché garantiza que se utilicen los recursos más recientes. Sin embargo, el rendimiento se ve afectado porque el servicio Output valida los elementos en caché con el repositorio con cada solicitud. Este modo de caché es adecuado para entornos de desarrollo y ensayo en los que los recursos se actualizan con frecuencia y el rendimiento no es una preocupación principal.

**Especificar almacenamiento en caché incondicional**

1. En la consola de administración, haga clic en Servicios > salida.
1. En Ajustes de control de caché de salida, seleccione Incondicionalmente y haga clic en Guardar.

### Usar el punto de comprobación de caché {#use-the-cache-check-point}

En este modo, el servicio Output solo comprueba el repositorio para ver si hay versiones más recientes de los recursos cuando la marca de tiempo del recurso almacenado en caché es anterior a la hora del punto de comprobación de la caché. La hora del último punto de comprobación de caché se muestra en la página Salida de la Consola de administración.

Utilice este modo de caché en entornos de producción de alto rendimiento en los que el rendimiento es un problema y los cambios en los recursos son poco frecuentes. Puede restablecer el tiempo de comprobación de la caché cuando desee implementar cualquier cambio realizado en los recursos del repositorio.

**Especificar el uso de un punto de comprobación de caché**

1. En la Consola de administración, haga clic en Servicios > salida.
1. En Configuración de control de caché de salida, seleccione Solo si la última validación se realizó antes de la hora de comprobación de caché y haga clic en Guardar.

**Restablecer el punto de comprobación de la caché**

1. En la consola de administración, haga clic en Servicios > salida.
1. En Ajustes de control de caché de salida, haga clic en Punto de comprobación de caché.

### Restablecer el contenido de la caché {#reset-the-cache-contents}

Puede borrar el contenido de la caché en cualquier momento. Después de un restablecimiento de caché, la primera solicitud para cada formulario es más lenta porque el servicio Output realiza una renderización completa y crea nuevo contenido de caché.

1. En la consola de administración, haga clic en Servicios > salida.
1. En Ajustes de control de caché de salida, haga clic en Restablecer caché.

## Configuración de la caché {#configuring-cache-settings}

Puede especificar la configuración que Output utiliza para el almacenamiento en caché, lo que puede optimizar el rendimiento del entorno de formularios AEM.

Para acceder a esta configuración, en la consola de administración, haga clic en Servicios > salida.

>[!NOTE]
>
>Los requisitos de disco para la caché deben ser iguales al repositorio.

### Especificación de la configuración global de caché {#specifying-global-cache-settings}

La configuración de la variable **Configuración de caché global** afecta a todos los tipos de cachés. Si cambia cualquiera de estas opciones, reinicie el servicio Output para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte [Iniciar o detener los servicios asociados con AEM módulos de formularios](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño máximo del documento de caché (KB):** Tamaño máximo, en kilobytes, de un diseño de formulario u otro recurso que se pueda almacenar en cualquier caché en memoria. Esta es una configuración global que se aplica a todas las cachés en memoria. Si el recurso es mayor que este valor, no se almacena en caché en la memoria. El valor predeterminado es 1024 kilobytes. Esta configuración no afecta a la caché del disco.

**Caché de procesamiento de formularios habilitada:** De forma predeterminada, esta opción está seleccionada, lo que significa que los formularios procesados se almacenan en la caché para su posterior recuperación. Esta configuración tiene poco efecto en el rendimiento del servicio Output porque no almacena en caché los documentos no interactivos. Esta opción no tiene ningún efecto cuando se utiliza el servicio Output en documentos no interactivos procesados en el cliente.

### Almacenamiento en caché de diseños de formulario {#caching-form-designs}

Cuando el servicio Output recibe una solicitud de renderización, recupera el diseño de formulario del repositorio o de un origen HTTP y lo almacena en la caché. Este almacenamiento en caché mejora el rendimiento porque para las solicitudes de procesamiento posteriores, el servicio Output recupera el diseño de formulario de la caché en lugar de del repositorio.

El servicio Output siempre almacena en caché los diseños de formulario en el disco. Si los diseños de formulario se almacenan en el servidor, esos archivos se consideran la caché del disco. El servicio Output también almacena en caché los diseños de formulario en la memoria, según la configuración de la variable **En caché de plantilla de memoria** . Si cambia cualquiera de estos ajustes, reinicie el servicio Output para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte [Iniciar o detener los servicios asociados con AEM módulos de formularios](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño de caché de configuración de plantilla:** El número máximo de objetos de configuración de plantilla que se deben mantener en la memoria. El valor predeterminado es 100. Se recomienda establecer este valor bueno o igual al valor Tamaño de caché de plantilla . Esta configuración no afecta a la caché del disco.

**Tamaño de caché de plantilla:** El número máximo de objetos de contenido de plantilla que se deben mantener en la memoria. El valor predeterminado es 100. Esta configuración no afecta a la caché del disco.

**Habilitado:** De forma predeterminada, esta casilla de verificación está seleccionada, lo que significa que las plantillas de formulario se almacenan en la memoria caché. Cuando no se selecciona esta opción, las plantillas de formulario se almacenan en la caché solo en el disco.

### Almacenamiento en caché de fragmentos e imágenes {#caching-fragments-and-images}

El servicio Output almacena en caché fragmentos e imágenes utilizados en diseños de formulario en disco. Esto mejora el rendimiento porque los fragmentos y las imágenes solo se leen desde el repositorio en la primera solicitud. A continuación, en las solicitudes posteriores, el servicio Output lee fragmentos e imágenes de la caché del disco. Los fragmentos y las imágenes se almacenan en caché solo en el disco y no en la memoria.

Puede utilizar la siguiente configuración para controlar el almacenamiento en caché en disco de fragmentos e imágenes. Estos ajustes se encuentran en la variable **Configuración de caché de recursos de plantilla** área:

**Almacenamiento en caché de recursos** Seleccione una de las siguientes opciones de la lista:

**Habilitado para fragmentos e imágenes:** El servicio Output almacena en caché fragmentos e imágenes. Esta es la opción predeterminada.

**Habilitado para fragmentos:** El servicio Output almacena en caché fragmentos, pero no imágenes.

**Deshabilitado:** El servicio Output no almacena en caché fragmentos ni imágenes.

**Intervalo de limpieza (segundos):** Especifica la frecuencia con la que el servicio Output elimina los archivos de caché antiguos no válidos. El servicio Output no elimina los archivos de caché válidos. Si cambia el intervalo de limpieza, reinicie el servicio Output para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte Inicio o parada de los servicios asociados con módulos de formularios AEM para obtener instrucciones.

## Consideraciones sobre clústeres para cachés {#clustering-considerations-for-caches}

En un entorno agrupado, cada nodo mantiene su propia caché en memoria y en disco. El contenido de la caché de cada nodo depende de qué formularios se hayan procesado en ese nodo.

La ubicación de la caché debe ser idéntica (el mismo disco y la misma ruta) en cada nodo del clúster. No coloque la caché en el almacenamiento compartido.

Si utiliza la página Salida en la consola de administración para cambiar la configuración de caché de un nodo concreto, la configuración de caché de otros nodos se actualiza cuando una solicitud va a ese nodo. Este comportamiento también se aplica al botón Restablecer caché. Si hace clic en el botón Restablecer caché para un nodo, la caché se elimina inmediatamente de ese nodo. La caché de otros nodos se borra cuando una solicitud va a ese nodo.
