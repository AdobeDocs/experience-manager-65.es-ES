---
title: Configuración general de AEM Forms
seo-title: Configuración general de AEM Forms
description: Aprenda a configurar las opciones de la página Configuraciones principales en la consola de administración para mejorar el rendimiento del sistema.
seo-description: Aprenda a configurar las opciones de la página Configuraciones principales en la consola de administración para mejorar el rendimiento del sistema.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Configuración general de AEM Forms {#general-aem-forms-settings}

La página Configuraciones principales de la consola de administración proporciona configuraciones que pueden ayudar a mejorar el rendimiento del sistema. Después de configurar o actualizar esta configuración, reinicie el servidor de aplicaciones.

Para obtener información sobre cómo habilitar el modo de copia de seguridad segura, consulte [Activación y desactivación del modo](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode)de copia de seguridad segura.


>[!NOTE]
>
>Los archivos del directorio temporal y los documentos de larga duración del directorio raíz global de almacenamiento de documentos (GDS) pueden contener información confidencial del usuario, como información que requiere credenciales especiales cuando se accede mediante las API o las interfaces de usuario. Por lo tanto, es importante que este directorio esté asegurado correctamente utilizando los métodos disponibles para el sistema operativo. Se recomienda que solo la cuenta del sistema operativo que se utiliza para ejecutar el servidor de aplicaciones tenga acceso de lectura y escritura a este directorio.


1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Configuración del sistema principal > Configuraciones]**.
1. En la página Configuraciones principales, cambie las opciones según sea necesario y haga clic en **[!UICONTROL Aceptar]**. Para obtener más información sobre las opciones, consulte Opciones de configuración [principales](configure-general-aem-forms-settings.md#core-configurations-options).


## Opciones de configuraciones principales {#core-configurations-options}

**Ubicación del directorio** temporal La ruta del directorio en la que los formularios AEM crearán archivos temporales de producto. Si el valor de esta configuración está vacío, la ubicación predeterminada es el directorio temp del sistema. Asegúrese de que el directorio temp sea una carpeta grabable.

***nota **: Asegúrese de que el directorio temporal está en el sistema de archivos local. Los formularios AEM no admiten un directorio temporal en una ubicación remota.*

**Directorio** raíz de almacenamiento de documentos global El directorio raíz de almacenamiento de documentos global (GDS) se utiliza para los siguientes fines:

* Almacenamiento de documentos de larga duración. Los documentos de larga duración no tienen un tiempo de caducidad y persisten hasta que se eliminan (por ejemplo, los archivos PDF utilizados en un proceso de flujo de trabajo). Los documentos de larga duración son una parte crítica del estado general del sistema. Si algunos o todos estos documentos se pierden o se dañan, el servidor de formularios puede volverse inestable. Por lo tanto, es importante que este directorio se almacene en un dispositivo RAID.
* Almacenamiento de documentos temporales necesarios durante el procesamiento.

   ***Nota **: También puede activar el almacenamiento de documentos en la base de datos de formularios de AEM. Sin embargo, el rendimiento del sistema es mejor cuando se utiliza el GDS.*

* Transferencia de documentos entre nodos de un clúster. Si ejecuta formularios AEM en un entorno agrupado, este directorio debe ser accesible desde todos los nodos del clúster.
* Recibir parámetros entrantes de llamadas de API remotas.

Si no especifica un directorio raíz GDS, el directorio se establece de forma predeterminada en un directorio de servidor de aplicaciones:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/[server]/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/[server]/adobe/AEMformsserver/DocumentStorage`

***Nota **: El cambio del valor del directorio raíz GDS debe realizarse con especial cuidado. El directorio GDS se utiliza para almacenar tanto archivos de larga duración utilizados en un proceso como componentes de producto de formularios AEM críticos. Cambiar la ubicación del directorio GDS es un cambio importante del sistema. Si se configura incorrectamente la ubicación del directorio GDS, los formularios AEM no estarán operativos y es posible que se requiera una reinstalación completa de los formularios AEM. Si especifica una nueva ubicación para el directorio GDS, el servidor de aplicaciones debe cerrarse y los datos migrados antes de poder reiniciar el servidor. El administrador del sistema debe mover todos los archivos de la ubicación antigua a la nueva ubicación, pero conservar la estructura de directorio interno.*

***Nota **: No especifique el mismo directorio para el directorio temp y el directorio GDS.*

Para obtener información adicional sobre el directorio GDS, consulte [Preparación de la instalación de formularios AEM (un solo servidor)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Ubicación del directorio** de fuentes de Adobe Server Escriba la ruta del directorio que contiene las fuentes del servidor de Adobe. Estas fuentes se instalan con formularios AEM. La ubicación predeterminada para estas fuentes es el directorio raíz [/fuentes]aem-forms. Si no se puede acceder a este directorio, puede copiar las fuentes en otra parte y utilizar esta configuración para especificar la nueva ubicación.

**Ubicación del directorio** Fuentes del cliente Escriba la ruta a un directorio que contenga fuentes adicionales que desee utilizar.

***nota **:Las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. Después de especificar el directorio de fuentes del cliente, asegúrese de reiniciar el sistema en el que están instalados los formularios AEM.*

**Ubicación del directorio** Fuentes del sistema Escriba la ruta al directorio de fuentes que proporcionó el sistema operativo. Se pueden agregar varios directorios, separados por punto y coma **;**.

**Ubicación del archivo** de configuración de Data Services Especifica la ubicación del archivo services-config.xml. De forma predeterminada, este archivo está incrustado en el archivo adobe-core-appserver.ear y no es accesible para el usuario. Una copia del archivo services-config.xml predeterminado se encuentra en [aem-forms root]\sdk\misc\DataServices\Server-Configuration. Si ha cambiado este archivo y lo ha movido, escriba la nueva ubicación en este campo.

El archivo de configuración de Data Services permite personalizar la configuración de Data Services, como el tipo de autenticación y la salida de depuración.

Esta configuración está vacía de forma predeterminada.

**Tamaño en línea máximo del documento predeterminado (bytes)** El número máximo de bytes guardados en memoria al pasar documentos entre varios componentes de formularios AEM. Utilice esta configuración para ajustar el rendimiento. Los documentos que son menores que este número se almacenan en la memoria y se conservan en la base de datos. Los documentos que superen este máximo se almacenarán en el disco duro.

Esta configuración es obligatoria. El valor predeterminado es 65536 bytes.

**Tiempo de espera predeterminado de eliminación de documentos (segundos)** La cantidad máxima de tiempo, en segundos, durante el cual se considera activo un documento que se pasa entre varios componentes de formularios AEM. Una vez transcurrido este tiempo, los archivos que se utilizan para almacenar este documento están sujetos a eliminación. Utilice esta configuración para controlar el uso del espacio en disco.

Esta configuración es obligatoria. El valor predeterminado es 600 segundos.

**Intervalo de barrido del documento (segundos)** La cantidad de tiempo, en segundos, entre los intentos de eliminar archivos que ya no son necesarios y se utilizaron para pasar datos del documento entre servicios.

Esta configuración es obligatoria. El valor predeterminado es 30 segundos.

**Activar FIPS** Seleccione esta opción para activar el modo FIPS. Federal Information Processing Standard (FIPS) 140-2 es un estándar de criptografía definido por el gobierno de Estados Unidos. Cuando se ejecuta en modo FIPS, los formularios AEM restringen la protección de datos a algoritmos aprobados por FIPS 140-2 mediante el módulo de cifrado RSA BSAFE Crypto-C 2.1.

El modo FIPS no admite algoritmos de codificación que se utilizan en versiones de Adobe Acrobat® anteriores a la 7.0. Si el modo FIPS está activado y utiliza el servicio Cifrado para cifrar el PDF mediante una contraseña con un nivel de compatibilidad establecido en Acrobat 5, el intento de codificación generará un error.

En general, cuando FIPS está activado, el servicio Ensamblador no aplicará cifrado de contraseña a ningún documento. Si se intenta esto, se genera una excepción FIPSModeException que indica que &quot;No se permite el cifrado de contraseña en el modo FIPS&quot;. Además, el elemento PDFsFromBookmarks de la descripción del documento XML (DDX) no se admite en el modo FIPS cuando el documento base está cifrado con contraseña.

***Nota **: El software de formularios AEM no valida el código para garantizar la compatibilidad con FIPS. Proporciona un modo de operación FIPS para que los algoritmos aprobados por FIPS se utilicen para servicios criptográficos de las bibliotecas aprobadas por FIPS (RSA).*

**Activar WSDL** Seleccione esta opción para activar la generación del lenguaje de definición de servicios Web (WSDL) en todos los servicios que forman parte de formularios AEM.

Active esta opción en entornos de desarrollo, donde los desarrolladores utilizan la generación WSDL para crear sus aplicaciones cliente. Puede desactivar la generación WSDL en un entorno de producción para evitar exponer los detalles internos de un servicio.

**Habilitar el almacenamiento de documentos en la base de datos** Seleccione esta opción para almacenar documentos de larga duración en la base de datos de formularios de AEM. Al habilitar esta opción no se elimina la necesidad de un directorio GDS. Sin embargo, si elige esta opción, se simplificarán las copias de seguridad de formularios AEM. Si solo utiliza el GDS, una copia de seguridad implica poner el sistema de formularios AEMs en modo de copia de seguridad y, a continuación, completar las copias de seguridad de la base de datos y del GDS. Si selecciona la opción de base de datos, la copia de seguridad implica completar la copia de seguridad de la base de datos para una nueva instalación o completar la copia de seguridad de la base de datos y la única copia de seguridad del GDS para una actualización. Es posible que se requiera una administración adicional de la base de datos para depurar trabajos y datos, en comparación con una configuración de GDS solamente. (Consulte Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos).

**Activar estadística** de invocación de DSC Cuando se selecciona esta opción, los formularios de AEM realizan un seguimiento de las estadísticas de invocación, como el número de invocaciones, la cantidad de tiempo que se tarda en invocar y el número de errores en las invocaciones. Esta información se almacena en un archivo frigorífico JMX para que pueda utilizar Java™ JConsole o software de terceros para ver las estadísticas. Si no desea ver estas estadísticas, anule la selección de esta opción para mejorar el rendimiento de los formularios AEM.

**Activar RDS** Al seleccionar esta opción, se habilita el servlet de Servicios de desarrollo remoto (RDS) en los formularios AEM. Cuando esta opción está habilitada, las herramientas del lado del cliente pueden interactuar con los servicios de datos para realizar tareas como implementar o anular la implementación de modelos para crear destinos y extremos, o para averiguar qué modelos se han implementado en extremos. De forma predeterminada, está opción no está seleccionada.

**Permitir solicitud** RDS no segura Cuando se selecciona esta opción, las solicitudes RDS no necesitan utilizar https. De forma predeterminada, esta opción no está seleccionada y todas las comunicaciones a los servicios de datos deben ser solicitudes https.

**** Permitir la carga de documentos no seguros desde aplicaciones de Flex: El servlet de carga de archivos utilizado para cargar documentos de aplicaciones Adobe Flex® en formularios AEM requiere que los usuarios se autentiquen y autoricen antes de poder cargar documentos. Se debe asignar al usuario la función de usuario de la aplicación de carga de documento u otra función que incluya el permiso de carga de documento. Esto ayuda a evitar que usuarios no autorizados carguen documentos en el servidor de formularios AEM. Seleccione esta opción si desea deshabilitar esta función de seguridad en un entorno de desarrollo o para la compatibilidad con versiones anteriores de formularios AEM. De forma predeterminada, está opción no está seleccionada. Para obtener más información, consulte &quot;Invocación de formularios AEM mediante AEM Forms Remoting&quot; en Programación con formularios AEM.

**** Permitir la carga de documentos no seguros desde aplicaciones de Java SDK: Las cargas HTTP de DocumentManager deben estar seguras. De forma predeterminada, las cargas HTTP requieren que los usuarios se autentiquen y autoricen antes de poder cargar documentos. Se debe asignar al usuario la función de usuario de servicios u otra función que contenga el permiso Invocar servicio. Esto ayuda a evitar que usuarios no autorizados carguen documentos en el servidor de formularios. Seleccione esta opción si desea deshabilitar esta función de seguridad en un entorno de desarrollo, para la compatibilidad con versiones anteriores de formularios AEM o en función de la configuración del cortafuegos. De forma predeterminada, está opción no está seleccionada. Para obtener más información, consulte &quot;Invocación de formularios AEM mediante la API de Java&quot; en Programación con formularios AEM.
