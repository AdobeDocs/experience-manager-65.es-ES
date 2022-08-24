---
title: Configuración general de AEM Forms
seo-title: General AEM Forms settings
description: Aprenda a configurar las opciones de la página Configuraciones principales en la consola de administración para ayudar a mejorar el rendimiento del sistema.
seo-description: Learn to configure the Core Configurations page settings in administration console that can help improve system performance.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 1%

---

# Configuración general de AEM Forms {#general-aem-forms-settings}

La página Configuraciones principales de la consola de administración proporciona una configuración que puede ayudar a mejorar el rendimiento del sistema. Después de configurar o actualizar esta configuración, reinicie el servidor de aplicaciones.

Para obtener información sobre cómo habilitar el modo de copia de seguridad segura, consulte [Activación y desactivación del modo de copia de seguridad segura](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>Los archivos del directorio temporal y los documentos de larga duración del directorio raíz global de almacenamiento de documentos (GDS) pueden contener información confidencial del usuario, como información que requiere credenciales especiales cuando se accede a ella mediante las API o interfaces de usuario. Por lo tanto, es importante que este directorio esté correctamente protegido utilizando los métodos disponibles para el sistema operativo. Se recomienda que solo la cuenta del sistema operativo que se utiliza para ejecutar el servidor de aplicaciones tenga acceso de lectura y escritura a este directorio.


1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Configuración del sistema principal > Configuraciones]**.
1. En la página Configuraciones principales , cambie las opciones según sea necesario y haga clic en **[!UICONTROL OK]**. Para obtener más información sobre las opciones, consulte [Opciones de configuraciones principales](configure-general-aem-forms-settings.md#core-configurations-options).


## Opciones de configuraciones principales {#core-configurations-options}

**Ubicación del directorio temporal** Ruta de acceso del directorio donde AEM formularios crearán archivos temporales del producto. Si el valor de esta configuración está vacío, la ubicación toma como valor predeterminado el directorio temporal del sistema. Asegúrese de que el directorio temporal es una carpeta grabable.

>[!NOTE]
>
>Asegúrese de que el directorio temporal esté en el sistema de archivos local. AEM formularios no admite un directorio temporal en una ubicación remota.

**Directorio raíz de almacenamiento de documentos globales** El directorio raíz del almacenamiento global de documentos (GDS) se utiliza para los siguientes fines:

* Almacenar documentos de larga duración. Los documentos de larga duración no tienen una caducidad y persisten hasta que se eliminan (por ejemplo, los archivos PDF utilizados en un proceso de flujo de trabajo). Los documentos de larga duración son una parte crítica del estado general del sistema. Si se pierden o dañan algunos o todos estos documentos, el servidor de formularios puede volverse inestable. Por lo tanto, es importante que este directorio se almacene en un dispositivo RAID.
* Almacenamiento de documentos temporales necesarios durante el procesamiento.

>[!NOTE]
>
>También puede habilitar el almacenamiento de documentos en la base de datos de AEM forms. Sin embargo, el rendimiento del sistema es mejor cuando se utiliza el GDS.

* Transferencia de documentos entre nodos de un clúster. Si está ejecutando AEM formularios en un entorno agrupado, debe poder acceder a este directorio desde todos los nodos del clúster.
* Recibir parámetros entrantes de llamadas a API remotas.

Si no especifica un directorio raíz GDS, el directorio toma como valor predeterminado un directorio de servidor de aplicaciones:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>Cambiar el valor de la configuración del directorio raíz de GDS debe hacerse con especial cuidado. El directorio GDS se utiliza para almacenar archivos de larga duración utilizados dentro de un proceso, así como componentes de producto de formularios de AEM esenciales. Cambiar la ubicación del directorio GDS es un cambio importante del sistema. Si se configura incorrectamente la ubicación del directorio GDS, los formularios AEM dejarán de funcionar y es posible que se requiera una reinstalación completa de AEM formularios. Si especifica una nueva ubicación para el directorio GDS, el servidor de aplicaciones debe cerrarse y los datos migrados antes de poder reiniciar el servidor. El administrador del sistema debe mover todos los archivos desde la ubicación antigua a la nueva ubicación, pero conservar la estructura de directorio interna.

>[!NOTE]
>
>No especifique el mismo directorio para el directorio temporal y el directorio GDS.

Para obtener información adicional sobre el directorio GDS, consulte [Preparación para instalar AEM formularios (un solo servidor)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Ubicación del directorio de fuentes del servidor de Adobe** Escriba la ruta al directorio que contiene las fuentes del servidor de Adobe. Estas fuentes se instalan con formularios AEM. La ubicación predeterminada para estas fuentes es la [raíz de aem-forms]directorio /fonts. Si no se puede acceder a este directorio, puede copiar las fuentes en otra parte y utilizar esta configuración para especificar la nueva ubicación.

**Ubicación del directorio de fuentes del cliente** Escriba la ruta a un directorio que contenga fuentes adicionales que desee usar.

***nota **: Las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. Después de especificar el directorio de fuentes del cliente, asegúrese de reiniciar el sistema en el que está instalado AEM formulario.*

**Ubicación del directorio de fuentes del sistema** Escriba la ruta de acceso al directorio de fuentes que proporcionó su sistema operativo. Se pueden agregar varios directorios separados por punto y coma **;**.

**Ubicación del archivo de configuración de Data Services** Especifica la ubicación del archivo services-config.xml. De forma predeterminada, este archivo está incrustado en el archivo adobe-core-appserver.ear y no es accesible para el usuario. Una copia del archivo services-config.xml predeterminado se encuentra en [raíz de aem-forms]\sdk\misc\DataServices\Server-Configuration. Si ha cambiado este archivo y lo ha movido, escriba la nueva ubicación en este campo.

El archivo de configuración de Servicios de datos permite la personalización de la configuración de Servicios de datos, como el tipo de autenticación y la salida de depuración.

Esta configuración está vacía de forma predeterminada.

**Tamaño en línea máximo del documento predeterminado (bytes)** Número máximo de bytes guardados en memoria al pasar documentos entre varios componentes de formularios AEM. Utilice esta configuración para ajustar el rendimiento. Los documentos que sean menores que este número se almacenan en la memoria y se conservan en la base de datos. Los documentos que superen este máximo se almacenan en el disco duro.

Esta configuración es obligatoria. El valor predeterminado es 65536 bytes.

**Tiempo de espera de eliminación de documentos predeterminado (segundos)** Cantidad máxima de tiempo, en segundos, durante el cual se considera activo un documento que se pasa entre varios componentes de formularios AEM. Una vez transcurrido este tiempo, los archivos utilizados para almacenar este documento están sujetos a eliminación. Utilice esta configuración para controlar el uso del espacio en disco.

Esta configuración es obligatoria. El valor predeterminado es 600 segundos.

**Intervalo de barrido del documento (segundos)** Cantidad de tiempo, en segundos, entre los intentos de eliminar archivos que ya no son necesarios y que se utilizaron para pasar datos de documento entre servicios.

Esta configuración es obligatoria. El valor predeterminado es de 30 segundos.

**Habilitar FIPS** Seleccione esta opción para activar el modo FIPS. Federal Information Processing Standard (FIPS) 140-2 es un estándar de criptología definido por el gobierno de Estados Unidos. Cuando se ejecuta en modo FIPS, AEM formularios restringe la protección de datos a algoritmos aprobados por FIPS 140-2 mediante el módulo de cifrado RSA BSAFE Crypto-C 2.1.

El modo FIPS no admite algoritmos de cifrado que se utilicen en versiones Adobe Acrobat® anteriores a la 7.0. Si el modo FIPS está habilitado y utiliza el servicio de cifrado para cifrar al PDF mediante una contraseña con un nivel de compatibilidad establecido en Acrobat 5, el intento de cifrado fallará y se producirá un error.

En general, cuando se habilita FIPS, el servicio Assembler no aplicará cifrado de contraseña a ningún documento. Si se intenta esto, se genera una excepción FIPSModeException que indica que &quot;No se permite el cifrado de contraseña en el modo FIPS&quot;. Además, el elemento PDFsFromBookmarks de la descripción del documento XML (DDX) no es compatible con el modo FIPS cuando el documento base está cifrado con contraseña.

>[!NOTE]
>
>AEM software de formularios no valida el código para garantizar la compatibilidad con FIPS. Proporciona un modo de operación FIPS para que los algoritmos aprobados por FIPS se utilicen para los servicios criptográficos de las bibliotecas aprobadas por FIPS (RSA).

**Habilitar WSDL** Seleccione esta opción para habilitar la generación del lenguaje de definición de servicios web (WSDL) para todos los servicios que forman parte de AEM formularios.

Active esta opción en entornos de desarrollo, donde los desarrolladores utilizan la generación WSDL para crear sus aplicaciones cliente. Puede optar por desactivar la generación de WSDL en un entorno de producción para evitar exponer los detalles internos de un servicio.

**Habilitar el almacenamiento de documentos en la base de datos** Seleccione esta opción para almacenar documentos de larga duración en la base de datos de AEM forms. Al habilitar esta opción, no se elimina la necesidad de un directorio GDS. Sin embargo, al elegir esta opción, se simplifican AEM copias de seguridad de formularios. Si solo utiliza el GDS, una copia de seguridad implica poner el sistema de AEM forms de AEM en modo de copia de seguridad y luego completar las copias de seguridad de la base de datos y el GDS. Si selecciona la opción de la base de datos, la copia de seguridad implica completar la copia de seguridad de la base de datos para una nueva instalación o completar la copia de seguridad de la base de datos y la única copia de seguridad del GDS para una actualización. Es posible que se requiera una administración adicional de la base de datos para depurar trabajos y datos en comparación con una configuración solo de GDS. (Consulte Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos).

**Habilitar estadística de invocación de DSC** Cuando se selecciona esta opción, AEM forms rastrea las estadísticas de invocación, como el número de invocaciones, el tiempo que se tarda en invocar y el número de errores en invocaciones. Esta información se almacena en un bean JMX para que pueda utilizar Java™ JConsole o software de terceros para ver las estadísticas. Si no desea ver estas estadísticas, anule la selección de esta opción para mejorar AEM rendimiento de los formularios.

**Habilitar RDS** Al seleccionar esta opción, se habilita el servlet de Servicios de desarrollo remoto (RDS) dentro de AEM formularios. Cuando esta opción está habilitada, las herramientas del lado del cliente pueden interactuar con los servicios de datos para hacer cosas como implementar o anular la implementación de modelos para crear destinos y extremos, o para averiguar qué modelos se han implementado en extremos. De forma predeterminada, está opción no está seleccionada.

**Permitir solicitud de RDS no segura** Cuando se selecciona esta opción, las solicitudes RDS no necesitan utilizar https. De forma predeterminada, esta opción no está seleccionada y todas las comunicaciones con los servicios de datos deben ser solicitudes https.

**Permitir carga de documentos no segura desde aplicaciones de Flex:** El servlet de carga de archivos utilizado para cargar documentos desde aplicaciones de Flex® de Adobe a formularios AEM requiere que los usuarios estén autenticados y autorizados antes de poder cargar documentos. Se debe asignar al usuario la función Usuario de la aplicación de carga de documento u otra función que incluya el permiso de carga de documento. Esto ayuda a evitar que los usuarios no autorizados carguen documentos en el servidor de AEM forms. Seleccione esta opción si desea deshabilitar esta función de seguridad en un entorno de desarrollo o para la compatibilidad con versiones anteriores de AEM formularios. De forma predeterminada, está opción no está seleccionada. Para obtener más información, consulte &quot;Invocación de formularios AEM mediante AEM reasignación de formularios&quot; en Programación con formularios AEM.

**Permitir carga de documentos no segura desde aplicaciones Java SDK:** Las cargas HTTP DocumentManager deben estar seguras. De forma predeterminada, las cargas HTTP requieren que los usuarios estén autenticados y autorizados antes de poder cargar documentos. Se debe asignar al usuario la función de usuario de servicios u otra función que contenga el permiso de invocación de servicio. Esto ayuda a evitar que usuarios no autorizados carguen documentos en el servidor de formularios. Seleccione esta opción si desea deshabilitar esta función de seguridad en un entorno de desarrollo, para la compatibilidad con versiones anteriores de AEM formularios o en función de la configuración del cortafuegos. De forma predeterminada, está opción no está seleccionada. Para obtener más información, consulte &quot;Invocación de AEM formularios con la API de Java&quot; en Programación con AEM formularios.
