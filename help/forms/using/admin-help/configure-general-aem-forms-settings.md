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
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 1%

---


# Configuración general de AEM Forms {#general-aem-forms-settings}

La página Configuraciones principales de la consola de administración proporciona configuraciones que pueden ayudar a mejorar el rendimiento del sistema. Después de configurar o actualizar esta configuración, reinicie el servidor de aplicaciones.

Para obtener información sobre cómo habilitar el modo de copia de seguridad segura, consulte [Activación y desactivación del modo de copia de seguridad segura](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>Los archivos del directorio temporal y los documentos de larga duración del directorio raíz del almacenamiento de documento global (GDS) pueden contener información confidencial del usuario, como información que requiere credenciales especiales cuando se accede mediante API o interfaces de usuario. Por lo tanto, es importante que este directorio esté asegurado correctamente utilizando los métodos disponibles para el sistema operativo. Se recomienda que solo la cuenta del sistema operativo que se utiliza para ejecutar el servidor de aplicaciones tenga acceso de lectura y escritura a este directorio.


1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Configuración del sistema principal > Configuraciones]**.
1. En la página Configuraciones principales, cambie las opciones según sea necesario y haga clic en **[!UICONTROL Aceptar]**. Para obtener más información sobre las opciones, consulte [Opciones de configuraciones principales](configure-general-aem-forms-settings.md#core-configurations-options).


## Opciones de configuraciones principales {#core-configurations-options}

**Ubicación del** directorio temporalRuta del directorio donde AEM formularios crearán archivos temporales de producto. Si el valor de esta configuración está vacío, la ubicación predeterminada es el directorio temp del sistema. Asegúrese de que el directorio temp sea una carpeta grabable.

>[!NOTE]
>
>Asegúrese de que el directorio temporal está en el sistema de archivos local. AEM formularios no admite un directorio temporal en una ubicación remota.

**Directorio raíz del almacenamiento de documento global** El directorio raíz del almacenamiento de documento global (GDS) se utiliza para los siguientes fines:

* Conservar documentos de larga vida. Los documentos de larga duración no tienen un tiempo de caducidad y persisten hasta que se eliminan (por ejemplo, los archivos PDF utilizados en un proceso de flujo de trabajo). Los documentos de larga duración son una parte crítica del estado general del sistema. Si algunos o todos estos documentos se pierden o se dañan, el servidor de formularios puede volverse inestable. Por lo tanto, es importante que este directorio se almacene en un dispositivo RAID.
* Almacenamiento de documentos temporales necesarios durante el procesamiento.

>[!NOTE]
>
>También puede activar el almacenamiento de documento en la base de datos de formularios AEM. Sin embargo, el rendimiento del sistema es mejor cuando se utiliza el GDS.

* Transferencia de documentos entre nodos de un clúster. Si está ejecutando AEM formularios en un entorno agrupado, este directorio debe ser accesible desde todos los nodos del clúster.
* Recibir parámetros entrantes de llamadas de API remotas.

Si no especifica un directorio raíz GDS, el directorio se establece de forma predeterminada en un directorio de servidor de aplicaciones:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>El cambio del valor del directorio raíz GDS debe realizarse con especial cuidado. El directorio GDS se utiliza para almacenar tanto archivos de larga duración utilizados en un proceso como componentes de producto de formularios AEM críticos. Cambiar la ubicación del directorio GDS es un cambio importante del sistema. Si se configura incorrectamente la ubicación del directorio GDS, los formularios AEM dejarán de funcionar y es posible que se requiera una reinstalación completa de AEM formularios. Si especifica una nueva ubicación para el directorio GDS, el servidor de aplicaciones debe cerrarse y los datos migrados antes de poder reiniciar el servidor. El administrador del sistema debe mover todos los archivos de la ubicación antigua a la nueva ubicación, pero conservar la estructura de directorio interno.

>[!NOTE]
>
>No especifique el mismo directorio para el directorio temp y el directorio GDS.

Para obtener información adicional sobre el directorio GDS, consulte [Preparación de la instalación de formularios AEM (Servidor único)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Ubicación del** directorio de fuentes de Adobe ServerEscriba la ruta al directorio que contiene las fuentes del servidor de Adobe. Estas fuentes se instalan con AEM formularios. La ubicación predeterminada para estas fuentes es el directorio [aem-forms root]/fonts. Si no se puede acceder a este directorio, puede copiar las fuentes en otra parte y utilizar esta configuración para especificar la nueva ubicación.

**Ubicación del** directorio de fuentes del clienteEscriba la ruta de acceso a un directorio que contenga fuentes adicionales que desee utilizar.

***nota **: Las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. Después de especificar el directorio de fuentes del cliente, asegúrese de reiniciar el sistema en el que están instalados AEM formularios.*

**Ubicación del** directorio Fuentes del sistemaEscriba la ruta al directorio de fuentes que proporcionó el sistema operativo. Se pueden agregar varios directorios, separados por un punto y coma **;**.

**Ubicación del** archivo de configuración de Data ServicesEspecifica la ubicación del archivo services-config.xml. De forma predeterminada, este archivo está incrustado en el archivo adobe-core-appserver.ear y no es accesible para el usuario. Una copia del archivo services-config.xml predeterminado se encuentra en [aem-forms root]\sdk\misc\DataServices\Server-Configuration. Si ha cambiado este archivo y lo ha movido, escriba la nueva ubicación en este campo.

El archivo de configuración de Data Services permite personalizar la configuración de Data Services, como el tipo de autenticación y la salida de depuración.

Esta configuración está vacía de forma predeterminada.

**Tamaño de línea máximo de documento predeterminado (bytes)** El número máximo de bytes que se guardan en memoria al pasar documentos entre varios componentes de formularios AEM. Utilice esta configuración para ajustar el rendimiento. Los documentos que son menores que este número se almacenan en la memoria y se conservan en la base de datos. Los documentos que excedan este máximo se almacenan en el disco duro.

Esta configuración es obligatoria. El valor predeterminado es 65536 bytes.

**Tiempo de espera de eliminación de documentos predeterminado (segundos)** La cantidad máxima de tiempo, en segundos, durante el cual se considera activo un documento que se pasa entre varios componentes de formularios AEM. Una vez transcurrido este tiempo, los archivos que se utilizan para almacenar este documento están sujetos a eliminación. Utilice esta configuración para controlar el uso del espacio en disco.

Esta configuración es obligatoria. El valor predeterminado es 600 segundos.

**Intervalo de barrido de documento (segundos)** La cantidad de tiempo, en segundos, entre los intentos de eliminar archivos que ya no son necesarios y se utilizaron para pasar datos de documento entre servicios.

Esta configuración es obligatoria. El valor predeterminado es 30 segundos.

**Activar** FIPSSeleccione esta opción para habilitar el modo FIPS. Federal Information Processing Standard (FIPS) 140-2 es un estándar de criptografía definido por el gobierno de Estados Unidos. Cuando se ejecuta en modo FIPS, AEM formularios restringe la protección de datos a algoritmos aprobados por FIPS 140-2 mediante el módulo de cifrado RSA BSAFE Crypto-C 2.1.

El modo FIPS no admite algoritmos de codificación que se utilizan en versiones de Adobe Acrobat® anteriores a la 7.0. Si el modo FIPS está activado y utiliza el servicio Cifrado para cifrar el PDF mediante una contraseña con un nivel de compatibilidad establecido en Acrobat 5, el intento de cifrado fallará con un error.

En general, cuando FIPS está habilitado, el servicio Ensamblador no aplicará cifrado de contraseña a ningún documento. Si se intenta esto, se genera una excepción FIPSModeException que indica que &quot;No se permite el cifrado de contraseña en el modo FIPS&quot;. Además, el elemento PDFsFromBookmarks de la descripción de Documento (DDX) no se admite en el modo FIPS cuando el documento base está cifrado con contraseña.

>[!NOTE]
>
>AEM software de formularios no valida el código para garantizar la compatibilidad con FIPS. Proporciona un modo de operación FIPS para que los algoritmos aprobados por FIPS se utilicen para servicios criptográficos de las bibliotecas aprobadas por FIPS (RSA).

**Activar** WSDLSeleccione esta opción para habilitar la generación del lenguaje de definición de servicios Web (WSDL) para todos los servicios que forman parte de AEM formularios.

Active esta opción en entornos de desarrollo, donde los desarrolladores utilizan la generación WSDL para crear sus aplicaciones cliente. Puede desactivar la generación WSDL en un entorno de producción para evitar exponer los detalles internos de un servicio.

**Activar almacenamiento de documento en la** base de datosSeleccione esta opción para almacenar documentos de larga duración en la base de datos de formularios AEM. Al habilitar esta opción no se elimina la necesidad de un directorio GDS. Sin embargo, si elige esta opción, se simplificarán AEM copias de seguridad de formularios. Si solo utiliza el GDS, una copia de seguridad implica poner el sistema de formularios AEMAEM en modo de copia de seguridad y, a continuación, completar las copias de seguridad de la base de datos y del GDS. Si selecciona la opción de base de datos, la copia de seguridad implica completar la copia de seguridad de la base de datos para una nueva instalación o completar la copia de seguridad de la base de datos y la única copia de seguridad del GDS para una actualización. Es posible que se requiera una administración adicional de la base de datos para depurar trabajos y datos, en comparación con una configuración de GDS solamente. (Consulte Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documento).

**Activar** estadística de invocación DSCa la vez que se selecciona esta opción, AEM formularios realiza un seguimiento de las estadísticas de invocación, como el número de invocaciones, el tiempo que se tarda en invocar y el número de errores en las invocaciones. Esta información se almacena en un archivo frigorífico JMX para que pueda utilizar Java™ JConsole o software de terceros para ver las estadísticas. Si no desea ver estas estadísticas, anule la selección de esta opción para mejorar el rendimiento de AEM formularios.

**Habilitar** RDSSeseleccionar esta opción habilita el servlet de Servicios de desarrollo remoto (RDS) dentro de AEM formularios. Cuando esta opción está habilitada, las herramientas del lado del cliente pueden interactuar con los servicios de datos para realizar tareas como implementar o anular la implementación de modelos para crear destinos y extremos, o para averiguar qué modelos se han implementado en extremos. De forma predeterminada, está opción no está seleccionada.

**Permitir** solicitud RDS no seguraCuando se selecciona esta opción, las solicitudes RDS no necesitan utilizar https. De forma predeterminada, esta opción no está seleccionada y todas las comunicaciones a los servicios de datos deben ser solicitudes https.

**Permitir la carga de documentos no seguros desde aplicaciones de Flex:** El servlet de carga de archivos utilizado para cargar documentos desde aplicaciones de Flex® de Adobe a formularios AEM requiere que los usuarios se autentiquen y autoricen antes de poder cargar documentos. Se debe asignar al usuario la función de usuario de la aplicación de carga de Documento u otra función que incluya el permiso de carga de Documento. Esto ayuda a evitar que usuarios no autorizados carguen documentos en el servidor de formularios AEM. Seleccione esta opción si desea deshabilitar esta función de seguridad en un entorno de desarrollo o para la compatibilidad con versiones anteriores de AEM formularios. De forma predeterminada, está opción no está seleccionada. Para obtener más información, consulte &quot;Invocación de formularios AEM mediante AEM reenvío de formularios&quot; en Programación con formularios AEM.

**Permitir carga de documento no segura desde aplicaciones de SDK de Java:las cargas de DocumentManager** HTTP deben estar seguras. De forma predeterminada, las cargas HTTP requieren que los usuarios estén autenticados y autorizados para poder cargar documentos. Se debe asignar al usuario la función de usuario de servicios u otra función que contenga el permiso Invocar servicio. Esto ayuda a evitar que usuarios no autorizados carguen documentos en el servidor de formularios. Seleccione esta opción si desea deshabilitar esta función de seguridad en un entorno de desarrollo, para la compatibilidad con versiones anteriores de AEM formularios o en función de la configuración del cortafuegos. De forma predeterminada, está opción no está seleccionada. Para obtener más información, consulte &quot;Invocación de formularios AEM con la API de Java&quot; en Programación con formularios AEM.
