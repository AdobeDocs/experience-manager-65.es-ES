---
title: Administración de derechos digitales en recursos
description: Obtenga información sobre cómo administrar los estados de caducidad de recursos y la información de los recursos con licencia en AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# Digital Rights Management for digital assets {#digital-rights-management-in-assets}

Los recursos digitales suelen estar asociados a una licencia, que especifica sus términos y duración de uso. Puesto que Recursos Adobe Experience Manager (AEM) está totalmente integrado con la plataforma AEM, puede administrar de forma eficaz la información de caducidad de recursos y los estados de los mismos. También puede asociar información de licencias con recursos.

## Caducidad del recurso {#asset-expiration}

La caducidad de los activos es una forma eficaz de aplicar los requisitos de licencia de los activos. Garantiza que el recurso publicado no se publique cuando caduque, lo que evita la posibilidad de cualquier infracción de licencia. Un usuario sin derechos de administrador no puede editar, copiar, mover, publicar ni descargar un recurso caducado.

Puede ver el estado de caducidad de un recurso en la consola Recursos, tanto en la vista de tarjeta como en la de lista.

![expired_flag_card](assets/expired_flag_card.png)

*Figura: En la vista de tarjeta, un indicador de la tarjeta indica que el recurso ha caducado*

**Vista de lista**

![expired_flag_list](assets/expired_flag_list.png)

*Figura: En la vista de lista, la columna[!UICONTROL Estado]muestra la pancarta[!UICONTROL Caducado].*

Puede ver el estado de caducidad de un recurso en la línea de tiempo. Seleccione el recurso y elija Línea de tiempo en el menú GlobalNav.

![chlimage_1-144](assets/chlimage_1-144.png)

También puede ver el estado de caducidad de los recursos en el carril **[!UICONTROL Referencias]** . Gestiona los estados de caducidad de los recursos y las relaciones entre los recursos compuestos y los subrecursos, colecciones y proyectos a los que se hace referencia.

1. Vaya al recurso para el que desea ver las páginas Web de referencia y los recursos compuestos.
1. Seleccione el recurso y el logotipo de Experience Manager.

1. Elija **[!UICONTROL Referencias]** en el menú.

   ![chlimage_1-146](assets/chlimage_1-146.png)

   En el caso de los recursos caducados, el carril Referencias muestra el estado de caducidad del **[!UICONTROL recurso]** en la parte superior.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Si el recurso tiene subrecursos caducados, el carril Referencias muestra el estado **[!UICONTROL Recurso con subrecursos]** Caducados.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### Buscar recursos caducados {#search-expired-assets}

Puede buscar recursos caducados, incluidos los subrecursos caducados, en el panel Buscar.

1. En la consola Recursos, haga clic en la opción **[!UICONTROL Buscar]** de la barra de herramientas para mostrar el cuadro Omniture Search.

1. Con el cursor en el cuadro Omniture Search, presione la tecla Retorno para mostrar la página Resultados de la búsqueda.

   ![chlimage_1-150](assets/chlimage_1-150.png)

1. Haga clic en el logotipo de Experience Manager para mostrar el panel de búsqueda.

   ![chlimage_1-151](assets/chlimage_1-151.png)

1. Pulse o haga clic en la opción **[!UICONTROL Estado de caducidad]** para expandirla.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Seleccione **[!UICONTROL Caducado]**. Los recursos caducados se muestran en los resultados de la búsqueda.

   ![chlimage_1-153](assets/chlimage_1-153.png)

Al elegir la opción **Caducado** , la consola Recursos solo muestra los recursos y subrecursos caducados a los que hacen referencia los recursos compuestos. Los recursos compuestos que hacen referencia a subrecursos caducados no se muestran inmediatamente después de que caduquen los subrecursos. En su lugar, se muestran después de que Recursos AEM detecte que hacen referencia a subrecursos caducados la próxima vez que se ejecute el programador.

Si modifica la fecha de caducidad de un recurso publicado a una fecha anterior al ciclo del programador actual, el programa seguirá detectando este recurso como recurso caducado la próxima vez que se ejecute y reflejará su estado en consecuencia.

Además, si un fallo o error impide que el programador detecte los recursos caducados en el ciclo actual, el programador vuelve a examinar estos recursos en el siguiente ciclo y detecta su estado caducado.

Para permitir que la consola de Assets muestre los recursos compuestos de referencia junto con los subrecursos caducados, configure un flujo de trabajo de **notificación de caducidad de Adobe CQ DAM** en AEM Configuration Manager.

1. Abra AEM Configuration Manager.
1. Seleccione **[!UICONTROL Adobe CQ DAM Expiry Notification]**. De forma predeterminada, está seleccionado Programador **[!UICONTROL basado en]** tiempo, que programa un trabajo para comprobar en un momento específico si un recurso tiene subrecursos caducados. Una vez finalizado el trabajo, los recursos que tienen subrecursos caducados y recursos a los que se hace referencia se muestran como caducados en los resultados de la búsqueda.

   ![chlimage_1-154](assets/chlimage_1-154.png)

1. Para ejecutar el trabajo periódicamente, desactive el campo **[!UICONTROL Regla de planificador basada en tiempo]** y modifique el tiempo en segundos en el campo **[!UICONTROL Programador periódico]**. Por ejemplo, la expresión &#39;0 0 0 &amp;ast; &amp;ast; ?&#39; activa el trabajo a las 00 horas.
1. Seleccione **[!UICONTROL enviar correo electrónico]** para recibir correos electrónicos cuando caduque un recurso.

   >[!NOTE]
   >
   >Solo el creador de recursos (la persona que carga un recurso concreto en Recursos AEM) recibe un correo electrónico cuando caduca el recurso. Consulte [Configuración de notificaciones](/help/sites-administering/notification.md) por correo electrónico para obtener más información sobre la configuración de las notificaciones por correo electrónico en todo el nivel de AEM.

1. En el campo Notificación **[!UICONTROL previa en segundos]** , especifique el tiempo en segundos antes de que caduque un recurso cuando desee recibir una notificación con respecto a la caducidad. Si es un administrador o el creador de recursos, recibirá un mensaje antes de que caduque el recurso, en el que se le notificará que el recurso está a punto de caducar después de la hora especificada.

   Una vez caducado el recurso, recibirá otra notificación que confirma la caducidad. Además, los recursos caducados se desactivan.

1. Haga clic en **[!UICONTROL Guardar]**.

## Estados de activos {#asset-states}

La consola Recursos de Recursos de Recursos Adobe Experience Manager (AEM) puede mostrar varios estados para los recursos. Según el estado actual de un recurso concreto, su vista de tarjeta muestra una etiqueta que describe su estado, por ejemplo, Caducado, Publicado, Aprobado, Rechazado, etc.

1. En la interfaz de usuario de Recursos, seleccione un recurso.

   ![chlimage_1-155](assets/chlimage_1-155.png)

1. Toque **[!UICONTROL Publicar]** en la barra de herramientas. Si no ve **Publicar** en la barra de herramientas, toque **[!UICONTROL Más]** en la barra de herramientas y la opción Buscar **[!UICONTROL publicación]** .

   ![chlimage_1-156](assets/chlimage_1-156.png)

1. Elija **[!UICONTROL Publicar]** en el menú y, a continuación, cierre el cuadro de diálogo de confirmación.
1. Salga del modo de selección. El estado de publicación del recurso aparece en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, la columna Publicado muestra la hora en que se publicó el recurso.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. En la interfaz de usuario de Recursos, seleccione un recurso y toque **[!UICONTROL Propiedades]** para mostrar la página de detalles del recurso.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. En la ficha Avanzado, establezca una fecha de caducidad para el recurso en el campo **[!UICONTROL Caduca]** .

   ![establecer fecha y hora de caducidad del recurso en el campo Caduca](assets/asset-properties-advanced-tab.png)


   *Figura: Ficha Avanzado de las propiedades del recurso para establecer la caducidad del recurso*

1. Haga clic en **[!UICONTROL Guardar]** y, a continuación, en **[!UICONTROL Cerrar]** para mostrar la consola Recursos.
1. El estado de publicación del recurso indica un estado caducado en la parte inferior de la miniatura del recurso en la vista de tarjeta. En la vista de lista, el estado del recurso se muestra como **[!UICONTROL Caducado]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. En la consola Recursos, seleccione una carpeta y cree una tarea de revisión en la carpeta.
1. Revise y apruebe/rechace los recursos de la tarea de revisión y haga clic en **[!UICONTROL Completar]**.
1. Vaya a la carpeta para la que creó la tarea de revisión. El estado de los recursos aprobados/rechazados se muestra en la parte inferior de la vista de tarjeta. En la vista de lista, los estados de aprobación y caducidad se muestran en las columnas correspondientes.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. Para buscar recursos en función de su estado, toque **[!UICONTROL Buscar]** para mostrar la barra de Omniture.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Pulse Volver y, a continuación, toque **[!UICONTROL GlobalNav]** para mostrar el panel Buscar.
1. En el panel Buscar, pulse o haga clic en **[!UICONTROL Estado de publicación]** y seleccione **[!UICONTROL Publicado]** para buscar recursos publicados en AEM Assets.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Pulse o haga clic en **[!UICONTROL Estado de aprobación]** y haga clic en la opción correspondiente para buscar recursos aprobados o rechazados.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Para buscar recursos en función de su estado de caducidad, seleccione **[!UICONTROL Estado de caducidad]** en el panel Buscar y elija la opción adecuada.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. También puede buscar recursos en función de una combinación de estados en varias facetas de búsqueda. Por ejemplo, puede buscar recursos publicados que hayan sido aprobados en una tarea de revisión y que aún no hayan caducado seleccionando las opciones correspondientes en las facetas de búsqueda.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management in Assets {#digital-rights-management-in-assets-1}

Esta función fuerza la aceptación del contrato de licencia antes de poder descargar un recurso con licencia desde Recursos Adobe Experience Manager (AEM).

Si selecciona un recurso protegido y toca **[!UICONTROL Descargar]**, se le redirigirá a una página de licencia en la que acepte el contrato de licencia. Si no acepta el contrato de licencia, se desactiva el botón **[!UICONTROL Descargar]** .

Si la selección contiene varios recursos protegidos, selecciónelos de uno en uno, acepte el contrato de licencia y continúe con la descarga del recurso.

Un recurso se considera protegido si se cumple cualquiera de estas condiciones:

* La propiedad de metadatos del recurso `xmpRights:WebStatement` apunta a la ruta de la página de CQ que contiene el contrato de licencia del recurso.
* El valor de la propiedad de metadatos del recurso `adobe_dam:restrictions` es un HTML sin procesar que especifica el contrato de licencia.

>[!NOTE]
>
>La ubicación `/etc/dam/drm/licenses` utilizada para almacenar licencias en versiones anteriores de AEM ya no se utiliza.
>
>Si crea o modifica páginas de licencia o las transfiere desde versiones anteriores de AEM, Adobe recomienda almacenarlas en `/apps/settings/dam/drm/licenses` o `/conf/&ast;/settings/dam/drm/licenses`.

### Descargar recursos protegidos con DRM {#downloading-drm-assets}

1. En la vista de tarjeta, seleccione los recursos que desea descargar y haga clic en **[!UICONTROL Descargar]**.
1. En la página **[!UICONTROL Administración de derechos de autor]**, seleccione el recurso que desee descargar de la lista.
1. En el panel Licencia, elija **[!UICONTROL Aceptar]**. Aparece una marca de graduación junto al recurso para el que acepta el contrato de licencia. Toque o haga clic en el botón **[!UICONTROL Descargar]** .

   >[!NOTE]
   >
   >El botón **[!UICONTROL Descargar]** solo se activa cuando se decide aceptar el contrato de licencia de un recurso protegido. Sin embargo, si la selección incluye recursos protegidos y no protegidos, solo los recursos protegidos aparecen en el panel izquierdo; el botón **[!UICONTROL Descargar]** se habilitará para obtener los recursos no protegidos. Para aceptar simultáneamente acuerdos de licencia para varios recursos protegidos, seleccione los recursos de la lista y, a continuación, elija **[!UICONTROL Aceptar]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. En el cuadro de diálogo, toque o haga clic en **[!UICONTROL Descargar]** para descargar el recurso o sus representaciones.
