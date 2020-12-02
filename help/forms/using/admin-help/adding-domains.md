---
title: Añadir dominios
seo-title: Añadir dominios
description: Obtenga información sobre cómo agregar un dominio empresarial, local o híbrido mediante la configuración de Administración de dominios y consideraciones generales para los nombres de dominio y las ID.
seo-description: Obtenga información sobre cómo agregar un dominio empresarial, local o híbrido mediante la configuración de Administración de dominios y consideraciones generales para los nombres de dominio y las ID.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---


# Añadiendo dominios {#adding-domains}

## Añadir un dominio de empresa {#add-an-enterprise-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio de empresa.
1. En el cuadro ID, escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes para los nombres de dominio y las ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique si desea habilitar el bloqueo de cuenta. (Consulte [Configuración del bloqueo de cuentas](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) De forma predeterminada, la opción Activar bloqueo de cuenta está seleccionada.
1. Haga clic en Añadir autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización. Los valores posibles son LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

   Si selecciona LDAP, puede utilizar el servidor LDAP especificado en la configuración del directorio, o bien elegir un servidor LDAP diferente para la autenticación. Si elige otro servidor, los usuarios deben existir en ambos servidores LDAP.

1. Proporcione la información adicional necesaria en la página. (Consulte [Configuración de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Añada un directorio o una interfaz de Proveedor de servicio personalizada (SPI). (Consulte [Añadir directorios o SPI personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)).
1. Haga clic en Finalizar y, a continuación, en Aceptar.

Después de crear un dominio de empresa, sincronice manualmente el directorio o cree un activador para realizar una sincronización antes de que la Administración de usuarios pueda utilizarlo. A continuación, puede configurar una programación de sincronización de directorios y realizar la sincronización manual según sea necesario. (Consulte [Sincronización de directorios](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Añadir un dominio local {#add-a-local-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio local.
1. En el cuadro ID, escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes para los nombres de dominio y las ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique si desea habilitar el bloqueo de cuenta y, a continuación, haga clic en Aceptar. (Consulte [Configuración del bloqueo de cuentas](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) De forma predeterminada, la opción Activar bloqueo de cuenta está seleccionada.

## Añadir un dominio híbrido {#add-a-hybrid-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio híbrido.
1. En el cuadro ID, escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes para los nombres de dominio y las ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Haga clic en Añadir autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización. Los valores posibles son LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.
1. Proporcione la información adicional necesaria en la página. (Consulte [Configuración de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Haga clic en Aceptar y, a continuación, en Aceptar nuevamente.

## Consideraciones importantes para los nombres de dominio e ID {#important-considerations-for-domain-names-and-ids}

Tenga en cuenta las siguientes consideraciones al elegir un nombre de dominio y un ID:

### Consideraciones generales {#general-considerations}

* Cuando se utiliza un proveedor de base de datos que no es DB2, el ID de dominio puede contener hasta 50 bytes. Si utiliza caracteres ASCII de byte único, el límite es de 50 caracteres. Si el identificador de dominio contiene caracteres multibyte, este límite se reduce. Por ejemplo, si crea un dominio cuyo identificador contiene caracteres de 3 bytes, el límite es de 16 caracteres. Además, no puede crear dominios que contengan caracteres de 4 bytes. Si crea un ID de dominio que supera este límite, AEM formularios estarán en un estado inestable. Para recuperarse de este estado inestable, consulte &quot; [Quitar un dominio que contiene caracteres extendidos o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; en esta página.
* El número de dominios de empresa y dominios locales que se pueden crear dentro de AEM formularios depende de la longitud de cada ID de dominio. Cuando se agrega un dominio empresarial o híbrido, Administración de usuarios actualiza la cadena configInstance en el nodo AuthProviders del archivo de configuración de formularios AEM (config.xml). La cadena configInstance contiene una lista separada por dos puntos de las rutas absolutas de todos los dominios asociados al proveedor de autorización. Esta cadena tiene un límite de tamaño de 8192 caracteres. Cuando se alcanza ese límite, no se pueden crear dominios adicionales.

### Consideraciones al usar DB2 {#considerations-when-using-db2}

Al utilizar DB2 para la base de datos de formularios AEM, la longitud máxima permitida del ID de dominio depende del tipo de caracteres utilizados:

* 100 de byte único (ASCII) (por ejemplo, caracteres utilizados en inglés, francés o alemán)
* 50 bytes de doble (por ejemplo, caracteres utilizados en chino, japonés o coreano)
* 25 de cuatro bytes (por ejemplo, caracteres utilizados en chino tradicional)

### Consideraciones al usar MySQL {#considerations-when-using-mysql}

Al utilizar MySQL como base de datos de formularios AEM, se aplican las siguientes limitaciones:

* Utilice únicamente caracteres de byte único (ASCII) para el ID de dominio y el nombre de dominio. Si utiliza caracteres ASCII extendidos, AEM formularios estarán en un estado inestable y pueden generar una excepción si intenta eliminar el dominio. Para recuperarse de este estado inestable, consulte el tema &quot; [Eliminar un dominio que contiene caracteres extendidos o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; en esta página.
* No se pueden crear dos dominios con el mismo nombre pero que difieran en mayúsculas y minúsculas. Por ejemplo, intentar crear un dominio denominado *Adobe* cuando ya existe un dominio denominado *adobe* resulta en un error.
* La Administración de usuarios no puede diferenciar entre dos nombres de dominio que solo difieran en el uso de caracteres extendidos. Por ejemplo, si crea un dominio con el nombre *abcde* y un dominio con el nombre *âbcdè*, se considerarán iguales.

### Quitar un dominio que contenga caracteres extendidos o multibyte {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Exporte el archivo de configuración, tal como se describe en [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Abra el archivo de configuración y, en el nodo Dominios, busque el nodo cuyo atributo de nombre coincida con el nombre del dominio creado con caracteres extendidos o multibyte. Elimine todo el nodo relacionado con ese dominio.
1. En la base de datos, busque el dominio en la tabla edcprincipaldomainentity:

   * Seleccione `*` de edcprincipaldomainentity.
   * Busque el nombre de dominio que contiene caracteres extendidos o de byte múltiple y establezca su estado en OBSOLETE.

1. Importe el archivo de configuración actualizado, tal como se describe en [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).

