---
title: Integración con el Search&Promote de Adobe
description: Aprenda a integrar con el Search&Promote de Adobe.
uuid: 7e9384d9-9e4f-4e00-a1c9-35547de6ceb8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: aca444f6-418a-4c01-ae19-663b4e04fab9
docset: aem65
exl-id: 15f45978-a983-49a0-91cf-c7610fc37eef
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 1%

---

# Integración con el Search&amp;Promote de Adobe{#integrating-with-adobe-search-promote}

Para llamar al servicio de Search&amp;Promote de Adobe desde su sitio web, realice las siguientes tareas:

1. Especifique la dirección URL de Cloud.
1. Configure la conexión con el servicio de Search&amp;Promote.
1. Agregar componentes de Search&amp;Promote a la barra de tareas.
1. Utilice los componentes para crear el contenido. (Consulte [Agregar características de Search&amp;Promote a una página web](/help/sites-authoring/search-and-promote.md)).
1. Agregue banners a sus páginas. Las imágenes de banner son sensibles a los datos de Search&amp;Promote.
1. Genere un mapa del sitio para el servicio de Search&amp;Promote que desee consumir.

>[!NOTE]
>
>Si utiliza Search&amp;Promote con una configuración de proxy personalizada, debe configurar ambas configuraciones de proxy del cliente HTTP, ya que algunas funcionalidades de Adobe Experience Manager utilizan las API 3.x y otras las API 4.x:
>
>* 3.x está configurado con [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



## Cambiar la URL del servicio de Search&amp;Promote {#changing-the-search-promote-service-url}

La dirección URL predeterminada configurada para el servicio de Search&amp;Promote es `https://searchandpromote.omniture.com/px/`. Para usar un servicio diferente, use la consola OSGi para especificar una URL diferente.

1. Abra la consola OSGi y seleccione la pestaña **[!UICONTROL Configuration]**. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Seleccione el elemento Configuración de Search&amp;Promote Day CQ.
1. Introduzca la dirección URL en el cuadro URI del servidor remoto y seleccione **[!UICONTROL Guardar]**.

## Configuración de la conexión a Search&amp;Promote {#configuring-the-connection-to-search-promote}

Configure una o más conexiones a Search&amp;Promote para que las páginas web puedan interactuar con el servicio. Para conectarse, necesita la identificación del miembro y el número de cuenta de su cuenta de Search&amp;Promote.

1. En el Experience Manager, vaya a **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > seleccione **[!UICONTROL Cloud Services]**.

   Si está en un equipo local, la dirección URL del panel es similar a la siguiente:

   [https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. En la página Cloud Services, seleccione el vínculo Search&amp;Promote de Adobe o el icono de Search&amp;Promote.

1. Si está configurando el Search&amp;Promote de Adobe por primera vez, seleccione **[!UICONTROL Configurar ahora]** para abrir el panel Crear configuración.

   Para obtener más información sobre Search&amp;Promote, seleccione **[!UICONTROL Más información]**.

   ![](assets/chlimage_1-59.png)

1. Introduzca un **[!UICONTROL Título]** reconocible para los autores de la página e introduzca un **[!UICONTROL Nombre]** único.
1. Seleccione **[!UICONTROL Crear]**.

   Además, la configuración recién creada aparece debajo del **Configuraciones disponibles** en el elemento de lista Search&amp;Promote de Adobe **Cloud Services dashboard**.

   ![](assets/chlimage_1-60.png)

1. En el cuadro de diálogo **[!UICONTROL Editar componente]**, agregue lo siguiente a los campos.

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
   >A continuación, debe mirar la dirección URL en la barra de direcciones del explorador, que debería tener este aspecto:
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >**Donde:**
   >
   >    * **** XXXXXXXX corresponde a su** Id. de miembro**
   >    * **** spAAAAcorresponde a su número de  **cuenta**


1. Seleccione **[!UICONTROL Conectar a Search&amp;Promote]**.

   Cuando aparezca el mensaje de éxito de la conexión, seleccione **[!UICONTROL OK]**.

   (Después de la conexión, el texto del botón cambia a** Conectarse de nuevo a Search&amp;Promote**).

1. Seleccione **[!UICONTROL OK]**. Aparecerá la página Configuración de Search&amp;Promote para la configuración que ha creado.

## Configuración del centro de datos {#configuring-the-data-center}

Si la cuenta de Search&amp;Promote está en Asia o Europa, debe cambiar el centro de datos predeterminado para que apunte al correcto (el centro de datos predeterminado es para cuentas de América del Norte).

**Para configurar el centro de datos:**

1. Vaya a la consola web en `https://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`

   ![](assets/chlimage_1-61.png)

1. Según la ubicación del servidor, cambie el URI a uno de los siguientes:

   * América del Norte: [https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA: [https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC: [https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. Seleccione **[!UICONTROL Guardar]**.

## Agregar componentes de Search&amp;Promote a la barra de tareas {#adding-search-promote-components-to-sidekick}

En el modo Diseño, edite un componente **par** para permitir los componentes de Search&amp;Promote en la barra de tareas. (Consulte la documentación [Componentes](/help/sites-developing/components.md#addinganewcomponenttotheparagraphsystemdesignmode) para obtener más información).

Para obtener información sobre el uso de los componentes, consulte [Agregar características de Search&amp;Promote a una página web](/help/sites-authoring/search-and-promote.md)).

## Especificar el servicio de Search&amp;Promote que utilizan las páginas {#specifying-the-search-promote-service-that-your-pages-use}

Configure las páginas web para que utilicen un servicio de Search&amp;Promote específico. Los componentes de Search&amp;Promote utilizan automáticamente el servicio de su página de host.

Al configurar las propiedades de Search&amp;Promote de una página, todas las páginas secundarias heredan la configuración. Si es necesario, puede configurar páginas secundarias para anular la configuración heredada.

>[!NOTE]
>
>La conexión de servicio debe configurarse de antemano. (Consulte [Configuración de la conexión a Search&amp;Promote](#connection)).

1. Abra el cuadro de diálogo **[!UICONTROL Propiedades de página]**. Por ejemplo, en la página** Sitios web**, haga clic con el botón derecho en la página y seleccione **[!UICONTROL Propiedades]**.
1. Seleccione la pestaña **[!UICONTROL Cloud Services]**.
1. Para desactivar la herencia de las configuraciones de servicios de nube de una página principal, seleccione el icono de cerrojo situado junto a la ruta de herencia.

   ![](assets/sandpinheritpadlock.png)

1. Seleccione **[!UICONTROL Agregar servicio]**.
1. Seleccione **[!UICONTROL Adobe Search&amp;Promote]** y luego seleccione **[!UICONTROL Aceptar]**.
1. Seleccione la configuración de conexión de su cuenta de Search&amp;Promote y, a continuación, seleccione **OK**.

## Fuente de productos {#product-feed}

La integración de Search&amp;Promote le permite hacer lo siguiente:

* Utilice la API de comercio electrónico, independientemente de la estructura de repositorios subyacente y la plataforma de comercio.
* Utilice la función Conector de índice de Search&amp;Promote para poder tener una fuente de producto en formato XML.
* Utilice la función Control remoto de Search&amp;Promote si desea realizar solicitudes programadas o bajo demanda de la fuente de productos.
* Generación de fuentes para distintas cuentas de Search&amp;Promote, configuradas como configuraciones de servicios en la nube.

Para obtener más información, consulte [Fuente de productos](/help/sites-administering/product-feed.md).
