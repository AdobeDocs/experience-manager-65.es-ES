---
title: Gestión de solicitudes de RGPD para la base de AEM
seo-title: Handling GDPR Requests for the AEM Foundation
description: Gestión de solicitudes de RGPD para la base de AEM
seo-description: null
uuid: d470061c-bbcf-4d86-9ce3-6f24a764ca39
contentOwner: sarchiz
discoiquuid: 8ee843b6-8cea-45fc-be6c-99c043f075d4
exl-id: 411d40ab-6be8-4658-87f6-74d2ac1a4913
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 55%

---

# Gestión de solicitudes de RGPD para la base de AEM{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

## Compatibilidad con el RGPD de AEM Foundation {#aem-foundation-gdpr-support}

En el nivel de base de AEM, los datos personales almacenados son el Perfil de usuario. Por lo tanto, la información de este artículo trata principalmente sobre cómo acceder y eliminar perfiles de usuario, para tratar las solicitudes de Acceso y Eliminación del RGPD respectivamente.

## Acceso a un perfil de usuario {#accessing-a-user-profile}

### Pasos manuales {#manual-steps}

1. Abra la consola Administración de usuarios, navegando hasta **[!UICONTROL Configuración - Seguridad - Usuarios]** o navegando directamente a `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`

   ![useradmin2](assets/useradmin2.png)

1. A continuación, busque el usuario en cuestión escribiendo su nombre en la barra de búsqueda situada en la parte superior de la página:

   ![usersearch](assets/usersearch.png)

1. Por último, abra el perfil de usuario haciendo clic en él y, a continuación, mire en la pestaña **[!UICONTROL Detalles]**.

   ![userprofile_small](assets/userprofile_small.png)

### API HTTP {#http-api}

Como ya se ha mencionado, Adobe proporciona API para acceder a los datos de usuario, con el fin de facilitar la automatización. Existen varios tipos de API que puede utilizar:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**API Sling**

*Descubrimiento del inicio del usuario:*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*Recuperación de datos de usuario*

Uso de la ruta del nodo desde la propiedad del inicio de la carga útil JSON devuelta desde el comando anterior:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Desactivación de un usuario y eliminación de los perfiles asociados {#disabling-a-user-and-deleting-the-associated-profiles}

### Desactivación de un usuario {#disable-user}

1. Abra la consola Administración de usuarios y busque el usuario en cuestión, tal como se ha descrito anteriormente.
1. Pase el ratón sobre el usuario y haga clic en el icono de selección. El perfil cambiará a gris para indicar que está seleccionado.

1. Pulse el botón Desactivar en el menú superior para desactivar el usuario:

   ![userdisable](assets/userdisable.png)

1. Finalmente, confirme la acción:

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   A continuación, la interfaz de usuario indicará que el usuario se ha desactivado atenuando y añadiendo un bloqueo a la tarjeta de perfil:

   ![disableduser](assets/disableduser.png)

### Eliminación de información del perfil de usuario {#delete-user-profile-information}

1. Inicie sesión en el CRXDE Lite y, a continuación, busque la variable `[!UICONTROL userId]`:

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. Abra el nodo de usuario que se encuentra en `[!UICONTROL /home/users]` de forma predeterminada:

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. Elimine los nodos de perfil y todos sus elementos secundarios. Existen dos formatos para los nodos de perfil, según la versión de AEM:

   1. El perfil privado predeterminado en `[!UICONTROL /profile]`
   1. `[!UICONTROL /profiles]`, para nuevos perfiles creados con AEM 6.5.

   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### API HTTP {#http-api-1}

Los siguientes procedimientos utilizan la herramienta de línea de comandos `curl` para ilustrar cómo deshabilitar al usuario con la **[!UICONTROL captura]** `userId` y eliminación de sus perfiles disponibles en la ubicación predeterminada.

* *Descubrimiento del inicio del usuario*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *Desactivación del usuario*

Uso de la ruta del nodo desde la propiedad del inicio de la carga útil JSON devuelta desde el comando anterior:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *Eliminación de perfiles de usuario*

Usando la ruta del nodo desde la propiedad principal de la carga útil JSON devuelta desde el comando de detección de cuentas y las ubicaciones de nodos de perfil conocidas fuera de cuadro:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
