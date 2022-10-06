---
title: Creación de un grupo de usuarios cerrado
seo-title: Creating a Closed User Group
description: Obtenga información sobre cómo crear un grupo de usuarios cerrado.
seo-description: Learn how to create a Closed User Group.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 4%

---

# Creación de un grupo de usuarios cerrado{#creating-a-closed-user-group}

Los grupos de usuarios cerrados (CUG) se utilizan para limitar el acceso a páginas específicas que residen dentro de un sitio de Internet publicado. Estas páginas requieren que los miembros asignados inicien sesión y proporcionen credenciales de seguridad.

Para configurar un área de este tipo dentro del sitio web, debe:

* [crear el grupo de usuarios cerrado real y asignar miembros](#creating-the-user-group-to-be-used).

* [aplicar este grupo a las páginas requeridas](#applying-your-closed-user-group-to-content-pages) y seleccione (o cree) la página de inicio de sesión para que la utilicen los miembros del CUG; también se especifica al aplicar un CUG a una página de contenido.

* [crear un vínculo, de cualquier forma, a al menos una página dentro del área protegida](#linking-to-the-realm), de lo contrario no será visible.
* [configuración de Dispatcher](#configure-dispatcher-for-cugs) si está en uso.

>[!CAUTION]
>
>Los grupos de usuarios cerrados (CUG) siempre deben crearse teniendo en cuenta el rendimiento.
>
>Aunque el número de usuarios y grupos de un CUG no está limitado, un número elevado de CUG en una página puede ralentizar el rendimiento de la renderización.
>
>Siempre debe tenerse en cuenta el impacto de los CUG al realizar pruebas de rendimiento.

## Creación Del Grupo De Usuarios Que Se Utilizará {#creating-the-user-group-to-be-used}

Para crear un grupo de usuarios cerrado:

1. Vaya a **Herramientas - Seguridad** de la pantalla AEM.

   >[!NOTE]
   >
   >Consulte [Administración de usuarios y grupos](/help/sites-administering/security.md#managing-users-and-groups) para obtener información completa sobre la creación y configuración de usuarios y grupos.

1. Seleccione el **Grupos** de la siguiente pantalla.

   ![captura de pantalla_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Pulse el botón **Crear** en la esquina superior derecha, para crear un nuevo grupo.
1. Asigne un nombre al nuevo grupo; por ejemplo, `cug_access`.

   ![captura de pantalla_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Vaya a la **Miembros** y asigne a este grupo los usuarios necesarios.

   ![captura de pantalla_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Active cualquier usuario que haya asignado al CUG; en este caso, todos los miembros de `cug_access`.
1. Active el grupo de usuarios cerrado para que esté disponible en el entorno de publicación; en este ejemplo, `cug_access`.

## Aplicación Del Grupo De Usuarios Cerrado A Las Páginas De Contenido {#applying-your-closed-user-group-to-content-pages}

Para aplicar el CUG a una página:

1. Navegue a la página raíz de la sección restringida que desee asignar a su CUG.
1. Seleccione la página haciendo clic en su miniatura y luego en **Propiedades** en el panel superior.

   ![captura de pantalla_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. En la siguiente ventana, vaya a la **Avanzadas** pestaña .
1. Desplácese hacia abajo y active la casilla de verificación en la **Requisito de autenticación** para obtener más información.

1. Añada la ruta de configuración a continuación y pulse Guardar.
1. A continuación, vaya a la **Permisos** y presione la **Editar grupo de usuarios cerrado** botón.

   ![captura de pantalla_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[NOTA!]
   >
   > Tenga en cuenta que los CUG de la pestaña Permisos no se pueden desplegar en Live Copies desde modelos. Tenga en cuenta esto al configurar Live Copy.
   >
   > Para obtener más información, consulte [esta página](closed-user-groups.md#aem-livecopy).

1. Busque y añada su CUG en la siguiente ventana - en este caso, añada el grupo llamado **cug_access**. Finalmente, presione **Guardar**.
1. Haga clic en **Habilitado** para definir que esta página (y las páginas secundarias) pertenecen a un CUG.
1. Especifique la variable **Página de inicio de sesión** los miembros del grupo que vayan a utilizar; por ejemplo:

   `/content/geometrixx/en/toolbar/login.html`

   Esto es opcional, si se deja en blanco, se utilizará la página de inicio de sesión estándar.

1. Agregue la variable **Grupos admitidos**. Utilice + para agregar grupos o - para quitar. Solo los miembros de estos grupos podrán iniciar sesión en las páginas y acceder a ellas.
1. Asignar un **Territorio** (un nombre para los grupos de páginas) si es necesario. Déjelo vacío para utilizar el título de página.
1. Haga clic en **OK** para guardar la especificación.

Consulte [Identity Management](/help/sites-administering/identity-management.md) para obtener información sobre perfiles en el entorno de publicación y proporcionar formularios para iniciar y cerrar sesión.

## Vinculación Al Reino {#linking-to-the-realm}

Dado que el objetivo de cualquier vínculo al Dominio CUG no es visible para el usuario anónimo, el verificador de enlaces elimina esos enlaces.

Para evitarlo, es aconsejable crear páginas de redireccionamiento no protegidas que apunten a páginas dentro del Reino CUG. Las entradas de navegación se procesan sin causar ningún problema al verificador de enlaces. Solo cuando realmente acceda a la página de redireccionamiento se redirigirá al usuario dentro del Reino CUG, después de proporcionar correctamente sus credenciales de inicio de sesión.

## Configuración de Dispatcher para CUG {#configure-dispatcher-for-cugs}

Si utiliza Dispatcher, debe definir una granja de Dispatcher con las siguientes propiedades:

* [hosts virtuales](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts): Coincide con la ruta a las páginas a las que se aplica el CUG.
* \sessionmanagement: consulte a continuación.
* [cache](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache): Un directorio de caché dedicado a los archivos a los que se aplica el CUG.

### Configuración de la administración de sesiones de Dispatcher para CUG {#configuring-dispatcher-session-management-for-cugs}

Configurar [administración de sesiones en el archivo dispatcher.any](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) para el CUG. El controlador de autenticación que se utiliza cuando se solicita el acceso a las páginas CUG determina cómo se configura la administración de sesiones.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Cuando una granja de Dispatcher tiene habilitada la administración de sesiones, todas las páginas que gestiona la granja no se almacenan en caché. Para almacenar en caché las páginas que están fuera del CUG, cree una segunda granja en dispatcher.any
>que gestiona las páginas que no son de CUG.

1. Configurar [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) definiendo `/directory`; por ejemplo:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Establezca [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) a `0`.
