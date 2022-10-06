---
title: El verificador de vínculos
description: El verificador de vínculos ayuda a validar vínculos internos y externos, y permite la reescritura de vínculos.
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
source-git-commit: 0b9de3261d8747f3e7107962b6aea1dbdf9d6773
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# El verificador de vínculos {#the-link-checker}

Los autores de contenido no deben preocuparse por validar cada vínculo que incluyen en sus páginas de contenido.

El verificador de vínculos se ejecuta automáticamente para ayudar a los autores de contenido con sus vínculos, incluidos:

* Validación de vínculos a medida que se añaden al contenido
* Mostrar una lista de todos los vínculos externos en el contenido
* Realización de transformaciones de vínculos

El verificador de enlaces tiene una serie de [opciones de configuración](#configuring) como definir la validación interna, permitir que se omitan ciertos vínculos o patrones de vínculo de la validación y reescribir reglas de reescritura de vínculos.

El verificador de vínculos valida ambos [vínculos internos](#internal) y [vínculos externos.](#external)

>[!NOTE]
>
>Como el verificador de vínculos comprueba los vínculos de todas las páginas de contenido, el verificador de vínculos puede afectar al rendimiento en repositorios grandes. En estos casos, es posible que necesite [configurar la frecuencia con la que se ejecuta el verificador de vínculos](#configuring) o [deshabilitarlo.](#disabling)

## Comprobación de vínculos internos {#internal}

Los vínculos internos son vínculos a otro contenido del repositorio de AEM. Los vínculos internos se pueden agregar utilizando el selector de rutas RTE o utilizando un componente personalizado. Por ejemplo:

* Su página `/content/wknd/us/en/adventures/ski-touring.html`
* Incluir un vínculo a `/content/wknd/us/en/adventures/extreme-ironing.html` en un [Componente de texto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Los vínculos internos se validan en cuanto el autor de contenido añade un vínculo interno a una página. Si el vínculo deja de ser válido:

* Se elimina del editor. El texto del vínculo permanece, pero se elimina el vínculo en sí.
* Se muestra como un vínculo roto en la interfaz de creación.

![Vínculo interno roto al crear una página](assets/link-checker-invalid-link-internal.png)

## Comprobación de vínculos externos {#external}

Los vínculos externos son vínculos a contenido fuera del repositorio de AEM. Los vínculos externos se pueden agregar utilizando RTE o utilizando un componente personalizado. Por ejemplo:

* Su página `/content/wknd/us/en/adventures/ski-touring.html`
* Incluir un vínculo a `https://bunwarmerthermalunderwear.com` en un [Componente de texto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

Los vínculos externos se validan para verificar la sintaxis y su disponibilidad. Esta comprobación se realiza asincrónicamente en un servidor interno configurable. Si el verificador de vínculos encuentra un vínculo externo no válido:

* Se elimina del editor. El texto del vínculo permanece, pero se elimina el vínculo en sí.
* Se muestra como un vínculo roto en la interfaz de creación.

![Vínculo interno roto al crear una página](assets/link-checker-invalid-link-external.png)

Además, la variable [Comprobador de vínculos externos](#external-link-checker) proporciona información general sobre todos los vínculos externos de las páginas de contenido.

### Uso del Comprobador de vínculos externos {#external-link-checker}

Para utilizar el Comprobador de vínculos externos:

1. Uso **Navegación**, seleccione **Herramientas**, luego **Sitios**.
1. Select **Comprobador de vínculos externos** y se muestra una lista de todos los vínculos externos.

![La ventana Comprobador de vínculos externos](assets/external-link-checker.png)

Se muestra la siguiente información:

* **Estado** - El estado de validación del vínculo que puede ser uno de los siguientes:
   * **Válido** - El verificador de enlaces puede acceder al enlace externo
   * **Pendiente** - El vínculo externo se agregó al contenido del sitio, pero el verificador de vínculos aún no lo ha validado
   * **No válido** - El verificador de enlaces no puede acceder al vínculo externo
* **URL** - El vínculo externo
* **Referente** - La página de contenido que contiene el vínculo externo
   * Esto solo se rellena [si está configurado.](#configuring)
* **Última comprobación** - La última vez que el verificador de enlaces validó el vínculo externo
   * La frecuencia con la que se comprueban los vínculos [se puede configurar.](#configuring)
* **Último estado** - El último código de estado del HTML devuelto cuando el vínculo activado por última vez marcó el vínculo externo
* **Última disponibilidad** - Tiempo transcurrido desde la última vez que el vínculo estuvo disponible para el verificador de vínculos
* **Último acceso** : tiempo transcurrido desde la última vez que se accedió a la página con el vínculo externo en la interfaz de creación

Puede manipular el contenido de la ventana utilizando los dos botones de la parte superior de la lista de vínculos:

* **Actualizar** - Para actualizar el contenido de la lista
* **Marque** - Para comprobar un vínculo externo individual seleccionado en la lista

### Cómo funciona el verificador de vínculos externos {#how-it-works}

A pesar de ser fácil de usar, el Comprobador de vínculos externos se basa en una serie de servicios y su comprensión de cómo funcionan le ayuda a comprender cómo hacerlo. [configurar el verificador de vínculos](#configuring) para satisfacer sus necesidades.

1. Cada vez que un autor de contenido guarda un vínculo a una página, se activa un controlador de eventos.
1. El controlador de eventos atraviesa todo el contenido en `/content` y comprueba si hay vínculos nuevos o actualizados y los agrega a una caché para el verificador de vínculos.
1. La variable **Servicio Day CQ Link Checker** a continuación, se ejecuta en una programación regular para comprobar la sintaxis válida de las entradas de la caché.
1. Los vínculos validados por la sintaxis aparecen en la [Comprobador de vínculos externos](#external-link-checker) ventana. Sin embargo, estarán en un **Pendiente** estado.
1. La variable **Tarea del verificador de vínculos de CQ de día** a continuación, se ejecuta de forma regular para validar los vínculos realizando una llamada de GET.
1. La variable **Tarea del verificador de vínculos de CQ de día** a continuación, actualiza las entradas de la ventana Comprobador de vínculos externos con los resultados de las llamadas de GET.

## Configuración del verificador de vínculos {#configuring}

El verificador de vínculos está disponible automáticamente de forma predeterminada en AEM. Sin embargo, hay varias configuraciones de OSGi que se pueden modificar para cambiar su comportamiento:

* **Servicio de almacenamiento de información del Verificador de enlaces CQ Day** - Este servicio define el tamaño de la caché de Link Checker en el repositorio.
* **Servicio Day CQ Link Checker** - Este servicio realiza una comprobación asincrónica de la sintaxis de los vínculos externos. Puede definir el periodo de comprobación y qué tipos de vínculos se omiten mediante el comprobador, entre otras opciones.
* **Tarea del verificador de vínculos de CQ de día** - Este servicio lleva a cabo la validación de GET de enlaces externos. Permite distintas definiciones de intervalos para comprobar los vínculos malos y buenos, entre otras opciones.
* **Transformador del verificador de vínculos de CQ de día** : permite convertir vínculos en función de un conjunto de reglas definido por el usuario.

Consulte el documento [Ajustes de configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md) para obtener más información sobre cómo cambiar la configuración de OSGi.

## Desactivación del verificador de vínculos {#disabling}

Puede optar por desactivar por completo el verificador de enlaces. Para ello:

1. Abra la consola OSGi.
1. Edite el **Transformador del verificador de vínculos de CQ de día**
1. Marque las opciones que desee desactivar:
   * **Deshabilitar comprobación** - para desactivar la validación de vínculos
   * **Desactivar reescritura** - para desactivar las transformaciones de vínculos

>[!NOTE]
>
>Si desactiva la comprobación de vínculos después de empezar a crear el contenido, es posible que siga viendo entradas en la variable [Ventana Comprobador de vínculos externos](#external-link-checker), pero ya no se actualizarán.
