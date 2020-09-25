---
title: Configuración manual de la integración con Adobe Target
seo-title: Configuración manual de la integración con Adobe Target
description: Obtenga información sobre cómo configurar manualmente la integración con Adobe Target.
seo-description: Obtenga información sobre cómo configurar manualmente la integración con Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 4%

---


# Configuración manual de la integración con Adobe Target {#manually-configuring-the-integration-with-adobe-target}

Puede modificar las configuraciones del asistente para la selección que realizó al utilizar el asistente o puede integrarlas manualmente con Adobe Target sin necesidad de utilizar el asistente.

## Modificación de las configuraciones del Asistente para la selección {#modifying-the-opt-in-wizard-configurations}

El asistente [para](/help/sites-administering/opt-in.md) la selección que [integra AEM con Adobe Target](/help/sites-administering/target.md) crea automáticamente una configuración de nube de Destinatario denominada Configuración de Destinatario aprovisionado. El asistente también crea un marco de Destinatario para la configuración de nube denominada Destinatario aprovisionado. Si es necesario, puede modificar las propiedades de la configuración de nube y del marco.

También puede configurar Adobe Target para que utilice Adobe Target como origen de sistema de informes al destinar contenido mediante la configuración de A4T Analytics Cloud.

Para localizar la configuración de nube y el marco, vaya a **Cloud Services** a través de **Herramientas** > **Implementación** > **Nube**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))Debajo de Adobe Target, toque o haga clic en **Mostrar configuraciones**.

### Propiedades de configuración de Destinatario aprovisionadas {#provisioned-target-configuration-properties}

Los siguientes valores de propiedad se utilizan en la configuración de nube de configuración de Destinatario aprovisionada que crea el asistente para la selección:

* **Código de cliente:** Tal como se especificó en el asistente para la selección.
* **Correo electrónico:** Tal como se especificó en el asistente para la selección.
* **Contraseña:** Tal como se especificó en el asistente para la selección.
* **Tipo de API:** REST
* **Sincronizar segmentos desde Adobe Target:** Seleccionado.

* **Biblioteca de cliente:** mbox.js.
* **Utilice la DTM para distribuir la biblioteca del cliente:** No seleccionado. Seleccione esta opción si [utiliza la DTM](/help/sites-administering/dtm.md) u otro sistema de administración de etiquetas para alojar el archivo mbox.js o AT.js. Adobe recomienda utilizar la DTM en lugar de AEM para distribuir la biblioteca.

* **Mbox.js personalizado:** No se especificó ninguna para que se utilice el archivo mbox.js predeterminado. Especifique un archivo mbox.js personalizado para utilizarlo según sea necesario. Solo aparece si ha seleccionado mbox.js.
* **AT.js personalizado:** No se especificó ninguna para que se utilice el archivo AT.js predeterminado. Especifique un archivo AT.js personalizado para utilizarlo según sea necesario. Solo aparece si ha seleccionado AT.js.

>[!NOTE]
>
>En AEM 6.3, puede seleccionar el archivo de biblioteca de Destinatarios, [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html), que es una nueva biblioteca de implementación para Adobe Target diseñada tanto para implementaciones web típicas como para aplicaciones de una sola página.
>
>AT.js oferta varias mejoras con respecto a la biblioteca mbox.js:
>
>* Se han mejorado los tiempos de carga de las páginas para implementaciones web
>* Seguridad mejorada
>* Mejores opciones de implementación para aplicaciones de una sola página
>* AT.js contiene los componentes que se incluyeron en destinatario.js, por lo que ya no hay una llamada a destinatario.js


### Propiedades de Destinatario Framework aprovisionadas {#provisioned-target-framework-properties}

El módulo Destinatario aprovisionado que crea el asistente para la selección está configurado para enviar datos de contexto desde el almacén de datos de Perfil. Los elementos de datos de edad y sexo de la tienda se envían al Destinatario de forma predeterminada. Es probable que la solución requiera que se envíen parámetros adicionales.

![chlimage_1-158](assets/chlimage_1-158.png)

Puede configurar la estructura para que envíe información de contexto adicional a Destinatario, tal como se describe al [Añadir un marco](/help/sites-administering/target-configuring.md#adding-a-target-framework)de Destinatario.

### Configuring A4T Analytics Cloud Configuration {#configuring-a-t-analytics-cloud-configuration}

Puede configurar Adobe Target para que utilice Adobe Analytics como origen de sistema de informes al destinar contenido.

Para ello, debe especificar la configuración de nube de A4T con la que conectar la configuración de nube de Adobe Target:

1. Vaya a **Cloud Services** mediante el logotipo **** AEM > **Herramientas** > **Implementación** > **Cloud Services**.
1. En la sección **Adobe Target** , haga clic en **Configurar ahora**.
1. Vuelva a conectarse a la configuración de Adobe Target.
1. En el menú desplegable Configuración **de Analytics Cloud de** A4T, seleccione el marco.

   >[!NOTE]
   >
   >Solo están disponibles las configuraciones de análisis habilitadas para A4T.
   >
   >Al configurar A4T con AEM, es posible que vea que falta una entrada de referencia de configuración. Para poder seleccionar el marco de análisis, haga lo siguiente:
   >
   >1. Vaya a **Herramientas** > **General** > **CRXDE Lite**.
   1. Vaya a **/libs/cq/analytics/components/testandtargetpage/dialog/items/tab/items/items/items/tab1_general/items/a4tConfiguración de Analytics**
   1. Establezca la propiedad **disable** en **false**.
   1. Tap or click **Save All**.


   ![chlimage_1-159](assets/chlimage_1-159.png)

   Haga clic en **Aceptar**. Cuando destinatario contenido con Adobe Target, puede [seleccionar el origen](/help/sites-authoring/content-targeting-touch.md)del informe.

## Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target}

Integración manual con Adobe Target en lugar de utilizar el asistente para la selección.

>[!NOTE]
El archivo de biblioteca de Destinatario, [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html), es una nueva biblioteca de implementación para Adobe Target que está diseñada tanto para implementaciones web típicas como para aplicaciones de una sola página. Adobe recomienda utilizar AT.js en lugar de mbox.js como biblioteca de cliente.
AT.js oferta varias mejoras con respecto a la biblioteca mbox.js:
* Se han mejorado los tiempos de carga de las páginas para implementaciones web
* Seguridad mejorada
* Mejores opciones de implementación para aplicaciones de una sola página
* AT.js contiene los componentes que se incluyeron en destinatario.js, por lo que ya no hay una llamada a destinatario.js

Puede seleccionar AT.js o mbox.js en el menú desplegable Biblioteca **de** cliente.

### Creación de una configuración de Destinatario Cloud {#creating-a-target-cloud-configuration}

Para habilitar AEM para interactuar con Adobe Target, cree una configuración de nube de Destinatario. Para crear la configuración, debe proporcionar el código de cliente y las credenciales de usuario de Adobe Target.

La configuración de la nube de Destinatario solo se crea una vez porque se puede asociar la configuración con varias campañas de AEM. Si tiene varios códigos de cliente de Adobe Target, cree una configuración para cada código de cliente.

Puede configurar la configuración de nube para sincronizar segmentos desde Adobe Target. Si activa la sincronización, los segmentos se importan desde Destinatario en segundo plano en cuanto se guarda la configuración de la nube.

Utilice el procedimiento siguiente para crear una configuración de nube de Destinatario en AEM:

1. Vaya a **Cloud Services** mediante el logotipo **** AEM > **Herramientas** > **Implementación** > **Cloud Services**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   Se abre la página de información general de **Adobe Marketing Cloud** .

1. En la sección **Adobe Target** , haga clic en **Configurar ahora**.
1. En el cuadro de diálogo **Crear configuración** :

   1. Asigne un **Título** a la configuración.
   1. Seleccione la plantilla Configuración **de** Adobe Target.
   1. Haga clic en **Crear**.

   Se abre el cuadro de diálogo de edición.

   ![chlimage_1-160](assets/chlimage_1-160.png)

   >[!NOTE]
   Al configurar A4T con AEM, es posible que vea que falta una entrada de referencia de configuración. Para poder seleccionar el marco de análisis, haga lo siguiente:
   1. Vaya a **Herramientas** > **General** > **CRXDE Lite**.
   1. Vaya a **/libs/cq/analytics/components/testandtargetpage/dialog/items/tab/items/items/items/tab1_general/items/a4tConfiguración de Analytics**
   1. Establezca la propiedad **disable** en **false**.
   1. Tap or click **Save All**.


1. En el cuadro de diálogo, proporcione valores para estas propiedades.

   * **Código** de cliente: el código de cliente de la cuenta de Destinatario
   * **Correo** electrónico: el correo electrónico de la cuenta de Destinatario.
   * **Contraseña**: la contraseña de la cuenta de Destinatario.
   * **Tipo** de API: REST o XML
   * **Configuración** de A4T Analytics Cloud: Seleccione la configuración de nube de Analytics que se utiliza para las métricas y los objetivos de actividad de destinatario. Esto es necesario si utiliza Adobe Analytics como fuente de sistema de informes al destinar contenido. Si no ve la configuración de nube, consulte la nota en [Configuración](#configuring-a-t-analytics-cloud-configuration)de A4T Analytics Cloud.

   * **Usar objetivos precisos:** De forma predeterminada, esta casilla de verificación está activada. Si se selecciona, la configuración del servicio en la nube esperará a que se cargue el contexto antes de cargar el contenido. Véase la nota siguiente.
   * **Sincronizar segmentos desde Adobe Target:** Seleccione esta opción para descargar los segmentos definidos en Destinatario y utilizarlos en AEM. Debe seleccionar esta opción cuando la propiedad Tipo de API sea REST, ya que los segmentos en línea no son compatibles y siempre debe utilizar segmentos de Destinatario. (Tenga en cuenta que el término AEM de &#39;segmento&#39; equivale al Destinatario &#39;audiencia&#39;).
   * **Biblioteca de cliente:** Seleccione si desea la biblioteca de cliente mbox.js o AT.js.
   * **Utilice la DTM para entregar la biblioteca** de cliente: seleccione esta opción para utilizar AT.js o mbox.js de la DTM o de otro sistema de administración de etiquetas. Debe [configurar la integración](/help/sites-administering/dtm.md) de DTM para utilizar esta opción. Adobe recomienda utilizar la DTM en lugar de AEM para distribuir la biblioteca.
   * **Mbox.js** personalizado: Déjelo en blanco si ha marcado la casilla de la DTM o para usar el mbox.js predeterminado. También puede cargar el archivo mbox.js personalizado. Solo aparece si ha seleccionado mbox.js.
   * **AT.js** personalizado: Deje en blanco si ha marcado la casilla de la DTM o para utilizar el valor predeterminado de AT.js. Como alternativa, cargue su AT.js personalizado. Solo aparece si ha seleccionado AT.js.

   >[!NOTE]
   De forma predeterminada, cuando se selecciona en el asistente de configuración de Adobe Target, la segmentación precisa está activada.
   La segmentación precisa significa que la configuración del servicio en la nube espera a que se cargue el contexto antes de cargar el contenido. Como resultado, en términos de rendimiento, la segmentación precisa puede crear un retraso de unos milisegundos antes de cargar el contenido.
   La segmentación precisa siempre está habilitada en la instancia de creación. Sin embargo, en la instancia de publicación, puede desactivar la segmentación precisa globalmente borrando la marca de verificación junto a Objetivo preciso en la configuración del servicio en la nube (**http://localhost:4502/etc/cloudservices.html**). También puede activar y desactivar la segmentación precisa para componentes individuales independientemente de la configuración del servicio en la nube.
   Si ***ya*** ha creado componentes de destino y cambia esta configuración, los cambios no afectarán a dichos componentes. Debe realizar cambios directamente en esos componentes.

1. Haga clic en **Conectar a Destinatario** para inicializar la conexión con Destinatario. Si la conexión se realiza correctamente, se muestra el mensaje **Conexión correcta** . Haga clic en **Aceptar** en el mensaje y, a continuación, en **Aceptar** en el cuadro de diálogo.

   Si no puede conectarse a Destinatario, consulte la sección de [solución de problemas](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) .

### Añadir un Destinatario Framework {#adding-a-target-framework}

Después de configurar la nube de Destinatario, agregue una estructura de Destinatario. La estructura identifica los parámetros predeterminados que se envían a Adobe Target desde los componentes [Client Context](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) disponibles. Destinatario utiliza los parámetros para determinar los segmentos que se aplican al contexto actual.

Puede crear varios marcos para una sola configuración de Destinatario. Los marcos de trabajo múltiples son útiles cuando necesita enviar un conjunto diferente de parámetros a Destinatario para diferentes secciones del sitio web. Cree un marco para cada conjunto de parámetros que necesite enviar. Asocie cada sección del sitio Web con la estructura adecuada. Tenga en cuenta que una página web solo puede utilizar un marco de trabajo a la vez.

1. En la página de configuración de Destinatario, haga clic en el **+** (signo más) situado junto a Marcos disponibles.
1. En el cuadro de diálogo Crear marco, especifique un **título**, seleccione **Adobe Target Framework** y haga clic en **Crear**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

   Se abre la página del marco. La barra de tareas proporciona componentes que representan información de [Client Context](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) que se puede asignar.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Arrastre el componente ClientContext que representa los datos que desea utilizar para la asignación al destinatario de colocación. Como alternativa, arrastre **el componente de la Tienda** ContextHub al marco.

   >[!NOTE]
   Al realizar la asignación, los parámetros se pasan a un mbox a través de cadenas sencillas. No se pueden asignar matrices desde ContextHub.

   Por ejemplo, para utilizar Datos **de** Perfil sobre los visitantes del sitio para controlar la campaña de Destinatario, arrastre el componente Datos **de** Perfil a la página. Aparecerán las variables de datos de perfil disponibles para la asignación a parámetros de Destinatario.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Seleccione las variables que desea que el sistema Adobe Target pueda ver seleccionando la casilla de verificación **Compartir** en las columnas correspondientes.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   La sincronización de parámetros es de una sola manera: de AEM a Adobe Target.

Se crea el marco. Para replicar el marco en la instancia de publicación, utilice la opción **Activar marco** de la barra de tareas.

### Asociación de Actividades con la configuración de Destinatario Cloud  {#associating-activities-with-the-target-cloud-configuration}

Asocie sus [AEM actividades](/help/sites-authoring/activitylib.md) con la configuración de la nube de Destinatario para que pueda reflejar las actividades en [Adobe Target](https://docs.adobe.com/content/help/en/target/using/experiences/offers/manage-content.html).

>[!NOTE]
Los tipos de actividades estarán disponibles dependiendo de lo siguiente:
* Si la opción **xt_only** está habilitada en el inquilino de Adobe Target (clientcode) que se usa en el lado AEM para conectar con Adobe Target, **solo** puede crear actividades de XT en AEM.

* Si las opciones **xt_only** **no** están habilitadas en el inquilino de Adobe Target (clientcode), puede crear **ambas** actividades de XT y de pruebas A/B en AEM.

**Nota adicional:** las opciones de **xt_only** son una configuración aplicada en un inquilino de Target (clientcode) y sólo se pueden modificar directamente en Adobe Target. No puede activar ni desactivar esta opción en AEM.

### Asociación del Destinatario Framework con el sitio {#associating-the-target-framework-with-your-site}

Después de crear una estructura de Destinatario en AEM, asocie las páginas web con la estructura. Los componentes de destino de las páginas envían los datos definidos por el marco a Adobe Target para su seguimiento. (Consulte Objetivo [de contenido](/help/sites-authoring/content-targeting-touch.md)).

Al asociar una página con el marco, las páginas secundarias heredan la asociación.

1. En la consola **Sitios** , navegue al sitio que desee configurar.
1. Mediante acciones [](/help/sites-authoring/basic-handling.md#quick-actions) rápidas o el modo [](/help/sites-authoring/basic-handling.md)de selección, seleccione Propiedades de **Vista.**
1. Seleccione la ficha **Cloud Services** .
1. Tap/click **Edit**.
1. Toque o haga clic en **Añadir configuración** en Configuraciones **de** Cloud Service y seleccione **Adobe Target**.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Seleccione el marco que desee en Referencia **de configuración**.

   >[!NOTE]
   Asegúrese de seleccionar la **estructura** específica que creó y no la configuración de nube de Destinatario en la que se creó.

1. Toque o haga clic en **Hecho**.
1. Active la página raíz del sitio web para replicarla en el servidor de publicación. (See [How To Publish Pages](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   Si el marco que ha adjuntado a la página aún no se ha activado, se abrirá un asistente que le permitirá publicarlo también.

## Resolución de problemas de conexión de Destinatario {#troubleshooting-target-connection-problems}

Realice las siguientes tareas para solucionar problemas que se producen al conectarse a Destinatario:

* Asegúrese de que las credenciales de usuario proporcionadas son correctas.
* Asegúrese de que la instancia de AEM se puede conectar al servidor de Destinatario. Por ejemplo, asegúrese de que las reglas de firewall no bloquean las conexiones de AEM salientes o que AEM está configurado para usar los proxies necesarios.
* Busque mensajes útiles en el registro de errores de AEM. El archivo error.log se encuentra en el directorio **crx-quickstart/logs** donde está instalado AEM.
* Al editar la actividad en Adobe Target, la dirección URL apunta a localhost. Para solucionar esto, establezca el AEM externalizador en la dirección URL correcta.

