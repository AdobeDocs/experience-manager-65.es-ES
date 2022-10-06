---
title: Adición de dominios
seo-title: Adding domains
description: Obtenga información sobre cómo agregar un dominio empresarial, local o híbrido mediante la configuración de Administración de dominios y consideraciones generales para nombres de dominio e ID.
seo-description: Learn how to add an enterprise, local, or hybrid domain using Domain Management settings and general considerations for domain names and IDs.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# Adición de dominios {#adding-domains}

## Añadir un dominio de empresa {#add-an-enterprise-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio de empresa.
1. En el cuadro ID, escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes sobre los nombres de dominio y los ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique si desea habilitar el bloqueo de cuenta. (Consulte [Configuración del bloqueo de cuentas](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) De forma predeterminada, la opción Habilitar bloqueo de cuenta está seleccionada.
1. Haga clic en Agregar autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización. Los valores posibles son LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

   Si selecciona LDAP, puede utilizar el servidor LDAP especificado en la configuración del directorio o elegir un servidor LDAP diferente para la autenticación. Si elige un servidor diferente, los usuarios deben existir en ambos servidores LDAP.

1. Proporcione la información adicional requerida en la página. (Consulte [Configuración de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Añada un directorio o una interfaz de proveedor de servicios personalizada (SPI). (Consulte [Añadir directorios o SPI personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Haga clic en Finalizar y, a continuación, en Aceptar.

Después de crear un dominio de empresa, sincronice manualmente el directorio o cree un déclencheur para realizar una sincronización antes de que la Administración de usuarios pueda utilizarla. A continuación, puede configurar una programación de sincronización de directorios y realizar la sincronización manual según sea necesario. (Consulte [Sincronización de directorios](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Añadir un dominio local {#add-a-local-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio local.
1. En el cuadro ID, escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes sobre los nombres de dominio y los ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique si desea habilitar el bloqueo de cuenta y haga clic en Aceptar. (Consulte [Configuración del bloqueo de cuentas](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) De forma predeterminada, la opción Habilitar bloqueo de cuenta está seleccionada.

## Añadir un dominio híbrido {#add-a-hybrid-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio híbrido.
1. En el cuadro ID, escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes sobre los nombres de dominio y los ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Haga clic en Agregar autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización. Los valores posibles son LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.
1. Proporcione la información adicional requerida en la página. (Consulte [Configuración de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Haga clic en Aceptar y, a continuación, en Aceptar de nuevo.

## Consideraciones importantes sobre los nombres de dominio y los ID {#important-considerations-for-domain-names-and-ids}

Tenga en cuenta las siguientes consideraciones a la hora de elegir un nombre de dominio y un ID:

### Consideraciones generales {#general-considerations}

* Cuando utiliza un proveedor de base de datos que no sea DB2, el ID de dominio puede contener hasta 50 bytes. Si utiliza caracteres ASCII de byte único, el límite es de 50 caracteres. Si el identificador de dominio contiene caracteres multibyte, este límite se reduce. Por ejemplo, si crea un dominio cuyo identificador contiene caracteres de 3 bytes, el límite es de 16 caracteres. Además, no se pueden crear dominios que contengan caracteres de 4 bytes. Si crea un ID de dominio que supera este límite, AEM formularios estarán en un estado inestable. Para recuperarse de este estado inestable, consulte &quot; [Eliminación de un dominio que contiene caracteres ampliados o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; en esta página.
* El número de dominios de empresa y dominios locales que se pueden crear dentro de AEM formularios depende de la longitud de cada ID de dominio. Cuando se agrega un dominio empresarial o híbrido, la Administración de usuarios actualiza la cadena configInstance en el nodo AuthProviders del archivo de configuración de formularios AEM (config.xml). La cadena configInstance contiene una lista separada por dos puntos de las rutas absolutas de todos los dominios asociados al proveedor de autorización. Esta cadena tiene un límite de tamaño de 8192 caracteres. Cuando se alcanza ese límite, no se pueden crear dominios adicionales.

### Consideraciones al usar DB2 {#considerations-when-using-db2}

Cuando se utiliza DB2 para la base de datos de AEM forms, la longitud máxima permitida del ID de dominio depende del tipo de caracteres utilizados:

* 100 bytes simples (ASCII) (por ejemplo, caracteres utilizados en inglés, francés o alemán)
* 50 bits dobles (por ejemplo, caracteres utilizados en chino, japonés o coreano)
* 25 de cuatro bytes (por ejemplo, caracteres utilizados en chino tradicional)

### Consideraciones al usar MySQL {#considerations-when-using-mysql}

Al usar MySQL como base de datos de formularios AEM, se aplican las siguientes limitaciones:

* Utilice únicamente caracteres de byte único (ASCII) para el ID de dominio y el nombre de dominio. Si utiliza caracteres ASCII extendidos, AEM formularios estarán en un estado inestable y pueden generar una excepción si intenta eliminar el dominio. Para recuperarse de este estado inestable, consulte &quot; [Eliminación de un dominio que contiene caracteres ampliados o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; en esta página.
* No se pueden crear dos dominios que tengan el mismo nombre pero que difieran en mayúsculas y minúsculas. Por ejemplo, al intentar crear un dominio denominado *Adobe* cuando un dominio tiene un nombre *adobe* ya existe, se produce un error.
* La administración de usuarios no puede diferenciar entre dos nombres de dominio que solo difieran en el uso de caracteres extendidos. Por ejemplo, si crea un dominio con el nombre *abcode* y un dominio denominado *âbcdè*, se consideran iguales.

### Eliminación de un dominio que contiene caracteres ampliados o multibyte {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Exporte el archivo de configuración, tal como se describe en [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Abra el archivo de configuración y, en el nodo Dominios , busque el nodo cuyo atributo de nombre coincida con el nombre del dominio creado con caracteres ampliados o multibyte. Elimine todo el nodo relacionado con ese dominio.
1. En la base de datos, busque el dominio en la tabla edcprincipaldomainentity :

   * Select `*` de edcprincipaldomainentity.
   * Busque el nombre de dominio que contiene caracteres ampliados o multibyte y establezca su estado en OBSOLETE.

1. Importe el archivo de configuración actualizado, tal como se describe en [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
