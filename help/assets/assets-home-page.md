---
title: "[!DNL Assets] Experiencia en la página de inicio"
description: Personalice el [!DNL Experience Manager Assets] Página de inicio para disfrutar de una pantalla de bienvenida enriquecida, que incluye una instantánea de las actividades recientes relacionadas con los recursos.
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] Experiencia de página de inicio {#aem-assets-home-page-experience}

Personalice el [!DNL Adobe Experience Manager Assets] página de inicio para disfrutar de una experiencia de pantalla de bienvenida enriquecida, que incluye una instantánea de las actividades recientes en torno a los recursos.

[!DNL Assets] la página de inicio proporciona una experiencia de pantalla de bienvenida enriquecida y personalizada, que incluye una instantánea de las actividades recientes, como los recursos que se han visto o cargado recientemente.

El [!DNL Assets] la página de inicio está desactivada de forma predeterminada. Para habilitarlo, realice los siguientes pasos:

1. Abrir [!DNL Experience Manager] Administrador de configuración `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el **[!UICONTROL Grabador de eventos de CQ DAM de día]** servicio.
1. Seleccione el **[!UICONTROL Habilitar este servicio]** para habilitar la grabación de actividades.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Desde el **[!UICONTROL Tipos de eventos]** , seleccione los eventos que desea registrar y guarde los cambios.

   >[!CAUTION]
   >
   >Al habilitar las opciones Recursos vistos, Proyectos vistos y Colecciones vistas, aumenta significativamente el número de eventos registrados.

1. Abra el **[!UICONTROL Marca de característica de página principal de recursos DAM]** servicio del Administrador de configuración `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleccione el `isEnabled.name` para activar la opción [!DNL Assets] Función Página de inicio. Guarde los cambios.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra el **[!UICONTROL Preferencias de usuario]** y seleccione. **[!UICONTROL Habilitar página de inicio de recursos]**. Guarde los cambios.

   ![Habilitar la página de inicio de los recursos en el cuadro de diálogo Preferencias de usuario](assets/Annotation-color.png)

Después de activar el [!DNL Assets] Página de inicio, vaya a [!DNL Assets] interfaz de usuario de desde la página de navegación o acceda a ella directamente desde la dirección URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configuración del vínculo de experiencia en la interfaz de usuario de Assets](assets/config-experience-link.png)

Haga clic en **[!UICONTROL Haga clic aquí para configurar su vínculo de experiencia]** para agregar su nombre de usuario, imagen de fondo e imagen de perfil.

El [!DNL Assets] La página de inicio incluye las siguientes secciones:

* Sección de bienvenida
* Sección Widget

**Sección de bienvenida**

Si su perfil existe, la sección Bienvenido muestra un mensaje de bienvenida dirigido a usted. Además, muestra la imagen de perfil y una imagen de bienvenida (si ya está configurada).

Si el perfil está incompleto, la sección Bienvenida muestra un mensaje de bienvenida genérico y un marcador de posición para la imagen de perfil.

**Sección Widget**

Esta sección aparece debajo de la sección Bienvenido y muestra widgets predeterminados en las siguientes secciones:

* Actividad
* Reciente
* Descubrir

**Actividad**: En esta sección, la variable **[!UICONTROL Mi actividad]** widget muestra las actividades recientes realizadas por el usuario que ha iniciado sesión con recursos (incluidos los recursos sin representaciones), por ejemplo cargas de recursos, descargas, creación de recursos, ediciones, comentarios, anotaciones y recursos compartidos.

**Reciente**: La **[!UICONTROL Vistos recientemente]** el widget de esta sección muestra las entidades a las que el usuario que ha iniciado sesión ha accedido recientemente, incluidas las carpetas, las colecciones y los proyectos.

**Discover**: La **[!UICONTROL Nuevo]** widget en esta sección muestra los recursos y representaciones cargados recientemente en [!DNL Assets] implementación.

Para habilitar la depuración de los datos de actividad del usuario, habilite la **[!UICONTROL Servicio de purga de eventos DAM]** en el Administrador de configuración. Después de habilitar este servicio, el sistema eliminará las actividades del usuario que haya iniciado sesión y que superen un número especificado.

La pantalla de bienvenida proporciona ayudas para la navegación sencillas, como iconos en la barra de herramientas para acceder a carpetas, colecciones y catálogos.

>[!NOTE]
>
>Activación de la [!UICONTROL Grabador de eventos de CQ DAM de día] y [!UICONTROL Depuración de eventos DAM] Los servicios de aumentan las operaciones de escritura en JCR y la indexación de búsqueda, lo que aumenta significativamente la carga en el [!DNL Experience Manager] servidor. La carga adicional en el [!DNL Experience Manager] puede afectar al rendimiento del servidor.

>[!CAUTION]
>
>Captura, filtrado y purga de las actividades de usuario necesarias para [!DNL Assets] la página principal impone una sobrecarga en el rendimiento. Por lo tanto, los administradores deben configurar Página principal de forma eficaz para los usuarios de destino.
>
>El Adobe recomienda que los administradores y usuarios que realizan operaciones masivas eviten utilizar la función Página principal de recursos para evitar un aumento en las actividades de los usuarios. Además, los administradores pueden excluir las actividades de grabación para usuarios específicos configurando [!UICONTROL Grabador de eventos de CQ DAM de día] de [!UICONTROL Administrador de configuración].
>
>Si utiliza la función, Adobe recomienda planificar la frecuencia de depuración en función de la carga del servidor.
