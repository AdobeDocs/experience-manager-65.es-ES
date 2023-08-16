---
title: Integración con Silverpop Engage
seo-title: Integrating with Silverpop Engage
description: AEM Aprenda a integrar el servicio de integración con el servicio de Silverpop Engage
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# Integración con Silverpop Engage{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

AEM AEM La integración de la con Silverpop Engage le permite administrar y enviar correos electrónicos creados en a través de Silverpop. AEM AEM También le permite utilizar las funciones de administración de posibles clientes de Silverpop a través de formularios en forma de en páginas de informes.

La integración ofrece las siguientes funciones:

* AEM La capacidad de crear correos electrónicos en la publicación y publicarlos en Silverpop para su distribución.
* AEM La capacidad de establecer la acción de un formulario para crear un suscriptor de Silverpop.

Una vez configurado Silverpop Engage, puede publicar boletines informativos o correos electrónicos en Silverpop Engage.

## Creación de una configuración de Silverpop {#creating-a-silverpop-configuration}

Las configuraciones de Silverpop se pueden añadir mediante **Cloud Service**, **Herramientas**, o **Puntos finales de API**. Todos los métodos se describen en esta sección.

### Configuración de Silverpop mediante Cloud Service {#configuring-silverpop-via-cloudservices}

Para crear una configuración de Silverpop en Cloud Service:

1. AEM En, toque o haga clic en **Herramientas** > **Implementación** > **Cloud Service**. (O acceda directamente a en `https://<hostname>:<port>/etc/cloudservices.html`.)
1. En Servicios de terceros, haga clic en **Silverop Engage** y luego **Configurar**. Se abre la ventana de configuración de Silverpop.

   >[!NOTE]
   >
   >Silverpop Engage no está disponible como opción en los servicios de terceros a menos que descargue el paquete desde Package Share.

1. Introduzca un título y, opcionalmente, un nombre y haga clic en **Crear**. Se abre la ventana de configuración de ** Configuración ** Silverpop.
1. Introduzca el nombre de usuario y la contraseña, y seleccione un punto final de API en la lista desplegable.
1. Clic **Conéctese a Silverpop.** Cuando se haya conectado correctamente, verá un cuadro de diálogo de éxito. Clic **OK** así que sales de la ventana. Puede ir a Silverpop haciendo clic en **Ir a Silverpop Engage**.
1. Silverpop se ha configurado. Puede editar la configuración haciendo clic en **Editar**.
1. Además, el marco de Silverpop Engage se puede configurar para acciones personalizadas proporcionando título y nombre (opcional). Al hacer clic en Crear, se crea correctamente el marco de trabajo para la conexión de Silverpop ya configurada.

   AEM Las columnas de extensión de datos importadas se pueden utilizar posteriormente a través del componente de: **Texto y personalización**.

### Configuración de Silverpop mediante Herramientas {#configuring-silverpop-via-tools}

Para crear una configuración de Silverpop en Herramientas:

1. AEM En, toque o haga clic en **Herramientas** > **Implementación** > **Cloud Service**. O vaya directamente a la página `https://<hostname>:<port>/misadmin#/etc`.
1. Seleccionar **Herramientas**, entonces **Configuraciones de Cloud Service,** entonces **Silverpop Engage**.
1. Clic **Nuevo**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. En el **Crear página** , introduzca la **Título** y, opcionalmente, el **Nombre** y haga clic en **Crear**.
1. Introduzca la información de configuración como se describe en el paso 4 del procedimiento anterior. Siga ese procedimiento para poder finalizar la configuración de Silverpop.

### Añadir varias configuraciones {#adding-multiple-configurations}

Para agregar varias configuraciones:

1. En la página de bienvenida, haga clic en **Cloud Service** y haga clic en **Silverpop Engage**. Clic **Mostrar configuraciones** que aparece si hay una o más configuraciones de Silverpop disponibles. Se muestran todas las configuraciones disponibles.
1. Haga clic en **+** junto a Configuraciones disponibles. Se abre el **Crear configuraciones** ventana. Siga el procedimiento de configuración anterior para poder crear una configuración.

### Configuración de puntos finales de API para conectarse a Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

AEM Actualmente, tiene seis puntos finales no seguros (Participación 1 a 6). Silverpop ahora proporciona dos nuevos puntos finales y puntos finales de conexión modificados para los existentes.

Para configurar los puntos finales de la API:

1. Ir a `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` el `https://<hostname>:<port>/crxde.`
1. Haga clic con el botón derecho y seleccione **Crear**, entonces **Crear nodo**.
1. Introduzca el **Nombre** as `sp-e0` y elija **Tipo** as `cq:Widget`.
1. Agregue dos propiedades al nodo recién agregado:

   1. **Nombre**: `text`, **Tipo**: `String`, **Valor**: `Engage 0`
   1. **Nombre**: `value`, **Tipo**: `String`, **Valor**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Haga clic en &quot;Guardar todo&quot;.

1. Cree un nodo más con **Nombre** as `sp-e7` y **Tipo** as `cq:Widget`.

   Agregue dos propiedades al nodo recién agregado:

   1. **Nombre**: `text`, **Tipo**: `String`, **Valor**: `Pilot`
   1. **Nombre**: `value`, **Tipo**: `String`, **Valor**: `https://apipilot.silverpop.com/XMLAPI`

1. Para cambiar los puntos finales de la API existentes (participación 1 a 6), haga clic en cada uno de ellos uno por uno y reemplace los valores de la siguiente manera:

   | **Nombre de nodo** | **Valor de punto final existente** | **Nuevo valor de punto final** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. Haga clic en **Guardar todo**. AEM Ahora está listo para conectarse a Silverpop a través de puntos finales seguros.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
