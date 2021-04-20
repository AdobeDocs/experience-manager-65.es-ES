---
title: Preparación de AEM Forms para copia de seguridad
seo-title: Preparación de AEM Forms para copia de seguridad
description: Aprenda a utilizar el servicio de copia de seguridad y restauración para entrar y salir del modo de copia de seguridad para el servidor de AEM Forms mediante la API de Java y la API del servicio web.
seo-description: Aprenda a utilizar el servicio de copia de seguridad y restauración para entrar y salir del modo de copia de seguridad para el servidor de AEM Forms mediante la API de Java y la API del servicio web.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2555'
ht-degree: 0%

---


# Preparación de AEM Forms para copia de seguridad {#preparing-aem-forms-for-backup}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

## Acerca del Servicio de Copia de Seguridad y Restauración {#about-the-backup-and-restore-service}

El servicio Copia de seguridad y restauración permite colocar AEM Forms en *modo de copia de seguridad*, lo que permite realizar copias de seguridad en caliente. El servicio de copia de seguridad y restauración no realiza una copia de seguridad de AEM Forms ni restaura el sistema. En su lugar, pone el servidor en un estado para realizar backups consistentes y confiables mientras permite que el servidor continúe ejecutándose. Usted es el responsable de las acciones para realizar una copia de seguridad del Almacenamiento global de documentos (GDS) y de la base de datos conectada al servidor de formularios. El GDS es un directorio utilizado para almacenar archivos utilizados en un proceso de larga duración.

El modo de copia de seguridad es un estado que introduce el servidor para que los archivos del GDS no se depuren mientras se produce un procedimiento de copia de seguridad. En su lugar, los subdirectorios se crean en el directorio GDS para mantener un registro de los archivos que se purgarán después de que termine el modo de copia de seguridad. Un archivo está diseñado para sobrevivir a reinicios del sistema y puede abarcar días, o incluso años. Estos archivos son una parte fundamental del estado general del servidor de formularios y pueden incluir archivos PDF, políticas o plantillas de formulario. Si alguno de estos archivos se pierde o se daña, los procesos del servidor de formularios pueden volverse inestables y se podrían perder datos.

Puede elegir realizar copias de seguridad de copias instantáneas, donde normalmente ingresaría al modo de copia de seguridad durante un período y luego salir del modo de copia de seguridad después de completar las actividades de copia de seguridad. Es necesario dejar el modo de copia de seguridad para que los archivos se puedan eliminar del GDS para garantizar que no crezcan innecesariamente grandes. Puede salir del modo de copia de seguridad explícitamente o esperar a que caduque el tiempo en una sesión en modo de copia de seguridad.

También puede dejar el servidor en modo de copia de seguridad perpetua, que es típico de estrategias de copia de seguridad para copias de seguridad móviles o cobertura continua del sistema. El modo de copia de seguridad móvil indica que el sistema siempre está en modo de copia de seguridad, con una nueva sesión de modo de copia de seguridad iniciada en cuanto se libera la sesión anterior. Cuando se encuentra en modo de copia de seguridad continua, un archivo se depura después de dos sesiones en modo de copia de seguridad y ya no se hace referencia a él.

Puede utilizar el servicio Copia de seguridad y restauración para agregar a aplicaciones existentes o nuevas que cree para realizar copias de seguridad del GDS o la base de datos conectada al servidor de formularios.

>[!NOTE]
>
>Al igual que con cualquier otro aspecto de su implementación de AEM Forms, su estrategia de backup y recuperación debe desarrollarse y probarse en un entorno de desarrollo o ensayo antes de utilizarse en producción para garantizar que toda la solución funcione según lo esperado sin pérdida de datos.

Puede realizar estas tareas mediante el servicio Copia de seguridad y restauración:

* Introduzca el modo de copia de seguridad.
* Deje el modo de copia de seguridad.

>[!NOTE]
>
>Para obtener más información sobre qué considerar al realizar copias de seguridad para AEM Forms, consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obtener más información acerca del servicio Copia de seguridad y restauración, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Introducción del modo de copia de seguridad en el servidor de formularios {#entering-backup-mode-on-the-forms-server}

Se introduce el modo de copia de seguridad para permitir copias de seguridad activas de un servidor de formularios. Al entrar al modo de copia de seguridad, debe especificar la siguiente información en función de los procedimientos de copia de seguridad de su organización:

* Una etiqueta única para identificar la sesión del modo de copia de seguridad que puede resultar útil para los procesos de copia de seguridad.
* Tiempo para que se complete el procedimiento de copia de seguridad.
* Un indicador que indica si debe estar en modo de copia de seguridad continua, lo que resulta útil solo si realiza copias de seguridad móviles.

Antes de escribir aplicaciones para entrar en el modo de copia de seguridad, se recomienda que entienda los procedimientos de copia de seguridad que se utilizarán después de colocar el servidor de formularios en modo de copia de seguridad. Para obtener más información sobre qué considerar al realizar copias de seguridad para AEM Forms, consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obtener más información acerca del servicio Copia de seguridad y restauración, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para crear una aplicación que entre en el modo de copia de seguridad, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente BackupService.
1. Determine una etiqueta única, la cantidad de tiempo para realizar la copia de seguridad y si debe estar en modo de copia de seguridad continua.
1. Introduzca el modo de copia de seguridad.
1. (Opcional) Recupere información sobre la sesión del modo de copia de seguridad en el servidor.
1. Realice la copia de seguridad del GDS (almacén de datos global) y la base de datos.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Estos archivos son importantes de incluir en el proyecto para compilar el código correctamente y utilizar la API de servicio de copia de seguridad y restauración.

Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto de API de cliente de BackupService**

Para salir del modo de copia de seguridad mediante programación, se crea un objeto de cliente BackupService para utilizar la API de servicio de copia de seguridad y restauración.

**Decida sobre una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si está en modo de copia de seguridad continua**

Antes de entrar en el modo de copia de seguridad, debe decidir una etiqueta única, determinar la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decidir si desea que el servidor de formularios permanezca en el modo de copia de seguridad. Estas consideraciones son importantes para integrarse con los procedimientos de copia de seguridad establecidos por su organización. (Consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63)).

**Introducir modo de copia de seguridad**

Introduzca el modo de copia de seguridad con los parámetros que son coherentes con los procedimientos de copia de seguridad de su organización.

**Recupere información sobre la sesión del modo de copia de seguridad en el servidor**

Después de entrar en el modo de copia de seguridad, puede recuperar información sobre la sesión. Esta información se puede utilizar para integrar con sus procedimientos de copia de seguridad

**Realizar la copia de seguridad de GDS y la base de datos**

Después de entrar correctamente en el modo de copia de seguridad, puede realizar una copia de seguridad del Almacenamiento global de documentos (GDS) y de la base de datos a la que está conectado el servidor de formularios. Este paso es específico de su organización, ya que puede realizar este paso manualmente o ejecutar otras herramientas para realizar el procedimiento de copia de seguridad.

### Introduzca el modo de copia de seguridad mediante la API de Java {#enter-backup-mode-using-the-java-api}

Introduzca el modo de copia de seguridad utilizando la API de servicio de copia de seguridad y restauración:

1. Incluir archivos de proyecto

   Incluya los archivos JAR del cliente necesarios, como adobe-backup-restore-client-sdk.jar, en la ruta de clase de su proyecto Java. Para crear la aplicación cliente Java, se deben añadir los siguientes archivos JAR a la ruta de clase del proyecto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
   * jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

1. Creación de un objeto de API de cliente de BackupService

   Se utiliza un objeto `ServiceClientFactory` y el objeto de API de cliente de BackupService juntos.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).
   * Cree un objeto `BackupService` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Decida sobre una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si está en modo de copia de seguridad continua

   Decida una etiqueta única, determine la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decida si desea que el servidor de formularios permanezca en modo de copia de seguridad continua.

1. Introducir modo de copia de seguridad

   Introduzca el modo de copia de seguridad invocando el método `enterBackupMode` con los siguientes parámetros:

   * Un valor `String` que especifica una etiqueta única legible en lenguaje natural que identifica la sesión del modo de copia de seguridad. Se recomienda no utilizar espacios o caracteres que no se puedan codificar en formato XML.
   * Un valor `int` que especifica el número de minutos que deben permanecer en el modo de copia de seguridad. Puede especificar un valor de `1` a `10080` (el número de minutos en una semana). Este valor se ignora al utilizar el modo de copia de seguridad continua.
   * Un valor `Boolean` que especifica si debe estar en modo de copia de seguridad continua. Un valor de `True` especifica estar en modo de copia de seguridad continua. Cuando se encuentra en modo de copia de seguridad continua, se ignora el valor que especifique para el número de minutos que deben permanecer en modo de copia de seguridad.

      El modo de copia de seguridad continua significa que se inicia una nueva sesión del modo de copia de seguridad una vez completada la actual. Un valor de `False` significa que no se utiliza el modo de copia de seguridad continua y, después de salir del modo de copia de seguridad, se reanuda la depuración de archivos del GDS.

1. Recupere información sobre la sesión del modo de copia de seguridad en el servidor

   Recupere información utilizando el objeto `BackupModeEntryResult` que se devuelve después de invocar el método `enterBackupMode`. La información que puede recuperar después de entrar en el modo de copia de seguridad puede ser útil para integrarla con los procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo para el procedimiento de copia de seguridad.

1. Realizar la copia de seguridad de GDS y la base de datos

   Haga una copia de seguridad del Almacenamiento global de documentos (GDS) y de la base de datos a la que está conectado el servidor de formularios. Las acciones para realizar la copia de seguridad no forman parte del SDK de AEM Forms e incluso pueden incluir pasos manuales específicos de los procedimientos de copia de seguridad de su organización.

### Introduzca el modo de copia de seguridad mediante la API de servicio web {#enter-backup-mode-using-the-web-service-api}

Introduzca el modo de copia de seguridad utilizando el servicio web proporcionado por la API del servicio de copia de seguridad y restauración:

1. Incluir archivos de proyecto

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de API de servicio de copia de seguridad y restauración.
   * Haga referencia al ensamblado cliente de Microsoft .NET.

1. Creación de un objeto de API de cliente de BackupService

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `BackupServiceService` invocando su constructor predeterminado y especifique las credenciales utilizando el método `Credentials`.

1. Decida sobre una etiqueta única, determine la cantidad de tiempo para realizar la copia de seguridad y decida si está en modo de copia de seguridad continua

   Decida una etiqueta única, determine la cantidad de tiempo que desea asignar para realizar la copia de seguridad y decida si desea que el servidor de formularios permanezca en modo de copia de seguridad continua.

1. Introducir modo de copia de seguridad

   Para entrar al modo de copia de seguridad, invoque el método enterBackupMode y pase los siguientes valores:

   * Un valor `String` que especifica una etiqueta única legible en lenguaje natural que identifica la sesión del modo de copia de seguridad. Se recomienda no utilizar espacios o caracteres que no se puedan codificar en formato XML.
   * Un valor `Uint32` que especifica el número de minutos que deben permanecer en el modo de copia de seguridad. Puede especificar un valor de `1` a `10080` (número de minutos en una semana). Este valor se ignora al utilizar el modo de copia de seguridad continua.
   * Un valor `Boolean` que especifica si debe estar en modo de copia de seguridad continua. Un valor de `True` especifica estar en modo de copia de seguridad continua. Cuando se encuentra en modo de copia de seguridad continua, se ignora el valor que especifique para el número de minutos que deben permanecer en modo de copia de seguridad. El modo de copia de seguridad continua significa que se inicia una nueva sesión del modo de copia de seguridad una vez completada la actual.

      Un valor de `False` significa que no se utiliza el modo de copia de seguridad continua y, después de salir del modo de copia de seguridad, se reanuda la depuración de archivos del GDS.

1. Recupere información sobre la sesión del modo de copia de seguridad en el servidor

   Recupere información sobre la sesión del modo de copia de seguridad después de invocar el método enterBackupMode desde BackupModeEntryResult que se devuelve para verificar que se ha realizado correctamente. La información que puede recuperar después de entrar en el modo de copia de seguridad puede ser útil para integrarla con los procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo para el procedimiento de copia de seguridad.

1. Realizar la copia de seguridad de GDS y la base de datos

   Haga una copia de seguridad del Almacenamiento global de documentos (GDS) y de la base de datos a la que está conectado el servidor de formularios. Las acciones para realizar la copia de seguridad no forman parte del SDK de AEM Forms e incluso pueden incluir pasos manuales específicos de los procedimientos de copia de seguridad de su organización.

## Dejar el modo de copia de seguridad en el servidor de formularios {#leaving-backup-mode-on-the-forms-server}

El modo de copia de seguridad se deja para que el servidor de formularios reanude la depuración de archivos del GDS (almacenamiento de documentos global) en el servidor de formularios.

Antes de escribir aplicaciones para entrar en el modo de baja, se recomienda que entienda los procedimientos de copia de seguridad que se utilizan con AEM Forms. Para obtener más información sobre qué considerar al realizar copias de seguridad para AEM Forms, consulte [ayuda de administración](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Para obtener más información acerca del servicio Copia de seguridad y restauración, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary_of_steps-1}

Para salir del modo de copia de seguridad, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Cree un objeto cliente BackupService.
1. Deje el modo de copia de seguridad.
1. (Opcional) Recupere información sobre la sesión del modo de copia de seguridad que se estaba ejecutando en el servidor de formularios.

**Incluir archivos de proyecto**

Incluya todos los archivos necesarios en el proyecto de desarrollo. Estos archivos son importantes para compilar el código correctamente y utilizar la API de servicio de copia de seguridad y restauración.

Para obtener información sobre la ubicación de estos archivos, consulte [Inclusión de archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creación de un objeto de API de cliente de BackupService**

Para salir del modo de copia de seguridad mediante programación, se crea un objeto de cliente BackupService para utilizar la API de servicio de copia de seguridad y restauración.

**Salir del modo de copia de seguridad**

Deje el modo de copia de seguridad para reanudar la depuración normal de archivos del Almacenamiento global de documentos (GDS). Antes de salir del modo de copia de seguridad, debe verificar que los procedimientos de copia de seguridad se hayan completado.

**Recupere información sobre la sesión del modo de copia de seguridad que ha finalizado.**

Después de salir del modo de copia de seguridad, puede recuperar información sobre la sesión. Esta información se puede utilizar para integrar con sus procedimientos de copia de seguridad.

### Deje el modo de copia de seguridad utilizando la API de Java {#leave-backup-mode-using-the-java-api}

Deje el modo de copia de seguridad utilizando la API de servicio de copia de seguridad y restauración (Java):

1. Incluir archivos de proyecto

   Incluya los archivos JAR del cliente necesarios, como adobe-backup-restore-client-sdk.jar, en la ruta de clase de su proyecto Java. Para crear la aplicación cliente Java, se deben añadir los siguientes archivos JAR a la ruta de clase del proyecto:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-Utilities.jar (obligatorio si AEM Forms está implementado en el servidor de aplicaciones JBoss)
   * jbossall-client.jar (requerido si AEM Forms está implementado en el servidor de aplicaciones JBoss)

1. Creación de un objeto de API de cliente de BackupService

   Se utiliza un objeto `ServiceClientFactory` y el objeto de API de cliente de BackupService juntos.

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión. (Consulte [Configuración de las propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).
   * Cree un objeto `BackupService` utilizando su constructor y pasando el objeto `ServiceClientFactory` como parámetro.

1. Introducir modo de copia de seguridad

   Deje el modo de copia de seguridad invocando el método `leaveBackupMode`.

1. Recupere información sobre la sesión del modo de copia de seguridad en el servidor

   Recupere información sobre la operación utilizando el objeto `BackupModeResult` que se devuelve. La información que puede recuperar después de entrar en el modo de copia de seguridad puede ser útil para integrarla con los procedimientos de copia de seguridad. Por ejemplo, la etiqueta, el ID de copia de seguridad y la hora de inicio pueden ser útiles como entrada para los nombres de archivo para el procedimiento de copia de seguridad.

### Deje el modo de copia de seguridad utilizando la API de servicio web {#leave-backup-mode-using-the-web-service-api}

Deje el modo de copia de seguridad utilizando la API del servicio de copia de seguridad y restauración (servicio web):

1. Incluir archivos de proyecto

   Para utilizar servicios web, debe asegurarse de incluir los archivos proxy. Siga estos pasos para configurar el proyecto y utilizar la API de servicio de copia de seguridad y restauración como servicio web.

   * Cree un ensamblado de cliente de Microsoft .NET que consuma el WSDL de API de servicio de copia de seguridad y restauración.
   * Haga referencia al ensamblado cliente de Microsoft .NET.

1. Creación de un objeto de API de cliente de BackupService

   Mediante el ensamblado de cliente de Microsoft .NET, cree un objeto `BackupServiceService` invocando su constructor predeterminado.

1. Introducir modo de copia de seguridad

   Deje el modo de copia de seguridad invocando la operación `leaveBackupMode` del servicio web.

1. Recupere información sobre la sesión del modo de copia de seguridad en el servidor

   Recupere el identificador del modo de copia de seguridad después de la operación para verificar que se ha realizado correctamente. La información que puede recuperar después de salir del modo de copia de seguridad puede ser útil para la integración con sus procedimientos de copia de seguridad.

