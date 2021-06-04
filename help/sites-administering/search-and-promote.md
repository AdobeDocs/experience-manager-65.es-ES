---
title: Integración con el Search&Promote de Adobe
seo-title: Integración con el Search&Promote de Adobe
description: Aprenda a integrar con el Search&Promote de Adobe.
seo-description: Aprenda a integrar con el Search&Promote de Adobe.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
exl-id: 15f45978-a983-49a0-91cf-c7610fc37eef
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---

# Integración con el Search&amp;Promote de Adobe{#integrating-with-adobe-search-promote}

Para llamar al servicio de Search&amp;Promote de Adobe desde su sitio web, realice las siguientes tareas:

1. Especifique la dirección URL de Cloud.
1. Configure la conexión con el servicio de Search&amp;Promote.
1. Agregar componentes de Search&amp;Promote a la barra de tareas.
1. Utilice los componentes para crear el contenido. (Consulte [Adición de funciones de Search&amp;Promote a una página web](/help/sites-authoring/search-and-promote.md)).
1. Agregue banners a sus páginas. Las imágenes de banner son sensibles a los datos de Search&amp;Promote.
1. Genere un mapa del sitio para el servicio de Search&amp;Promote que desee consumir.

>[!NOTE]
>
>Si utiliza Search&amp;Promote con una configuración de proxy personalizada, debe configurar ambas configuraciones de proxy del cliente HTTP, ya que algunas funcionalidades de AEM utilizan las API 3.x y otras las API 4.x:
>
>* 3.x está configurado con [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Cambio de la URL del servicio de Search&amp;Promote {#changing-the-search-promote-service-url}

La dirección URL predeterminada configurada para el servicio de Search&amp;Promote es `https://searchandpromote.omniture.com/px/`. Para usar un servicio diferente, use la consola OSGi para especificar una URL diferente.

1. Abra la consola OSGi y haga clic en la ficha Configuración . ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Haga clic en el elemento Configuración de Search&amp;Promote de CQ de día .
1. Introduzca la URL en el cuadro URI del servidor remoto y haga clic en Guardar.

## Configuración de la conexión a Search&amp;Promote {#configuring-the-connection-to-search-promote}

Configure una o más conexiones a Search&amp;Promote para que las páginas web puedan interactuar con el servicio. Para conectarse, necesita la identificación del miembro y el número de cuenta de su cuenta de Search&amp;Promote.

1. En el icono **Tools** > **Deployment**, seleccione **Cloud Services**.

   Esto le lleva al panel de Cloud Services. Si se encuentra en un equipo local, la dirección URL del tablero tendrá este aspecto:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. En la página Cloud Services, haga clic en el vínculo Search&amp;Promote de Adobe o en el icono de Search&amp;Promote.

1. Si es la primera vez que configura el Search&amp;Promote de Adobe, haga clic en **Configurar ahora** para abrir el panel Crear configuración.

   Si desea obtener más información sobre la Search&amp;Promote, haga clic en **Más información** en su lugar.

   ![](assets/chlimage_1-59.png)

1. Introduzca un **Título** reconocible para los autores de la página, introduzca un **Nombre** único y, a continuación, haga clic en **Crear**.

   Se abre la ventana **Editar componente**.

   Además, la configuración recién creada aparece debajo del **Configuraciones disponibles** en el elemento de lista Search&amp;Promote de Adobe **Cloud Services dashboard**.

   ![](assets/chlimage_1-60.png)

1. Agregue lo siguiente a los campos del cuadro de diálogo **Editar componente**.

   * **ID de miembro**
   * **Número de cuenta**

   >[!NOTE]
   >
   >Para obtener esta información **usted mismo,** primero debe iniciar sesión
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >
   >con sus credenciales válidas de Search&amp;Promote (correo electrónico/contraseña).
   >A continuación, debe mirar la dirección URL en la barra de direcciones del explorador, que debería tener un aspecto similar al siguiente:
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Donde:**
   >
   >    * **** XXXXXXXX corresponde a su** Id. de miembro**
   >    * **** spAAAAcorresponde a su número de  **cuenta**


1. Haga clic en **Conectar a Search&amp;Promote**.

   Cuando aparezca el mensaje de éxito de la conexión, haga clic en **OK**.

   (Después de la conexión, el texto del botón cambia a** Conectarse de nuevo a Search&amp;Promote**).

1. Haga clic en **Aceptar**. Aparecerá la página Configuración de Search&amp;Promote para la configuración que acaba de crear.

## Configuración del centro de datos {#configuring-the-data-center}

Si la cuenta de Search&amp;Promote está en Asia o Europa, debe cambiar el centro de datos predeterminado para que apunte al correcto (el centro de datos predeterminado es para cuentas de América del Norte).

Para configurar el centro de datos:

1. Vaya a la consola web en `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. Según la ubicación del servidor, cambie el URI a uno de los siguientes:

   * América del Norte: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Haga clic en **Guardar**.

## Adición de componentes de Search&amp;Promote a la barra de tareas {#adding-search-promote-components-to-sidekick}

En el modo Diseño, edite un componente **par** para permitir los componentes de Search&amp;Promote en la barra de tareas. (Consulte la documentación [Componentes](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) para obtener más información).

Para obtener información sobre el uso de los componentes, consulte [Adición de funciones de Search&amp;Promote a una página web](/help/sites-authoring/search-and-promote.md)).

## Especificación del servicio de Search&amp;Promote que utilizan las páginas {#specifying-the-search-promote-service-that-your-pages-use}

Configure las páginas web para que utilicen un servicio de Search&amp;Promote específico. Los componentes de Search&amp;Promote utilizan automáticamente el servicio de su página de host.

Al configurar las propiedades de Search&amp;Promote de una página, todas las páginas secundarias heredan la configuración. Si es necesario, puede configurar páginas secundarias para anular la configuración heredada.

>[!NOTE]
>
>La conexión de servicio ya debe estar configurada. (Consulte [Configuración de la conexión a Search&amp;Promote](#connection)).

1. Abra el cuadro de diálogo **Propiedades de página**. Por ejemplo, en la página** Sitios web**, haga clic con el botón derecho en la página y haga clic en **Propiedades**.
1. Haga clic en la pestaña **Cloud Services**.
1. Para desactivar la herencia de las configuraciones de servicios de nube de una página principal, haga clic en el icono de cerrojo situado junto a la ruta de herencia.

   ![](assets/sandpinheritpadlock.png)

1. Haga clic en **Añadir servicio**, seleccione **Search&amp;Promote de Adobe** y haga clic en **Aceptar**.
1. Seleccione la configuración de conexión de su cuenta de Search&amp;Promote y haga clic en **OK**.

## Fuente de productos {#product-feed}

La integración de Search&amp;Promote le permite:

* utilice la API de comercio electrónico, independientemente de la estructura de repositorios subyacente y la plataforma de comercio.
* utilice la función Conector de índice de Search&amp;Promote para proporcionar una fuente de producto en formato XML.
* aproveche la función Control remoto de Search&amp;Promote para realizar solicitudes programadas o bajo demanda de la fuente de productos
* generación de fuentes para distintas cuentas de Search&amp;Promote, configuradas como configuraciones de servicios en la nube.

Para obtener más información, lea [Fuente de productos](/help/sites-administering/product-feed.md).
