---
title: Configuración general de AEM Forms
description: Aprenda a configurar las opciones de la página Configuraciones principales en la consola de administración para mejorar el rendimiento del sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 3%

---

# Configuración general de AEM Forms {#general-aem-forms-settings}

La página Configuraciones principales de la consola de administración proporciona opciones que pueden ayudar a mejorar el rendimiento del sistema. Después de configurar o actualizar esta configuración, reinicie el servidor de aplicaciones.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

Para obtener información acerca de cómo habilitar el modo de copia de seguridad segura, vea [Habilitar y deshabilitar el modo de copia de seguridad segura](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>Los archivos del directorio temporal y los documentos de larga duración del directorio raíz del almacenamiento global de documentos (GDS) pueden contener información confidencial del usuario, como la información que requiere credenciales especiales cuando se accede a ella mediante las API o las interfaces de usuario. Por lo tanto, es importante que este directorio esté protegido correctamente mediante los métodos disponibles para el sistema operativo. Se recomienda que sólo la cuenta del sistema operativo utilizada para ejecutar el servidor de aplicaciones tenga acceso de lectura y escritura a este directorio.


1. En la consola de administración, seleccione **[!UICONTROL Configuración > Configuración del sistema principal > Configuraciones]**.
1. En la página Configuraciones principales, cambie las opciones según sea necesario y seleccione **[!UICONTROL Aceptar]**. Para obtener más información sobre las opciones, consulte [Opciones de configuración principales](configure-general-aem-forms-settings.md#core-configurations-options).


## Opciones de configuraciones principales {#core-configurations-options}

AEM **Ubicación del directorio temporal** Ruta de acceso al directorio en el que los formularios de la aplicación crearán los archivos temporales del producto. Si el valor de esta configuración está vacío, la ubicación predeterminada es el directorio temporal del sistema. Asegúrese de que el directorio temporal sea una carpeta en la que se pueda escribir.

>[!NOTE]
>
>Asegúrese de que el directorio temporal se encuentra en el sistema de archivos local. AEM Los formularios no son compatibles con un directorio temporal en una ubicación remota.

**Directorio raíz del almacenamiento global de documentos** *ndash; El directorio raíz del almacenamiento global de documentos (GDS) se usa para los siguientes propósitos:

* Almacenamiento de documentos de larga duración. Los documentos de larga duración no tienen una fecha de caducidad y se conservan hasta que se eliminan (por ejemplo, los archivos de PDF utilizados en un proceso de flujo de trabajo). Los documentos de larga duración son una parte crítica del estado general del sistema. Si se pierden o dañan algunos o todos estos documentos, el servidor de Forms puede volverse inestable. Por lo tanto, es importante que este directorio se almacene en un dispositivo RAID.
* Almacenar los documentos temporales necesarios durante el procesamiento.

>[!NOTE]
>
>AEM También puede habilitar el almacenamiento de documentos en la base de datos de formularios de la. Sin embargo, el rendimiento del sistema es mejor cuando se utiliza el GDS.

* Transferir documentos entre nodos de un clúster. AEM Si está ejecutando formularios en un entorno agrupado, se debe poder acceder a este directorio desde todos los nodos del clúster.
* Recibir parámetros entrantes de llamadas a API remotas.

Si no especifica un directorio raíz de GDS, el directorio predeterminado será un directorio de servidor de aplicaciones:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>El cambio del valor del directorio raíz de GDS debe realizarse con especial cuidado. AEM El directorio GDS se utiliza para almacenar tanto los archivos de larga duración utilizados dentro de un proceso como los componentes de producto de formularios críticos. Cambiar la ubicación del directorio GDS es un cambio importante en el sistema. AEM AEM Si configura incorrectamente la ubicación del directorio del GDS, los formularios de la quedarán inoperantes y podrían requerir una reinstalación completa de los formularios de la. Si especifica una nueva ubicación para el directorio GDS, es necesario cerrar el servidor de aplicaciones y migrar los datos antes de reiniciar el servidor. El administrador del sistema debe mover todos los archivos de la ubicación antigua a la nueva ubicación, pero mantener la estructura de directorios interna.

>[!NOTE]
>
>No especifique el mismo directorio para el directorio temporal y el directorio GDS.

AEM Para obtener información adicional sobre el directorio GDS, consulte [Preparación para instalar formularios de la aplicación (un solo servidor)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Ubicación del directorio de fuentes del servidor de Adobe** *ndash; Escriba la ruta de acceso al directorio que contiene las fuentes del servidor de Adobe. AEM Estas fuentes se instalan con los formularios de. La ubicación predeterminada para estas fuentes es el directorio [aem-forms root]/fonts. Si no puede acceder a este directorio, puede copiar las fuentes en otra parte y utilizar esta configuración para especificar la nueva ubicación.

**Ubicación del directorio de fuentes del cliente** *ndash; Escriba la ruta de acceso a un directorio que contenga fuentes adicionales que desee utilizar.

***nota **: las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. AEM Después de especificar el directorio de fuentes del cliente, asegúrese de reiniciar el sistema en el que está instalado el formulario de la aplicación de datos de usuario ().*

**Ubicación del directorio de fuentes del sistema** *ndash; Escriba la ruta al directorio de fuentes proporcionado por el sistema operativo. Se pueden agregar varios directorios separados por punto y coma **;**.

**Ubicación del archivo de configuración de los servicios de datos** *ndash; Especifica la ubicación del archivo services-config.xml. De forma predeterminada, este archivo está incrustado en el archivo adobe-core-appserver.ear y no es accesible para el usuario. Hay una copia del archivo predeterminado services-config.xml en [raíz de aem-forms]\sdk\misc\DataServices\Server-Configuration. Si cambió este archivo y lo movió, escriba la nueva ubicación en este campo.

El archivo de configuración de los servicios de datos permite personalizar la configuración de los servicios de datos, como el tipo de autenticación y el resultado de depuración.

Esta configuración está vacía de forma predeterminada.

AEM **Tamaño máximo en línea del documento predeterminado (bytes)** *ndash; El número máximo de bytes guardados en la memoria al pasar documentos entre varios componentes de formularios en forma de. Utilice esta configuración para ajustar el rendimiento. Los documentos menores que este número se almacenan en la memoria y se conservan en la base de datos. Los documentos que exceden este máximo se almacenan en el disco duro.

Esta configuración es obligatoria. El valor predeterminado es 65536 bytes.

AEM **Tiempo de espera predeterminado para la eliminación de documentos (segundos)** *ndash; La cantidad máxima de tiempo, en segundos, durante el cual se considera activo un documento que se pasa entre varios componentes de formularios de la. Transcurrido este tiempo, los archivos que se utilicen para almacenar este documento estarán sujetos a eliminación. Utilice esta opción para controlar el uso del espacio en disco.

Esta configuración es obligatoria. El valor predeterminado es 600 segundos.

**Intervalo de barrido de documentos (segundos)** *ndash; Cantidad de tiempo, en segundos, entre intentos de eliminar archivos que ya no son necesarios y que se utilizaron para pasar datos de documentos entre servicios.

Esta configuración es obligatoria. El valor predeterminado es 30 segundos.

**Habilitar FIPS** *ndash; seleccione esta opción para habilitar el modo FIPS. El Estándar Federal de Procesamiento de Información (FIPS) 140-2 es un estándar de criptología definido por el gobierno de Estados Unidos. AEM Cuando se ejecuta en modo FIPS, los formularios de restringen la protección de datos a los algoritmos aprobados por FIPS 140-2 mediante el módulo de cifrado RSA BSAFE Crypto-C 2.1.

El modo FIPS no admite algoritmos de cifrado utilizados en versiones de Adobe Acrobat® anteriores a la 7.0. Si el modo FIPS está habilitado y utiliza el servicio Encryption para cifrar el PDF mediante una contraseña con un nivel de compatibilidad establecido en Acrobat 5, el intento de cifrado fallará y producirá un error.

En general, cuando FIPS está habilitado, el servicio Assembler no aplicará el cifrado de contraseña a ningún documento. Si se intenta, se produce una excepción FIPSModeException indicando que &quot;No se permite el cifrado de contraseña en el modo FIPS&quot;. Además, el elemento PDFsFromBookmarks XML de descripción de documento (DDX) no se admite en el modo FIPS cuando el documento base está cifrado con contraseña.

>[!NOTE]
>
>AEM El software de formularios no valida el código para garantizar la compatibilidad con FIPS. Proporciona un modo de operación FIPS para que se utilicen algoritmos aprobados por FIPS para los servicios criptográficos de las bibliotecas aprobadas por FIPS (RSA).

AEM **Habilitar WSDL** *ndash; seleccione esta opción para habilitar la generación del lenguaje de definición de servicios web (WSDL) para todos los servicios que forman parte de los formularios.

Habilite esta opción en entornos de desarrollo, donde los desarrolladores utilizan la generación de WSDL para generar sus aplicaciones cliente. Puede optar por deshabilitar la generación de WSDL en un entorno de producción para evitar exponer los detalles internos de un servicio.

AEM **Habilitar el almacenamiento de documentos en la base de datos** *ndash; seleccione esta opción para almacenar documentos de larga duración en la base de datos de formularios de la. Al habilitar esta opción, no se elimina la necesidad de un directorio GDS. AEM Sin embargo, al elegir esta opción, se simplifican las copias de seguridad de formularios de. AEM Si solo utiliza el GDS, una copia de seguridad implica poner el sistema de formularios de AEM Forms en modo de copia de seguridad y, a continuación, completar las copias de seguridad de la base de datos y del GDS. Si selecciona la opción de base de datos, la copia de seguridad implica completar la copia de seguridad de la base de datos para una nueva instalación o completar la copia de seguridad de la base de datos y la copia de seguridad única del GDS para una actualización. Es posible que se requiera una administración adicional de la base de datos para purgar trabajos y datos en comparación con una configuración de solo GDS. (Consulte Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos).

AEM **Habilitar la estadística de invocación de DSC** *ndash; Cuando se selecciona esta opción, los formularios de formularios de datos de invocación de formularios de datos de seguimiento, como el número de invocaciones, la cantidad de tiempo que se tarda en invocar y el número de errores en invocaciones de formularios de datos. Esta información se almacena en un bean JMX para que pueda utilizar Java™ JConsole o software de terceros para ver las estadísticas. AEM Si no desea ver estas estadísticas, anule la selección de esta opción para mejorar el rendimiento de los formularios de la.

AEM **Habilitar RDS** *ndash; si se selecciona esta opción, se habilita el servlet de Servicios de desarrollo remoto (RDS) en los formularios de la lista de permitidos. Cuando esta opción está habilitada, las herramientas del lado del cliente pueden interactuar con los servicios de datos para hacer cosas como implementar o anular la implementación de modelos para crear destinos y extremos, o para averiguar qué modelos se han implementado en extremos. Esta opción no está seleccionada de forma predeterminada.

**Permitir solicitud de RDS no segura** *ndash; cuando se selecciona esta opción, las solicitudes de RDS no necesitan usar https. De forma predeterminada, esta opción no está seleccionada y todas las comunicaciones con los servicios de datos deben ser solicitudes https.

**Permitir la carga de documentos no seguros desde aplicaciones de Flex** *ndash; El servlet de carga de archivos utilizado para cargar documentos desde aplicaciones de Flex® AEM de Adobe a formularios de requiere que los usuarios estén autenticados y autorizados para poder cargar documentos. Se debe asignar al usuario la función de usuario de la aplicación de carga de documentos u otra función que incluya el permiso de carga de documentos. Esto ayuda a evitar que usuarios no autorizados carguen documentos en el servidor de AEM Forms. AEM Seleccione esta opción si desea deshabilitar esta característica de seguridad en un entorno de desarrollo o para mantener la compatibilidad con versiones anteriores de los formularios de la aplicación de seguridad de la aplicación de seguridad de la aplicación de seguridad de la aplicación. Esta opción no está seleccionada de forma predeterminada. AEM AEM AEM Para obtener más información, consulte &quot;Invocación de formularios de mediante la comunicación remota de formularios de la aplicación&quot; en Programación con formularios de la aplicación de la llamada a la comunicación remota de formularios de la.

**Permitir la carga de documentos no seguros desde aplicaciones de SDK de Java** *ndash; las cargas de HTTP Document Manager deben ser seguras. De forma predeterminada, las cargas HTTP requieren que los usuarios estén autenticados y autorizados para poder cargar documentos. Se debe asignar al usuario la función Usuario de servicios u otra función que contenga el permiso Invocar servicio. Esto ayuda a evitar que usuarios no autorizados carguen documentos en el servidor de Forms. AEM Seleccione esta opción si desea deshabilitar esta característica de seguridad en un entorno de desarrollo, por compatibilidad con versiones anteriores de formularios de la aplicación o en función de la configuración del cortafuegos. Esta opción no está seleccionada de forma predeterminada. AEM AEM Para obtener más información, consulte &quot;Invocación de formularios en la aplicación de la API de Java&quot; en Programación con formularios en la aplicación de la API de.
