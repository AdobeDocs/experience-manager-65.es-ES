---
title: '[!DNL Assets] Experiencia de página de inicio'
description: Personalice la Página de inicio [!DNL Experience Manager Assets] para disfrutar de una experiencia de pantalla de bienvenida completa, incluida una instantánea de las actividades recientes sobre los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] Experiencia de página de inicio  {#aem-assets-home-page-experience}

Personalice la página de inicio [!DNL Adobe Experience Manager Assets] para disfrutar de una experiencia de pantalla de bienvenida rica, incluida una instantánea de las actividades recientes sobre los recursos.

[!DNL Assets] página de inicio ofrece una experiencia de pantalla de bienvenida completa y personalizada, que incluye una instantánea de actividades recientes, como recursos que se han visualizado o cargado recientemente.

La página de inicio [!DNL Assets] está deshabilitada de forma predeterminada. Para habilitarlo, realice los siguientes pasos:

1. Abra [!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Grabador de Eventos CQ DAM]**.
1. Seleccione **[!UICONTROL Habilitar este servicio]** para habilitar la grabación de actividad.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. En la lista **[!UICONTROL Tipos de evento]**, seleccione los eventos que se van a registrar y guarde los cambios.

   >[!CAUTION]
   >
   >Al habilitar las opciones de vista de recursos, de proyectos vistos y de colecciones, se aumenta considerablemente el número de eventos registrados.

1. Abra el servicio **[!UICONTROL Marca de característica de Página de inicio de recursos de DAM]** desde Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleccione la opción `isEnabled.name` para habilitar la función de Página de inicio [!DNL Assets]. Guarde los cambios.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra el cuadro de diálogo **[!UICONTROL Preferencias del usuario]** y seleccione **[!UICONTROL Habilitar Página de inicio de recursos]**. Guarde los cambios.

   ![Activar página de inicio de recursos en el cuadro de diálogo Preferencias del usuario](assets/Annotation-color.png)

Después de habilitar la Página de inicio [!DNL Assets], navegue a la interfaz de usuario [!DNL Assets] desde la página de navegación o acceda a ella directamente desde la dirección URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar vínculo de experiencia en la interfaz de usuario de Recursos](assets/config-experience-link.png)

Haga clic en **[!UICONTROL Haga clic aquí para configurar el vínculo de experiencia]** para agregar el nombre de usuario, la imagen de fondo y la imagen de perfil.

La Página de inicio [!DNL Assets] incluye las siguientes secciones:

* Sección de bienvenida
* Sección de utilidades

**Sección de bienvenida**

Si su perfil existe, la sección de bienvenida muestra un mensaje de bienvenida dirigido a usted. Además, muestra la imagen del perfil y una imagen de bienvenida (si ya está configurada).

Si el perfil está incompleto, la sección de bienvenida muestra un mensaje de bienvenida genérico y un marcador de posición para la imagen del perfil.

**Sección de utilidades**

Esta sección aparece debajo de la sección de bienvenida y muestra los widgets predeterminados en las siguientes secciones:

* Actividad
* Reciente
* Descubrir

**Actividad**: En esta sección, la utilidad  **[!UICONTROL Mi]** actividad muestra actividades recientes realizadas por el usuario que ha iniciado sesión con recursos (incluidos recursos sin representaciones), por ejemplo, cargas de recursos, descargas, creación de recursos, ediciones, comentarios, anotaciones y compartidos.

**Reciente**: La utilidad  **[!UICONTROL Vista]** reciente de esta sección muestra las entidades a las que ha accedido recientemente el usuario que ha iniciado sesión, incluidas las carpetas, las colecciones y los proyectos.

**Discover**: La  **** nueva utilidad de esta sección muestra los recursos y las representaciones cargados recientemente en la  [!DNL Assets] implementación.

Para habilitar la depuración de datos de actividad de usuario, habilite el **[!UICONTROL servicio de depuración de Eventos DAM]** desde Configuration Manager. Después de habilitar este servicio, el sistema elimina las actividades del usuario que ha iniciado sesión y que exceden un número especificado.

La pantalla de bienvenida proporciona ayuda para la navegación sencilla, por ejemplo, iconos en la barra de herramientas para acceder a carpetas, colecciones y catálogos.

>[!NOTE]
>
>Al habilitar los servicios [!UICONTROL Day CQ DAM Evento Recorder] y [!UICONTROL DAM Evento Purge], aumentan las operaciones de escritura en JCR e indexación de búsqueda, lo que aumenta significativamente la carga en el servidor [!DNL Experience Manager]. La carga adicional en el servidor [!DNL Experience Manager] puede afectar a su rendimiento.

>[!CAUTION]
>
>Capturar, filtrar y purgar las actividades de usuario necesarias para la página de inicio [!DNL Assets] impone una sobrecarga en el rendimiento. Por lo tanto, los administradores deben configurar la Página de inicio de forma eficaz para los usuarios de destinatario.
>
>Adobe recomienda que los administradores y usuarios que realizan operaciones masivas eviten utilizar la función de Página de inicio de recursos para evitar un aumento de las actividades de los usuarios. Además, los administradores pueden excluir actividades de grabación para usuarios específicos configurando [!UICONTROL Grabador de Eventos DAM CQ de día] desde [!UICONTROL Configuration Manager].
>
>Si utiliza la función, Adobe recomienda programar la frecuencia de purga en función de la carga del servidor.
