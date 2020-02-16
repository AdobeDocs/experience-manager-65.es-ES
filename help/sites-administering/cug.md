---
title: Creación de un grupo de usuarios cerrado
seo-title: Creación de un grupo de usuarios cerrado
description: Obtenga información sobre cómo crear un grupo de usuarios cerrado.
seo-description: Obtenga información sobre cómo crear un grupo de usuarios cerrado.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
translation-type: tm+mt
source-git-commit: 29328ff7fde4ed0e7f9728af1be911133259dc6c

---


# Creación de un grupo de usuarios cerrado{#creating-a-closed-user-group}

Los grupos de usuarios cerrados (CUG) se utilizan para limitar el acceso a páginas específicas que residen en un sitio de Internet publicado. Estas páginas requieren que los miembros asignados inicien sesión y proporcionen credenciales de seguridad.

Para configurar dicho área dentro del sitio web:

* [cree el grupo de usuarios cerrado real y asigne miembros](#creating-the-user-group-to-be-used).

* [aplicar este grupo a las páginas](#applying-your-closed-user-group-to-content-pages) requeridas y seleccionar (o crear) la página de inicio de sesión para que la utilicen los miembros del CUG; también se especifica al aplicar un CUG a una página de contenido.

* [cree un vínculo, de alguna forma, a al menos una página dentro del área](#linking-to-the-realm)protegida; de lo contrario, no será visible.
* [configure el despachante](#configure-dispatcher-for-cugs) si está en uso.

>[!CAUTION]
>
>Los grupos de usuarios cerrados (CUG) siempre deben crearse teniendo en cuenta el rendimiento.
>
>Aunque el número de usuarios y grupos en un CUG no está limitado, un número elevado de CUG en una página puede ralentizar el rendimiento de la representación.
>
>Siempre se debe tener en cuenta el impacto de los CUG al realizar pruebas de rendimiento.

## Creación Del Grupo De Usuarios Que Se Utilizará {#creating-the-user-group-to-be-used}

Para crear un grupo de usuarios cerrado:

1. Vaya a **Herramientas - Seguridad** desde la pantalla de inicio de AEM.

   >[!NOTE]
   >
   >Consulte [Administración de usuarios y grupos](/help/sites-administering/security.md#managing-users-and-groups) para obtener información completa sobre cómo crear y configurar usuarios y grupos.

1. Seleccione la tarjeta **Grupos** en la siguiente pantalla.

   ![captura de pantalla_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Pulse el botón **Crear** en la esquina superior derecha para crear un nuevo grupo.
1. Asigne un nombre al nuevo grupo; por ejemplo, `cug_access`.

   ![captura de pantalla_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Vaya a la ficha **Miembros** y asigne los usuarios necesarios a este grupo.

   ![captura de pantalla_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Active cualquier usuario que haya asignado a su CUG; en este caso, todos los miembros de `cug_access`.
1. Active el grupo de usuarios cerrado para que esté disponible en el entorno de publicación; en este ejemplo, `cug_access`.

## Aplicación Del Grupo De Usuarios Cerrado A Las Páginas De Contenido {#applying-your-closed-user-group-to-content-pages}

Para aplicar el CUG a una página:

1. Navegue a la página raíz de la sección restringida que desee asignar a su CUG.
1. Para seleccionar la página, haga clic en su miniatura y, a continuación, en **Propiedades** en el panel superior.

   ![captura de pantalla_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. En la siguiente ventana, vaya a la ficha **Avanzadas** .
1. Desplácese hacia abajo y active la casilla de verificación en la sección Requisito **de autenticación** .

1. Agregue la ruta de configuración siguiente y, a continuación, presione Guardar.
1. A continuación, vaya a la ficha **Permisos** y presione el botón **Editar grupo** cerrado de usuarios.

   ![captura de pantalla_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[NOTA!]
   >
   > Tenga en cuenta que los CUG de la ficha Permisos no se pueden revertir de Blueprints a Live Copies. Planee esto al configurar Live Copy.
   >
   > Para obtener más información, consulte [esta página](closed-user-groups.md#aem-livecopy).

1. Busque y agregue su CUG en la siguiente ventana; en este caso, agregue el grupo llamado **cug_access**. Finalmente, presione **Guardar**.
1. Haga clic en **Habilitado** para definir que esta página (y las páginas secundarias) pertenecen a un CUG.
1. Especifique la página **de** inicio de sesión que utilizarán los miembros del grupo; por ejemplo:

   `/content/geometrixx/en/toolbar/login.html`

   Esto es opcional, si se deja en blanco, se utilizará la página de inicio de sesión estándar.

1. Agregue los grupos **** admitidos. Utilice + para agregar grupos o - para eliminar. Sólo los miembros de estos grupos podrán iniciar sesión y acceder a las páginas.
1. Asigne un **territorio** (un nombre para los grupos de páginas) si es necesario. Déjelo vacío para utilizar el título de página.
1. Click **OK** to save the specification.

Consulte Administración [de identidades](/help/sites-administering/identity-management.md) para obtener información sobre perfiles en el entorno de publicación y formularios para iniciar y cerrar sesión.

## Vinculación al reino {#linking-to-the-realm}

Dado que el objetivo de cualquier vínculo al Reino de CUG no es visible para el usuario anónimo, el comprobador de vínculos eliminará dichos vínculos.

Para evitarlo, es aconsejable crear páginas de redireccionamiento no protegidas que apunten a páginas dentro del reino de CUG. Las entradas de navegación se procesan sin causar ningún problema al comprobador de vínculos. Solo cuando se acceda realmente a la página de redireccionamiento se redirigirá al usuario dentro del reino CUG, después de proporcionar correctamente sus credenciales de inicio de sesión.

## Configurar Dispatcher para CUG {#configure-dispatcher-for-cugs}

Si utiliza Dispatcher, debe definir una granja de Dispatcher con las siguientes propiedades:

* [hosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts)virtuales: Coincide con la ruta de las páginas a las que se aplica el CUG.
* \sessionmanagement: véase más abajo.
* [caché](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache): Directorio de caché dedicado a los archivos a los que se aplica el CUG.

### Configuración de Dispatcher Session Management para CUGs {#configuring-dispatcher-session-management-for-cugs}

Configure la administración de [sesiones en el archivo](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) dispatcher.any para el CUG. El controlador de autenticación que se utiliza cuando se solicita el acceso para páginas CUG determina cómo se configura la administración de sesiones.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Cuando un conjunto de servidores Dispatcher tiene habilitada la administración de sesiones, no se almacenan en caché todas las páginas que controla el conjunto de servidores. Para almacenar en caché las páginas que están fuera del CUG, cree un segundo conjunto de servidores en dispatcher.any
>que controla las páginas que no son de CUG.

1. Configure [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) definiendo `/directory`; por ejemplo:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Establezca [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) en `0`.

