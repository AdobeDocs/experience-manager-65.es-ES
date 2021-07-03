---
title: Digital Rights Management de los activos
description: Aprenda a administrar los estados de caducidad de los recursos y la información de los recursos con licencia en [!DNL Experience Manager].
contentOwner: AG
role: User, Admin
feature: DRM,Administración de activos
exl-id: a49cfd25-e8d9-492f-be5e-acab0cf67a28
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 5%

---

# Digital Rights Management para los recursos {#digital-rights-management-in-assets}

Los recursos digitales suelen estar asociados a una licencia que especifica los términos y la duración del uso. Como [!DNL Adobe Experience Manager Assets] está totalmente integrado con la plataforma [!DNL Experience Manager], puede administrar de forma eficaz la información de caducidad de recursos y los estados de los recursos. También puede asociar información de licencias con recursos.

## Caducidad del recurso {#asset-expiration}

La caducidad de los activos es una forma eficaz de hacer cumplir los requisitos de licencia de los activos. Garantiza que el recurso publicado se cancele cuando caduque, lo que evita la posibilidad de que se produzca cualquier infracción de licencia. Un usuario sin permisos de administrador no puede editar, copiar, mover, publicar ni descargar un recurso caducado.

Puede ver el estado de caducidad de un recurso en la consola [!DNL Assets] en las vistas de tarjeta y lista.

![expire_flag_list](assets/expired_flag_list.png)

*Figura: En la vista de lista, la columna   Estado muestra el   titular Caducado.*

Puede ver el estado de caducidad de un recurso en la [!UICONTROL Línea de tiempo] en el carril izquierdo.

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>La fecha de caducidad de un recurso se muestra de forma diferente para los usuarios de diferentes zonas horarias.

También puede ver el estado de caducidad de los recursos en el carril **[!UICONTROL Referencias]**. Administra los estados de caducidad de los recursos y las relaciones entre los recursos compuestos y los subrecursos, colecciones y proyectos a los que se hace referencia.

1. Desplácese al recurso para el que desea ver las páginas web de referencia y los recursos compuestos.
1. Seleccione el recurso y abra **[!UICONTROL References]** en el carril izquierdo. Para los recursos caducados, el carril [!UICONTROL References] muestra el estado de caducidad **[!UICONTROL Asset is Expired]** en la parte superior.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Si el recurso tiene subrecursos caducados, el carril [!UICONTROL References] muestra el estado **[!UICONTROL Asset has Expired Sub-Assets]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Buscar recursos caducados {#search-expired-assets}

Puede buscar recursos caducados, incluidos subrecursos caducados, en el panel Buscar .

1. En la consola [!DNL Assets], haga clic en **[!UICONTROL Buscar]** en la barra de herramientas para mostrar el cuadro Omnisearch.

1. Con el cursor en el cuadro Omnisearch , seleccione la clave `Enter` para mostrar la página de resultados de la búsqueda.
1. Abra el panel de búsqueda en el carril izquierdo. Haga clic en la opción **[!UICONTROL Expiry Status]** para expandirla.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Seleccione **[!UICONTROL Caducado]**. Solo se muestran los recursos caducados después de filtrar los resultados de la búsqueda.

Al elegir la opción **[!UICONTROL Expired]**, la consola [!DNL Assets] solo muestra los recursos y subrecursos caducados a los que hacen referencia los recursos compuestos. Los recursos compuestos que hacen referencia a subrecursos caducados no se muestran inmediatamente después de que caduquen los subrecursos. En su lugar, se muestran después de que [!DNL Experience Manager] detecte que hacen referencia a subrecursos caducados la próxima vez que se ejecute el planificador.

Si modifica la fecha de caducidad de un recurso publicado a una fecha anterior al ciclo del planificador actual, la programación seguirá detectando este recurso como activo caducado la próxima vez que se ejecute y reflejará su estado en consecuencia.

Además, si un fallo o error impide que el planificador detecte activos caducados en el ciclo actual, el planificador vuelve a examinar estos activos en el siguiente ciclo y detecta su estado caducado.

Para permitir que la consola [!DNL Assets] muestre los recursos compuestos de referencia junto con los subrecursos caducados, configure un flujo de trabajo **[!UICONTROL Adobe CQ DAM Expiry Notification]** en el Administrador de configuración [!DNL Experience Manager].

1. Abra el Administrador de configuración [!DNL Experience Manager].
1. Seleccione **[!UICONTROL Notificación de caducidad de Adobe CQ DAM]**. De forma predeterminada, está seleccionado **[!UICONTROL Programador basado en tiempo]**, que programa un trabajo para comprobar en un momento específico si un recurso tiene subrecursos caducados. Una vez finalizado el trabajo, los recursos que tienen subrecursos caducados y recursos a los que se hace referencia se muestran como caducados en los resultados de la búsqueda.

1. Para ejecutar el trabajo periódicamente, desactive el campo **[!UICONTROL Regla de planificador basada en tiempo]** y modifique el tiempo en segundos en el campo **[!UICONTROL Programador periódico]**. Por ejemplo, la expresión de ejemplo `0 0 0 &ast; &ast; ?` déclencheur el trabajo a las 00 horas.
1. Seleccione **[!UICONTROL enviar correo electrónico]** para recibir correos electrónicos cuando caduque un recurso.

   >[!NOTE]
   >
   >Solo el creador de recursos (la persona que carga un recurso en particular en [!DNL Assets]) recibe un correo electrónico cuando caduca el recurso. Consulte [cómo configurar la notificación por correo electrónico](/help/sites-administering/notification.md) para obtener más información sobre la configuración de las notificaciones por correo electrónico en el nivel general [!DNL Experience Manager].

1. En el campo **[!UICONTROL Notificación previa en segundos]**, especifique el tiempo en segundos antes de que un recurso caduque cuando desee recibir una notificación sobre su caducidad. Los creadores de recursos reciben un mensaje antes de la caducidad del recurso que les informa de que el recurso está a punto de caducar después de la hora especificada. Una vez que el recurso caduca, recibe otra notificación que confirma la caducidad. Además, los recursos caducados se desactivan.

1. Haga clic en **[!UICONTROL Guardar]**.

## Estados de los recursos {#asset-states}

La consola [!DNL Assets] puede mostrar varios estados para los recursos. En función del estado actual de un recurso concreto, su vista de tarjeta muestra una etiqueta que describe su estado, por ejemplo, Caducado, Publicado, Aprobado, Rechazado, etc.

1. En la interfaz de usuario [!DNL Assets], seleccione un recurso.
1. Haga clic en **[!UICONTROL Publicar]** en la barra de herramientas. Si no ve **Publish** en la barra de herramientas, haga clic en **[!UICONTROL Más]** en la barra de herramientas y busque la opción **[!UICONTROL Publish]** ![publish option](assets/do-not-localize/publish-globe.png).
1. Elija **[!UICONTROL Publicar]** en el menú y cierre el cuadro de diálogo de confirmación.
1. Salga del modo de selección. El estado de publicación del recurso aparece en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, la columna Publicado muestra la hora en que se publicó el recurso.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Para mostrar la página de detalles del recurso, en la interfaz [!DNL Assets], seleccione un recurso y haga clic en **[!UICONTROL Propiedades]** ![ver propiedades](assets/do-not-localize/info-circle-icon.png).

1. En la pestaña [!UICONTROL Advanced], establezca una fecha de caducidad para el recurso en el campo **[!UICONTROL Expires]**.

   ![establecer la fecha y hora de caducidad del recurso en el campo Caduca](assets/asset-properties-advanced-tab.png)

   *Figura:   Pestaña Avanzada de la página   Propiedades del recurso para establecer la caducidad del recurso.*

1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, haga clic en **[!UICONTROL Cerrar]** para mostrar la consola de recursos.
1. El estado de publicación del recurso indica un estado caducado en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, el estado del recurso se muestra como **[!UICONTROL Expired]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. En la consola [!DNL Assets], seleccione una carpeta y cree una tarea de revisión en la carpeta.
1. Revise y apruebe/rechace los recursos en la tarea de revisión y haga clic en **[!UICONTROL Completar]**.
1. Vaya a la carpeta para la que creó la tarea de revisión. El estado de los recursos que ha aprobado o rechazado se muestra en la parte inferior de la vista de tarjeta. En la vista de lista, los estados de aprobación y caducidad se muestran en las columnas correspondientes.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. Para buscar recursos en función de su estado, haga clic en **[!UICONTROL Buscar]** ![opción de búsqueda](assets/do-not-localize/search_icon.png) para mostrar la barra Omnisearch.
1. Seleccione `Return` y haga clic en [!DNL Experience Manager] para mostrar el panel de búsqueda.
1. En el panel de búsqueda, haga clic en **[!UICONTROL Estado de publicación]** y seleccione **[!UICONTROL Publicado]** para buscar recursos publicados en [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Haga clic en **[!UICONTROL Approval Status]** y haga clic en la opción correspondiente para buscar recursos aprobados o rechazados.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Para buscar recursos en función de su estado de caducidad, seleccione **[!UICONTROL Estado de caducidad]** en el panel Buscar y elija la opción adecuada.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. También puede buscar recursos en función de una combinación de estados en varias facetas de búsqueda. Por ejemplo, puede buscar recursos publicados que se hayan aprobado en una tarea de revisión y que aún no hayan caducado seleccionando las opciones adecuadas en las facetas de búsqueda.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management en [!DNL Assets] {#digital-rights-management-in-assets-1}

Esta función exige la aceptación del acuerdo de licencia antes de poder descargar un recurso con licencia desde [!DNL Adobe Experience Manager Assets].

Si selecciona un recurso protegido y hace clic en **[!UICONTROL Descargar]**, se le redirigirá a una página de licencia para aceptar el acuerdo de licencia. Si no acepta el acuerdo de licencia, la opción **[!UICONTROL Download]** no está disponible.

Si la selección contiene varios recursos protegidos, seleccione un recurso a la vez, acepte el acuerdo de licencia y continúe descargando el recurso.

Un recurso se considera protegido si se cumple cualquiera de estas condiciones:

* La propiedad de metadatos de recursos `xmpRights:WebStatement` apunta a la ruta de la página que contiene el acuerdo de licencia para el recurso.
* El valor de la propiedad de metadatos del recurso `adobe_dam:restrictions` es un HTML sin procesar que especifica el acuerdo de licencia.

>[!NOTE]
>
>La ubicación `/etc/dam/drm/licenses` utilizada para almacenar licencias en versiones anteriores de [!DNL Experience Manager] está en desuso.
>
>Si crea o modifica páginas de licencia, o las transfiere desde versiones anteriores de [!DNL Experience Manager] , Adobe recomienda almacenarlas en `/apps/settings/dam/drm/licenses` o `/conf/&ast;/settings/dam/drm/licenses`.

### Descargar recursos protegidos por DRM {#downloading-drm-assets}

1. En la vista de tarjeta, seleccione los recursos que desee descargar y haga clic en **[!UICONTROL Descargar]**.
1. En la página **[!UICONTROL Administración de derechos de autor]**, seleccione el recurso que desee descargar de la lista.
1. En el panel [!UICONTROL Licencia], elija **[!UICONTROL Aceptar]**. Aparece una marca de verificación junto al recurso. Haga clic en la opción **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >La opción **[!UICONTROL Download]** solo se habilita cuando se decide aceptar el contrato de licencia de un recurso protegido. Sin embargo, si la selección incluye recursos protegidos y no protegidos, solo los recursos protegidos aparecen en el panel y la opción **[!UICONTROL Descargar]** está activada para descargar los recursos no protegidos. Para aceptar simultáneamente acuerdos de licencia para varios recursos protegidos, seleccione los recursos de la lista y, a continuación, elija **[!UICONTROL Aceptar]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar]** para descargar el recurso o sus representaciones.
