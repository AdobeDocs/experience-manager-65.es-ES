---
title: Gestión de solicitudes GDPR para AEM Foundation
seo-title: Gestión de solicitudes GDPR para AEM Foundation
description: nulo
seo-description: nulo
uuid: d470061c-bbcf-4d86-9ce3-6f24a764ca39
contentOwner: sarchiz
discoiquuid: 8ee843b6-8cea-45fc-be6c-99c043f075d4
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# Gestión de solicitudes GDPR para AEM Foundation{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones que figuran a continuación, pero los detalles abarcados son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

## Compatibilidad con GDPR de AEM Foundation {#aem-foundation-gdpr-support}

A nivel de AEM Foundation, los datos personales almacenados son el perfil de usuario. Por lo tanto, la información de este artículo trata principalmente de cómo acceder a los perfiles de usuario y eliminarlos, para abordar las solicitudes de acceso y eliminación del RGPD, respectivamente.

## Acceso a un perfil de usuario {#accessing-a-user-profile}

### Pasos manuales {#manual-steps}

1. Abra la consola Administración de usuarios, navegando a **[!UICONTROL Configuración - Seguridad - Usuarios]** o navegando directamente a `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`

   ![useradmin2](assets/useradmin2.png)

1. A continuación, busque el usuario en cuestión escribiendo el nombre en la barra de búsqueda situada en la parte superior de la página:

   ![usersearch](assets/usersearch.png)

1. Por último, abra el perfil de usuario haciendo clic en él y, a continuación, marque la casilla de verificación en la ficha **[!UICONTROL Detalles]** .

   ![userprofile_small](assets/userprofile_small.png)

### API HTTP {#http-api}

Como se mencionó anteriormente, Adobe proporciona API para acceder a los datos de usuario, con el fin de facilitar la automatización. Existen varios tipos de API que puede utilizar:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

*Descubriendo la página principal del usuario:*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*Recuperación de datos de usuario*

Utilizando la ruta de nodo de la propiedad home de la carga útil JSON devuelta por el comando anterior:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Desactivación de un usuario y eliminación de los perfiles asociados {#disabling-a-user-and-deleting-the-associated-profiles}

### Deshabilitar usuario {#disable-user}

1. Abra la consola Administración de usuarios y busque al usuario en cuestión, tal como se describe más arriba.
1. Pase el ratón sobre el usuario y haga clic en el icono de selección. El perfil cambiará a gris indicando que está seleccionado.

1. Pulse el botón Deshabilitar en el menú superior para deshabilitar al usuario:

   ![userdisable](assets/userdisable.png)

1. Por último, confirme la acción:

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   A continuación, la interfaz de usuario indicará que el usuario se ha desactivado al atenuar y agregar un bloqueo a la tarjeta de perfil:

   ![disableduser](assets/disableduser.png)

### Eliminar información de perfil de usuario {#delete-user-profile-information}

1. Inicie sesión en CRXDE Lite y luego busque la `[!UICONTROL userId]`:

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. Abra el nodo de usuario que se encuentra en `[!UICONTROL /home/users]` de forma predeterminada:

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. Elimine los nodos de perfil y todos sus elementos secundarios. Existen dos formatos para los nodos de perfil, según la versión de AEM:

   1. El perfil privado predeterminado en `[!UICONTROL /profile]`
   1. `[!UICONTROL /profiles]`, para los nuevos perfiles creados con AEM 6.5.
   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### API HTTP {#http-api-1}

Los siguientes procedimientos utilizan la herramienta de línea de comandos para ilustrar cómo deshabilitar al usuario con la `curl` captura **** `userId` y eliminar sus perfiles disponibles en la ubicación predeterminada.

* *Descubrimiento de la página principal del usuario*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *Desactivación del usuario*

Utilizando la ruta de nodo de la propiedad home de la carga útil JSON devuelta por el comando anterior:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *Eliminación de perfiles de usuario*

Utilizando la ruta de acceso del nodo de la propiedad home de la carga útil JSON devuelta por el comando de detección de cuenta y las ubicaciones de nodos de perfil conocidas fuera del cuadro:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

