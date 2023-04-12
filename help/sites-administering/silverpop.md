---
title: Integración con Silverpop Engage
seo-title: Integrating with Silverpop Engage
description: Aprenda a integrar AEM con Silverpop Engage
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# Integración con Silverpop Engage{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

La integración de AEM con Silverpop Engage le permite administrar y enviar correos electrónicos creados en AEM a través de Silverpop. También le permite utilizar las funciones de administración de posibles clientes de Silverpop mediante AEM formularios en páginas AEM.

La integración le ofrece las siguientes funciones:

* La capacidad de crear correos electrónicos en AEM y publicarlos en Silverpop para su distribución.
* La capacidad de definir la acción de un formulario AEM para crear un suscriptor de Silverpop.

Una vez configurado Silverpop Engage, puede publicar newsletters o correos electrónicos en Silverpop Engage.

## Creación de una configuración de Silverpop {#creating-a-silverpop-configuration}

Las configuraciones de Silverpop se pueden agregar mediante **Cloud Services**, **Herramientas** o **Puntos finales de API**. Todos los métodos se describen en esta sección.

### Configuración de Silverpop mediante Cloud Services {#configuring-silverpop-via-cloudservices}

Para crear una configuración de Silverpop en Cloud Services:

1. En AEM, toque o haga clic en **Herramientas** > **Implementación** > **Cloud Services**. (O acceder directamente a `https://<hostname>:<port>/etc/cloudservices.html`.)
1. En Servicios de terceros, haga clic en **Silverop Engage** y luego **Configurar**. Se abre la ventana de configuración de Silverpop.

   >[!NOTE]
   >
   >Silverpop Engage no está disponible como opción en servicios de terceros a menos que descargue el paquete desde Package Share.

1. Introduzca un título y, opcionalmente, un nombre y haga clic en **Crear**. Se abre la ventana de configuración** Configuración de Silverpop**.
1. Introduzca el nombre de usuario, la contraseña y seleccione un extremo de API en la lista desplegable.
1. Haga clic en **Conéctese a Silverpop.** Cuando se haya conectado correctamente, verá un cuadro de diálogo de éxito. Haga clic en **OK** así que salga de la ventana. Puede ir a Silverpop haciendo clic en **Vaya a Silverpop Engage**.
1. Se ha configurado Silverpop. Puede editar la configuración haciendo clic en **Editar**.
1. Además, el marco de Silverpop Engage se puede configurar para acciones personalizadas proporcionando título y nombre (opcional). Haga clic en Crear crea correctamente el marco para la conexión de Silverpop ya configurada.

   Las columnas de extensión de datos importadas se pueden utilizar posteriormente a través del componente AEM: **Texto y personalización**.

### Configuración de Silverpop mediante Herramientas {#configuring-silverpop-via-tools}

Para crear una configuración de Silverpop en Herramientas:

1. En AEM, toque o haga clic en **Herramientas** > **Implementación** > **Cloud Services**. O navegue hasta allí directamente yendo a `https://<hostname>:<port>/misadmin#/etc`.
1. Select **Herramientas**, luego **Configuraciones de Cloud Services,** then **Silverpop Engage**.
1. Haga clic en **Nuevo**.

   ![Chlimage_1-6](assets/chlimage_1-6.jpeg)

1. En el **Crear página** , introduzca la variable **Título** y, opcionalmente, la variable **Nombre** y haga clic en **Crear**.
1. Introduzca la información de configuración tal como se indica en el paso 4 del procedimiento anterior. Siga ese procedimiento para finalizar la configuración de Silverpop.

### Adición de varias configuraciones {#adding-multiple-configurations}

Para agregar varias configuraciones:

1. En la página de bienvenida, haga clic en **Cloud Services** y haga clic en **Silverpop Engage**. Haga clic en **Mostrar configuraciones** que aparece si hay una o más configuraciones de Silverpop disponibles. Se enumeran todas las configuraciones disponibles.
1. Haga clic en el **+** junto a Configuraciones disponibles. Abre el **Crear configuraciones** ventana. Siga el procedimiento de configuración anterior para crear una configuración.

### Configuración de puntos finales de API para conectarse a Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Actualmente, AEM tiene seis puntos finales no protegidos (Participación 1 - 6). Silverpop ahora proporciona dos nuevos puntos finales y puntos finales de conexión cambiados para los existentes.

Para configurar los puntos finales de la API:

1. Vaya a `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` en `https://<hostname>:<port>/crxde.`
1. Haga clic con el botón derecho y seleccione **Crear**, luego **Crear nodo**.
1. Introduzca la variable **Nombre** como `sp-e0` y elija **Tipo** como `cq:Widget`.
1. Agregue dos propiedades al nodo recién agregado:

   1. **Nombre**: `text`, **Tipo**: `String`, **Valor**: `Engage 0`
   1. **Nombre**: `value`, **Tipo**: `String`, **Valor**: `https://api0.silverpop.com`

   ![imagen_1-42](assets/chlimage_1-42.png)

   Haga clic en Guardar todo.

1. Cree un nodo más con **Nombre** como `sp-e7` y **Tipo** como `cq:Widget`.

   Agregue dos propiedades al nodo recién agregado:

   1. **Nombre**: `text`, **Tipo**: `String`, **Valor**: `Pilot`
   1. **Nombre**: `value`, **Tipo**: `String`, **Valor**: `https://apipilot.silverpop.com/XMLAPI`

1. Para cambiar los puntos finales de la API existente (Participación 1 a 6), haga clic en cada uno de ellos de forma individual y reemplace los valores de la siguiente manera:

   | **Nombre de nodo** | **Valor de punto final existente** | **Nuevo valor de punto final** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. Haga clic en **Guardar todo**. AEM está listo para conectarse a Silverpop sobre puntos finales protegidos.

   ![Chlimage_1-7](assets/chlimage_1-7.jpeg)
