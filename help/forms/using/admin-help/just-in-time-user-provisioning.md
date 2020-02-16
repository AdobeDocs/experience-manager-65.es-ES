---
title: Aprovisionamiento de usuarios justo a tiempo
seo-title: Aprovisionamiento de usuarios justo a tiempo
description: Utilice el aprovisionamiento justo a tiempo para agregar usuarios a Administración de usuarios después de autenticarse correctamente y asignar dinámicamente roles y grupos relevantes al nuevo usuario.
seo-description: Utilice el aprovisionamiento justo a tiempo para agregar usuarios a Administración de usuarios después de autenticarse correctamente y asignar dinámicamente roles y grupos relevantes al nuevo usuario.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Aprovisionamiento de usuarios justo a tiempo {#just-in-time-user-provisioning}

Los formularios de AEM admiten el aprovisionamiento puntual de usuarios que aún no existen en Administración de usuarios. Con el aprovisionamiento justo a tiempo, los usuarios se agregan automáticamente a Administración de usuarios después de autenticar correctamente sus credenciales. Además, las funciones y los grupos relevantes se asignan de forma dinámica al nuevo usuario.

## Necesidad de aprovisionamiento de usuarios justo a tiempo {#need-for-just-in-time-user-provisioning}

Así es como funciona la autenticación tradicional:

1. Cuando un usuario intenta iniciar sesión en formularios AEM, la Administración de usuarios pasa las credenciales del usuario secuencialmente a todos los proveedores de autenticación disponibles. (Las credenciales de inicio de sesión incluyen una combinación de nombre de usuario y contraseña, vale Kerberos, firma PKCS7, etc.)
1. El proveedor de autenticación valida las credenciales.
1. A continuación, el proveedor de autenticación comprueba si el usuario existe en la base de datos de Administración de usuarios. Los siguientes son posibles resultados:

   **** Existe: Si el usuario está actualizado y desbloqueado, Administración de usuarios devuelve la autenticación correcta. Sin embargo, si el usuario no está actualizado o está bloqueado, Administración de usuarios devuelve un error de autenticación.

   **** No existe: Administración de usuarios devuelve un error de autenticación.

   **** No válido: Administración de usuarios devuelve un error de autenticación.

1. Se evalúa el resultado devuelto por el proveedor de autenticación. Si el proveedor de autenticación devolvió la autenticación correctamente, se permite al usuario iniciar sesión. De lo contrario, la Administración de usuarios comprueba con el siguiente proveedor de autenticación (pasos 2 a 3).
1. Se devuelve un error de autenticación si ningún proveedor de autenticación disponible valida las credenciales de usuario.

Cuando se implementa el aprovisionamiento justo a tiempo, se crea dinámicamente un nuevo usuario en Administración de usuarios si uno de los proveedores de autenticación valida las credenciales del usuario. (Después del paso 3 del procedimiento de autenticación tradicional, arriba).

## Implementar el aprovisionamiento de usuarios justo a tiempo {#implement-just-in-time-user-provisioning}

### API para aprovisionamiento justo a tiempo {#apis-for-just-in-time-provisioning}

Los formularios AEM proporcionan las siguientes API para el aprovisionamiento justo a tiempo:

```as3
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### Consideraciones a la hora de crear un dominio que se active justo en el tiempo {#considerations-while-creating-a-just-in-time-enabled-domain}

* Al crear una personalización `IdentityCreator` para un dominio híbrido, asegúrese de que se especifica una contraseña ficticia para el usuario local. No deje vacío este campo de contraseña.
* Recomendación: Se utiliza `DomainSpecificAuthentication` para validar las credenciales de usuario en un dominio específico.

### Creación de un dominio con capacidad para usar justo a tiempo {#create-a-just-in-time-enabled-domain}

1. Escriba una DSC para implementar las API en la sección &quot;API para aprovisionamiento justo a tiempo&quot;.
1. Implementar DSC en el servidor de formularios.
1. Cree un dominio con tiempo justo:

   * En la Consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios > Nuevo dominio de empresa.
   * Configure el dominio y seleccione Habilitar aprovisionamiento justo a tiempo. <!--Fix broken link (See Setting up and managing domains).-->
   * Agregue proveedores de autenticación. Al agregar proveedores de autenticación, en la pantalla Nueva autenticación, seleccione un Creador de identidad y un Proveedor de asignación registrados.

1. Guarde el nuevo dominio.

## Entre bastidores {#behind-the-scenes}

Supongamos que un usuario está intentando iniciar sesión en formularios AEM y que un proveedor de autenticación acepta sus credenciales de usuario. Si el usuario aún no existe en la base de datos de Administración de usuarios, se produce un error en la comprobación de identidad del usuario. Los formularios AEM ahora realizan las siguientes acciones:

1. Cree un `UserProvisioningBO` objeto con los datos de autenticación y colóquelo en un mapa de credenciales.
1. Según la información de dominio devuelta por `UserProvisioningBO`, recupere e e invoque el registro `IdentityCreator` y `AssignmentProvider` para el dominio.
1. Invocar `IdentityCreator`. Si devuelve un resultado correcto `AuthResponse`, extraiga `UserInfo` del mapa de credenciales. Páselo al `AssignmentProvider` para la asignación de grupos/funciones y cualquier otro proceso posterior después de crear el usuario.
1. Si el usuario se ha creado correctamente, devuelva el intento de inicio de sesión del usuario como correcto.
1. Para dominios híbridos, extraiga la información de usuario de los datos de autenticación proporcionados al proveedor de autenticación. Si esta información se obtiene correctamente, cree el usuario sobre la marcha.

>[!NOTE]
>
>La función de aprovisionamiento justo a tiempo incluye una implementación predeterminada de la `IdentityCreator` que puede utilizar para crear usuarios de forma dinámica. Los usuarios se crean con la información asociada a los directorios del dominio.

