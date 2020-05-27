---
title: Experiencia de Página de inicio de recursos de Adobe Experience Manager
description: Personalice la Página de inicio Experience Manager Assets para disfrutar de una experiencia de pantalla de bienvenida completa, incluida una instantánea de las actividades recientes sobre los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---


# Experiencia de Página de inicio de recursos de Adobe Experience Manager {#aem-assets-home-page-experience}

Personalice la página de inicio Recursos Adobe Experience Manager para disfrutar de una experiencia de pantalla de bienvenida completa, incluida una instantánea de las actividades recientes sobre los recursos.

La página de inicio de recursos proporciona una experiencia de pantalla de bienvenida completa y personalizada, que incluye una instantánea de actividades recientes, como recursos que se han visualizado o cargado recientemente.

La página de inicio Recursos está deshabilitada de forma predeterminada. Para habilitarlo, realice los siguientes pasos:

1. Abra Experience Manager Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Day CQ DAM Evento Recorder]** .
1. Seleccione **[!UICONTROL Activar este servicio]** para activar la grabación de actividades.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. En la lista **[!UICONTROL Tipos de evento]** , seleccione los eventos que desea registrar y guarde los cambios.

   >[!CAUTION]
   >
   >Al habilitar las opciones de vista de recursos, de proyectos vistos y de colecciones, se aumenta considerablemente el número de eventos registrados.

1. Abra el servicio Marca **[!UICONTROL de característica de Página de inicio de recursos]** DAM desde Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleccione la `isEnabled.name` opción para activar la función de Página de inicio de recursos. Guarde los cambios.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra el cuadro de diálogo Preferencias **[!UICONTROL de]** usuario y seleccione **[!UICONTROL Activar Página de inicio]** de recursos. Guarde los cambios.

   ![Activar página de inicio de recursos en el cuadro de diálogo Preferencias del usuario](assets/Annotation-color.png)

Después de activar la Página de inicio Recursos, navegue a la interfaz de usuario de Recursos desde la página de navegación o acceda a ella directamente desde la URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar vínculo de experiencia en la interfaz de usuario de Recursos](assets/config-experience-link.png)

Haga clic en el **[!UICONTROL vínculo]** Haga clic aquí para configurar la experiencia y agregar el nombre de usuario, la imagen de fondo y la imagen de perfil.

La Página de inicio Recursos incluye las siguientes secciones:

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

**Actividad**: En esta sección, la utilidad **[!UICONTROL Mi Actividad]** muestra las actividades recientes realizadas por el usuario que ha iniciado sesión con los recursos (incluidos los recursos sin representaciones), como cargas de recursos, descargas, creación de recursos, ediciones, comentarios, anotaciones y compartidos.

**Reciente**: La utilidad Vista **** recientemente de esta sección muestra las entidades a las que ha accedido recientemente el usuario que ha iniciado sesión, incluidas las carpetas, las colecciones y los proyectos.

**Discover**: La **[!UICONTROL nueva]** utilidad de esta sección muestra los recursos y las representaciones cargados recientemente en la instancia de Recursos.

Para habilitar la depuración de datos de actividad de usuario, habilite el servicio **[!UICONTROL de depuración de Eventos]** DAM desde Configuration Manager. Después de habilitar este servicio, el sistema elimina las actividades del usuario que ha iniciado sesión y que exceden un número especificado.

La pantalla de bienvenida proporciona ayuda para la navegación sencilla, por ejemplo, iconos en la barra de herramientas para acceder a carpetas, colecciones y catálogos.

>[!NOTE]
>
>Al habilitar los servicios de grabación [!UICONTROL de Evento de CQ DAM] Day y de depuración de Eventos  DAM, aumentan las operaciones de escritura en JCR e indexación de búsqueda, lo que aumenta considerablemente la carga en el servidor de Experience Manager. La carga adicional en el servidor de Experience Manager puede afectar a su rendimiento.

>[!CAUTION]
>
>La captura, el filtrado y la depuración de actividades de usuario necesarias para la página de inicio de Recursos imponen una sobrecarga en el rendimiento. Por lo tanto, los administradores deben configurar la Página de inicio de forma eficaz para los usuarios de destinatario.
>
>Adobe recomienda que los administradores y usuarios que realizan operaciones masivas eviten utilizar la función de Página de inicio de recursos para evitar un aumento en las actividades de los usuarios. Además, los administradores pueden excluir las actividades de grabación para usuarios específicos configurando el grabador [!UICONTROL de Evento CQ DAM] de Day desde [!UICONTROL Configuration Manager].
>
>Si utiliza la función, Adobe recomienda programar la frecuencia de purga en función de la carga del servidor.
