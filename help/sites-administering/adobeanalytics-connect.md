---
title: Conectarse a Adobe Analytics y crear marcos
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: Obtenga información sobre cómo conectar AEM al SiteCatalyst y crear marcos.
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 9%

---

# Conectarse a Adobe Analytics y crear marcos {#connecting-to-adobe-analytics-and-creating-frameworks}

Para rastrear datos web de sus páginas AEM en Adobe Analytics, cree una configuración de Adobe Analytics Cloud Services y un marco de trabajo de Adobe Analytics:

* **Configuración de Adobe Analytics:** La información sobre su cuenta de Adobe Analytics. La configuración de Adobe Analytics permite AEM conectarse a Adobe Analytics. Cree una configuración de Adobe Analytics para cada cuenta que utilice.
* **Adobe Analytics Framework:** Conjunto de asignaciones entre las propiedades de los grupos de informes de Adobe Analytics y las variables de CQ. Utilice un marco para configurar el modo en que los datos del sitio web rellenan los informes de Adobe Analytics. Los módulos están asociados a una configuración de Adobe Analytics. Puede crear varios marcos de trabajo para cada configuración.

Cuando asocia una página web con un marco, el marco realiza un seguimiento para esa página y los descendientes de dicha página. Las vistas de página se pueden recuperar de Adobe Analytics y mostrar en la consola Sitios .

## Requisitos previos {#prerequisites}

### Cuenta de Adobe Analytics {#adobe-analytics-account}

Para realizar un seguimiento de AEM datos en Adobe Analytics, debe tener una cuenta de Adobe Experience Cloud Adobe Analytics válida.

La cuenta de Adobe Analytics debe:

* Tiene **Administrador** privilegios
* Se asignará a la variable **Acceso a servicio web** grupo de usuarios.

>[!CAUTION]
>
>Proporcionar **Administrador** privilegios (dentro de Adobe Analytics) no es suficiente para permitir que un usuario se conecte de AEM a Adobe Analytics. La cuenta también debe tener **Acceso a servicio web** privilegios.

![chlimage_1-67](assets/chlimage_1-67.png)

Antes de continuar, asegúrese de que sus credenciales le permiten iniciar sesión en Adobe Analytics. A través de cualquiera de las siguientes opciones:

* [Inicio de sesión en Adobe Experience Cloud](https://experience.adobe.com/#/@login/home)

* [Inicio de sesión en Adobe Analytics](https://sc.omniture.com/login/)

### Configuración de AEM para usar sus centros de datos de Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [centros de datos](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) recopilar, procesar y almacenar datos asociados a su grupo de informes de Adobe Analytics. Configure AEM para utilizar el centro de datos que aloja su grupo de informes de Adobe Analytics. El centro de datos se menciona en el contrato. Póngase en contacto con un administrador de su organización para obtener esta información.

Si es necesario, utilice lo siguiente para enrutar al centro de datos correcto: `https://api.omniture.com/`.

Si su organización requiere la recopilación o recuperación de datos desde un centro de datos específico, utilice lo siguiente:

| Centro de datos | URL |
|---|---|
| Londres | `https://api3.omniture.com/` |
| Singapur | `https://api4.omniture.com/` |
| Oregón | `https://api5.omniture.com/` |

Utilice la variable [Consola web para configurar el paquete OSGi](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Adobe AEM cliente HTTP de Analytics**. Agregue la variable **URL del centro de datos** para el centro de datos que aloja un grupo de informes para el que sus páginas AEM recopilan datos.

![aa-07](assets/aa-07.png)

1. Abra la consola web en el explorador web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Para acceder a la consola, introduzca sus credenciales.

   >[!NOTE]
   >
   >Para averiguar si tiene acceso a esta consola, póngase en contacto con el administrador del sitio.

1. Seleccione el elemento de configuración denominado **Adobe AEM cliente HTTP de Analytics**.
1. Para añadir la dirección URL de un centro de datos, pulse el botón + situado junto al **Direcciones URL del centro de datos** y escriba la dirección URL en el cuadro.

1. Para eliminar una dirección URL de la lista, haga clic en el botón - situado junto a la dirección URL.
1. Haga clic en Guardar.

## Configuración de la conexión a Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>La variable [Complemento Activity Map proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es) debe usarse ahora.

## Configuración del Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>La variable [Complemento Activity Map proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es) debe usarse ahora.

## Creación de un marco de Adobe Analytics {#creating-a-adobe-analytics-framework}

Para el ID de grupo de informes (RSID) que utilice, puede controlar qué instancias de servidor (autor, publicación o ambas) contribuyen a los datos del grupo de informes:

* **Todo**: La información del autor y de la instancia de publicación rellena el grupo de informes.
* **Autor**: Solo la información de la instancia de autor rellena el grupo de informes.
* **Publicación**: Solo la información de la instancia de publicación rellena el grupo de informes.

>[!NOTE]
>
>La selección del tipo de instancia de servidor no restringe las llamadas a Adobe Analytics, solo controla qué llamadas incluyen el RSID.
>
>Por ejemplo, un marco de trabajo está configurado para usar el *diweretail* grupo de informes y autor es la instancia de servidor seleccionada. Cuando las páginas se publican junto con la infraestructura, las llamadas se realizan a Adobe Analytics, aunque estas llamadas no contienen el RSID. Solo las llamadas de la instancia de autor incluyen el RSID.

1. Uso **Navegación**, seleccione **Herramientas**, **Cloud Services**, luego **Cloud Services heredados**.
1. Desplácese hasta **Adobe Analytics** y seleccione **Mostrar configuraciones**.
1. Haga clic en el **[+]** vínculo junto a la configuración de Adobe Analytics.

1. En el **Crear marco** diálogo:

   * Especifique un **Título**.
   * Si lo desea, puede especificar la variable **Nombre**, para el nodo que almacena los detalles del marco en el repositorio.
   * Select **Adobe Analytics Framework**

   Y haga clic en **Crear**.

   El marco de trabajo se abrirá para editarlo.

1. En el **Grupos de informes** sección del pod lateral (lado derecho del panel principal), haga clic en **Agregar elemento**. A continuación, utilice la lista desplegable para seleccionar la ID del grupo de informes (por ejemplo, `geometrixxauth`) con la que interactúa el marco.

   >[!NOTE]
   >
   >El buscador de contenido de la izquierda se rellena con variables de Adobe Analytics (variables de SiteCatalyst) al seleccionar una ID de grupo de informes.

1. Para seleccionar las instancias de servidor a las que desea enviar información al grupo de informes, utilice el **Ejecutar modo** desplegable (junto al ID del grupo de informes).

   ![aa-framework-01](assets/aa-framework-01.png)

1. Para que el marco esté disponible en la instancia de publicación del sitio, en la variable **Página** ficha de la barra de tareas, haga clic en **Activar marco.**

### Configuración del servidor para Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

El sistema marco permite cambiar la configuración del servidor en cada marco de Adobe Analytics.

>[!CAUTION]
>
>Estos ajustes determinan dónde se envían los datos y cómo, por lo tanto, es imprescindible que *no manipule esta configuración* y deje que su representante de Adobe Analytics lo configure en su lugar.

Comience abriendo el panel. Presione la flecha hacia abajo junto a **Servidores**:

![server_001](assets/server_001.png)

* **Servidor de seguimiento**

   * contiene la dirección URL utilizada para enviar llamadas de Adobe Analytics

      * `cname` : toma el valor predeterminado de la cuenta de Adobe Analytics *Nombre de la empresa*
      * `d1` - corresponde al centro de datos al que se envía la información (o bien `d1`, `d2`o `d3`)
      * `sc.omtrdc.net` - nombre de dominio

* **Servidor de seguimiento seguro**

   * Tiene los mismos segmentos que el servidor de seguimiento
   * Se utiliza para enviar datos desde páginas seguras (`https://`)

* **Espacio de nombres del visitante**

   * El área de nombres determina la primera parte de la dirección URL de seguimiento.
   * Por ejemplo, si se cambia el área de nombres a **CNAME** hace que las llamadas realizadas a Adobe Analytics se asemejen a **CNAME.d1.omtrdc.net** en lugar del valor predeterminado.

## Asociación de una página a un marco de Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Cuando una página está asociada con un marco de Adobe Analytics, la página envía datos a Adobe Analytics cuando se carga la página. Las variables que rellena la página se asignan y recuperan de las variables de Adobe Analytics en la infraestructura. Por ejemplo, las vistas de página se recuperan de Adobe Analytics.

Los descendientes de la página heredan la asociación con la estructura. Por ejemplo, cuando se asocia la página raíz del sitio con un marco, todas las páginas del sitio se asocian con el marco.

1. En el **Sitios** , seleccione la página que desea configurar con seguimiento.
1. Abra el **[Propiedades de página](/help/sites-authoring/editing-page-properties.md)**, ya sea directamente desde la consola o desde el editor de páginas.
1. Abra la pestaña** Cloud Services**.

1. Utilice la variable **Agregar configuración** lista desplegable para seleccionar **Adobe Analytics** de las opciones disponibles. Si la herencia está en su lugar, deshabilite antes de que el selector esté disponible.

1. El selector desplegable de **Adobe Analytics** se anexa a las opciones disponibles. Seleccione la configuración del marco necesaria.

1. Select **Guardar y cerrar**.
1. Para activar la página y cualquier configuración o archivo conectado, **[Publicación](/help/sites-authoring/publishing-pages.md)** la página.
1. El paso final es visitar la página en la instancia de publicación y buscar una palabra clave (por ejemplo, eggfactory) utilizando la variable **Buscar** componente.
1. A continuación, puede comprobar las llamadas realizadas a Adobe Analytics con una herramienta adecuada; por ejemplo, [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. Utilizando el ejemplo proporcionado, la llamada debe contener el valor introducido (es decir, eggfactory) en eVar7 y la lista de eventos debe contener event3.

### Vistas de la página {#page-views}

Cuando una página está asociada con un marco de Adobe Analytics, el número de vistas de página se puede mostrar en la vista Lista de la consola Sitios .

Consulte [Visualización de datos de análisis de página](/help/sites-authoring/page-analytics-using.md) para obtener más información.

### Configuración del intervalo de importación {#configuring-the-import-interval}

Configure la instancia adecuada del **Adobe AEM configuración de sondeo administrado** servicio:

* **Intervalo de encuesta**: Intervalo, en segundos, en el que el servicio recupera los datos de vista de página de Adobe Analytics.
El intervalo predeterminado es 43200000 ms (12 horas).

* **Habilitar**: Habilite o deshabilite el servicio. De forma predeterminada, el servicio está habilitado.

Para configurar este servicio OSGi, puede usar la variable [Consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [nodo osgiConfig en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (el PID de servicio es `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Edición de configuraciones y/o marcos de Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Al igual que cuando se crea una configuración o un marco de Adobe Analytics, vaya a (heredado) **Cloud Services** en el Navegador. Select **Mostrar configuraciones** y, a continuación, haga clic en el vínculo a la configuración específica que desea actualizar.

Al editar una configuración de Adobe Analytics, presione **Editar** en la propia página de configuración para abrir el **Editar componente** diálogo.

## Eliminación de marcos de Adobe Analytics {#deleting-adobe-analytics-frameworks}

Para eliminar un marco de Adobe Analytics, primero [ábrala para editarla](#editing-adobe-analytics-configurations-and-or-frameworks).

A continuación, seleccione **Eliminar marco** de la variable **Página** de la barra de tareas.
