---
title: Promocionar lanzamientos
description: Las páginas de lanzamiento se promocionan para devolver el contenido al origen (producción) antes de publicarlo.
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: e85aacd45a2bbc38f10d03915e68286f0a55364e
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 32%

---

# Promoción de lanzamientos{#promoting-launches}

Debe promocionar las páginas de lanzamiento para devolver el contenido al origen (producción) antes de publicar. Cuando se promociona una página de lanzamiento, la página correspondiente de las páginas de origen se reemplaza con el contenido de la página promocionada. Las siguientes opciones están disponibles al promocionar una página de lanzamiento:

* Indica si se promocionará solo la página actual o todo el lanzamiento.
* Indica si se promocionarán las páginas secundarias de la página actual.
* Si se promociona el lanzamiento completo o solo las páginas que han cambiado.
* Si se elimina el lanzamiento después de la promoción.

>[!NOTE]
>
>Tras promocionar las páginas de lanzamiento al destino (**producción**), puede activar las páginas de **producción** como entidad (para que el proceso sea más rápido). Añada las páginas a un paquete de flujo de trabajo y utilícelo como carga útil para un flujo de trabajo que active un paquete de páginas. Debe crear el paquete de flujo de trabajo antes de promocionar el lanzamiento. Consulte [AEM Procesamiento De Páginas Promocionadas Mediante Flujo De Trabajo De](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Un solo lanzamiento no se puede promocionar de forma simultánea. Esto significa que dos acciones promocionales en el mismo lanzamiento al mismo tiempo pueden dar lugar a un error: `Launch could not be promoted` (así como errores de conflictos en el registro).

>[!CAUTION]
>
>Al promocionar lanzamientos para *modificado* , se tienen en cuenta las modificaciones tanto en la rama de origen como en la de lanzamiento.

## Promoción de páginas de lanzamiento {#promoting-launch-pages}

>[!NOTE]
>
>Esta sección trata sobre la operación manual de promocionar las páginas de lanzamiento cuando solo hay un nivel de lanzamiento. Consulte:
>
>* [Promoción de un lanzamiento anidado](#promoting-a-nested-launch) cuando hay más de un lanzamiento en la estructura.
>* [Lanzamientos: el orden de los eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obtener más información sobre la promoción y publicación automáticas.
>

Puede promocionar lanzamientos desde el **Sites** o la **Lanzamientos** consola:

1. Abra:

   * el **Sites** consola:

      1. Abra el [carril de referencias](/help/sites-authoring/author-environment-tools.md#showingpagereferences) y seleccione la página de origen necesaria con el [modo de selección](/help/sites-authoring/basic-handling.md) (o seleccione y abra el carril de referencias, el orden no importa). Todas las referencias se mostrarán.

      1. Seleccionar **Lanzamientos** (por ejemplo, Lanzamientos (1)) para mostrar una lista de los lanzamientos específicos.
      1. Seleccione el lanzamiento específico para mostrar las acciones disponibles.
      1. Seleccione **Promocionar lanzamiento** para abrir el asistente.

   * el **Lanzamientos** consola:

      1. Seleccione el lanzamiento (toque o haga clic en la miniatura).
      1. Seleccionar **Promocionar**.

1. En el primer paso puede especificar:

   * **Destino**

      * **Eliminar lanzamiento después de la promoción**

   * **Ámbito**

      * **Promocionar lanzamiento completo**
      * **Promocionar las páginas modificadas**
      * **Promocionar página actual**
      * **Promocionar la página actual y sus páginas secundarias**

   Por ejemplo, al seleccionar para promocionar solo las páginas modificadas:

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >Esto cubre un solo lanzamiento, si tiene lanzamientos anidados consulte [Promoción de un lanzamiento anidado](#promoting-a-nested-launch).

1. Seleccionar **Siguiente** para continuar.
1. Puede revisar las páginas que se promocionarán, que dependerán del intervalo de páginas que haya elegido:

   ![Revisar páginas para promocionar](assets/chlimage_1-102.png)

1. Seleccionar **Promocionar**.

## Promoción de páginas de lanzamiento al editar {#promoting-launch-pages-when-editing}

Cuando está editando una página de lanzamiento, la acción **Promocionar lanzamiento** también está disponible en **Información de la página**. Esta acción abrirá el asistente para recopilar la información necesaria.

![Promocionar lanzamiento](assets/chlimage_1-103.png)

>[!NOTE]
>
>Esta opción está disponible para los formatos individual y [lanzamientos anidados](#promoting-a-nested-launch).

## Promoción de un lanzamiento anidado {#promoting-a-nested-launch}

Después de crear un lanzamiento anidado, puede promoverlo de nuevo a cualquiera de los orígenes, incluido el origen raíz (producción).

![Información general sobre la promoción de un lanzamiento anidado](assets/chlimage_1-104.png)

1. Al igual que con [Creación de un lanzamiento anidado](#creatinganestedlaunchlaunchwithinalaunch), vaya a y seleccione el lanzamiento necesario en el **Lanzamientos** o la **Referencias** carril.
1. Seleccione **Promocionar lanzamiento** para abrir el asistente.

1. Introduzca la información necesaria:

   * **Destino**

      * **Destino del cambio**
Puede promocionar a cualquiera de los orígenes.

      * **Eliminar lanzamiento después de la promoción**
Después de la promoción, se eliminarán el lanzamiento seleccionado y los lanzamientos anidados en él.

   * **Ámbito**
Aquí puede seleccionar si desea promocionar el lanzamiento completo o solo las páginas que se han editado. En este último caso, puede seleccionar incluir/excluir páginas secundarias. La configuración predeterminada es promocionar solo los cambios de página para la página actual:

      * **Promocionar lanzamiento completo**
      * **Promocionar las páginas modificadas**
      * **Promocionar página actual**
      * **Promocionar la página actual y sus páginas secundarias**

   ![Configuración para promocionar un lanzamiento](assets/chlimage_1-105.png)

1. Seleccione **Siguiente**.
1. Revise los detalles de la promoción antes de seleccionar **Promocionar**:

   ![Revisar detalles y promocionar](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >Las páginas enumeradas dependerán de lo siguiente **Ámbito** definido y posiblemente las páginas que se han editado.

1. Sus cambios se promocionarán y reflejarán en la **Lanzamientos** consola:

   ![Consola de lanzamientos](assets/chlimage_1-107.png)

## Procesamiento de páginas promocionadas mediante el flujo de trabajo de AEM {#processing-promoted-pages-using-aem-workflow}

Utilice modelos de flujo de trabajo para realizar el procesamiento masivo de páginas de Lanzamientos promocionados:

1. Cree un paquete de flujo de trabajo.
1. Cuando los autores promocionan páginas de Launch, las almacenan en el paquete de flujo de trabajo.
1. Inicie un modelo de flujo de trabajo utilizando el paquete como carga útil.

Para iniciar un flujo de trabajo automáticamente cuando se promocionan páginas, [configuración de un lanzador de flujo de trabajo](/help/sites-administering/workflows-starting.md#workflows-launchers) para el nodo del paquete.

Por ejemplo, puede generar automáticamente solicitudes de activación de página cuando los autores promocionen páginas de Lanzamiento. Configure un iniciador de flujo de trabajo para iniciar el flujo de trabajo de activación de solicitud cuando se modifique el nodo del paquete.

![Iniciador de flujo de trabajo](assets/chlimage_1-108.png)
