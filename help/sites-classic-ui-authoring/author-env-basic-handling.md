---
title: Gestión básica
description: Información general sobre la gestión básica cuando se utiliza el entorno de creación de AEM. Utiliza la consola Sitios como base.
uuid: ab488d7c-7b7f-4a23-a80c-99d37ac84246
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9737ead9-e324-43c9-9780-7abd292f4e5b
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 6%

---

# Gestión básica{#basic-handling}

>[!NOTE]
>
>* Esta página se ha diseñado para ofrecer una descripción general de la gestión básica cuando se utiliza el entorno de creación de AEM. Utiliza la consola **Sitios** como base. 
>
>* Algunas funciones no están disponibles en todas las consolas o algunas funciones adicionales están disponibles en algunas consolas. La información específica sobre las consolas individuales y sus funciones relacionadas se tratará con más detalle en otras páginas.
>* Los métodos abreviados del teclado están disponibles mediante AEM, sobre todo al [utilizar las consolas](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) y [al editar páginas](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>


## La pantalla de bienvenida {#the-welcome-screen}

La IU clásica proporciona una selección de consolas mediante el uso de mecanismos conocidos para desplazarse e iniciar acciones, como hacer clic, hacer doble clic y [menús contextuales](#context-menus).

Al iniciar sesión, se mostrará la pantalla de bienvenida, que proporciona una lista de vínculos a consolas y servicios:

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## Consolas {#consoles}

Las consolas principales son:

<table>
 <tbody>
  <tr>
   <td><strong>Consola</strong></td>
   <td><strong>Función</strong></td>
  </tr>
  <tr>
   <td><strong>Bienvenido</strong></td>
   <td>Proporciona información general y acceso directo (mediante vínculos) a la funcionalidad principal de AEM.</td>
  </tr>
  <tr>
   <td><strong>Recursos digitales</strong><br /> </td>
   <td>Estas consolas le permiten importar y <a href="/help/sites-classic-ui-authoring/classicui-assets.md">administrar recursos digitales</a> como imágenes, vídeos, documentos y archivos de audio. Estos recursos se pueden utilizar en cualquier sitio web que ejecute la misma instancia de AEM. </td>
  </tr>
  <tr>
   <td><strong>Lanzamientos</strong></td>
   <td>Esto le ayuda a administrar su <a href="/help/sites-classic-ui-authoring/classic-launches.md">lanzamientos</a>; esto le permite desarrollar el contenido para una versión futura de una o más páginas web activadas.<br /> <i>Nota: En la IU táctil, muchas de las mismas funcionalidades están disponibles en la consola Sitios, junto con el carril Referencias .</i> <i>Si es necesario, esta consola está disponible desde la consola Herramientas ; seleccione Operaciones y luego Lanzamientos.</i></td>
  </tr>
  <tr>
   <td><strong>Bandeja de entrada </strong></td>
   <td>En muchos casos, varias personas participan en las subtareas de un flujo de trabajo y cada una debe completar su paso antes de transferir el trabajo a la persona siguiente. La bandeja de entrada permite ver notificaciones relacionadas con estas tareas. Consulte <a href="/help/sites-administering/workflows.md">Uso de flujos de trabajo</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>Etiquetado</strong></td>
   <td>Las consolas Etiquetado le permiten administrar etiquetas. Las etiquetas son frases o nombres cortos que se pueden usar para clasificar y anotar contenido, lo que facilita su localización y organización. Para obtener más información, consulte <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">Uso y administración de etiquetas</a>.</td>
  </tr>
  <tr>
   <td><strong>Herramientas</strong></td>
   <td>La variable <a href="/help/sites-administering/tools-consoles.md">Consolas de herramientas</a> proporciona acceso a varias herramientas y consolas especializadas que le ayudan a administrar sus sitios web, recursos digitales y otros aspectos de su repositorio de contenido.</td>
  </tr>
  <tr>
   <td><strong>Usuarios</strong></td>
   <td>Estas consolas le permiten administrar los derechos de acceso para usuarios y grupos. Para obtener más información, consulte <a href="/help/sites-administering/security.md">Administración de usuarios y seguridad</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Sitios web</strong></td>
   <td>Las consolas Sitios/Sitios web le permiten <a href="/help/sites-classic-ui-authoring/classic-page-author.md">crear, ver y administrar sitios web</a> en la instancia de AEM. Mediante estas consolas puede crear, copiar, mover y eliminar páginas de sitios web, iniciar flujos de trabajo y activar (publicar) páginas. También puede abrir una página para editarla.<br /> </td>
  </tr>
  <tr>
   <td><strong>Flujos de trabajo</strong></td>
   <td>Un flujo de trabajo es una serie definida de pasos que describen el proceso para completar una tarea. En muchos casos, varias personas participan en una tarea y cada una debe completar su paso antes de transferir el trabajo a la persona siguiente. La consola Flujo de trabajo permite crear modelos de flujo de trabajo y administrar la ejecución de instancias de flujo de trabajo. Consulte <a href="/help/sites-administering/workflows.md">Uso de flujos de trabajo</a>.<br /> </td>
  </tr>
 </tbody>
</table>

La variable **Sitios web** proporciona dos paneles para desplazarse y administrar sus páginas:

* Panel izquierdo

   Muestra la estructura de árbol de los sitios web y las páginas de dichos sitios web.

   También muestra información sobre otros aspectos o AEM, incluidos proyectos, modelos y recursos.

* Panel derecho

   Muestra las páginas (en la ubicación seleccionada en el panel izquierdo) y se puede utilizar para realizar acciones.

Desde aquí puede [administrar sus páginas](/help/sites-authoring/managing-pages.md) mediante la barra de herramientas, un menú contextual o abriendo una página para realizar más acciones.

>[!NOTE]
>
>La gestión básica es la misma en todas las consolas. Esta sección se centra en la variable **Sitios web** ya que es la consola principal que se utiliza durante la creación.

![Chlimage_1-9](assets/chlimage_1-9a.png)

## Acceso a la Ayuda   {#accessing-help}

En varias consolas (p. ej., Sitios web) también hay **Ayuda** está disponible, se abrirá Uso compartido de paquetes o el sitio de documentación.

![imagen_1-10](assets/chlimage_1-10a.png)

Al editar una página, el [la barra de tareas también tiene un botón para acceder a la ayuda](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## Navegación con la consola Sitios web {#navigating-with-the-websites-console}

La variable **Sitios web** la consola enumera las páginas de contenido en una estructura de árbol (panel izquierdo). Para facilitar la navegación, las secciones de la estructura de árbol pueden expandirse (+) o contraerse (-) según sea necesario:

* Si hace clic en el nombre de página (en el panel izquierdo):

   * Enumerar las páginas secundarias en el panel derecho
   * Expanda también la estructura en el panel izquierdo.

      Por motivos de rendimiento, esta acción depende del número de nodos secundarios. Con una instalación estándar, este método de expansión funciona cuando hay `30` o menos nodos secundarios.

* Al hacer doble clic en el nombre de página (panel izquierdo) también se ampliará el árbol, aunque, como la página se abre al mismo tiempo, este efecto no es tan obvio.

>[!NOTE]
>
>Este valor predeterminado ( `30`) se puede cambiar por consola en las configuraciones específicas de la aplicación del widget siteadmin:
>
>En el nodo siteadmin:
>
>Establezca el valor de la propiedad:
>`treeAutoExpandMax`
>el:
>`/apps/wcm/core/content/siteadmin`
>
>O globalmente en el tema:
>Establezca el valor de:
>`TREE_AUTOEXPAND_MAX`
>en:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>Consulte [SiteAdmin en la API Widget CQ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin) para obtener más información.

## Información de página en la consola Sitios web {#page-information-on-the-websites-console}

El panel derecho del **Sitios web** La consola proporciona una vista de lista con información sobre páginas:

![page-info](assets/page-info.png)

Están disponibles las siguientes: se muestra un subconjunto de estos campos como predeterminado:

<table>
 <tbody>
  <tr>
   <td><strong>Columna</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Miniatura   </td>
   <td>Muestra una miniatura de la página.</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>El título que aparece en la página</td>
  </tr>
  <tr>
   <td>Nombre</td>
   <td>El nombre AEM hace referencia a la página</td>
  </tr>
  <tr>
   <td>Publicado</td>
   <td>Indica si la página se ha publicado y proporciona la fecha y hora de publicación.</td>
  </tr>
  <tr>
   <td>Modificado</td>
   <td>Indica si la página se ha modificado y proporciona la fecha y hora de modificación. Para guardar cualquier modificación, debe activar la página.</td>
  </tr>
  <tr>
   <td>Publicación en Scene7</td>
   <td>Indica si la página se ha publicado en Scene7.<br /> </td>
  </tr>
  <tr>
   <td>Estado</td>
   <td>Indica el estado actual de la página, como si forma parte de un flujo de trabajo o Live Copy o si una página está bloqueada actualmente.</td>
  </tr>
  <tr>
   <td>Impresiones</td>
   <td>Muestra la actividad en una página en número de visitas.</td>
  </tr>
  <tr>
   <td>Plantilla</td>
   <td>Indica la plantilla en la que se basa una página.</td>
  </tr>
  <tr>
   <td>En flujo de trabajo</td>
   <td>Indica si la página está en un flujo de trabajo.</td>
  </tr>
  <tr>
   <td>Bloqueado por</td>
   <td>Muestra si una página se ha bloqueado y la cuenta de usuario que la ha bloqueado.</td>
  </tr>
  <tr>
   <td>Live Copy   </td>
   <td>Indica si la página forma parte de una Live Copy.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Para seleccionar las columnas visibles, pase el ratón por el título de una columna. Se mostrará un menú desplegable, desde el que podrá usar la variable **Columnas** .

Los colores junto a las páginas en la **Publicado** y **Modificado** las columnas indican el estado de publicación:

| **Columna** | **Color** | **Descripción** |
|---|---|---|
| Publicado | Verde | La publicación se realizó correctamente. Se publica el contenido. |
| Publicado | Amarillo | Publicación pendiente. El sistema aún no ha recibido confirmación de la publicación. |
| Publicado | Rojo | Error de publicación. No hay conexión con la instancia de publicación. Esto también puede significar que el contenido se desactivó. |
| Publicado | *blank* | Esta página nunca se ha publicado. |
| Modificado | Azul | La página se ha modificado desde la última publicación. |
| Modificado | *blank* | Esta página nunca se ha modificado o no se ha modificado desde la última publicación. |

## Menús contextuales {#context-menus}

La IU clásica utiliza mecanismos conocidos para desplazarse e iniciar acciones, como hacer clic y hacer doble clic. Según la situación actual, también hay disponible una serie de menús contextuales (normalmente abiertos con el botón derecho del ratón):

![imagen_1-11](assets/chlimage_1-11a.png)
