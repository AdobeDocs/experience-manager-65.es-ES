---
title: Integración con Adobe Search&Promote
seo-title: Integración con Adobe Search&Promote
description: Obtenga información sobre cómo integrarse con Adobe Search&Promote.
seo-description: Obtenga información sobre cómo integrarse con Adobe Search&Promote.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Integrating with Adobe Search&amp;Promote{#integrating-with-adobe-search-promote}

Para llamar al servicio Adobe Search&amp;Promote desde su sitio web, realice las siguientes tareas:

1. Especifique la dirección URL de la nube.
1. Configure la conexión con el servicio Search&amp;Promote.
1. Agregue componentes de Search&amp;Promote a la barra de tareas.
1. Utilice los componentes para crear el contenido. (Consulte [Adición de funciones de Search&amp;Promote a una página](/help/sites-authoring/search-and-promote.md)Web).
1. Agregue letreros a las páginas. Las imágenes de pancarta son sensibles a los datos de Search&amp;Promote.
1. Genere un mapa del sitio para que lo consuma el servicio Search&amp;Promote.

>[!NOTE]
>
>Si utiliza Search&amp;Promote con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de AEM están usando las API 3.x y otras las API 4.x:
>
>* 3.x está configurado con [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



## Cambio de la dirección URL del servicio de Search&amp;Promote {#changing-the-search-promote-service-url}

La dirección URL predeterminada configurada para el servicio Search&amp;Promote es `https://searchandpromote.omniture.com/px/`. Para utilizar un servicio diferente, utilice la consola OSGi para especificar una dirección URL diferente.

1. Abra la consola OSGi y haga clic en la ficha Configuración. ([https://localhost:4502/system/console/configMgr.](https://localhost:4502/system/console/configMgr))
1. Haga clic en el elemento Configuración de Day CQ Search&amp;Promote.
1. Introduzca la dirección URL en el cuadro URI del servidor remoto y haga clic en Guardar.

## Configuración de la conexión con Search&amp;Promote {#configuring-the-connection-to-search-promote}

Configure una o más conexiones a Search&amp;Promote para que las páginas Web puedan interactuar con el servicio. Para conectarse, necesita la identificación de miembros y el número de cuenta de su cuenta de Search&amp;Promote.

1. En el icono **Herramientas** > **Implementación**, seleccione **Cloud Services**.

   Esto lo lleva al panel de servicios de nube. Si se encuentra en un equipo local, la dirección URL del tablero tendrá este aspecto:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. En la página Servicios de nube, haga clic en el vínculo de Adobe Search&amp;Promote o en el icono de Search&amp;Promote.

1. Si es la primera vez que configura Adobe Search&amp;Promote, haga clic en **Configurar ahora** para abrir el panel Crear configuración.

   Si desea obtener más información sobre Search&amp;Promote, haga clic en **Más información** en su lugar.

   ![](assets/chlimage_1-59.png)

1. Introduzca un **Título** que sea reconocible por los autores de la página, un **Nombre**&#x200B;único y, a continuación, haga clic en **Crear**.

   The **Edit Component** window opens.

   Además, la configuración recién creada aparece debajo de Configuraciones **** disponibles en el elemento de lista del panel **Servicios de** nube de Adobe Search&amp;Promote.

   ![](assets/chlimage_1-60.png)

1. Agregue lo siguiente a los campos del cuadro de diálogo **Editar componente** .

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
   >Luego, debe mirar su dirección URL en la barra de direcciones del explorador, que debería tener este aspecto:
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Donde:**
   >
   >    * **XXXXXXXX** corresponde a su** identificación de miembro***
   >    * **spYYYYYY** corresponde con su número **de cuenta**


1. Click **Connect To Search&amp;Promote**.

   Cuando aparezca el mensaje de éxito de la conexión, haga clic en **Aceptar**.

   (Después de la conexión, el texto del botón cambia a** Volver a conectar con Search&amp;Promote**).

1. Haga clic en **Aceptar**. Aparece la página Configuración de Search&amp;Promote para la configuración que acaba de crear.

## Configuración del centro de datos {#configuring-the-data-center}

Si su cuenta de Search&amp;Promote está en Asia o Europa, debe cambiar el centro de datos predeterminado para que apunte al correcto (el centro de datos predeterminado es para cuentas de Norteamérica).

Para configurar el centro de datos:

1. Vaya a la consola web en `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. Según la ubicación del servidor, cambie el URI a uno de los siguientes:

   * Norteamérica: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Haga clic en **Guardar**.

## Adición de componentes de Search&amp;Promote a la barra de tareas {#adding-search-promote-components-to-sidekick}

En el modo Diseño, edite un componente **par** para permitir los componentes de Search&amp;Promote en la barra de tareas. (See the [Components](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) documentation for more information.)

Para obtener información sobre el uso de los componentes, consulte [Adición de funciones de Search&amp;Promote a una página](/help/sites-authoring/search-and-promote.md)Web).

## Especificación del servicio Search&amp;Promote que utilizan las páginas {#specifying-the-search-promote-service-that-your-pages-use}

Configure las páginas web para que utilicen un servicio Search&amp;Promote específico. Los componentes de Search&amp;Promote utilizan automáticamente el servicio de la página de host.

Al configurar las propiedades de Search&amp;Promote para una página, todas las páginas secundarias heredan la configuración. Si es necesario, puede configurar las páginas secundarias para anular la configuración heredada.

>[!NOTE]
>
>La conexión de servicio ya debe estar configurada. (Consulte [Configuración de la conexión con Search&amp;Promote](#connection)).

1. Abra el cuadro de diálogo Propiedades **de la página** . Por ejemplo, en la página** Sitios web**, haga clic con el botón secundario en la página y haga clic en **Propiedades**.
1. Haga clic en la ficha Servicios **de** nube.
1. Para desactivar la herencia de las configuraciones de servicios en la nube desde una página principal, haga clic en el icono de cerrojo situado junto a la ruta de herencia.

   ![](assets/sandpinheritpadlock.png)

1. Haga clic en **Agregar servicio**, seleccione **Adobe Search&amp;Promote** y haga clic en **Aceptar**.
1. Seleccione la configuración de conexión de su cuenta de Search&amp;Promote y, a continuación, haga clic en **Aceptar**.

## Product Feed {#product-feed}

La integración de Search&amp;Promote permite:

* utilice la API de comercio electrónico, independientemente de la estructura de repositorio subyacente y la plataforma de comercio.
* aproveche la función Conector de índice de Search&amp;Promote para proporcionar una fuente de producto en formato XML.
* aproveche la función de control remoto de Search&amp;Promote para realizar solicitudes programadas o a petición de la fuente de productos
* generación de fuentes para distintas cuentas de Search&amp;Promote, configuradas como configuraciones de servicios en la nube.

Para obtener más información, consulte [Alimentación](/help/sites-administering/product-feed.md)de productos.
