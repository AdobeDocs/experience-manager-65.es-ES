---
title: Configuración manual de la integración con Adobe Target
description: Obtenga información sobre cómo configurar manualmente la integración con Adobe Target.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 28%

---

# Configuración manual de la integración con Adobe Target {#manually-configuring-the-integration-with-adobe-target}

Puede modificar las configuraciones del asistente de inclusión que realizó al utilizar el asistente o puede integrarlas manualmente con Adobe Target sin utilizar el asistente.

## Modificación de las configuraciones del asistente de Opt-In {#modifying-the-opt-in-wizard-configurations}

El [Asistente de inclusión](/help/sites-administering/opt-in.md) que [AEM se integra con el de Adobe Target](/help/sites-administering/target.md) crea automáticamente una configuración de nube de Target llamada Configuración de Target aprovisionada. El asistente también crea un marco de trabajo de Target para la configuración de nube denominada Marco de trabajo de Target aprovisionado. Si es necesario, puede modificar las propiedades de la configuración y el marco de trabajo de la nube.

También puede configurar Adobe Target para que utilice Adobe Target como fuente de informes al segmentar contenido. Para ello, configure la Configuración de Analytics Cloud de A4T.

Para localizar la configuración de la nube y el marco de trabajo, vaya a **Cloud Service** mediante **Herramientas** > **Implementación** > **Nube**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)) Bajo Adobe Target, haga clic en **Mostrar configuraciones**.

### Propiedades de configuración de Target aprovisionadas {#provisioned-target-configuration-properties}

Los siguientes valores de propiedad se utilizan en la configuración de nube de Configuración de Target aprovisionada que crea el asistente de inclusión:

* **Código de cliente:** Tal como se ha introducido en el asistente de Opt-in.
* **Correo electrónico:** Tal como se ha introducido en el asistente de Opt-in.
* **Contraseña:** Tal como se ha introducido en el asistente de Opt-in.
* **Tipo de API:** REST
* **Sincronizar Segmentos De Adobe Target:** Seleccionado.

* **Biblioteca de cliente:** mbox.js.
* **Utilizar DTM para ofrecer la biblioteca de cliente:** No seleccionado. Seleccione esta opción si [usar DTM](/help/sites-administering/dtm.md) u otro sistema de administración de etiquetas para alojar el archivo mbox.js o AT.js. El Adobe AEM recomienda utilizar DTM en lugar de utilizar el servicio de asistencia para enviar la biblioteca de, en lugar de la.

* **Mbox.js personalizado:** Ninguno especificado para que se use el archivo mbox.js predeterminado. Especifique el archivo mbox.js personalizado que desee utilizar, según sea necesario. Solo aparece si ha seleccionado mbox.js.
* **AT.js personalizado:** Ninguno especificado para utilizar el archivo AT.js predeterminado. Especifique un archivo AT.js personalizado que desee utilizar, según sea necesario. Solo aparece si ha seleccionado AT.js.

>[!NOTE]
>
>AEM En la versión 6.3, puede seleccionar el archivo Biblioteca de objetivos, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/), una nueva biblioteca de implementación para Adobe Target que está diseñada tanto para implementaciones web típicas como para aplicaciones de una sola página.
>
>AT.js ofrece varias mejoras con respecto a la biblioteca mbox.js:
>
>* Se han mejorado los tiempos de carga de las páginas en implementaciones web
>* Seguridad mejorada
>* Mejores opciones de implementación para aplicaciones de una sola página
>* AT.js contiene los componentes que se incluían en target.js, de modo que ya no se llama a target.

<!-- OLD URL WHICH IS 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Propiedades de Target Framework aprovisionadas {#provisioned-target-framework-properties}

El marco de trabajo de Target aprovisionado que crea el asistente de inclusión está configurado para enviar datos de contexto desde el almacén de datos de perfil. Los elementos de datos de edad y sexo del almacén se envían a Target de forma predeterminada. Es probable que la solución requiera que se envíen parámetros adicionales.

![Marco de destino aprovisionado](assets/chlimage_1-158.png)

Puede configurar el marco de trabajo para enviar información contextual adicional a Target como se describe en [Agregar un marco de trabajo de Target](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Configuración de A4T Analytics Cloud {#configuring-a-t-analytics-cloud-configuration}

Puede configurar Adobe Target para que utilice Adobe Analytics como fuente de informes al segmentar contenido.

>[!NOTE]
>
>La autenticación de credencial de usuario (heredada) no funciona con A4T (tanto para Target como para Analytics). Como tal, los clientes deben utilizar la autenticación IMS en lugar de la autenticación de credencial de usuario.

Para ello, especifique con qué configuración de nube de A4T conectar su configuración de nube de Adobe Target:

1. Vaya a **Cloud Service** a través de **AEM logotipo de la** > **Herramientas** > **Implementación** > **Cloud Service**.
1. En la sección **Adobe Target**, haga clic en **Configurar ahora**.
1. Vuelva a conectarse a la configuración de Adobe Target.
1. En el **Configuración de A4T Analytics Cloud** , seleccione el marco de trabajo.

   >[!NOTE]
   >
   >Solo están disponibles las configuraciones de análisis habilitadas para A4T.
   >
   >AEM Al configurar A4T con la opción de configuración, es posible que vea una entrada que falta en la referencia de configuración. Para poder seleccionar el marco de análisis, haga lo siguiente:
   >
   >1. Vaya a **Herramientas** > **General** > **CRXDE Lite**.
   1. Vaya a [Cuadro de diálogo Configuración de A4T Analytics](#a4t-analytics-config-dialog) (ver más abajo)
   1. Establezca la propiedad **disable** hasta **false**.
   1. Haga clic en **Guardar todo**.

#### Cuadro de diálogo Configuración de A4T Analytics {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

Haga clic en **Aceptar**. Al segmentar contenido con Adobe Target, puede: [seleccionar el origen del informe](/help/sites-authoring/content-targeting-touch.md).

## Integración manual con Adobe Target {#manually-integrating-with-adobe-target}

Integre manualmente con Adobe Target en lugar de utilizar el asistente de inclusión.

>[!NOTE]
>
El archivo de la biblioteca de Target, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/), es una nueva biblioteca de implementación para Adobe Target que está diseñada tanto para implementaciones web típicas como para aplicaciones de una sola página. Adobe recomienda usar AT.js en lugar de mbox.js como biblioteca de cliente.
>
AT.js ofrece varias mejoras con respecto a la biblioteca mbox.js:
>
* Se han mejorado los tiempos de carga de las páginas en implementaciones web
* Seguridad mejorada
* Mejores opciones de implementación para aplicaciones de una sola página
* AT.js contiene los componentes que se incluían en target.js, de modo que ya no se llama a target.js
>
Puede seleccionar AT.js o mbox.js en el menú desplegable **Biblioteca de cliente**.

<!-- OLD URL from above was 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Creación de una configuración de Target Cloud {#creating-a-target-cloud-configuration}

Para permitir que AEM interactúe con Adobe Target, cree una configuración de nube de Target. Para crear la configuración, proporcione el código de cliente de Adobe Target y las credenciales de usuario.

La configuración de la nube de Target solo se crea una vez porque se puede asociar con varias campañas de AEM. Si tiene varios códigos de cliente de Adobe Target, cree una configuración para cada código de cliente.

Puede configurar la configuración de nube para sincronizar segmentos desde Adobe Target. Si activa la sincronización, los segmentos se importan desde Target en segundo plano cuando se guarda la configuración de la nube.

Utilice el siguiente procedimiento para crear una configuración de nube de Target en AEM:

1. Vaya a **Cloud Service** a través de **AEM logotipo de la** > **Herramientas** > **Cloud Service** > **Cloud Service heredados**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   El **Cloud Service** se abre la página información general.

1. En la sección **Adobe Target**, haga clic en **Configurar ahora**.
1. En el cuadro de diálogo **Crear configuración**:

   1. Asigne una configuración a **Título**.
   1. Seleccione la plantilla **Configuración de Adobe Target**.
   1. Haga clic en **Crear**.

   Se abre el cuadro de diálogo de edición.

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   >
   AEM Al configurar A4T con la opción de configuración, es posible que vea una entrada que falta en la referencia de configuración. Para poder seleccionar el marco de análisis, haga lo siguiente:
   >
   1. Vaya a **Herramientas** > **General** > **CRXDE Lite**.
   1. Vaya a **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Establezca la propiedad **disable** hasta **false**.
   1. Haga clic en **Guardar todo**.

1. En el cuadro de diálogo, proporcione valores para estas propiedades.

   * **Código de cliente**: el código de cliente de la cuenta de Target
   * **Correo electrónico**: el correo electrónico de la cuenta de Target.
   * **Contraseña**: la contraseña de la cuenta de Target.
   * **Tipo de API**: REST o XML
   * **Configuración de A4T Analytics Cloud**: seleccione la configuración de Analytics Cloud que se utiliza para los objetivos y las métricas de las actividades de Target. Necesita esta configuración si utiliza Adobe Analytics como fuente de informes al segmentar contenido. Si no ve la configuración de nube, consulte la nota en [Configuración de A4T Analytics Cloud](#configuring-a-t-analytics-cloud-configuration).

   * **Use objetivos precisos:** De forma predeterminada, esta casilla de verificación está seleccionada. Si se selecciona, la configuración del servicio en la nube espera a que el contexto se cargue antes de cargar el contenido. Véase la nota siguiente.
   * **Sincronizar segmentos desde Adobe Target:** AEM Seleccione esta opción para poder descargar los segmentos definidos en Target y utilizarlos en la configuración de segmentos de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de. Seleccione esta opción cuando la propiedad Tipo de API sea REST, ya que los segmentos en línea no son compatibles y debe utilizar segmentos de Target. AEM (El término de de &quot;segmento&quot; equivale a la &quot;audiencia&quot; de Target).
   * **Biblioteca de cliente:** Seleccione si quiere la biblioteca de cliente mbox.js o AT.js.
   * **Usar DTM para ofrecer la biblioteca de cliente** : seleccione esta opción para utilizar AT.js o mbox.js desde DTM u otro sistema de administración de etiquetas. Configurar [la integración de DTM](/help/sites-administering/dtm.md) para utilizar esta opción. El Adobe AEM recomienda utilizar DTM en lugar de utilizar el servicio de asistencia para enviar la biblioteca de, en lugar de la.
   * **Mbox.js personalizado**: Déjelo en blanco si marcó la casilla de la DTM o para usar el mbox.js predeterminado. También puede cargar su mbox.js personalizado. Solo aparece si ha seleccionado mbox.js.
   * **AT.js personalizado**: Déjelo en blanco si marcó la casilla de la DTM o para usar el AT.js predeterminado. También puede cargar su archivo AT.js personalizado. Solo aparece si ha seleccionado AT.js.

   >[!NOTE]
   >
   De forma predeterminada, al entrar en el asistente de configuración de Adobe Target, el direccionamiento preciso está habilitado.
   >
   El direccionamiento preciso significa que la configuración del servicio en la nube espera a que el contexto se cargue antes de cargar el contenido. Como resultado, en términos de rendimiento, un direccionamiento preciso puede provocar un retraso de unos milisegundos antes de cargar el contenido.
   >
   El direccionamiento preciso siempre está habilitado en la instancia de autor. Sin embargo, en la instancia de publicación puede optar por desactivar el direccionamiento preciso globalmente, desactivando la marca de verificación junto al direccionamiento preciso en la configuración del servicio en la nube (**http://localhost:4502/etc/cloudservices.html**). También puede activar y desactivar el direccionamiento preciso para componentes individuales independientemente de la configuración del servicio en la nube.
   >
   Si ***ya*** ha creado componentes de destino y cambia esta configuración, los cambios no afectan a esos componentes. Cambie esos componentes directamente.

1. Clic **Conectar con Target** para inicializar la conexión con Target. Si la conexión se realiza correctamente, aparecerá el mensaje **Conexión correcta**. Haga clic en **OK** en el mensaje y, a continuación, **OK** en el cuadro de diálogo.

   Si no puede conectarse a Target, consulte la sección [solución de problemas](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems).

### Adición de un marco de trabajo de destino {#adding-a-target-framework}

Después de configurar la nube de Target, agregue un marco de trabajo de Target. El marco de trabajo identifica los parámetros predeterminados que se envían a Adobe Target desde el [Client Context](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) componentes. Target usa los parámetros para determinar los segmentos que se aplican al contexto actual.

Puede crear varios marcos de trabajo para una sola configuración de Target. Los marcos de trabajo múltiples son útiles cuando debe enviar un conjunto diferente de parámetros a Target para diferentes secciones del sitio web. Cree un marco de trabajo para cada conjunto de parámetros que envíe. Asocie cada sección del sitio web con el marco de trabajo adecuado. Una página web solo puede utilizar un marco de trabajo a la vez.

1. En la página de configuración de Target, haga clic en **+** (signo más) junto a Marcos disponibles.
1. En el cuadro de diálogo Crear marco de trabajo, especifique un **Título**, seleccione **Adobe Target Framework** y haga clic en **Crear**.

   ![Cuadro de diálogo Crear marco](assets/chlimage_1-161.png)

   Se abre la página marco de trabajo. Sidekick proporciona componentes que representan información de la variable [Client Context](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) que puede asignar.

   ![Componentes para el marco](assets/chlimage_1-162.png)

1. Arrastre el componente Client Context que representa los datos que desea utilizar para la asignación al destino de colocación. También puede arrastrar el **Tienda de ContextHub** al marco de trabajo.

   >[!NOTE]
   >
   Al asignar, los parámetros se pasan a un mbox mediante cadenas simples. No se pueden asignar matrices desde ContextHub.

   Por ejemplo, para utilizar **Datos de perfil** acerca de los visitantes del sitio para controlar la campaña de Target, arrastre el **Datos de perfil** a la página. Aparecen las variables de datos de perfil disponibles para su asignación a parámetros de Target.

   ![Datos de perfil](assets/chlimage_1-163.png)

1. Seleccione las variables que desea que sean visibles para el sistema de Adobe Target seleccionando la casilla de verificación **Compartir** en las columnas correspondientes.

   ![Compartir](assets/chlimage_1-164.png)

   >[!NOTE]
   >
   La sincronización de parámetros es solo de una manera, de AEM a Adobe Target.

Se crea el marco de trabajo. Para replicar el marco de trabajo en la instancia de publicación, utilice la opción **Activar marco de trabajo** de la barra de tareas.

### Asociación de actividades con la configuración de nube de Target  {#associating-activities-with-the-target-cloud-configuration}

Asocie su [AEM actividades de](/help/sites-authoring/activitylib.md) con la configuración de nube de Target para poder reflejar las actividades en [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
Los tipos de actividades estarán disponibles dependiendo de lo siguiente:
>
>
* Si la variable **xt_only** La opción está habilitada en el inquilino de Adobe Target AEM (clientcode) que se utiliza en el lado del para conectarse a Adobe Target. A continuación, puede crear lo siguiente **solamente** AEM Actividades XT en.
>
* Si la variable **xt_only** La opción es **no** habilitado en el inquilino de Adobe Target (clientcode), a continuación, puede crear **ambos** AEM Las actividades XT y A/B en la.
>
**Nota adicional:** **xt_only** es una configuración aplicada a un determinado inquilino de Target (clientcode) y solo se puede modificar directamente en Adobe Target. No puede activar ni desactivar esta opción en AEM.

### Asociación del marco de trabajo de Target con el sitio {#associating-the-target-framework-with-your-site}

AEM Después de crear un marco de trabajo de Target en la creación de páginas web, asocie las páginas web con el marco de trabajo de, que se encuentra en la página de inicio. Los componentes de destino de las páginas envían los datos definidos por el marco de trabajo a Adobe Target para su seguimiento. (Consulte [Segmentación de contenido](/help/sites-authoring/content-targeting-touch.md).)

Cuando asocia una página con el marco de trabajo, las páginas secundarias heredan la asociación.

1. En el **Sites** , desplácese hasta el sitio que desee configurar.
1. Uso de [acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions) o [modo de selección](/help/sites-authoring/basic-handling.md), seleccione **Ver propiedades.**
1. Seleccione la pestaña **Cloud Services**.
1. Clic **Editar**.
1. Clic **Agregar configuración** bajo **Configuraciones del Cloud Service** y seleccione **Adobe Target**.

   ![Agregar configuración](assets/chlimage_1-165.png)

1. Seleccione el marco de trabajo en el que desee **Referencia de configuración**.

   >[!NOTE]
   >
   Asegúrese de seleccionar la variable específica **marco** que ha creado y no la configuración de nube de Target en la que se creó.

1. Haga clic en **Listo**.
1. Active la página raíz del sitio web para replicarla en el servidor de publicación. (Consulte [Cómo Publicar Páginas](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   >
   Si el marco de trabajo adjunto a la página aún no se ha activado, se abre un asistente que también le permite publicarlo.

## Solución de problemas de conexión de Target {#troubleshooting-target-connection-problems}

Para solucionar los problemas que se producen al conectarse a Target, puede realizar las siguientes tareas:

* Asegúrese de que las credenciales de usuario que ha proporcionado son correctas.
* AEM Asegúrese de que la instancia de pueda conectarse al servidor de Target. AEM AEM Por ejemplo, asegúrese de que las reglas del cortafuegos no bloquean las conexiones de salida de la red de seguridad o de que la configuración de los servidores de seguridad para utilizar los servidores proxy necesarios está configurada para que se utilicen los servidores proxy necesarios.
* AEM Busque mensajes útiles en el registro de errores de la. El archivo error.log se encuentra en el **crx-quickstart/logs** AEM directorio donde está instalado el.
* Al editar la actividad en Adobe Target, la URL apunta a localhost. AEM Solucione este problema configurando el externalizador de en la dirección URL correcta.
