---
title: Configuración de la configuración de fuera de la oficina
seo-title: Configuración de la configuración de fuera de la oficina
description: Configuración de RConfiguración fuera de la oficina
seo-description: Configuración de la configuración de fuera de la oficina
translation-type: tm+mt
source-git-commit: 52e4564ecab61cedaf3aca3d10339f6bcee2f71e

---



# Configuración de fuera de la oficina {#configure-out-of-office-settings}

Si planea salir de la oficina, puede especificar lo que sucede con los artículos que se le han asignado para ese período.

Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Si se encuentra en un huso horario distinto del servidor, el huso horario utilizado es el del cliente.

Puede establecer una persona predeterminada a la que se enviarán todos los elementos. También puede especificar excepciones para los elementos de procesos específicos que se enviarán a un usuario diferente o que permanecerán en la Bandeja de entrada hasta que vuelva. Si la persona designada también está fuera de la oficina, el artículo se dirige al usuario que ha designado. Si el elemento no se puede asignar a un usuario que no está fuera de la oficina, permanecerá en la Bandeja de entrada.

Puede segregar la delegación de elementos en función de los modelos de flujo de trabajo. Por ejemplo, puede asignar un elemento relacionado con el flujo de trabajo A al usuario A y asignar un elemento relacionado con el flujo de trabajo B al usuario B.


>[!NOTE]
>
> * Cuando se activa la opción Fuera de la oficina, todos los elementos disponibles en la Bandeja de entrada, antes de habilitar la configuración, permanecen en la bandeja de entrada. Solo se delegan los elementos recibidos después de habilitar la configuración.
> * Al desactivar la opción Desactivar Office, los elementos delegados no se le asignarán automáticamente. Puede utilizar la funcionalidad de notificación para asignarle artículos.
> * Cuando el usuario A delega elementos en el usuario B y el usuario B delega elementos en el usuario C, los elementos se asignan únicamente al usuario C y no al usuario B.
> * Cuando hay un bucle en la asignación, las tareas permanecen con el usuario original. Por ejemplo, cuando el usuario A delega elementos en el usuario B delega elementos en el usuario C, el usuario C delega en el usuario D y el usuario D delega en el usuario B, se crea un bucle en. En este caso, el elemento permanece con el usuario original. El usuario A es el usuario original en el ejemplo anterior.


## Habilite la configuración de Fuera de la oficina para su cuenta {#enable-out-of-office}

Realice los siguientes pasos para activar la configuración fuera de la oficina de su cuenta y delegar los elementos de la bandeja de entrada en otro usuario:

1. Inicie sesión en la instancia de AEM. Toque el icono de la ![Bandeja de entrada](assets/bell.svg) y toque **[!UICONTROL Ver todo]**. Aparecerá una lista de los elementos de la bandeja de entrada.
1. Toque el icono ![Selector](assets/viewlist.svg) de vista o Selector ![de](assets/calendar.svg) vista situado junto al botón **[!UICONTROL Crear]** y toque **[!UICONTROL Configuración]**. Aparecerá el cuadro de diálogo de configuración.
1. Abra la ficha **[!UICONTROL Fuera de Office]** en el cuadro de diálogo de configuración.
1. Toque el botón **[!UICONTROL Activar/Desactivar]** para habilitar la configuración de Fuera de Office.
1. Especifique la hora **[!UICONTROL de]** inicio y la hora **[!UICONTROL de]** finalización para la configuración. Los elementos solo se delegan durante el período especificado. Deje vacío el campo **[!UICONTROL Hora]** de finalización para delegar elementos durante un período de tiempo indefinido.
1. Seleccione la casilla **[!UICONTROL Reenviar mis elementos durante este período]** . Si no selecciona la opción y no especifica un usuario asignado, los elementos no se reenviarán a ningún usuario. Aunque esté ausente y la configuración esté habilitada, los elementos permanecerán en la Bandeja de entrada.
1. Toque **[!UICONTROL Agregar usuario asignado]**. Especifique un usuario en el campo **[!UICONTROL Asignado]** para delegar los elementos en. Especifique el modelo **[!UICONTROL de]** flujo de trabajo que se va a delegar al usuario especificado. Puede seleccionar más de un modelo de flujo de trabajo.

   Además, para asignar todos los elementos, independientemente del modelo de flujo de trabajo, a un usuario determinado, seleccione **[!UICONTROL Todos los flujos de trabajo]** en la lista desplegable Modelo de flujo de trabajo. <br>

   Para asignar elementos a un usuario concreto para todos los modelos de flujo de trabajo, excepto algunos, seleccione **[!UICONTROL Todos los flujos]** de trabajo en la lista desplegable Modelo de flujo de trabajo, toque **[!UICONTROL + Añadir excepciones]**y especifique los modelos de flujo de trabajo que se van a excluir.
   <br>

   Repita el paso para agregar más usuarios asignados. <br>

   >[!NOTE]
   >El orden de los cesionarios es importante. Cuando se asigna un elemento a un usuario que ha habilitado la configuración fuera de la oficina, el elemento se evalúa en relación con la lista de destinatarios especificada en el orden en que se agregan los usuarios asignados. Cuando un elemento coincide con los criterios, se asigna al usuario asignado y el siguiente usuario asignado no se comprueba.

1. Toque **[!UICONTROL Guardar]**. La configuración surte efecto en la fecha y hora de inicio especificadas. Si inicia sesión mientras está fuera de la oficina, no se le considerará en la oficina hasta que cambie la configuración.

Ahora, los elementos asignados durante el período de tiempo fuera de la oficina se asignan automáticamente al usuario asignado especificado.\
![Fuera de la oficina](assets/out-of-office.png)

>[!NOTE]
>
> (Solo para elementos de flujo de trabajo centrados en formularios) Active la opción **Permitir que el usuario asignado delegue mediante la opción** de configuración &#39;Fuera de la oficina&#39; del paso de tarea **** Asignar en el flujo de trabajo. Solo se delegan a otros usuarios los elementos que tengan habilitada la opción mencionada.

## Restricciones {#limitations}

* No se admite la asignación de elementos a un grupo.
* Actualmente no se admite la activación de Fuera de la oficina para tareas de proyecto.
