---
title: Conectarse a Adobe Analytics y crear marcos
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: AEM Obtenga información acerca de cómo conectar a los usuarios con el SiteCatalyst y crear marcos de trabajo.
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

AEM Para realizar un seguimiento de los datos web de sus páginas de en Adobe Analytics, cree una configuración de servicios de Adobe Analytics Cloud y un marco de trabajo de Adobe Analytics:

* **Configuración de Adobe Analytics:** La información sobre su cuenta de Adobe Analytics. La configuración de Adobe Analytics AEM le permite a los usuarios conectarse a Adobe Analytics de forma remota. Cree una configuración de Adobe Analytics para cada cuenta que utilice.
* **Adobe Analytics Framework:** Un conjunto de asignaciones entre las propiedades del grupo de informes de Adobe Analytics y las variables de CQ. Utilice un marco de trabajo para configurar cómo los datos del sitio web rellenan los informes de Adobe Analytics. Los módulos están asociados a una configuración de Adobe Analytics. Puede crear varios marcos de trabajo para cada configuración.

Cuando asocia una página web con un marco de trabajo, este realiza el seguimiento de esa página y de sus descendientes. Las vistas de página se pueden recuperar desde Adobe Analytics y mostrar en la consola Sitios.

## Requisitos previos {#prerequisites}

### Cuenta de Adobe Analytics {#adobe-analytics-account}

AEM Para realizar un seguimiento de los datos de la en Adobe Analytics, debe tener una cuenta de Adobe Experience Cloud Adobe Analytics válida.

La cuenta de Adobe Analytics debe:

* Tener **Administrador** privilegios
* Se le asignará al **Acceso a servicio web** grupo de usuarios.

>[!CAUTION]
>
>Proporcionar **Administrador** Los privilegios de (en Adobe Analytics AEM Adobe Analytics) no son suficientes para permitir que un usuario se conecte desde la red de trabajo a la red de trabajo de. La cuenta también debe tener **Acceso a servicio web** privilegios.

![chlimage_1-67](assets/chlimage_1-67.png)

Antes de continuar, asegúrese de que sus credenciales le permiten iniciar sesión en Adobe Analytics. Mediante cualquiera de las siguientes acciones:

* [Inicio de sesión en Adobe Experience Cloud](https://experience.adobe.com/#/@login/home)

* [Inicio de sesión en Adobe Analytics](https://sc.omniture.com/login/)

### AEM Configuración de la configuración para utilizar los centros de datos de Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [centros de datos](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) recopilar, procesar y almacenar datos asociados a su grupo de informes de Adobe Analytics. AEM Configure para utilizar el centro de datos que aloja el grupo de informes de Adobe Analytics. El centro de datos se menciona en el contrato. Póngase en contacto con un administrador de su organización para obtener esta información.

Si es necesario, utilice lo siguiente para dirigirlo al centro de datos correcto: `https://api.omniture.com/`.

Si su organización requiere la recopilación o recuperación de datos de un centro de datos específico, utilice lo siguiente:

| Centro de datos | URL |
|---|---|
| Londres | `https://api3.omniture.com/` |
| Singapur | `https://api4.omniture.com/` |
| Oregón | `https://api5.omniture.com/` |

Utilice el [Consola web para configurar el paquete OSGi](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Cliente HTTP de Adobe AEM Analytics**. Añada el **URL del centro de datos** AEM para el centro de datos que aloja un grupo de informes para el que las páginas de la aplicación recopilan datos de forma.

![aa-07](assets/aa-07.png)

1. Abra la consola web en el explorador web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Para acceder a la consola, introduzca sus credenciales.

   >[!NOTE]
   >
   >Para saber si tiene acceso a esta consola, póngase en contacto con el administrador del sitio.

1. Seleccione el elemento de configuración llamado **Cliente HTTP de Adobe AEM Analytics**.
1. Para añadir la dirección URL de un centro de datos, pulse el botón + situado junto al **URL del centro de datos** y escriba la dirección URL en el cuadro.

1. Para quitar una dirección URL de la lista, haga clic en el botón - situado junto a la dirección URL.
1. Haga clic en Guardar.

## Configuración de la conexión con Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>El [Complemento Activity Map proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es) debería utilizarse ahora.

## Configuración para el Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>El [Complemento Activity Map proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es) debería utilizarse ahora.

## Creación de un marco de Adobe Analytics {#creating-a-adobe-analytics-framework}

En el caso del ID del grupo de informes (RSID) que esté utilizando, puede controlar qué instancias de servidor (autor, publicación o ambas) aportan datos al grupo de informes:

* **Todo**: la información tanto del autor como de la instancia de publicación rellena el grupo de informes.
* **Autor**: Solo la información de la instancia de autor rellena el grupo de informes.
* **Publish**: Solo la información de la instancia de publicación rellena el grupo de informes.

>[!NOTE]
>
>La selección del tipo de instancia de servidor no restringe las llamadas a Adobe Analytics, solo controla qué llamadas incluyen el RSID.
>
>Por ejemplo, un marco de trabajo está configurado para utilizar la variable *diweretail* report suite and author es la instancia de servidor seleccionada. Cuando las páginas se publican junto con el marco de trabajo, se siguen realizando llamadas a Adobe Analytics, pero estas llamadas no contienen el RSID. Solo las llamadas de la instancia de autor incluyen el RSID.

1. Uso de **Navegación**, seleccione **Herramientas**, **Cloud Services**, entonces **Cloud Services heredados**.
1. Desplazarse a **Adobe Analytics** y seleccione **Mostrar configuraciones**.
1. Haga clic en **[+]** junto a la configuración de Adobe Analytics.

1. En el **Crear marco** diálogo:

   * Especifique un **Título**.
   * Si lo desea, puede especificar **Nombre**, para el nodo que almacena los detalles del marco de trabajo en el repositorio.
   * Seleccionar **Adobe Analytics Framework**

   Y haga clic en **Crear**.

   El marco de trabajo se abrirá para editarlo.

1. En el **Grupos de informes** de la barra lateral (lado derecho del panel principal), haga clic en **Agregar elemento**. A continuación, utilice la lista desplegable para seleccionar el ID del grupo de informes (por ejemplo, `geometrixxauth`) con el que interactúa el marco de trabajo.

   >[!NOTE]
   >
   >El buscador de contenido de la izquierda se rellena con variables de Adobe Analytics (variables de SiteCatalyst) al seleccionar un ID de grupo de informes.

1. Para seleccionar las instancias de servidor que desea enviar información al grupo de informes, utilice el **Modo de ejecución** desplegable (junto a la ID del grupo de informes).

   ![aa-framework-01](assets/aa-framework-01.png)

1. Para que el marco de trabajo esté disponible en la instancia de publicación del sitio, en **Página** pestaña de la barra de tareas, haga clic en **Activar marco.**

### Configuración del servidor para Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

El sistema de marcos permite cambiar la configuración del servidor dentro de cada marco de trabajo de Adobe Analytics.

>[!CAUTION]
>
>Esta configuración determina dónde se envían los datos y cómo, por lo que es imperativo que *no alterar esta configuración* y deje que su representante de Adobe Analytics lo configure en su lugar.

Comience por abrir el panel. Presione la flecha hacia abajo situada junto a **Servidores**:

![server_001](assets/server_001.png)

* **Servidor de seguimiento**

   * contiene la dirección URL utilizada para enviar llamadas de Adobe Analytics

      * `cname` - toma como valor predeterminado el de la cuenta de Adobe Analytics *Nombre de empresa*
      * `d1` : corresponde al centro de datos al que se envía la información (o bien `d1`, `d2`, o `d3`)
      * `sc.omtrdc.net` - nombre de dominio

* **Servidor de seguimiento seguro**

   * Tiene los mismos segmentos que el servidor de seguimiento
   * Se utiliza para enviar datos desde páginas seguras (`https://`)

* **Espacio de nombres del visitante**

   * El área de nombres determina la primera parte de la dirección URL de seguimiento.
   * Por ejemplo, cambiar el área de nombres a **CNAME** hace que las llamadas realizadas a Adobe Analytics tengan el aspecto siguiente **CNAME.d1.omtrdc.net** en lugar del predeterminado.

## Asociación de una página a un marco de trabajo de Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Cuando una página está asociada a un marco de trabajo de Adobe Analytics, la página envía datos a Adobe Analytics cuando se carga la página. Las variables que rellena la página se asignan y recuperan de las variables de Adobe Analytics en el marco de trabajo. Por ejemplo, las vistas de página se recuperan de Adobe Analytics.

Los descendientes de la página heredan la asociación con el marco. Por ejemplo, cuando asocia la página raíz del sitio con un marco de trabajo, todas las páginas del sitio se asocian al marco de trabajo.

1. Desde el **Sites** , seleccione la página que desea configurar con el seguimiento.
1. Abra el **[Propiedades de página](/help/sites-authoring/editing-page-properties.md)**, directamente desde la consola o desde el editor de páginas.
1. Abra la pestaña** Cloud Services **.

1. Utilice el **Agregar configuración** menú desplegable para seleccionar **Adobe Analytics** en las opciones disponibles. Si se hereda, desactívelo antes de que el selector esté disponible.

1. El selector desplegable de **Adobe Analytics** se anexa a las opciones disponibles. Seleccione la configuración del marco de trabajo necesaria.

1. Seleccionar **Guardar y cerrar**.
1. Para activar la página y cualquier configuración o archivo conectado, **[Publish](/help/sites-authoring/publishing-pages.md)** la página.
1. El paso final es visitar la página en la instancia de publicación y buscar una palabra clave (por ejemplo, berenjena) utilizando **Buscar** componente.
1. A continuación, puede comprobar las llamadas realizadas a Adobe Analytics mediante una herramienta adecuada; por ejemplo, [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. Utilizando el ejemplo proporcionado, la llamada debe contener el valor introducido (es decir, berenjena) en eVar 7 y la lista de eventos debe contener event3.

### Vistas de la página {#page-views}

Cuando una página está asociada a un marco de trabajo de Adobe Analytics, el número de vistas de página se puede mostrar en la vista de lista de la consola Sitios.

Consulte [Ver datos de análisis de página](/help/sites-authoring/page-analytics-using.md) para obtener más información.

### Configuración del intervalo de importación {#configuring-the-import-interval}

Configure la instancia adecuada del **Configuración de encuestas administradas de Adobe AEM** servicio:

* **Intervalo de encuesta**: Intervalo, en segundos, con el que el servicio recupera los datos de vista de página de Adobe Analytics.
El intervalo predeterminado es de 43200000 ms (12 horas).

* **Activar**: habilite o deshabilite el servicio. El servicio está habilitado de forma predeterminada.

Para configurar este servicio OSGi, puede usar el [Consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un [nodo osgiConfig en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (el PID de servicio es `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Edición de configuraciones y/o marcos de Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Al igual que al crear una configuración o un marco de trabajo de Adobe Analytics, vaya a (heredado) **Cloud Services** pantalla. Seleccionar **Mostrar configuraciones** A continuación, haga clic en el vínculo a la configuración específica que desee actualizar.

Al editar una configuración de Adobe Analytics, pulse **Editar** cuando se encuentra en la propia página de configuración para abrir **Editar componente** diálogo.

## Eliminación de marcos de Adobe Analytics {#deleting-adobe-analytics-frameworks}

Para eliminar un módulo de Adobe Analytics, primero debe hacer lo siguiente [ábralo para editarlo](#editing-adobe-analytics-configurations-and-or-frameworks).

A continuación seleccione **Eliminar marco** desde el **Página** pestaña de la barra de tareas.
