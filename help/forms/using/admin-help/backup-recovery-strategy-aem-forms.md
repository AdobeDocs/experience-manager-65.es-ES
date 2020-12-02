---
title: Estrategia de backup y recuperación para formularios AEM
seo-title: Estrategia de backup y recuperación para formularios AEM
description: Obtenga información sobre cómo implementar una estrategia para realizar copias de seguridad de los datos y asegurarse de que se mantengan sincronizados con los datos de los formularios AEM.
seo-description: Obtenga información sobre cómo implementar una estrategia para realizar copias de seguridad de los datos y asegurarse de que se mantengan sincronizados con los datos de los formularios AEM.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---


# Estrategia de backup y recuperación para formularios AEM{#backup-and-recovery-strategy-for-aem-forms}

Si la implementación de formularios AEM almacena datos personalizados adicionales en una base de datos diferente, usted es el responsable de implementar una estrategia para realizar una copia de seguridad de estos datos y asegurarse de que se mantengan sincronizados con los datos de formularios AEM. Además, la aplicación debe diseñarse de modo que sea lo suficientemente robusta como para gestionar un escenario en el que las bases de datos adicionales no estén sincronizadas. Se recomienda encarecidamente que cualquier operación de base de datos que se realice se realice en el contexto de una transacción para ayudar a mantener un estado coherente.

Después de identificar cómo se utilizan los formularios AEM, determine qué archivos se deben realizar copias de seguridad, con qué frecuencia y la ventana de copia de seguridad que se va a poner a disposición.

>[!NOTE]
>
>Al igual que con cualquier otro aspecto de la implementación de formularios AEM, la estrategia de copia de seguridad y recuperación debe desarrollarse y probarse en un entorno de desarrollo o ensayo antes de utilizarse en producción para garantizar que toda la solución funcione según lo esperado sin pérdida de datos.

Adobe Experience Manager (AEM) es una parte integral de AEM formularios. Por lo tanto, es necesario realizar copias de seguridad de AEM también sincronizadas con AEM copia de seguridad de formularios como solución y servicios de gestión de correspondencia, como el administrador de formularios, se basan en datos almacenados en AEM parte de AEM formularios.Para evitar cualquier pérdida de datos, se debe realizar una copia de seguridad de los datos específicos de los formularios AEM de forma que GDS y AEM (repositorio) se correlacionen con las referencias de base de datos.Los directorios raíz de base de datos, GDS, AEM, y Almacenamiento y contenido y deben restaurarse en un equipo con el mismo nombre DNS como el original.

## Tipos de backups {#types-of-backups}

La estrategia de copia de seguridad de formularios AEM incluye dos tipos de copias de seguridad:

**Imagen del sistema:** Una copia de seguridad completa del sistema que puede utilizar para restaurar el contenido del equipo si el disco duro o todo el equipo deja de funcionar. Sólo es necesario realizar una copia de seguridad de la imagen del sistema antes de la implementación de producción de AEM formularios. Las políticas corporativas internas dictan la frecuencia con la que se requieren los backups de imágenes del sistema.

**AEM datos específicos de formularios:los datos** de la aplicación existen en la base de datos, el Almacenamiento de Documento global (GDS) y AEM repositorio, y se debe realizar una copia de seguridad en tiempo real. GDS es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan en un proceso. Estos archivos pueden incluir archivos PDF, políticas o plantillas de formulario.

>[!NOTE]
>
>Si está instalado Content Services (obsoleto), también realice una copia de seguridad del directorio raíz de Content Almacenamiento. Consulte [Directorio raíz de Almacenamiento de contenido (sólo servicios de contenido)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

La base de datos se utiliza para almacenar artefactos de formulario, configuraciones de servicio, estado de proceso y referencias de base de datos a archivos GDS. Si ha activado el almacenamiento de documentos en la base de datos, los datos y documentos persistentes en el GDS también se almacenan en la base de datos. La base de datos se puede hacer backup y recuperar mediante los siguientes métodos:

* **El** modo de copia de seguridad de instantáneas indica que el sistema de formularios AEM está en modo de copia de seguridad indefinidamente o durante un número especificado de minutos, tras los cuales ya no se habilita el modo de copia de seguridad. Para entrar o salir del modo de copia de seguridad instantánea, puede utilizar una de las siguientes opciones. Después de un escenario de recuperación, el modo de copia de seguridad instantánea no debe estar habilitado.

   * Utilice la página Configuración de copia de seguridad de la Consola de administración. Para acceder al modo de instantánea, seleccione la casilla de verificación Operar en modo de copia de seguridad segura. Anule la selección de la casilla de verificación para salir del modo de instantánea.
   * Utilice la secuencia de comandos LCBackupMode (consulte [Copia de seguridad de los directorios raíz de la base de datos, GDS y Almacenamiento de contenido](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Para salir del modo de copia de seguridad de instantáneas, en el argumento script, establezca el parámetro `continuousCoverage` en `false` o utilice la opción `leaveContinuousCoverage`.
   * Utilice la API de copia de seguridad y recuperación proporcionada. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **El** modo de copia de seguridad móvil indica que el sistema siempre está en modo de copia de seguridad, con una nueva sesión de modo de copia de seguridad que se inicia en cuanto se libera la sesión anterior. No hay tiempo de espera asociado con el modo de copia de seguridad móvil. Cuando se llama a la secuencia de comandos o las API de LCBackupMode para que dejen el modo de copia de seguridad móvil, se inicia una nueva sesión del modo de copia de seguridad móvil. Este modo es útil para admitir copias de seguridad continuas, pero aún así permite limpiar documentos antiguos e innecesarios del directorio GDS. El modo de copia de seguridad móvil no se admite a través de la página Backup and Recovery. Después de un escenario de recuperación, el modo de copia de seguridad móvil aún está habilitado. Puede dejar el modo de copia de seguridad continua (modo de copia de seguridad móvil) utilizando la secuencia de comandos LCBackupMode con la opción `leaveContinuousCoverage`.

>[!NOTE]
>
>Si se deja el modo de copia de seguridad móvil inmediatamente, se inicia una nueva sesión de modo de copia de seguridad. Para deshabilitar completamente el modo de copia de seguridad móvil, utilice la opción `leaveContinuousCoverage` en la secuencia de comandos, que sobrescribe la sesión de copia de seguridad móvil existente. En el modo de copia de seguridad instantánea, puede salir del modo de copia de seguridad como suele hacer.

Para evitar la pérdida de datos, se debe realizar una copia de seguridad de los datos específicos de los formularios AEM de forma que los documentos de directorio raíz de GDS y Almacenamiento de contenido se correlacionen con las referencias de base de datos.

>[!NOTE]
>
>Cuando el GDS se almacena en el sistema de archivos y no en la base de datos, realice la copia de seguridad de la base de datos antes de la copia de seguridad del GDS.

## Consideraciones especiales para backup y recuperación {#special-considerations-for-backup-and-recovery}

Utilice las siguientes directrices si debe recuperar AEM formularios en otro entorno debido a los siguientes cambios:

* Cambio en la dirección IP, el nombre de host o el puerto del servidor de formularios AEM
* Cambio en las letras de la unidad o en la ruta del directorio
* Cambiar a un host, puerto o nombre de base de datos diferente

Normalmente, estos escenarios de recuperación se deben a un error de hardware del servidor que aloja el servidor de aplicaciones, el servidor de bases de datos o el servidor de formularios. Además de las configuraciones específicas de formularios AEM que se describen en esta sección, también debe realizar los cambios necesarios para otras partes de la implementación de formularios AEM, como equilibradores de carga y servidores de seguridad, si cambia el nombre de host o la dirección IP de un servidor de formularios AEM.

### Qué no se puede cambiar {#what-cannot-be-changed}

Aunque puede cambiar el servidor de la base de datos y muchos otros parámetros, no puede cambiar el tipo de servidor de aplicaciones o el tipo de base de datos al recuperar AEM formularios de una copia de seguridad. Por ejemplo, si está recuperando una copia de seguridad de formularios AEM, no puede cambiar el servidor de aplicaciones de JBoss a WebLogic o base de datos de Oracle a DB2. Además, los formularios AEM recuperados deben utilizar las mismas rutas del sistema de archivos, como el directorio de fuentes.

### Reinicio después de una recuperación {#restarting-after-a-recovery}

Antes de reiniciar el servidor de formularios después de una recuperación, haga lo siguiente:

1. Inicio el sistema en modo de mantenimiento.
1. Para asegurarse de que el Administrador de formularios se sincroniza con AEM formularios en el modo de mantenimiento, haga lo siguiente:

   1. Vaya a https://&lt;*server*>:&lt;*port*>/lc/fm e inicie sesión con credenciales de administrador/contraseña.
   1. Haga clic en el nombre del usuario (Super Administrator en este caso) en la esquina superior derecha.
   1. Haga clic en **Opciones de administración**.
   1. Haga clic en **Inicio** para sincronizar los recursos del repositorio.

1. En un entorno agrupado, el nodo principal (con respecto a AEM) debe estar arriba antes que los nodos secundarios.
1. Asegúrese de que no se inicien procesos desde fuentes internas o externas como los iniciadores de procesos Web, SOAP o EJB hasta que se valide el funcionamiento normal del sistema.

Si la base de datos de formularios AEM principal se mueve o cambia, revise las guías de instalación relevantes para el servidor de aplicaciones para obtener información sobre la actualización de la información de conexión de base de datos para los orígenes de datos de formularios AEM IDP_DS y EDC_DS.

### Cambio del nombre de host o la dirección IP de los formularios AEM {#changing-the-aem-forms-hostname-or-ip-address}

En un clúster, si utiliza el almacenamiento en caché TCP en lugar de UDP, debe actualizar la configuración del localizador de caché. Consulte &quot;Configuración de los localizadores de almacenamiento en caché (solo en caché mediante TCP)&quot; en la guía de configuración relevante para el servidor de aplicaciones.

### Cambio de las rutas del sistema de archivos del nodo de formularios AEM {#changing-the-aem-forms-node-file-system-paths}

Si cambia las rutas del sistema de archivos para un nodo independiente, debe actualizar las referencias adecuadas en las preferencias, otras configuraciones del sistema, aplicaciones personalizadas y aplicaciones de formularios AEM implementadas. Por otro lado, para un clúster, todos los nodos deben utilizar la misma configuración de ruta del sistema de archivos. Debe configurar el directorio raíz del Almacenamiento de Documento global (GDS) y asegurarse de que señala a una copia del GDS recuperado que está sincronizada con la base de datos recuperada. La configuración de la ruta de GDS es importante porque el GDS puede contener datos que se pretenden que persistan en los reinicios del servidor de aplicaciones.

En un entorno agrupado, la configuración de la ruta del sistema de archivos del repositorio debe ser la misma para todos los nodos del clúster antes de la copia de seguridad y después de la recuperación.

Utilice la secuencia de comandos `LCSetGDS`de la carpeta `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` para establecer la ruta de GDS después de cambiar las rutas del sistema de archivos. Consulte el archivo `ReadMe.txt` en la misma carpeta para obtener más información. Si no se puede utilizar la ruta de acceso del directorio GDS anterior, se debe utilizar la secuencia de comandos `LCSetGDS` para establecer la nueva ruta de acceso al GDS antes de inicio AEM formularios.

>[!NOTE]
>
>Esta circunstancia es la única en la que debe utilizar esta secuencia de comandos para cambiar la ubicación del GDS. Para cambiar la ubicación de GDS mientras se ejecutan AEM formularios, utilice la Consola de administración. (Consulte [Configuración general de AEM formularios](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

Después de definir la ruta GDS, inicio el servidor de formularios en modo de mantenimiento y utilice la consola de administración para actualizar las rutas restantes del sistema de archivos para el nuevo nodo. Después de comprobar que se han actualizado todas las configuraciones necesarias, reinicie y pruebe AEM formularios.
