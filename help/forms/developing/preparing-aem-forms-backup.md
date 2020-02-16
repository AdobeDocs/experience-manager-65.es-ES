---
title: Preparación de AEM Forms para la copia de seguridad
seo-title: Preparación de AEM Forms para la copia de seguridad
description: nulo
seo-description: nulo
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Preparación de AEM Forms para la copia de seguridad {#preparing-aem-forms-for-backup}

## Acerca del servicio de backup y restauración {#about-the-backup-and-restore-service}

El servicio de copia de seguridad y restauración permite colocar los formularios AEM en el modo *de* copia de seguridad, lo que permite realizar copias de seguridad en caliente. El servicio de copia de seguridad y restauración no realiza una copia de seguridad de AEM Forms ni restaura el sistema. En su lugar, pone el servidor en un estado para realizar copias de seguridad coherentes y fiables, permitiendo al mismo tiempo que el servidor continúe ejecutándose. Usted es responsable de las acciones para realizar una copia de seguridad del Almacenamiento de documentos global (GDS) y de la base de datos conectada al servidor de formularios. El GDS es un directorio que se utiliza para almacenar los archivos que se utilizan en un proceso duradero.

El modo de copia de seguridad es un estado en el que entra el servidor para que los archivos del GDS no se purguen mientras se realiza un procedimiento de copia de seguridad. En su lugar, los subdirectorios se crean en el directorio GDS para mantener un registro de los archivos que se van a purgar después de que finalice el modo de copia de seguridad guardada. Un archivo está diseñado para sobrevivir a reinicios del sistema y puede abarcar días o incluso años. Estos archivos son una parte crítica del estado general del servidor de formularios y pueden incluir archivos PDF, políticas o plantillas de formulario. Si alguno de estos archivos se pierde o se daña, los procesos del servidor de formularios pueden volverse inestables y se podrían perder datos.

Puede elegir realizar copias de seguridad instantáneas, donde normalmente entrará en el modo de copia de seguridad durante un período y, a continuación, dejará el modo de copia de seguridad después de completar las actividades de copia de seguridad. Es necesario dejar el modo de copia de seguridad para que los archivos se puedan purgar del GDS a fin de garantizar que no crezcan innecesariamente. Puede salir del modo de copia de seguridad explícitamente o esperar a que caduque en una sesión de modo de copia de seguridad.

También puede dejar el servidor en modo de copia de seguridad perpetua, que es típico para estrategias de copia de seguridad para copias de seguridad móviles o cobertura continua del sistema. El modo de copia de seguridad móvil indica que el sistema siempre está en modo de copia de seguridad, con una nueva sesión de modo de copia de seguridad iniciada en cuanto se libera la sesión anterior. Cuando se encuentra en modo de copia de seguridad continua, un archivo se purga después de dos sesiones de modo de copia de seguridad y ya no se hace referencia a él.

Puede utilizar el servicio de copia de seguridad y restauración para agregar aplicaciones existentes o nuevas que cree para realizar copias de seguridad del GDS o de la base de datos conectada al servidor de formularios.

>[!NOTE]
>
>Al igual que con cualquier otro aspecto de la implementación de AEM Forms, la estrategia de copia de seguridad y recuperación debe desarrollarse y probarse en un entorno de desarrollo o ensayo antes de utilizarse en la producción para garantizar que toda la solución funcione según lo esperado sin pérdida de datos.

Puede realizar estas tareas mediante el servicio de copia de seguridad y restauración:

* Introduzca el modo de copia de seguridad.
* Deje el modo de copia de seguridad.

>[!NOTE]
>
>Para obtener más información sobre qué considerar al realizar copias de seguridad de AEM Forms, consulte la ayuda [de](https://www.adobe.com/go/learn_aemforms_admin_63)administración.

>[!NOTE]
>
>Para obtener más información sobre el servicio de copia de seguridad y restauración, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Introducción del modo de copia de seguridad en el servidor de formularios {#entering-backup-mode-on-the-forms-server}

El modo de copia de seguridad permite realizar copias de seguridad en caliente de un servidor de formularios. Al entrar en el modo de copia de seguridad, se especifica la siguiente información en función de los procedimientos de copia de seguridad de la organización:

* Una etiqueta única para identificar la sesión del modo de copia de seguridad que puede resultar útil para los procesos de copia de seguridad.
* Hora a la que se completa el procedimiento de copia de seguridad.
* Un indicador que indica si debe estar en modo de copia de seguridad continua, lo que resulta útil sólo si realiza copias de seguridad móviles.

Antes de escribir aplicaciones para entrar en el modo de copia de seguridad, se recomienda que comprenda los procedimientos de copia de seguridad que se utilizarán después de colocar el servidor de formularios en el modo de copia de seguridad. Para obtener más información sobre qué considerar al realizar copias de seguridad de AEM Forms, consulte la ayuda [de](https://www.adobe.com/go/learn_aemforms_admin_63)administración.

>[!NOTE]
>
>Para obtener más información sobre el servicio de copia de seguridad y restauración, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear una aplicación que entre en el modo de copia de seguridad, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente de BackupService.
1. Determinar una etiqueta única, la cantidad de tiempo para realizar la copia de seguridad y si debe estar en modo de copia de seguridad continua.
1. Introduzca el modo de copia de seguridad.
1. (Opcional) Recupere información sobre la sesión del modo de copia de seguridad en el servidor.
1. Realice la copia de seguridad del GDS (almacén de datos global) y la base de datos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Estos archivos son importantes para incluirlos en el proyecto para compilar el código correctamente y utilizar la API de servicio de copia de seguridad y restauración.

Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Creación de un objeto de API de cliente de BackupService**

Para salir del modo de copia de seguridad mediante programación, cree un objeto cliente de BackupService para utilizar la API de servicio de copia de seguridad y restauración.

**Decida sobre una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si se encuentra en modo de copia de seguridad continua**

Antes de entrar en el modo de copia de seguridad, debe decidir una etiqueta única, determinar la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decidir si desea que el servidor de formularios permanezca en el modo de copia de seguridad. Estas consideraciones son importantes para integrarse con los procedimientos de copia de seguridad establecidos por su organización. (Consulte la ayuda [de](https://www.adobe.com/go/learn_aemforms_admin_63)administración).

**Entrar al modo de copia de seguridad**

Introduzca el modo de copia de seguridad con los parámetros que son coherentes con los procedimientos de copia de seguridad de su organización.

**Recuperar información sobre la sesión de modo de copia de seguridad en el servidor**

Después de entrar en el modo de copia de seguridad, puede recuperar información sobre la sesión. Esta información se puede utilizar para integrarse con los procedimientos de copia de seguridad

**Realizar la copia de seguridad del GDS y la base de datos**

Una vez que haya entrado correctamente en el modo de copia de seguridad, puede realizar una copia de seguridad de Global Document Storage (GDS) y de la base de datos a la que está conectado el servidor de formularios. Este paso es específico de su organización, ya que puede realizar este paso manualmente o puede ejecutar otras herramientas para realizar el procedimiento de copia de seguridad.

### Introduzca el modo de copia de seguridad mediante la API de Java {#enter-backup-mode-using-the-java-api}

Introduzca el modo de copia de seguridad mediante la API de servicio de copia de seguridad y restauración:

1. Incluir archivos de proyecto

   Incluya los archivos JAR de cliente necesarios, como adobe-backup-restore-client-sdk.jar, en la ruta de clases del proyecto Java. Para crear la aplicación cliente Java, se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)
   * jbossall-client.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)

1. Creación de un objeto de API de cliente de BackupService

   Se utiliza un `ServiceClientFactory` objeto y el objeto API de cliente de BackupService juntos.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión. (Consulte [Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
   * Cree un `BackupService` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto.

1. Decida sobre una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si se encuentra en modo de copia de seguridad continua

   Decida sobre una etiqueta única, determine la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decida si desea que el servidor de formularios permanezca en modo de copia de seguridad continua.

1. Entrar al modo de copia de seguridad

   Introduzca el modo de copia de seguridad invocando el `enterBackupMode` método con los parámetros siguientes:

   * Un `String` valor que especifica una etiqueta única legible en lenguaje natural que identifica la sesión de modo de copia de seguridad. Se recomienda no utilizar espacios ni caracteres que no se puedan codificar en formato XML.
   * Un `int` valor que especifica el número de minutos que se deben permanecer en el modo de copia de seguridad. Puede especificar un valor de `1` a `10080` (el número de minutos en una semana). Este valor se ignora cuando se utiliza el modo de copia de seguridad continua.
   * Un `Boolean` valor que especifica si se debe estar en modo de copia de seguridad continua. Un valor de `True` especifica que se encuentra en modo de copia de seguridad continua. Cuando se encuentra en modo de copia de seguridad continua, se ignora el valor que se especifica para el número de minutos que deben permanecer en modo de copia de seguridad.

      El modo de copia de seguridad continua significa que se inicia una nueva sesión de modo de copia de seguridad después de completar la sesión actual. Un valor de `False` significa que no se utiliza el modo de copia de seguridad continua y, después de salir del modo de copia de seguridad, se reanuda la depuración de archivos del GDS.

1. Recuperar información sobre la sesión de modo de copia de seguridad en el servidor

   Recupere información utilizando el `BackupModeEntryResult` objeto que se devuelve después de invocar el `enterBackupMode` método. La información que puede recuperar después de entrar en el modo de copia de seguridad puede resultar útil para la integración con los procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo del procedimiento de copia de seguridad.

1. Realizar la copia de seguridad del GDS y la base de datos

   Haga una copia de seguridad del Almacenamiento de documentos global (GDS) y de la base de datos a la que está conectado el servidor de formularios. Las acciones para realizar la copia de seguridad no forman parte del SDK de AEM Forms e incluso pueden incluir pasos manuales específicos de los procedimientos de copia de seguridad de la organización.

### Introduzca el modo de copia de seguridad mediante la API de servicio Web {#enter-backup-mode-using-the-web-service-api}

Introduzca el modo de copia de seguridad mediante el servicio Web proporcionado por la API de servicio de copia de seguridad y restauración:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de la API de servicio de copia de seguridad y restauración.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Creación de un objeto de API de cliente de BackupService

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `BackupServiceService` objeto invocando su constructor predeterminado y especifique las credenciales mediante el `Credentials` método .

1. Decida sobre una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si se encuentra en modo de copia de seguridad continua

   Decida sobre una etiqueta única, determine la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decida si desea que el servidor de formularios permanezca en modo de copia de seguridad continua.

1. Entrar al modo de copia de seguridad

   Para acceder al modo de copia de seguridad, invoque el método enterBackupMode y pase los valores siguientes:

   * Un `String` valor que especifica una etiqueta única legible en lenguaje natural que identifica la sesión de modo de copia de seguridad. Se recomienda no utilizar espacios ni caracteres que no se puedan codificar en formato XML.
   * Un `Uint32` valor que especifica el número de minutos que deben permanecer en el modo de copia de seguridad. Puede especificar un valor de `1` a `10080` (número de minutos en una semana). Este valor se ignora cuando se utiliza el modo de copia de seguridad continua.
   * Un `Boolean` valor que especifica si se debe estar en modo de copia de seguridad continua. Un valor de `True` especifica que se encuentra en modo de copia de seguridad continua. Cuando se encuentra en modo de copia de seguridad continua, se ignora el valor que se especifica para el número de minutos que deben permanecer en modo de copia de seguridad. El modo de copia de seguridad continua significa que se inicia una nueva sesión de modo de copia de seguridad después de completar la sesión actual.

      Un valor de `False` significa que no se utiliza el modo de copia de seguridad continua y, después de salir del modo de copia de seguridad, se reanuda la depuración de archivos del GDS.

1. Recuperar información sobre la sesión de modo de copia de seguridad en el servidor

   Recupere información sobre la sesión del modo de copia de seguridad después de invocar el método enterBackupMode desde BackupModeEntryResult que se devuelve para verificar que se ha realizado correctamente. La información que puede recuperar después de entrar en el modo de copia de seguridad puede resultar útil para la integración con los procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo del procedimiento de copia de seguridad.

1. Realizar la copia de seguridad del GDS y la base de datos

   Haga una copia de seguridad del Almacenamiento de documentos global (GDS) y de la base de datos a la que está conectado el servidor de formularios. Las acciones para realizar la copia de seguridad no forman parte del SDK de AEM Forms e incluso pueden incluir pasos manuales específicos de los procedimientos de copia de seguridad de la organización.

## Salida del modo de copia de seguridad en el servidor de formularios {#leaving-backup-mode-on-the-forms-server}

El modo de copia de seguridad se deja para que el servidor de formularios reanude la depuración de archivos del GDS (Global Document Storage) en el servidor de formularios.

Antes de escribir aplicaciones para entrar en el modo de salida, se recomienda comprender los procedimientos de copia de seguridad que se utilizan con AEM Forms. Para obtener más información sobre qué considerar al realizar copias de seguridad de AEM Forms, consulte la ayuda [de](https://www.adobe.com/go/learn_aemforms_admin_63)administración.

>[!NOTE]
>
>Para obtener más información sobre el servicio de copia de seguridad y restauración, consulte Referencia de [servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para salir del modo de copia de seguridad, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto de cliente de BackupService.
1. Deje el modo de copia de seguridad.
1. (Opcional) Recupere información sobre la sesión de modo de copia de seguridad que se estaba ejecutando en el servidor de formularios.

**Incluir archivos de proyecto**

Incluya todos los archivos necesarios en el proyecto de desarrollo. Estos archivos son importantes para compilar el código correctamente y utilizar la API de servicio de copia de seguridad y restauración.

Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)de biblioteca Java de AEM Forms.

**Creación de un objeto de API de cliente de BackupService**

Para salir del modo de copia de seguridad mediante programación, cree un objeto cliente de BackupService para utilizar la API de servicio de copia de seguridad y restauración.

**Salir del modo de copia de seguridad**

Deje el modo de copia de seguridad para reanudar la depuración normal de archivos desde Global Document Storage (GDS). Antes de salir del modo de copia de seguridad, debe comprobar que los procedimientos de copia de seguridad se han completado.

**Recuperar información sobre la sesión de modo de copia de seguridad que finalizó**

Después de salir del modo de copia de seguridad, puede recuperar información sobre la sesión. Esta información puede utilizarse para integrarse con los procedimientos de copia de seguridad.

### Salir del modo de copia de seguridad mediante la API de Java {#leave-backup-mode-using-the-java-api}

Deje el modo de copia de seguridad mediante la API de servicio de copia de seguridad y restauración (Java):

1. Incluir archivos de proyecto

   Incluya los archivos JAR de cliente necesarios, como adobe-backup-restore-client-sdk.jar, en la ruta de clases del proyecto Java. Para crear una aplicación cliente Java, se deben agregar los siguientes archivos JAR a la ruta de clases del proyecto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)
   * jbossall-client.jar (obligatorio si AEM Forms se implementa en el servidor de aplicaciones JBoss)

1. Creación de un objeto de API de cliente de BackupService

   Se utiliza un `ServiceClientFactory` objeto y el objeto API de cliente de BackupService juntos.

   * Cree un `ServiceClientFactory` objeto que contenga propiedades de conexión. (Consulte [Configuración de propiedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexión).
   * Cree un `BackupService` objeto utilizando su constructor y pasando el `ServiceClientFactory` objeto como parámetro.

1. Entrar al modo de copia de seguridad

   Deje el modo de copia de seguridad invocando el `leaveBackupMode` método.

1. Recuperar información sobre la sesión de modo de copia de seguridad en el servidor

   Recupere información sobre la operación con el `BackupModeResult` objeto devuelto. La información que puede recuperar después de entrar en el modo de copia de seguridad puede resultar útil para la integración con los procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo del procedimiento de copia de seguridad.

### Abandonar el modo de copia de seguridad mediante la API de servicio Web {#leave-backup-mode-using-the-web-service-api}

Deje el modo de copia de seguridad mediante la API de servicio de copia de seguridad y restauración (servicio Web):

1. Incluir archivos de proyecto

   Para utilizar servicios Web, debe asegurarse de incluir los archivos proxy. Siga estos pasos para configurar el proyecto y utilizar la API de servicio de copia de seguridad y restauración como un servicio Web.

   * Cree un ensamblado de cliente de Microsoft .NET que utilice el WSDL de la API de servicio de copia de seguridad y restauración.
   * Haga referencia al ensamblado de cliente de Microsoft .NET.

1. Creación de un objeto de API de cliente de BackupService

   Mediante el ensamblado de cliente de Microsoft .NET, cree un `BackupServiceService` objeto invocando su constructor predeterminado.

1. Entrar al modo de copia de seguridad

   Deje el modo de copia de seguridad invocando la operación del servicio `leaveBackupMode` Web.

1. Recuperar información sobre la sesión de modo de copia de seguridad en el servidor

   Recupere el identificador del modo de copia de seguridad después de la operación para comprobar que se ha realizado correctamente. La información que puede recuperar después de salir del modo de copia de seguridad puede resultar útil para la integración con los procedimientos de copia de seguridad.

