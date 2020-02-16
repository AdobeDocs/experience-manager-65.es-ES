---
title: Conexión a Adobe Analytics y creación de marcos
seo-title: Conexión a Adobe Analytics y creación de marcos
description: Obtenga información sobre cómo conectar AEM a SiteCatalyst y crear marcos.
seo-description: Obtenga información sobre cómo conectar AEM a SiteCatalyst y crear marcos.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Conexión a Adobe Analytics y creación de marcos {#connecting-to-adobe-analytics-and-creating-frameworks}

Para rastrear datos web de sus páginas de AEM en Adobe Analytics, cree una configuración de Adobe Analytics Cloud Services y un marco de trabajo de Adobe Analytics:

* **** Configuración de Adobe Analytics: Información sobre su cuenta de Adobe Analytics. La configuración de Adobe Analytics permite que AEM se conecte a Adobe Analytics. Cree una configuración de Adobe Analytics para cada cuenta que utilice.
* **** Adobe Analytics Framework: Un conjunto de asignaciones entre las propiedades del grupo de informes de Adobe Analytics y las variables de CQ. Utilice un marco para configurar la forma en que los datos del sitio web rellenan los informes de Adobe Analytics. Los marcos están asociados a una configuración de Adobe Analytics. Puede crear varios marcos para cada configuración.

Cuando asocia una página web con un marco, el marco realiza el seguimiento de esa página y de los descendientes de dicha página. Las vistas de página se pueden recuperar de Adobe Analytics y mostrar en la consola Sitios.

## Requisitos previos {#prerequisites}

### Adobe Analytics Account {#adobe-analytics-account}

Para rastrear datos de AEM en Adobe Analytics, debe tener una cuenta válida de Adobe Marketing Cloud Analytics.

La cuenta de Adobe Analytics debe:

* Tiene privilegios **de administrador**
* Se asignará al grupo de usuarios de Acceso **a servicios** Web.

>[!CAUTION]
>
>Proporcionar privilegios de **administrador** (en Adobe Analytics) no es suficiente para permitir que un usuario se conecte de AEM a Adobe Analytics. La cuenta también debe tener privilegios de acceso **a servicios** Web.

![chlimage_1-67](assets/chlimage_1-67.png)

Antes de continuar, asegúrese de que sus credenciales le permiten iniciar sesión en Adobe Analytics. Mediante:

* [https://marketing.adobe.com](https://marketing.adobe.com)

* [https://sc.omniture.com/login/](https://sc.omniture.com/login/)

### Configuración de AEM para utilizar los centros de datos de Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Los centros [de](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) datos de Adobe Analytics recopilan, procesan y almacenan datos asociados a su grupo de informes de Adobe Analytics. Debe configurar AEM para que utilice el centro de datos que aloja su grupo de informes de Adobe Analytics. La siguiente tabla enumera los centros de datos disponibles y su dirección URL.

| Centro de datos | URL |
|---|---|
| San José | https://api.omniture.com/admin/1.4/rest/ |
| Dallas | https://api2.omniture.com/admin/1.4/rest/ |
| Londres | https://api3.omniture.com/admin/1.4/rest/ |
| Singapur | https://api4.omniture.com/admin/1.4/rest/ |
| Oregón | https://api5.omniture.com/admin/1.4/rest/ |

AEM utiliza el centro de datos de San José (https://api.omniture.com/admin/1.4/rest/) de forma predeterminada.

Utilice la consola [web para configurar el paquete](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) OSGi cliente **HTTP de** Adobe AEM Analytics. Agregue la dirección URL **del centro de** datos para el centro de datos que aloja un grupo de informes para el que las páginas de AEM recopilan datos.

![aa-07](assets/aa-07.png)

1. Abra la consola web en el explorador web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Introduzca sus credenciales para acceder a la consola.

   >[!NOTE]
   >
   >Póngase en contacto con el administrador del sitio para averiguar si tiene acceso a esta consola.

1. Seleccione el elemento de configuración denominado **Adobe AEM Analytics HTTP Client**.
1. Para agregar la dirección URL de un centro de datos, presione el botón + junto a la lista de direcciones URL **del centro de** datos y escriba la dirección URL en el cuadro.

1. Para eliminar una dirección URL de la lista, haga clic en el botón - situado junto a la dirección URL.
1. Haga clic en Guardar.

## Configuring the Connection to Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.

## Configuring for the Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.

## Creación de un marco de Adobe Analytics {#creating-a-adobe-analytics-framework}

Para la ID del grupo de informes (RSID) que está utilizando, puede controlar qué instancias del servidor (autor, publicación o ambas) contribuyen a los datos al grupo de informes:

* **Todo**: La información del autor y de la instancia de publicación rellena el grupo de informes.
* **Autor**: Solo la información de la instancia de autor rellena el grupo de informes.
* **Publicar**: Solo la información de la instancia de publicación rellena el grupo de informes.

>[!NOTE]
>
>Si se selecciona el tipo de instancia de servidor, no se restringen las llamadas a Adobe Analytics, solo se controla qué llamadas incluyen el RSID.
>
>Por ejemplo, un marco de trabajo está configurado para utilizar el grupo de informes *digital* y el autor es la instancia de servidor seleccionada. Cuando las páginas se publican junto con el marco, las llamadas se siguen realizando a Adobe Analytics, pero estas llamadas no contienen el RSID. Sólo las llamadas de la instancia de autor incluyen el RSID.

1. Con **Navegación**, seleccione **Herramientas**, Servicios **de** nube y, a continuación, Servicios **de nube** preexistentes.
1. Desplácese a **Adobe Analytics** y haga clic en **[+]** junto a Configuraciones **** disponibles.
1. Haga clic en el vínculo **[+]** junto a la configuración de Adobe Analytics.

1. En el cuadro de diálogo **Crear marco** :

   * Especifique un **título**.
   * Opcionalmente, puede especificar el **Nombre** para el nodo que almacena los detalles del marco en el repositorio.
   * Seleccione **Adobe Analytics Framework**
   Y haga clic en **Crear**.

   El marco se abre para la edición.

1. En la sección Grupos **de** informes del pod lateral (lado derecho del panel principal), haga clic en **Agregar elemento**. A continuación, utilice la lista desplegable para seleccionar la ID del grupo de informes (por ejemplo, `geometrixxauth`) con la que interactuará la estructura.

   >[!NOTE]
   >
   >El buscador de contenido de la izquierda se rellena con variables de Adobe Analytics (variables de SiteCatalyst) al seleccionar una ID de grupo de informes.

1. A continuación, utilice la lista desplegable Modo **de** ejecución (junto a la ID del grupo de informes) para seleccionar las instancias de servidor que desea enviar información al grupo de informes.

   ![aa-framework-01](assets/aa-framework-01.png)

1. Para que el marco esté disponible en la instancia de publicación de su sitio, en la ficha **Página** de la barra de tareas, haga clic en **Activar marco.**

### Configuración del servidor para Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

El sistema de marco permite cambiar la configuración del servidor en cada marco de Adobe Analytics.

>[!CAUTION]
>
>Esta configuración determina dónde se envían los datos y cómo, por lo que es imperativo *no alterar esta configuración* y dejar que su representante de Adobe Analytics la configure.

Comience abriendo el panel. Pulse la flecha hacia abajo junto a **Servidores**:

![server_001](assets/server_001.png)

* **Servidor de seguimiento**

   * contiene la dirección URL utilizada para enviar llamadas de Adobe Analytics

      * cname: el nombre predeterminado de la *empresa de la cuenta de Adobe Analytics*
      * d1 - corresponde al centro de datos al que se enviará la información (puede ser d1, d2 o d3)
      * sc.omtrdc.net - nombre de dominio

* **Servidor de seguimiento seguro**

   * Tiene los mismos segmentos que el servidor de seguimiento
   * Se utiliza para enviar datos desde páginas seguras (https://)

* **Espacio de nombres del visitante**

   * El espacio de nombres determina la primera parte de la dirección URL de seguimiento.
   * Por ejemplo, si se cambia el espacio de nombres a **CNAME** , las llamadas realizadas a Adobe Analytics tendrán un aspecto **CNAME.d1.omtrdc.net** en lugar del predeterminado.

## Asociación de una página con un marco de Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Cuando una página está asociada a un marco de Adobe Analytics, la página envía datos a Adobe Analytics cuando se carga la página. Las variables que rellena la página se asignan y recuperan de las variables de Adobe Analytics en el marco. Por ejemplo, las vistas de página se recuperan de Adobe Analytics.

Los descendientes de la página heredan la asociación con la estructura. Por ejemplo: cuando asocia la página raíz del sitio con un marco, todas las páginas del sitio están asociadas con el marco.

1. Desde la consola **Sitios** , seleccione la página que desee configurar con el seguimiento.
1. Abra las Propiedades **[de la](/help/sites-authoring/editing-page-properties.md)**página, directamente desde la consola o desde el editor de páginas.
1. Abra la ficha** Cloud Services**.

1. Utilice la lista desplegable **Agregar configuración** para seleccionar **Adobe Analytics** entre las opciones disponibles. Si la herencia está colocada, debe deshabilitarla antes de que el selector esté disponible.

1. El selector desplegable de **Adobe Analytics** se agregará a las opciones disponibles. Utilícelo para seleccionar la configuración de marco requerida.

1. Seleccione **Guardar y cerrar**.
1. **[Publique](/help/sites-authoring/publishing-pages.md)**la página para activar la página y los archivos o configuraciones conectados.
1. El paso final es visitar la página en la instancia de publicación y buscar una palabra clave (por ejemplo, eggplate) utilizando el componente **Buscar** .
1. A continuación, puede comprobar las llamadas realizadas a Adobe Analytics con una herramienta adecuada; por ejemplo, [Adobe Marketing Cloud Debugger](https://marketing.adobe.com/resources/help/en_US/sc/implement/debugger_install.html).
1. Utilizando el ejemplo proporcionado, la llamada debe contener el valor introducido (es decir, eggcentral) en eVar7 y la lista de eventos debe contener event3.

### Vistas de la página {#page-views}

Cuando una página está asociada a un marco de Adobe Analytics, el número de vistas de página se puede mostrar en la vista de lista de la consola Sitios.

Consulte [Visualización de datos](/help/sites-authoring/page-analytics-using.md) de análisis de página para obtener más información.

### Configuración del intervalo de importación {#configuring-the-import-interval}

Configure la instancia adecuada del servicio de configuración **de encuestas administradas de** Adobe AEM:

* **Intervalo**de encuesta:
Intervalo, en segundos, en el que el servicio recupera datos de vista de página de Adobe Analytics.
El intervalo predeterminado es 43200000 ms (12 horas).

* **Habilitar**:
Habilite o deshabilite el servicio. De forma predeterminada, el servicio está habilitado.

Para configurar este servicio OSGi, puede utilizar la consola [](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) Web o un nodo [osgiConfig en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (el PID de servicio es `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Edición de configuraciones y/o marcos de Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Al igual que al crear una configuración o marco de Adobe Analytics, vaya a la pantalla (heredada) Servicios **de** nube. Seleccione **Mostrar configuraciones** y, a continuación, haga clic en el vínculo a la configuración específica que desee actualizar.

Al editar una configuración de Adobe Analytics, también debe pulsar el botón **Editar** en la página de configuración misma para abrir el cuadro de diálogo **Editar componente** .

## Eliminación de marcos de Adobe Analytics {#deleting-adobe-analytics-frameworks}

Para eliminar un marco de Adobe Analytics, primero [ábralo para editarlo](#editing-adobe-analytics-configurations-and-or-frameworks).

A continuación, seleccione **Eliminar marco** en la ficha **Página** de la barra de tareas.

