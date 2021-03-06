---
title: Configurar colas compartidas
seo-title: Configurar colas compartidas
description: Aprenda a utilizar colas compartidas para flujos de trabajo centrados en Forms en AEM Forms en OSGi.
seo-description: Aprenda a utilizar colas compartidas para flujos de trabajo centrados en Forms en AEM Forms en OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 1%

---


# Compartir y solicitar acceso a los elementos de la Bandeja de entrada de un usuario {#share-and-request-access}

Una cola es una lista de elementos en AEM Bandeja de entrada de un usuario. Pueden ser elementos asignados a un usuario o elementos compartidos con el grupo al que pertenece un usuario. Puede acceder a la Bandeja de entrada para realizar vistas y realizar acciones en el elemento Bandeja de entrada. Por ejemplo, comparta un elemento con otro usuario.

También puede compartir los elementos de la Bandeja de entrada con otro usuario. Una vez que otro usuario tiene acceso a los elementos de la Bandeja de entrada, el usuario puede reclamar y realizar las acciones correspondientes en los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada a otros usuarios.

## Requisitos previos {#pre-requisites}

El usuario que ha iniciado sesión debe ser miembro del grupo `workflow-users`. El usuario puede compartir elementos o solicitar acceso a elementos solo de los usuarios en los que el usuario que ha iniciado sesión tiene permisos de lectura o solo de los usuarios que han activado el perfil público.

## Compartir un solo elemento o todos los elementos de la bandeja de entrada con otro usuario

AEM bandeja de entrada le permite compartir un solo elemento o todos los elementos de la bandeja de entrada con otro usuario.

### Compartir todos los elementos de la bandeja de entrada

Siga estos pasos para compartir todos los elementos de una bandeja de entrada con otro usuario:

1. Inicie sesión en la instancia de AEM. Toque el icono ![Bandeja de entrada](assets/bell.svg) y toque **[!UICONTROL Vista de todo]**. Aparece una lista de los elementos de la bandeja de entrada.
1. Toque el icono ![Selector de Vista](assets/viewlist.svg) o ![Selector de Vista](assets/calendar.svg) junto al botón **[!UICONTROL Crear]** y toque **[!UICONTROL Configuración]**. Aparecerá el cuadro de diálogo de configuración.
1. Abra la ficha **[!UICONTROL Compartir]** en el cuadro de diálogo de configuración.
1. Escriba el nombre de un usuario en el cuadro de texto **[!UICONTROL Conceder acceso a los elementos de la Bandeja de entrada]** y toque **[!UICONTROL Conceder]**. Repita el paso para agregar más usuarios. Todos los usuarios con acceso a sus elementos aparecen en la sección **Nombre de usuario**.
1. Toque **[!UICONTROL Guardar]**.

>[!NOTE]
>
>(Solo para elementos de flujo de trabajo centrados en Forms) Active la opción **[Permitir que el usuario asignado comparta a través de la bandeja de entrada](aem-forms-workflow-step-reference.md)** del paso **Asignar tarea** del flujo de trabajo. Los demás usuarios solo verán los elementos que tengan habilitada la opción mencionada.

### Compartir elementos individuales

Siga estos pasos para compartir un elemento de la Bandeja de entrada con otro usuario:

1. Inicie sesión en la instancia de AEM. Toque el icono ![Bandeja de entrada](assets/bell.svg) y toque **[!UICONTROL Vista de todo]**. Aparece una lista de los elementos de la bandeja de entrada.
1. Seleccione un elemento y toque **[!UICONTROL Compartir]**. Aparecerá un cuadro de diálogo.
1. Escriba el nombre de un usuario en el cuadro de texto Añadir usuarios para compartir este elemento y toque **[!UICONTROL Añadir]**. Repita el paso para agregar más usuarios. Todos los usuarios con acceso a sus elementos aparecen en la sección **[!UICONTROL Nombre de usuario]**.
1. Toque **[!UICONTROL Guardar]**.


>[!NOTE]
>
>(Solo para elementos de flujo de trabajo centrados en Forms) Active la opción **[Permitir que el usuario asignado comparta explícitamente en la Bandeja de entrada](aem-forms-workflow-step-reference.md)** del paso **Asignar tarea** del flujo de trabajo. Los demás usuarios solo verán los elementos que tengan habilitada la opción mencionada.

## Solicitar acceso a los elementos de la bandeja de entrada {#request-access}

Puede solicitar acceso a los elementos de la Bandeja de entrada de otro usuario. Una vez concedido el acceso, puede realizar la vista, reclamar y realizar las acciones correspondientes en los elementos compartidos. Realice los siguientes pasos para solicitar acceso a los elementos de la Bandeja de entrada de otro usuario:

1. Inicie sesión en la instancia de AEM. Toque el icono ![Selector de Vista](assets/bell.svg) y toque **[!UICONTROL Vista de todo]**.
1. Toque el icono ![Selector de Vista](assets/viewlist.svg) o ![Selector de Vista](assets/calendar.svg) junto al botón **[!UICONTROL Crear]** y toque **[!UICONTROL Configuración]**. Aparecerá el cuadro de diálogo de configuración.
1. Escriba el nombre de un usuario en el cuadro de texto **[!UICONTROL Solicitar acceso a la bandeja de entrada del usuario]** y toque **[!UICONTROL Solicitar]**. Se envía una solicitud al usuario y el estado de la misma se muestra con el nombre del usuario. Repita el paso para agregar más usuarios.
1. Toque **[!UICONTROL Guardar]**. La solicitud se envía como elemento de la Bandeja de entrada a los usuarios. El usuario puede seleccionar el elemento y tocar Aprobar o Rechazar para conceder o rechazar el acceso.


## Reclamar elementos compartidos por otros usuarios {#claim-items}

Solo puede realizar inicios para trabajar en un elemento compartido después de reclamarlo. Evita que varios usuarios trabajen en un solo elemento. Realice los siguientes pasos para reclamar un artículo:

1. Inicie sesión en la instancia de AEM. Toque el icono Bandeja de entrada ![Bandeja de entrada](assets/bell.svg) y toque **[!UICONTROL Vista de todo]**.
1. Toque el icono ![Solo contenido](assets/railleft.svg) para abrir el selector de filtros.
1. Toque la lista desplegable **[!UICONTROL Seleccionar usuario asignado]** para la vista y seleccione los usuarios que han compartido con usted los elementos de la Bandeja de entrada.
1. Seleccione un elemento y toque **[!UICONTROL Reclamar]**. El elemento se agrega a la Bandeja de entrada.

## Liberar elementos reclamados {#release-items}

Solo puede trabajar en un elemento compartido después de reclamarlo. Otros usuarios no pueden ver ni trabajar en un elemento que usted haya reclamado. Si no puede continuar trabajando en un elemento, puede volver a soltarlo en el grupo.   Después de liberar el artículo, otros usuarios pueden reclamarlo y trabajar en él:

Realice los siguientes pasos para liberar un elemento:

1. Inicie sesión en la instancia de AEM. Toque el icono Bandeja de entrada ![Bandeja de entrada](assets/bell.svg) y toque **[!UICONTROL Vista de todo]**. Aparece una lista de los elementos de la bandeja de entrada.
1. Seleccione el elemento que desea liberar y toque **[!UICONTROL UnClaim]**. El elemento se vuelve a agregar al grupo. Otros ahora pueden reclamar el artículo.

## Restricciones     {#limitations}

* No se admite el uso compartido de elementos con un grupo.
* No se admite el uso compartido de tareas de proyectos.
