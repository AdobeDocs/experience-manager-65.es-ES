---
title: Estrategia de backup y recuperación para formularios AEM
seo-title: Backup and recovery strategy for AEM forms
description: Aprenda a implementar una estrategia para realizar copias de seguridad de los datos y garantizar que se mantengan sincronizados con los datos de los formularios AEM.
seo-description: Learn how to implement a strategy to back up data and ensuring that it remains in sync with the AEM forms data.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 0%

---

# Estrategia de backup y recuperación para formularios AEM{#backup-and-recovery-strategy-for-aem-forms}

Si la implementación de AEM forms almacena datos personalizados adicionales en una base de datos diferente, usted es el responsable de implementar una estrategia para realizar una copia de seguridad de estos datos y garantizar que se mantengan sincronizados con los datos de AEM forms. Además, la aplicación debe diseñarse para que sea lo suficientemente robusta como para gestionar un escenario en el que las bases de datos adicionales no estén sincronizadas. Es muy recomendable que cualquier operación de base de datos que se realice se realice en el contexto de una transacción para ayudar a mantener un estado coherente.

Después de identificar cómo se utilizan AEM formularios, determine qué archivos se deben realizar copias de seguridad, con qué frecuencia y la ventana de copia de seguridad que se va a poner a disposición.

>[!NOTE]
>
>Al igual que con cualquier otro aspecto de la implementación de los formularios AEM, su estrategia de backup y recuperación debe desarrollarse y probarse en un entorno de desarrollo o ensayo antes de utilizarse en producción para garantizar que toda la solución funcione según lo esperado sin pérdida de datos.

Adobe Experience Manager (AEM) es una parte integral de AEM formularios. Por lo tanto, es necesario realizar una copia de seguridad de AEM también en sincronía con AEM copia de seguridad de formularios como Gestión de correspondencia La solución y los servicios, como el administrador de formularios, se basan en datos almacenados en AEM parte de AEM formularios.Para evitar cualquier pérdida de datos, se debe realizar una copia de seguridad de los datos específicos de los formularios AEM de forma que se asegure que GDS y AEM (repositorio) se correlacionen con referencias de base de datos.La base de datos, GDS, AEM,, y y los directorios raíz de almacenamiento de contenido se deben restaurar a un equipo con el mismo nombre DNS el original.

## Tipos de copias de seguridad {#types-of-backups}

La estrategia de copia de seguridad de los formularios AEM incluye dos tipos de copias de seguridad:

**Imagen del sistema:** Una copia de seguridad completa del sistema que puede usar para restaurar el contenido del equipo si el disco duro o todo el equipo deja de funcionar. Sólo es necesario realizar una copia de seguridad de la imagen del sistema antes de la implementación de producción de AEM formularios. Las políticas corporativas internas dictan la frecuencia con la que se requieren backups de imágenes del sistema.

**AEM datos específicos de formularios:** Los datos de las aplicaciones existen en la base de datos, el Almacenamiento de documentos globales (GDS) y AEM repositorio, y se deben realizar backups en tiempo real. GDS es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan en un proceso. Estos archivos pueden incluir PDF, políticas o plantillas de formulario.

>[!NOTE]
>
>Si los servicios de contenido (obsoletos) están instalados, realice una copia de seguridad del directorio raíz del almacenamiento de contenido. Consulte [Directorio raíz del almacenamiento de contenido (solo servicios de contenido)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

La base de datos se utiliza para almacenar artefactos de formulario, configuraciones de servicio, estados de proceso y referencias de base de datos a archivos GDS. Si ha habilitado el almacenamiento de documentos en la base de datos, los datos persistentes y los documentos del GDS también se almacenan en la base de datos. Se puede realizar una copia de seguridad y recuperar la base de datos mediante los métodos siguientes:

* **Copia de seguridad instantánea** indica que el sistema de AEM forms está en modo de copia de seguridad indefinidamente o durante un número determinado de minutos, tras lo cual el modo de copia de seguridad ya no está activado. Para entrar o salir del modo de copia de seguridad instantánea, puede utilizar una de las siguientes opciones. Después de un escenario de recuperación, el modo de copia instantánea de seguridad no debe estar habilitado.

   * Utilice la página Configuración de copia de seguridad en la Consola de administración. Para entrar en el modo de instantánea, seleccione la casilla de verificación Operar en modo de copia de seguridad segura . Desmarque la casilla de verificación para salir del modo de instantánea.
   * Utilice el script LCBackupMode (consulte [Haga una copia de seguridad de los directorios raíz de la base de datos, GDS y almacenamiento de contenido](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Para salir del modo de copia de seguridad de instantánea, en el argumento script, establezca la variable `continuousCoverage` parámetro a `false` o use el `leaveContinuousCoverage` .
   * Utilice la API de copia de seguridad/recuperación suministrada. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **Copia de seguridad móvil** indica que el sistema siempre está en modo de copia de seguridad, con una nueva sesión en modo de copia de seguridad que se inicia en cuanto se libera la sesión anterior. No hay tiempo de espera asociado con el modo de copia de seguridad móvil. Cuando se llama a la secuencia de comandos o API LCBackupMode para abandonar el modo de copia de seguridad móvil, comienza una nueva sesión del modo de copia de seguridad móvil. Este modo es útil para admitir copias de seguridad continuas, pero aún así permite limpiar documentos antiguos e innecesarios del directorio GDS. El modo de copia de seguridad móvil no se admite a través de la página Copia de seguridad y recuperación. Después de un escenario de recuperación, el modo de copia de seguridad móvil sigue habilitado. Puede dejar el modo de copia de seguridad continua (modo de copia de seguridad móvil) utilizando el script LCBackupMode con el `leaveContinuousCoverage` .

>[!NOTE]
>
>Si deja el modo de copia de seguridad móvil inmediatamente, se inicia una nueva sesión del modo de copia de seguridad. Para desactivar completamente el modo de copia de seguridad móvil, utilice el `leaveContinuousCoverage` en la secuencia de comandos, que sobrescribe la sesión de copia de seguridad móvil existente. En el modo de copia de seguridad instantánea, puede salir del modo de copia de seguridad como lo hace normalmente.

Para evitar la pérdida de datos, se debe realizar una copia de seguridad de los datos específicos de los formularios AEM de forma que los documentos de directorio raíz de almacenamiento de contenido y GDS se correlacionen con referencias de base de datos.

>[!NOTE]
>
>Cuando el GDS está almacenado en el sistema de archivos y no en la base de datos, realice la copia de seguridad de la base de datos antes de la copia de seguridad de GDS.

## Consideraciones especiales para backup y recuperación {#special-considerations-for-backup-and-recovery}

Utilice las siguientes directrices si debe recuperar AEM formularios en un entorno diferente debido a los cambios siguientes:

* Cambio en la dirección IP, el nombre de host o el puerto del servidor de AEM forms
* Cambio en las letras de la unidad o en la ruta del directorio
* Cambiar a un host, puerto o nombre de base de datos diferente

Normalmente, estos escenarios de recuperación están causados por un fallo de hardware del servidor que aloja el servidor de aplicaciones, el servidor de bases de datos o el servidor de formularios. Además de las configuraciones específicas de los formularios AEM que se describen en esta sección, también debe realizar los cambios necesarios en otras partes de la implementación de formularios AEM, como equilibradores de carga y cortafuegos, si cambia el nombre de host o la dirección IP de un servidor de formularios AEM.

### Qué no se puede cambiar {#what-cannot-be-changed}

Aunque puede cambiar el servidor de base de datos y muchos otros parámetros, no puede cambiar el tipo de servidor de aplicaciones o tipo de base de datos cuando recupera AEM formularios de una copia de seguridad. Por ejemplo, si está recuperando una copia de seguridad de formularios AEM, no puede cambiar el servidor de aplicaciones de JBoss a WebLogic o base de datos de Oracle a DB2. Además, los formularios AEM recuperados deben utilizar las mismas rutas del sistema de archivos, como el directorio de fuentes.

### Reinicio después de una recuperación {#restarting-after-a-recovery}

Antes de reiniciar el servidor de formularios después de una recuperación, haga lo siguiente:

1. Inicie el sistema en modo de mantenimiento.
1. Haga lo siguiente para asegurarse de que el Administrador de formularios está sincronizado con AEM formularios en el modo de mantenimiento:

   1. Vaya a https://&lt;*server*>:&lt;*puerto*>/lc/fm e inicie sesión con credenciales de administrador/contraseña.
   1. Haga clic en el nombre del usuario (superadministrador en este caso) en la esquina superior derecha.
   1. Haga clic en **Opciones de administración**.
   1. Haga clic en **Inicio** para sincronizar recursos desde el repositorio.

1. En un entorno agrupado, el nodo principal (con respecto a AEM) debe estar arriba antes de los nodos secundarios.
1. Asegúrese de que no se inicien procesos desde fuentes internas o externas como los iniciadores de procesos Web, SOAP o EJB hasta que se valide el funcionamiento normal del sistema.

Si la base de datos de formularios AEM principal se mueve o cambia, revise las guías de instalación correspondientes al servidor de aplicaciones para obtener información sobre la actualización de la información de conexión de base de datos para los orígenes de datos de formularios AEM IDP_DS y EDC_DS.

### Cambio del nombre de host o la dirección IP de los formularios AEM {#changing-the-aem-forms-hostname-or-ip-address}

En un clúster, si utiliza el almacenamiento en caché TCP en lugar de UDP, debe actualizar la configuración del localizador de caché. Consulte &quot;Configuración de los localizadores de almacenamiento en caché (almacenamiento en caché solo mediante TCP)&quot; en la guía de configuración correspondiente a su servidor de aplicaciones.

### Cambio de las rutas del sistema de archivos del nodo de formularios AEM {#changing-the-aem-forms-node-file-system-paths}

Si cambia las rutas del sistema de archivos para un nodo independiente, debe actualizar las referencias adecuadas en las preferencias, otras configuraciones del sistema, aplicaciones personalizadas y aplicaciones de formularios AEM implementadas. Por otro lado, para un clúster, todos los nodos deben utilizar la misma configuración de ruta del sistema de archivos. Debe establecer el directorio raíz de Global Document Storage (GDS) y asegurarse de que señala a una copia del GDS recuperado que está sincronizado con la base de datos recuperada. La configuración de la ruta GDS es importante porque el GDS puede contener datos que pretenden persistir durante los reinicios del servidor de aplicaciones.

En un entorno agrupado, la configuración de la ruta del sistema de archivos del repositorio debe ser la misma para todos los nodos del clúster antes de la copia de seguridad y después de la recuperación.

Utilice la variable `LCSetGDS`en el `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` para establecer la ruta GDS después de cambiar las rutas del sistema de archivos. Consulte la `ReadMe.txt` en la misma carpeta para obtener más información. Si no se puede utilizar la ruta de acceso del directorio GDS anterior, `LCSetGDS` antes de iniciar AEM formularios, debe utilizarse la secuencia de comandos para establecer la nueva ruta al GDS.

>[!NOTE]
>
>Esta circunstancia es la única en la que debe utilizar esta secuencia de comandos para cambiar la ubicación de GDS. Para cambiar la ubicación de GDS mientras se ejecutan AEM formularios, utilice la Consola de administración. (Consulte [Configuración general de AEM formularios](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*) *

Después de establecer la ruta GDS, inicie el servidor de formularios en modo de mantenimiento y utilice la consola de administración para actualizar las rutas restantes del sistema de archivos para el nuevo nodo. Después de comprobar que se han actualizado todas las configuraciones necesarias, reinicie y pruebe AEM formularios.
