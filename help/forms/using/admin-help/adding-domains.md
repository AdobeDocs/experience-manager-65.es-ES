---
title: Agregar dominios
description: Obtenga información sobre cómo agregar un dominio empresarial, local o híbrido mediante la configuración de Administración de dominios y consideraciones generales para nombres de dominio e ID.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---

# Agregar dominios {#adding-domains}

## Agregar un dominio de empresa {#add-an-enterprise-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio de empresa.
1. En el cuadro Id., escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes sobre los nombres de dominio y los ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique si desea habilitar el bloqueo de cuentas. (Consulte [Configurar el bloqueo de cuentas](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) De forma predeterminada, la opción Habilitar bloqueo de cuentas está seleccionada.
1. Haga clic en Agregar autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización. Los valores posibles son LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.

   Si selecciona LDAP, puede utilizar el servidor LDAP especificado en la configuración del directorio, o bien puede elegir otro servidor LDAP para la autenticación. Si elige un servidor diferente, los usuarios deben existir en ambos servidores LDAP.

1. Proporcione la información adicional que necesite en la página. (Consulte [Configuración de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Agregue un directorio o una interfaz de proveedor de servicios (SPI) personalizada. (Consulte [Adición de directorios o SPI personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Haga clic en Finalizar y, a continuación, en Aceptar.

Después de crear un dominio de empresa, sincronice manualmente el directorio o cree un déclencheur para realizar una sincronización antes de que Administración de usuarios pueda utilizarlo. A continuación, puede configurar una programación de sincronización de directorios y realizar la sincronización manual según sea necesario. (Consulte [Sincronización de directorios](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Añadir un dominio local {#add-a-local-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio local.
1. En el cuadro Id., escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes sobre los nombres de dominio y los ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Especifique si desea habilitar el bloqueo de cuentas y haga clic en Aceptar. (Consulte [Configurar el bloqueo de cuentas](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) De forma predeterminada, la opción Habilitar bloqueo de cuentas está seleccionada.

## Añadir un dominio híbrido {#add-a-hybrid-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en Nuevo dominio híbrido.
1. En el cuadro Id., escriba un identificador único para el dominio y, en el cuadro Nombre, escriba un nombre descriptivo para el dominio. (Consulte [Consideraciones importantes sobre los nombres de dominio y los ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Haga clic en Agregar autenticación y, en la lista Proveedor de autenticación, seleccione un proveedor, según el mecanismo de autenticación que utilice su organización. Los valores posibles son LDAP, Kerberos, SAML o un proveedor de autenticación personalizado.
1. Proporcione la información adicional que necesite en la página. (Consulte [Configuración de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Haga clic en Aceptar y vuelva a hacer clic en Aceptar.

## Consideraciones importantes sobre los nombres de dominio y los ID {#important-considerations-for-domain-names-and-ids}

Tenga en cuenta las siguientes consideraciones al elegir un nombre de dominio y un ID:

### Consideraciones generales {#general-considerations}

* Si utiliza un proveedor de base de datos distinto de DB2, el identificador de dominio puede contener hasta 50 bytes. Si utiliza caracteres ASCII de un solo byte, el límite es de 50 caracteres. Si el identificador de dominio contiene caracteres multibyte, este límite se reduce. Por ejemplo, si crea un dominio cuyo identificador contiene caracteres de 3 bytes, el límite es de 16 caracteres. Además, no se pueden crear dominios que contengan caracteres de 4 bytes. AEM Si crea un ID de dominio que supere este límite, los formularios de la se encontrarán en un estado inestable. Para recuperarse de este estado inestable, consulte el &quot; [Quite un dominio que contenga caracteres extendidos o de bytes múltiples](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; en esta página.
* AEM El número de dominios de empresa y dominios locales que se pueden crear en los formularios de la aplicación depende de la longitud de cada uno de los ID de dominio. AEM Cuando se agrega un dominio empresarial o híbrido, Administración de usuarios actualiza la cadena configInstance en el nodo AuthProviders del archivo de configuración de formularios de la aplicación (config.xml). La cadena configInstance contiene una lista separada por dos puntos de las rutas absolutas de todos los dominios asociados al proveedor de autorización. Esta cadena tiene un límite de tamaño de 8192 caracteres. Cuando se alcanza ese límite, no se pueden crear dominios adicionales.

### Consideraciones al utilizar DB2 {#considerations-when-using-db2}

AEM Cuando se utiliza DB2 para la base de datos de formularios de la, la longitud máxima permitida del ID de dominio depende del tipo de caracteres utilizados:

* 100 byte simple (ASCII) (por ejemplo, caracteres utilizados en inglés, francés o alemán)
* 50 bytes dobles (por ejemplo, caracteres utilizados en chino, japonés o coreano)
* 25 de cuatro bytes (por ejemplo, caracteres utilizados en chino tradicional)

### Consideraciones al utilizar MySQL {#considerations-when-using-mysql}

AEM Al utilizar MySQL como base de datos de formularios de la, se aplican las siguientes limitaciones:

* Utilice únicamente caracteres de byte único (ASCII) para el identificador y el nombre de dominio. AEM Si utiliza caracteres ASCII extendidos, los formularios de la aplicación se encontrarán en un estado inestable y podrían generar una excepción si intenta eliminar el dominio. Para recuperarse de este estado inestable, consulte el &quot; [Quite un dominio que contenga caracteres extendidos o de bytes múltiples](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)Tema &quot; en esta página.
* No puede crear dos dominios que tengan el mismo nombre pero que difieran en mayúsculas y minúsculas. Por ejemplo, intentar crear un dominio llamado *Adobe* cuando un dominio llamado *adobe* ya existe y genera un error.
* Administración de usuarios no puede diferenciar dos nombres de dominio que solo difieren en el uso de caracteres extendidos. Por ejemplo, si crea un dominio denominado *abcde* y un dominio denominado *âbcdè*, se consideran iguales.

### Quite un dominio que contenga caracteres extendidos o de bytes múltiples {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Exporte el archivo de configuración como se describe en [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Abra el archivo de configuración y, en el nodo Dominios, busque el nodo cuyo atributo name coincida con el nombre del dominio creado con caracteres extendidos o multibyte. Elimine todo el nodo relacionado con ese dominio.
1. En la base de datos, busque el dominio en la tabla edcprincipaldomainentity:

   * Seleccionar `*` de edcprincipaldomainentity.
   * Busque el nombre de dominio que contiene caracteres extendidos o multibyte y establezca su estado en OBSOLETO.

1. Importe el archivo de configuración actualizado tal como se describe en [Importación y exportación del archivo de configuración](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
