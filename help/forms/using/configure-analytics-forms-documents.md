---
title: Configuración de análisis e informes
seo-title: Configuración de análisis e informes
description: Obtenga información sobre cómo configurar Adobe Analytics para que detecte los patrones de interacción y los problemas que enfrentan los usuarios al utilizar formularios adaptables, documentos adaptables y formularios HTML5.
seo-description: Obtenga información sobre cómo configurar Adobe Analytics para que detecte los patrones de interacción y los problemas que enfrentan los usuarios al utilizar formularios adaptables, documentos adaptables y formularios HTML5.
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
translation-type: tm+mt
source-git-commit: 5aa2fe48578633cbe5e4324f9e956e1dbbdab8af
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 1%

---


# Configuración de análisis e informes{#configuring-analytics-and-reports}

AEM Forms se integra con Adobe Analytics que le permite capturar y rastrear las métricas de rendimiento de los formularios y documentos publicados. El objetivo detrás del análisis de estas métricas es tomar decisiones informadas en base a los datos sobre los cambios necesarios para que los formularios o documentos sean más utilizables.

>[!NOTE]
>
>La función de análisis de AEM Forms está disponible como parte del paquete del complemento AEM Forms. Para obtener información sobre la instalación del paquete de complemento, consulte [Instalación y configuración de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).
>
>Además del paquete de complemento, necesita una cuenta de Adobe Analytics y privilegios de administrador en la instancia de AEM. Para obtener información sobre la solución, consulte [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

## Información general {#overview}

Puede utilizar Adobe Analytics para descubrir patrones de interacción y problemas que los usuarios enfrentan al utilizar formularios adaptables, formularios HTML5 y comunicación interactiva. De forma predeterminada, el análisis de Adobe rastrea y almacena información sobre los siguientes parámetros:

* **Tiempo** de relleno promedio: Tiempo promedio empleado para rellenar el formulario.
* **Representaciones**: Número de veces que se abre un formulario.
* **Borradores**: Número de veces que un formulario se guarda en estado borrador.
* **Envíos**: Número de veces que se envía un formulario.
* **Anular**: Número de veces que los usuarios se van sin completar el formulario.

Puede personalizar Adobe Analytics para agregar o quitar más parámetros. Junto con la información anterior, el informe contiene la siguiente información sobre cada panel de HTML5 y formulario adaptable:

* **Hora**: Tiempo empleado en el panel y en los campos del panel.
* **Error**: Número de errores encontrados en el panel y en los campos del panel.
* **Ayuda**: Número de veces que un usuario abre la ayuda de un panel y los campos del mismo.

## Creando grupo de informes {#creating-report-suite}

Los datos de Analytics se almacenan en repositorios específicos del cliente, denominados grupos de informes. Para crear un grupo de informes y utilizar Adobe Analytics, debe tener una cuenta de Adobe Marketing Cloud válida. Antes de realizar los siguientes pasos, asegúrese de que dispone de una cuenta de Adobe Marketing Cloud válida.

Realice los siguientes pasos para crear un grupo de informes.

1. Inicie sesión en [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. En el Marketing Cloud, seleccione **Administración** > **Admin Console** > **Grupos de informes**.
1. Seleccione **Crear nuevo** > **Grupo de informes** en el Administrador de grupos de informes.

   ![Crear nuevo grupo de informes](assets/newreportsuite_new.png)

   Crear nuevo grupo de informes

1. Asegúrese de que la primera lista desplegable esté establecida en **Crear a partir de una plantilla** y, a continuación, seleccione **Comercio**.
1. Busque el campo **ID del grupo de informes** y agregue una nueva ID del grupo de informes. Por ejemplo, JJEsquire. Debajo del campo ID del grupo de informes aparece una ID del grupo de informes. Incluye un prefijo automático, que suele ser el nombre de la compañía.
1. Añada el nuevo **Título del sitio**. Por ejemplo, Grupo de introducción de JJEsquire. Este título se utiliza en la interfaz de usuario de Analytics. Utilice la ID del grupo de informes en su código.
1. Seleccione un **Huso horario** en el menú desplegable. Todos los datos que llegan a este grupo de informes se registran en función de la zona horaria definida.
1. Deje vacíos los campos **URL base** y **Página predeterminada**. Estos dos valores solo se utilizan desde la interfaz de Adobe Marketing Cloud para establecer vínculos con su sitio web.
1. Deje la **Fecha de lanzamiento** establecida en hoy. La Fecha de lanzamiento determina el día en que se activa el grupo de informes.
1. En el campo **Vistas de página estimadas por día**, escriba 100. Utilice este campo para calcular el número de vistas de página que espera para el sitio web por día. Este cálculo permite a Adobe implementar la cantidad adecuada de hardware para procesar los datos que estará recopilando.
1. Seleccione una **Moneda base** en la lista desplegable. Todos los datos de moneda que ingresan a este grupo de informes se convierten y almacenan en este formato de moneda.
1. Haga clic en **Crear grupo de informes**. Debe ver la actualización de la página con un mensaje que indica que el grupo de informes se ha creado correctamente.
1. Seleccione el grupo de informes recién creado. Vaya a **Editar configuración** > **General** > **Configuración general de cuenta**.

   ![Configuración general de cuenta](assets/geographic_settings.png)

   Configuración general de cuenta

1. En la pantalla Configuración general de cuenta, habilite **Sistema de informes geográfico** y haga clic en **Guardar.**
1. Vaya a **Editar configuración** > **Tráfico** > **Variables de tráfico**.
1. En el grupo de informes, configure y habilite las siguientes variables de tráfico.

   * **formName**: Identificador de un formulario adaptable.
   * **formInstance**: Identificador de una instancia de formulario adaptable. Habilite los informes de ruta para esta variable.
   * **fieldName**: Identificador de un campo de formulario adaptable. Habilite los informes de ruta para esta variable.
   * **panelName**: Identificador de un panel de formulario adaptable. Habilite los informes de ruta para esta variable.
   * **formTitle**: Título del formulario.
   * **fieldTitle**: Título del campo de formulario.
   * **panelTitle**: Título del panel Formulario.
   * **analyticsVersion**: Versión de análisis de formularios.

1. Vaya a **Editar configuración** > **Conversión** > **Eventos de éxito**. Defina y habilite los siguientes eventos de éxito:

   | Evento de éxito | Tipo |
   |---|---|
   | abandono | Contador |
   | procesar | Contador |
   | panelVisit | Contador |
   | fieldVisit | Contador |
   | save | Contador |
   | error | Contador |
   | ayuda | Contador |
   | submit | Contador |
   | timeSpent | Numérica |

   >[!NOTE]
   >
   >Un número de evento y un número de propiedad utilizados para configurar los análisis de AEM Forms deben ser diferentes del número de evento y el número de propiedad utilizados en la configuración de [análisis de AEM](/help/sites-administering/adobeanalytics.md).

1. Cierre la sesión de la cuenta de Adobe Marketing Cloud.

## Creación de la configuración de Cloud Service {#creating-cloud-service-configuration}

La configuración del Cloud Service es información sobre su cuenta de Adobe Analytics. La configuración permite que Adobe Experience Manager (AEM) se conecte a Adobe Analytics. Cree una configuración independiente para cada cuenta de Analytics que utilice.

1. Inicie sesión en la instancia de creación de AEM como administrador.
1. En la esquina superior izquierda, haga clic en **Adobe Experience Manager** > **Herramientas** ![](/help/forms/using/assets/tools.png) > **Cloud Services** > **Cloud Services heredados**.
1. Busque el icono **Adobe Analytics**. Haga clic en **Mostrar configuraciones** y luego haga clic en **[+]** para agregar nueva configuración.

   Si es la primera vez que utiliza la aplicación, haga clic en **Configurar ahora**.

1. Añada un Título a la nueva configuración (rellenar el campo Nombre es opcional). Por ejemplo, Configuración de Mis análisis. Haga clic en **Crear**.

1. Cuando se abra el panel Editar en la página de configuración, rellene los campos:

   * **Compañía**: El nombre de su compañía aparece en Adobe Analytics.
   * **Nombre de usuario**: Nombre utilizado para iniciar sesión en Adobe Analytics.
   * **Contraseña**: La contraseña de Adobe Analytics para la cuenta anterior.
   * **Centro** de datos: Centro de datos de su cuenta de Adobe Analytics.

1. Haga clic en **Conectar con Analytics**. Aparece un cuadro de diálogo con el mensaje de que la conexión se realizó correctamente. Haga clic en **Aceptar**.

## Creación de Cloud Service Framework {#creating-cloud-service-framework}

Un marco de trabajo de Adobe Analytics es un conjunto de asignaciones entre variables de Adobe Analytics y variables de AEM. Utilice un marco para configurar la forma en que los formularios rellenan los datos en los informes de Adobe Analytics. Los marcos están asociados con una configuración de Adobe Analytics. Puede crear varios marcos para cada configuración.

1. En la consola de servicios en la nube de AEM, haga clic en **Mostrar configuraciones**, en Adobe Analytics.
1. Haga clic en el vínculo **[+]** al lado de la configuración de Analytics.

   ![Configuración de Adobe Analytics](assets/adobe-analytics-cloud-services.png)

   Configuración de Adobe Analytics

1. Escriba un **Título** y **Nombre** para la estructura, seleccione **Adobe Analytics** Framework y haga clic en **Crear**. El marco se abre para la edición.
1. En la sección Grupos de informes del pod lateral, haga clic en **Añadir elemento** y, a continuación, utilice la lista desplegable para seleccionar la ID del grupo de informes (por ejemplo, JJEsquire) con la que interactuará la estructura.
1. Junto a la ID del grupo de informes, seleccione las instancias de servidor que desee enviar información al grupo de informes.

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. Arrastre un **componente de Análisis de formularios** desde la categoría **other** desde SideKick hasta la estructura.
1. Para asignar variables de Analytics con variables definidas en el componente, arrastre una variable desde AEM Buscador de contenido a un campo del componente de seguimiento.

   ![Asignación de variables AEM con variables de Adobe Analytics](assets/analytics_new.png)

1. Active el marco de trabajo con la **ficha de página** en la barra de tareas, haga clic en **Activar marco**.

## Configuración del servicio de configuración de AEM Forms Analytics {#configuring-aem-forms-analytics-configuration-service}

1. En la instancia de creación, abra AEM administrador de configuración de la consola web en `https://<server>:<port>;/system/console/configMgr`.
1. Localizar y abrir la configuración de AEM Forms Analytics

   ![Servicio de configuración de AEM Forms Analytics](assets/analytics_configuration.png)

   Servicio de configuración de AEM Forms Analytics

1. Especifique los valores adecuados para los campos siguientes y haga clic en **Guardar**.

   * **SiteCatalyst Framework**: Seleccione el marco o la configuración que definió en la sección Configurar un marco para el seguimiento.
   * **Base** de seguimiento de tiempo de campo: Especifique la duración, en segundos, después de la cual se debe realizar el seguimiento de la visita al campo. El valor predeterminado es 0. Cuando el valor es bueno a 0 (cero), se envían dos eventos de seguimiento independientes al servidor Adobe Analytics. El primer evento indica al servidor de Analytics que deje de realizar el seguimiento del campo de salida. El segundo evento se envía una vez transcurrida la duración especificada. El segundo evento indica al servidor de análisis que realice un seguimiento de inicios del campo visitado. El uso de dos eventos independientes ayuda a medir con precisión el tiempo empleado en un campo. Cuando el valor es 0 (cero), se envía un solo evento de seguimiento al servidor de Adobe Analytics.

   * **Cron** de sincronización de informes de Analytics: Especifique la expresión cron para recuperar informes de Adobe Analytics. El valor predeterminado es 0 0 2 ? * *.

   * **Tiempo de espera del informe de recuperación:** especifique la duración, en segundos, que se espera a que el servidor responda al informe de análisis. El tiempo predeterminado es de 120 segundos.
   >[!NOTE]
   >
   >Puede tardar hasta 10 segundos más en la operación de recuperación de informes de tiempo de espera que el número de segundos especificado.

1. Repita los pasos 1 a 3 en la instancia de publicación para configurar los análisis.

Ahora puede activar los análisis para los formularios y generar un informe de análisis.

## Habilitación del análisis para un formulario o documento {#enabling-analytics-for-a-form-or-document}

1. Inicie sesión en AEM portal en `https://[hostname]:'port'`.
1. Haga clic en **Forms > Forms y Documentos**, seleccione un formulario o documento y haga clic en **Habilitar Analytics**. El análisis está habilitado.

   ![Activación del análisis para un formulario o documento](assets/enable-analytics-1.png)

   Activación del análisis para un formulario

   **A.** Botón Activar Analytics  **B.Formulario** seleccionado

   Para obtener información detallada sobre la visualización de informes de análisis de formularios, consulte [Visualización y comprensión de informes de análisis de AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md)

