---
title: Integración con Silverpop Engage
seo-title: Integración con Silverpop Engage
description: Aprenda a integrar AEM con Silverpop Engage
seo-description: Aprenda a integrar AEM con Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e

---


# Integración con Silverpop Engage{#integrating-with-silverpop-engage}

>[!NOTE]
>
>La integración de Silverpop **no está** disponible de forma predeterminada. Debe descargar el paquete [de integración de](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) Silverpop desde Package Share e instalarlo en su instancia. Después de instalar el paquete, puede configurarlo como se describe en este documento.

La integración de AEM con Silverpop Engage le permite administrar y enviar correos electrónicos creados en AEM mediante Silverpop. También le permite utilizar las funciones de administración de posibles clientes de Silverpop mediante formularios AEM en páginas de AEM.

La integración proporciona las siguientes funciones:

* La capacidad de crear correos electrónicos en AEM y publicarlos en Silverpop para su distribución.
* La capacidad de definir la acción de un formulario AEM para crear un suscriptor de Silverpop.

Una vez configurado el compromiso de Silverpop, puede publicar newsletters o correos electrónicos en el compromiso de Silverpop.

## Creación de una configuración de Silverpop {#creating-a-silverpop-configuration}

Las configuraciones de Silverpop se pueden agregar mediante **Cloudservices**, **Herramientas** o puntos **finales** de API. Todos los métodos se describen en esta sección.

### Configuración de Silverpop mediante Cloudservices {#configuring-silverpop-via-cloudservices}

Para crear una configuración de Silverpop en Cloud Services:

1. En AEM, toque o haga clic en **Herramientas** > **Implementación** > Servicios **de nube**. (O acceso directo en `https://<hostname>:<port>/etc/cloudservices.html`).
1. En Servicios de terceros, haga clic en **Participación** de Silverop y, a continuación, en **Configurar**. Se abre la ventana de configuración de Silverpop.

   >[!NOTE]
   >
   >Silverpop Engage no está disponible como opción en servicios de terceros a menos que descargue el paquete desde Package Share.

1. Enter a title and optionally, a name and click **Create**. Se abre la ventana de configuración** Configuración de Silverpop**.
1. Introduzca el nombre de usuario, la contraseña y seleccione un punto final de API en la lista desplegable.
1. Haga clic en **Conectar a Silverpop.** Cuando se ha conectado correctamente, se muestra un cuadro de diálogo de éxito. Haga clic en **Aceptar** para salir de la ventana. Puede ir a Silverpop haciendo clic en **Ir a Participación** de Silverpop.
1. Silverpop se ha configurado. Puede editar la configuración haciendo clic en **Editar**.
1. Además, el marco de participación de Silverpop puede configurarse para acciones personalizadas proporcionando título y nombre (opcional). Haga clic en Crear creará correctamente el marco para la conexión Silverpop ya configurada.

   Las columnas de extensión de datos importados se pueden utilizar posteriormente a través del componente AEM: **Texto y Personalización**.

### Configuración de Silverpop mediante Herramientas {#configuring-silverpop-via-tools}

Para crear una configuración de Silverpop en Herramientas:

1. En AEM, toque o haga clic en **Herramientas** > **Implementación** > Servicios **de nube**. O navegue allí directamente yendo a `https://<hostname>:<port>/misadmin#/etc`.
1. Seleccione **Herramientas**, Configuración de servicios de **nube y, a continuación,** Participación de **Silverpop**.
1. Haga clic en **Nuevo** para abrir la ventana **Crear página**.

   ![climage_1-6](assets/chlimage_1-6.jpeg)

1. Introduzca el **Título** y, opcionalmente, el **Nombre** y haga clic en **Crear**.
1. Introduzca la información de configuración como se indica en el paso 4 del procedimiento anterior. Siga ese procedimiento para finalizar la configuración de Silverpop.

### Adición de varias configuraciones {#adding-multiple-configurations}

Para agregar varias configuraciones:

1. En la página de bienvenida, haga clic en Servicios **de** nube y en Participación de **Silverpop**. Haga clic en el botón **Mostrar configuraciones** que aparece si hay una o más configuraciones de Silverpop disponibles. Se enumeran todas las configuraciones disponibles.
1. Haga clic en el signo **+** junto a Configuraciones disponibles. Se abre la ventana **Crear configuraciones** . Siga el procedimiento de configuración anterior para crear una nueva configuración.

### Configuración de los puntos finales de API para la conexión a Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Actualmente, AEM cuenta con seis puntos finales no seguros (Participación 1 a 6). Silverpop ahora proporciona dos nuevos puntos finales, así como puntos finales de conexión cambiados para los existentes.

Para configurar los puntos finales de la API:

1. Ir a `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` la `https://<hostname>:<port>/crxde.`
1. Haga clic con el botón derecho y seleccione **Crear** y, a continuación, **Crear nodo**.
1. Introduzca el **Nombre** como `sp-e0` y elija **Tipo** como `cq:Widget`.
1. Agregue dos propiedades al nodo recién agregado:

   1. **Nombre**: `text`, **Tipo**: `String`, **Valor**: `Engage 0`
   1. **Nombre**: `value`, **Tipo**: `String`, **Valor**: `https://api0.silverpop.com`
   ![chlimage_1-42](assets/chlimage_1-42.png)

   Haga clic en el botón &quot;Guardar todo&quot;.

1. Cree un nodo más con **Nombre** como `sp-e7` y **Tipo** como `cq:Widget`.

   Agregue dos propiedades al nodo recién agregado:

   1. **Nombre**: `text`, **Tipo**: `String`, **Valor**: `Pilot`
   1. **Nombre**: `value`, **Tipo**: `String`, **Valor**: `https://apipilot.silverpop.com/XMLAPI`

1. Para cambiar los puntos finales de API existentes (Participación del 1 al 6), haga clic en cada uno de ellos uno por uno y sustituya los valores de la siguiente manera:

   | **Nombre de nodo** | **Valor de punto final existente** | **Nuevo valor de punto final** |
   |---|---|---|
   | sp-e1 | https://api.engage2.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. Haga clic en **Guardar todo**. AEM ya está listo para conectarse a Silverpop en puntos finales protegidos.

   ![climage_1-7](assets/chlimage_1-7.jpeg)

