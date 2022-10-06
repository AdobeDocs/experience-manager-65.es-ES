---
title: "[!DNL Assets] Experiencia de la página principal"
description: Personalice el [!DNL Experience Manager Assets] Página de inicio para una experiencia de pantalla de bienvenida completa, que incluye una instantánea de las actividades recientes relacionadas con los recursos.
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] Experiencia de la página principal {#aem-assets-home-page-experience}

Personalice el [!DNL Adobe Experience Manager Assets] página de inicio para una experiencia de pantalla de bienvenida completa, que incluye una instantánea de las actividades recientes relacionadas con los recursos.

[!DNL Assets] la página de inicio proporciona una experiencia de pantalla de bienvenida completa y personalizada, que incluye una instantánea de actividades recientes, como recursos que se han visualizado o cargado recientemente.

La variable [!DNL Assets] la página principal está deshabilitada de forma predeterminada. Para habilitarlo, realice los pasos siguientes:

1. Apertura [!DNL Experience Manager] Administrador de configuración `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el **[!UICONTROL Grabador de eventos de CQ DAM de día]** servicio.
1. Seleccione el **[!UICONTROL Habilitar este servicio]** para activar el registro de actividades.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. En el **[!UICONTROL Tipos de eventos]** , seleccione los eventos que desea registrar y guarde los cambios.

   >[!CAUTION]
   >
   >Al habilitar las opciones Recurso visto, Proyectos vistos y Colecciones vistas , aumenta significativamente la cantidad de eventos registrados.

1. Abra el **[!UICONTROL Indicador de características de la página principal del recurso DAM]** servicio desde Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`.
1. Seleccione el `isEnabled.name` para habilitar la variable [!DNL Assets] función de la página principal. Guarde los cambios.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Abra el **[!UICONTROL Preferencias de usuario]** y seleccione **[!UICONTROL Activar la página principal de los recursos]**. Guarde los cambios.

   ![Activar la página de inicio de los recursos en el cuadro de diálogo Preferencias de usuario](assets/Annotation-color.png)

Después de habilitar la variable [!DNL Assets] Página de inicio, vaya a la [!DNL Assets] interfaz de usuario desde la página Navegación o acceda a ella directamente desde la dirección URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![configurar el vínculo de experiencia en la interfaz de usuario de Assets](assets/config-experience-link.png)

Haga clic en el **[!UICONTROL Haga clic aquí para configurar el vínculo de experiencia]** para agregar su nombre de usuario, imagen de fondo e imagen de perfil.

La variable [!DNL Assets] La página principal incluye las siguientes secciones:

* Sección de bienvenida
* Sección Widget

**Sección de bienvenida**

Si su perfil existe, la sección de bienvenida muestra un mensaje de bienvenida dirigido a usted. Además, muestra la imagen de perfil y una imagen de bienvenida (si ya está configurada).

Si el perfil está incompleto, la sección de bienvenida muestra un mensaje de bienvenida genérico y un marcador de posición para la imagen del perfil.

**Sección Widget**

Esta sección aparece debajo de la sección de bienvenida y muestra las utilidades integradas en las siguientes secciones:

* Actividad
* Reciente
* Descubrir

**Actividad**: En esta sección, la variable **[!UICONTROL Mi actividad]** widget muestra las actividades recientes realizadas por el usuario que ha iniciado sesión con recursos (incluidos los recursos sin representaciones), por ejemplo, cargas de recursos, descargas, creación de recursos, ediciones, comentarios, anotaciones y compartidos.

**Reciente**: La variable **[!UICONTROL Vistos recientemente]** en esta sección se muestran las entidades a las que el usuario que ha iniciado sesión ha accedido recientemente, incluidas las carpetas, las colecciones y los proyectos.

**Discover**: La variable **[!UICONTROL Nuevo]** en esta sección se muestran los recursos y las representaciones cargados recientemente en el [!DNL Assets] implementación.

Para habilitar la depuración de los datos de actividad del usuario, habilite la variable **[!UICONTROL Servicio de depuración de eventos DAM]** de Configuration Manager. Después de habilitar este servicio, el sistema eliminará las actividades del usuario que ha iniciado sesión y que superen un número especificado.

La pantalla de bienvenida proporciona ayuda para la navegación sencilla, por ejemplo, iconos en la barra de herramientas para acceder a carpetas, colecciones y catálogos.

>[!NOTE]
>
>Al habilitar la variable [!UICONTROL Grabador de eventos de CQ DAM de día] y [!UICONTROL Depuración de eventos DAM] Los servicios aumentan las operaciones de escritura en JCR y la indexación de búsquedas, lo que aumenta significativamente la carga en el [!DNL Experience Manager] servidor. La carga adicional en el [!DNL Experience Manager] el servidor puede afectar a su rendimiento.

>[!CAUTION]
>
>Captura, filtrado y depuración de las actividades de usuario necesarias para [!DNL Assets] la página principal impone una sobrecarga en el rendimiento. Por lo tanto, los administradores deben configurar la página principal de forma eficaz para los usuarios objetivo.
>
>Adobe recomienda que los administradores y usuarios que realizan operaciones masivas eviten utilizar la función Página principal de los recursos para evitar un aumento en las actividades de los usuarios. Además, los administradores pueden excluir las actividades de grabación para usuarios específicos configurando [!UICONTROL Grabador de eventos de CQ DAM de día] from [!UICONTROL Administrador de configuración].
>
>Si utiliza la función , Adobe recomienda programar la frecuencia de depuración en función de la carga del servidor.
