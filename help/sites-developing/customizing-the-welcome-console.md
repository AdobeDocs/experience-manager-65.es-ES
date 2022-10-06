---
title: Personalización de la consola de bienvenida (IU clásica)
seo-title: Customizing the Welcome Console (Classic UI)
description: La consola de bienvenida proporciona una lista de vínculos a las distintas consolas y funcionalidades de AEM
seo-description: The Welcome console provides a list of links to the various consoles and functionality within AEM
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 9%

---

# Personalización de la consola de bienvenida (IU clásica){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>Esta página trata la IU clásica.
>
>Consulte [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md) para obtener más información sobre la IU táctil estándar.

La consola de bienvenida proporciona una lista de vínculos a las distintas consolas y funcionalidades de AEM.

![cq_welcomescreen](assets/cq_welcomescreen.png)

Es posible configurar los vínculos que son visibles. Esto se puede definir para usuarios o grupos específicos. Las acciones que se van a realizar dependen del tipo de objetivo (que se correlaciona con la sección de la consola en la que se encuentran):

* [Consolas principales](#links-in-main-console-left-pane) - Vínculos en la consola principal (panel izquierdo)
* [Recursos, documentación y referencias, funciones](#links-in-sidebar-right-pane) - Vínculos en la barra lateral (panel derecho)

## Vínculos en la consola principal (panel izquierdo) {#links-in-main-console-left-pane}

Muestra las consolas principales de AEM.

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### Configuración de si los vínculos de la consola principal son visibles {#configuring-whether-main-console-links-are-visible}

Los permisos de nivel de nodo determinan si el vínculo se puede ver o no. Los nodos en cuestión son:

* **Sitios web:** `/libs/wcm/core/content/siteadmin`

* **Recursos digitales:** `/libs/wcm/core/content/damadmin`

* **Comunidad:** `/libs/collab/core/content/admin`

* **Campañas:** `/libs/mcm/content/admin`

* **Bandeja de entrada:** `/libs/cq/workflow/content/inbox`

* **Usuarios:** `/libs/cq/security/content/admin`

* **Herramientas:** `/libs/wcm/core/content/misc`

* **Etiquetado:** `/libs/cq/tagging/content/tagadmin`

Por ejemplo:

* Para restringir el acceso a **Herramientas**, elimine el acceso de lectura de

   `/libs/wcm/core/content/misc`

Consulte la [Sección de seguridad](/help/sites-administering/security.md) para obtener más información sobre cómo configurar los permisos deseados.

### Vínculos en la barra lateral (panel derecho) {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

Estos vínculos se basan en la existencia de *y* lea el acceso a los nodos en la siguiente ruta:

`/libs/cq/core/content/welcome`

De forma predeterminada, hay tres secciones (con una separación ligeramente diferente):

<table>
 <tbody>
  <tr>
   <td><strong>Medios</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Cloud Services</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> Flujos de trabajo</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> Administración de tareas</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> Replicación</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> Informes</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> Publicaciones</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> Manuscritos</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>Documentación y referencia</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Documentación</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> Medios del desarrollador</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>Características</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> Paquetes</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> Uso compartido de paquetes</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> Clúster</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> Copia de seguridad</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Consola web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Volcado de estado de la consola web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### Configuración de si los vínculos de la barra lateral son visibles {#configuring-whether-sidebar-links-are-visible}

Es posible ocultar un vínculo de usuarios o grupos específicos eliminando el acceso de lectura a los nodos que representan el vínculo.

* Recursos: elimine el acceso a:

   `/libs/cq/core/content/welcome/resources/<link-target>`

* Documentos: quitar acceso a:

   `/libs/cq/core/content/welcome/docs/<link-target>`

* Funciones: elimine el acceso a:

   `/libs/cq/core/content/welcome/features/<link-target>`

Por ejemplo:

* Para quitar el vínculo a **Informes**, elimine el acceso de lectura de

   `/libs/cq/core/content/welcome/resources/reports`

* Para quitar el vínculo a **Paquetes**, elimine el acceso de lectura de

   `/libs/cq/core/content/welcome/features/packages`

Consulte la [Sección de seguridad](/help/sites-administering/security.md) para obtener más información sobre cómo configurar los permisos deseados.

### Mecanismo de selección de vínculos {#link-selection-mechanism}

En `/libs/cq/core/components/welcome/welcome.jsp` se usa de [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html), que ejecuta una consulta en nodos que tienen la propiedad :

* `jcr:mixinTypes` con el valor: `cq:Console`

>[!NOTE]
>
>Ejecute la siguiente consulta para ver la lista existente:
>
>* `select * from cq:Console`
>


Cuando un usuario o grupo no tiene permiso de lectura en un nodo con la mezcla `cq:Console`, el nodo no se recupera con el `ConsoleUtil` buscar, por lo que no aparece en la consola.

### Adición de un elemento personalizado {#adding-a-custom-item}

La variable [mecanismo de selección de vínculos](#link-selection-mechanism) se puede usar para agregar su propio elemento personalizado a la lista de vínculos.

Agregue el elemento personalizado a la lista agregando la variable `cq:Console` mezclar con el widget o recurso. Esto se hace definiendo la propiedad :

* `jcr:mixinTypes` con el valor: `cq:Console`
