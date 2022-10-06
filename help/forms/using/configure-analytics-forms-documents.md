---
title: Configuración de análisis e informes
seo-title: Configuring analytics and reports
description: Aprenda a configurar Adobe Analytics para que detecte patrones de interacción y problemas a los que se enfrentan los usuarios al utilizar formularios adaptables, documentos adaptables y formularios HTML5.
seo-description: Learn how to configure Adobe Analytics to discover interaction patterns and problems users face while using adaptive forms, adaptive documents, and HTML5 forms.
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
source-git-commit: 66631fd0813f623f3321072fc00fd90f7fa33d21
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 3%

---

# Analytics con Cloud Service Framework {#analyticsusingcloudframework}

AEM Forms se integra con Analytics, lo que le permite capturar y rastrear las métricas de rendimiento de los formularios y documentos publicados. El objetivo detrás del análisis de estas métricas es tomar decisiones informadas basadas en los datos sobre los cambios necesarios para que los formularios o documentos sean más utilizables.

>[!NOTE]
>
>La función de análisis de AEM Forms está disponible como parte del paquete de complementos de AEM Forms. Para obtener información sobre la instalación del paquete de complementos, consulte [Instalación y configuración de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).
>
>Además del paquete de complementos, necesita una cuenta de Adobe Analytics y privilegios de administrador en la instancia de AEM. Para obtener información sobre la solución, consulte [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

También puede realizar análisis mediante Adobe Launch. Para obtener más información sobre cómo integrar AEM Forms con Adobe Launch, consulte [Analytics con Adobe Launch](/help/forms/using/integrate-aem-forms-with-adobe-analytics.md).

## Información general {#overview}

Puede utilizar Adobe Analytics para detectar patrones de interacción y problemas que los usuarios afrontan al utilizar formularios adaptables, formularios HTML5 y comunicación interactiva. De serie, Adobe Analytics realiza un seguimiento y almacena información sobre los siguientes parámetros:

* **Promedio de tiempo de llenado**: Tiempo promedio empleado para rellenar el formulario.
* **Representaciones**: Número de veces que se abre un formulario.
* **Borradores**: Número de veces que un formulario se guarda en estado de borrador.
* **Envíos**: Número de veces que se envía un formulario.
* **Anular**: Número de veces que los usuarios se van sin completar el formulario.

Puede personalizar Adobe Analytics para agregar o eliminar más parámetros. Junto con la información anterior, el informe contiene la siguiente información sobre cada panel del HTML5 y la forma adaptativa:

* **Tiempo**: Tiempo invertido en el panel y en los campos del panel.
* **Error**: Número de errores identificados en el panel y en los campos del panel.
* **Ayuda**: Número de veces que un usuario abre la ayuda de un panel y los campos del panel.

## Creación de un grupo de informes {#creating-report-suite}

Los datos de Analytics se almacenan en repositorios específicos del cliente, denominados grupos de informes. Para crear un grupo de informes y usar Adobe Analytics, debe tener una cuenta de Adobe Marketing Cloud válida. Antes de realizar los siguientes pasos, asegúrese de que tiene una cuenta de Adobe Marketing Cloud válida.

Siga estos pasos para crear un grupo de informes.

1. Iniciar sesión en [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. En el Marketing Cloud, seleccione **Administrador** > **Admin Console** > **Grupos de informes**.
1. Select **Crear nuevo** > **Grupo de informes** en el Administrador de grupos de informes.

   ![Crear nuevo grupo de informes](assets/newreportsuite_new.png)

   Crear nuevo grupo de informes

1. Asegúrese de que la primera lista desplegable esté configurada en **Crear a partir de una plantilla** y, a continuación, seleccione **Comercio**.
1. Busque la variable **ID del grupo de informes** y agregar una nueva ID de grupo de informes. Por ejemplo, JJEsquire. Aparece una ID de grupo de informes debajo del campo ID de grupo de informes . Incluye un prefijo automático, que suele ser el nombre de la empresa.
1. Agregar nuevo **Título del sitio**. Por ejemplo, Grupo de introducción de JJEsquire. Este título se utiliza en la interfaz de usuario de Analytics. Utilice el ID del grupo de informes en su código.
1. Seleccione un **Zona horaria** en la lista desplegable . Todos los datos que llegan a este grupo de informes se registran en función de la zona horaria definida.
1. Deje el **Dirección URL base** y **Página predeterminada** campos vacíos. Estos dos valores solo se utilizan desde la interfaz de Adobe Marketing Cloud para vincular al sitio web.
1. Deje el **Fecha de lanzamiento** configurado como hoy. La Fecha de lanzamiento determina el día en que se activa el grupo de informes.
1. En el **Vistas de la página estimadas por día** , escriba 100. Utilice este campo para calcular la cantidad de vistas de página que espera para su sitio web por día. Esta estimación permite que el Adobe ponga en marcha la cantidad adecuada de hardware para procesar los datos que va a recopilar.
1. Seleccione un **Moneda base** en la lista desplegable . Todos los datos de moneda que entran en este grupo de informes se convierten y almacenan en este formato de moneda.
1. Haga clic en **Crear informe** Suite. Debería ver la actualización de la página con un mensaje que indique que el grupo de informes se ha creado correctamente.
1. Seleccione el grupo de informes recién creado. Vaya a **Editar configuración** > **General** > **Configuración general de la cuenta**.

   ![Configuración general de la cuenta](assets/geographic_settings.png)

   Configuración general de la cuenta

1. En la pantalla Configuración general de la cuenta , habilite **Informes de geografía** y haga clic en **Guardar.**
1. Vaya a **Editar configuración** > **Tráfico** > **Variables de tráfico**.
1. En el grupo de informes, configure y habilite las siguientes variables de tráfico.

   * **formName**: Identificador de un formulario adaptable.
   * **formInstance**: Identificador de una instancia de formulario adaptable. Habilite los informes de ruta para esta variable.
   * **fieldName**: Identificador de un campo de formulario adaptable. Habilite los informes de ruta para esta variable.
   * **panelName**: Identificador de un panel de formulario adaptable. Habilite los informes de ruta para esta variable.
   * **formTitle**: Título del formulario.
   * **fieldTitle**: Título del campo de formulario.
   * **panelTitle**: Título del panel de formulario.
   * **analyticsVersion**: Versión de análisis de formulario.

1. Vaya a **Editar configuración** > **Conversión** > **Eventos de éxito**. Defina y habilite los siguientes eventos de éxito:

   | Evento de éxito | Tipo |
   |---|---|
   | abandon | Contador |
   | procesar | Contador |
   | panelVisit | Contador |
   | fieldVisit | Contador |
   | guardar | Contador |
   | error | Contador |
   | Ayuda de  | Contador |
   | submit | Contador |
   | timeSpent | Numérica |

   >[!NOTE]
   >
   >Un número de evento y un número de propiedad que se usen para configurar AEM Forms Analytics deben ser diferentes del número de evento y el número de propiedad que se usan en [AEM analytics](/help/sites-administering/adobeanalytics.md) configuración.

1. Cierre la sesión de la cuenta de Adobe Marketing Cloud.

## Creación de la configuración del Cloud Service {#creating-cloud-service-configuration}

La configuración del Cloud Service es información sobre su cuenta de Adobe Analytics. La configuración permite que Adobe Experience Manager (AEM) se conecte a Adobe Analytics. Cree una configuración diferente para cada cuenta de Analytics que utilice.

1. Inicie sesión en la instancia de autor de AEM como administrador.
1. En la esquina superior izquierda, haga clic en **Adobe Experience Manager** > **Herramientas** ![](/help/forms/using/assets/tools.png) > **Cloud Services** > **Cloud Services heredados**.
1. Localizar **Adobe Analytics** icono. Haga clic en **Mostrar configuraciones** y, a continuación, haga clic en **[+]** para agregar nueva configuración.

   Si es la primera vez que utiliza, haga clic en **Configurar ahora**.

1. Añada un Título a la nueva configuración (rellenar el campo Nombre es opcional). Por ejemplo, la configuración de My analytics . Haga clic en **Crear**.

1. Cuando el panel Editar se abra en la página de configuración, rellene los campos:

   * **Empresa**: El nombre de su empresa aparece en Adobe Analytics.
   * **Nombre de usuario**: Nombre utilizado para iniciar sesión en Adobe Analytics.
   * **Contraseña**: La contraseña de Adobe Analytics para la cuenta anterior.
   * **Centro de datos**: El centro de datos de su cuenta de Adobe Analytics.

1. Haga clic en **Conectarse a Analytics**. Aparece un cuadro de diálogo con el mensaje de que la conexión se ha realizado correctamente. Haga clic en **Aceptar**.

## Creación de un marco de Cloud Service {#creating-cloud-service-framework}

Un marco de Adobe Analytics es un conjunto de asignaciones entre variables de Adobe Analytics y variables de AEM. Utilice un marco para configurar cómo los formularios rellenan los datos en los informes de Adobe Analytics. Los módulos están asociados a una configuración de Adobe Analytics. Puede crear varios marcos para cada configuración.

1. En la consola de servicios de nube de AEM, haga clic en **Mostrar configuraciones**, en Adobe Analytics.
1. Haga clic en el **[+]** junto a la configuración de Analytics.

   ![Configuración de Adobe Analytics](assets/adobe-analytics-cloud-services.png)

   Configuración de Adobe Analytics

1. Tipo a **Título** y **Nombre** para el marco, seleccione **Adobe Analytics** Marco y haga clic en **Crear**. El marco se abre para su edición.
1. En la sección Grupos de informes de la pod lateral, haga clic en **Agregar elemento**, utilice la lista desplegable para seleccionar la ID del grupo de informes (por ejemplo, JJEsquire) con la que interactuará la estructura.
1. Junto al ID del grupo de informes, seleccione las instancias de servidor a las que desea enviar información al grupo de informes.

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. Arrastre un **Componente de Form Analytics** de la variable **other** de SideKick al marco de trabajo.
1. Para asignar variables de Analytics con variables definidas en el componente, arrastre una variable desde AEM Buscador de contenido a un campo del componente de seguimiento.

   ![Asignación de variables de AEM con variables de Adobe Analytics](assets/analytics_new.png)

1. Active el marco de trabajo mediante el **ficha de página** en la barra de tareas, haga clic en **Activar marco**.

## Configuración del servicio de configuración de AEM Forms Analytics {#configuring-aem-forms-analytics-configuration-service}

1. En la instancia de autor, abra AEM administrador de configuración de la consola web en `https://<server>:<port>;/system/console/configMgr`.
1. Localizar y abrir la configuración de AEM Forms Analytics

   ![Servicio de configuración de AEM Forms Analytics](assets/analytics_configuration.png)

   Servicio de configuración de AEM Forms Analytics

1. Especifique los valores adecuados para los campos siguientes y haga clic en **Guardar**.

   * **Marco de SiteCatalyst**: Seleccione el marco o la configuración que definió en la sección Configurar un marco para el seguimiento .
   * **Línea base de seguimiento de tiempo de campo**: Especifique la duración, en segundos, tras la cual se debe realizar el seguimiento de la visita al campo. El valor predeterminado es 0. Cuando el valor es bueno a 0 (cero), se envían dos eventos de seguimiento independientes al servidor de Adobe Analytics. El primer evento indica al servidor de análisis que deje de rastrear el campo de salida. El segundo evento se envía después de que transcurra la duración especificada. El segundo evento ordena al servidor de análisis que inicie el seguimiento del campo visitado. El uso de dos eventos independientes ayuda a medir con precisión el tiempo empleado en un campo. Cuando el valor es 0 (cero), el evento de seguimiento único se envía al servidor de Adobe Analytics.

   * **Cron de sincronización de informes de Analytics**: Especifique la expresión cron para recuperar informes de Adobe Analytics. El valor predeterminado es 0 0 2 ? &#42; &#42;.

   * **Recuperar tiempo de espera de informe:** Especifique la duración, en segundos, que hay que esperar para que el servidor responda al informe de análisis. El tiempo predeterminado es de 120 segundos.
   >[!NOTE]
   >
   >Puede tardar hasta 10 segundos más en agotar el tiempo de espera en la operación de recuperación de informes y, a continuación, en el número de segundos especificado.

1. Repita los pasos del 1 al 3 en la instancia de publicación para configurar analytics.

Ahora puede habilitar analytics para formularios y generar un informe de análisis.

## Activación de Analytics para un formulario o documento {#enabling-analytics-for-a-form-or-document}

1. Inicie sesión en AEM portal en `https://[hostname]:'port'`.
1. Haga clic en **Forms > Forms y documentos**, seleccione un formulario o documento y haga clic en **Habilitar Analytics**. El análisis está habilitado.

   ![Activación de Analytics para un formulario o documento](assets/enable-analytics-1.png)

   Activación de analytics para un formulario

   **A.** Botón Habilitar Analytics **B.** Formulario seleccionado

   Para obtener información detallada sobre la visualización de informes de análisis de formularios, consulte [Visualización y comprensión de los informes de análisis de AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).
