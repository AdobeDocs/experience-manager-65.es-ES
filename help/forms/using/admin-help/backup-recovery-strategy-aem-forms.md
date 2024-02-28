---
title: Estrategia de copia de seguridad y recuperación para AEM Forms
description: AEM Obtenga información sobre cómo implementar una estrategia para realizar copias de seguridad de los datos y asegurarse de que permanecen sincronizados con los datos de los formularios de.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: d195ac80ee59439bab5b1219a2c1f16e93e3d22b
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 0%

---

# Estrategia de copia de seguridad y recuperación para AEM Forms{#backup-and-recovery-strategy-for-aem-forms}

AEM AEM Si la implementación de los formularios de la aplicación de la aplicación almacena datos personalizados adicionales en una base de datos diferente, usted es el responsable de implementar una estrategia para realizar una copia de seguridad de estos datos y asegurarse de que permanecen sincronizados con los datos de los formularios de la. Además, la aplicación debe diseñarse para que sea lo suficientemente sólida como para gestionar un escenario en el que las bases de datos adicionales no estén sincronizadas. Se recomienda encarecidamente que cualquier operación de base de datos que se realice se realice en el contexto de una transacción para mantener un estado coherente.

AEM Después de identificar cómo se utilizan los formularios de la, determine de qué archivos se debe hacer una copia de seguridad, con qué frecuencia y la ventana de copia de seguridad que se debe hacer disponible.

>[!NOTE]
>
>AEM Al igual que con cualquier otro aspecto de la implementación de los formularios de la aplicación, la estrategia de copia de seguridad y recuperación debe desarrollarse y probarse en un entorno de desarrollo o ensayo antes de utilizarse en la producción para garantizar que toda la solución funcione según lo esperado sin perder datos.

Adobe Experience Manager AEM AEM () es una parte integral de los formularios de la. AEM AEM AEM AEM AEM AEM AEM Por lo tanto, también debe realizar una copia de seguridad de los formularios en sincronización con la copia de seguridad de formularios de la misma manera que la solución y los servicios de Administración de correspondencia, como el administrador de formularios, se basan en datos almacenados en parte de los formularios de la.Para evitar la pérdida de datos, se debe realizar una copia de seguridad de los datos específicos de los formularios de forma que se garantice que el GDS y el repositorio (repositorio) se correlacionan con las referencias de la base de datos.Los directorios de la base de datos, el GDS, el GDS y la raíz de almacenamiento de contenido deben restaurarse en un equipo con el mismo nombre DNS que el original.

## Tipos de copias de seguridad {#types-of-backups}

AEM La estrategia de copia de seguridad de formularios incluye dos tipos de copias de seguridad:

**Imagen del sistema:** Una copia de seguridad completa del sistema que puede utilizar para restaurar el contenido del equipo si el disco duro o todo el equipo deja de funcionar. AEM Una copia de seguridad de imagen del sistema solo es necesaria antes de la implementación de producción de los formularios de. Las políticas corporativas internas dictan con qué frecuencia se requieren los backups de imágenes del sistema.

**AEM Datos específicos de los formularios de:** AEM Los datos de la aplicación existen en la base de datos, el almacenamiento global de documentos (GDS) y el repositorio de la, y se debe realizar una copia de seguridad de ellos en tiempo real. GDS es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan dentro de un proceso. Estos archivos pueden incluir PDF, directivas o plantillas de formulario.

>[!NOTE]
>
>Si Content Services (Obsoleto) está instalado, haga también una copia de seguridad del directorio raíz de almacenamiento de contenido. Consulte [Directorio raíz de almacenamiento de contenido (solo servicios de contenido)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

La base de datos se utiliza para almacenar artefactos de formulario, configuraciones de servicio, estados de proceso y referencias de base de datos a archivos GDS. Si ha habilitado el almacenamiento de documentos en la base de datos, los datos persistentes y los documentos del GDS también se almacenan en la base de datos. Se puede realizar una copia de seguridad y recuperar la base de datos utilizando los métodos siguientes:

* **Copia de seguridad de instantáneas** AEM Este modo indica que el sistema de formularios de la está en modo de copia de seguridad indefinidamente o durante un número determinado de minutos, después de lo cual el modo de copia de seguridad ya no estará habilitado. Para entrar o salir del modo de copia de seguridad de instantánea, puede utilizar una de las siguientes opciones. Después de un escenario de recuperación, el modo de copia de seguridad de instantáneas no debe estar habilitado.

   * Utilice la página Valores de Copia de Seguridad de la Consola de Administración. Para entrar en el modo de instantánea, active la casilla de verificación Operar en modo de copia de seguridad segura. Anule la selección de la casilla de verificación para salir del modo de instantánea.
   * Utilice el script LCBackupMode (consulte [Realizar una copia de seguridad de los directorios raíz de la base de datos, GDS y Almacenamiento de contenido](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Para salir del modo de copia de seguridad de instantáneas, en el argumento script, establezca el valor `continuousCoverage` parámetro a `false` o use el `leaveContinuousCoverage` opción.
   * Utilice la API de copia de seguridad/recuperación proporcionada. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **Copia de seguridad** Este modo indica que el sistema está siempre en modo de copia de seguridad, con una nueva sesión de modo de copia de seguridad que se inicia en cuanto se libera la sesión anterior. No hay tiempo de espera asociado al modo de copia de seguridad móvil. Cuando se llama al script LCBackupMode o a las API para dejar el modo de copia de seguridad móvil, se inicia una nueva sesión de modo de copia de seguridad móvil. Este modo es útil para admitir copias de seguridad continuas, pero sigue permitiendo que los documentos antiguos e innecesarios se limpien del directorio GDS. El modo de copia de seguridad móvil no es compatible a través de la página Copia de seguridad y recuperación. Después de un escenario de recuperación, el modo de copia de seguridad móvil sigue habilitado. Puede salir del modo de copia de seguridad continua (modo de copia de seguridad móvil) utilizando el script LCBackupMode con el `leaveContinuousCoverage` opción.

>[!NOTE]
>
>Si se abandona el modo de copia de seguridad móvil inmediatamente, se iniciará una nueva sesión de modo de copia de seguridad. Para desactivar completamente el modo de copia de seguridad móvil, utilice el `leaveContinuousCoverage` en el script, que sobrescribe la sesión de copia de seguridad móvil existente. En el modo de copia de seguridad de instantáneas, puede dejar el modo de copia de seguridad como lo hace habitualmente.

AEM Para evitar la pérdida de datos, se debe realizar una copia de seguridad de los datos específicos de los formularios de forma que se garantice que los documentos del directorio raíz de GDS y de almacenamiento de contenido se correlacionen con las referencias de la base de datos.

>[!NOTE]
>
>Cuando el GDS esté almacenado en el sistema de archivos y no en la base de datos, realice la copia de seguridad de la base de datos antes de la copia de seguridad del GDS.

## Consideraciones especiales para el backup y la recuperación {#special-considerations-for-backup-and-recovery}

AEM Siga estas directrices si debe recuperar formularios en un entorno diferente debido a los siguientes cambios:

* Cambio en la dirección IP, el nombre de host o el puerto del servidor de AEM Forms
* Cambio en las letras de unidad o en la ruta de acceso del directorio
* Cambiar a un host, puerto o nombre de base de datos diferente

Normalmente, estos escenarios de recuperación se deben a un error de hardware del servidor que aloja el servidor de aplicaciones, el servidor de base de datos o el servidor de Forms. AEM AEM Además de las configuraciones específicas de formularios de la aplicación que se describen en esta sección, también debe realizar los cambios necesarios en otras partes de la implementación de formularios de la aplicación, como equilibradores de carga y firewalls, si cambia el nombre de host o la dirección IP de un servidor de AEM Forms.

### Qué no se puede cambiar {#what-cannot-be-changed}

AEM Aunque puede cambiar el servidor de base de datos y muchos otros parámetros, no puede cambiar el tipo de servidor de aplicaciones ni el tipo de base de datos al recuperar formularios de una copia de seguridad. AEM Por ejemplo, si está recuperando una copia de seguridad de formularios de la aplicación, no puede cambiar el servidor de aplicaciones de JBoss a WebLogic o la base de datos de Oracle a DB2. AEM Además, los formularios recuperados deben utilizar las mismas rutas del sistema de archivos, como el directorio de fuentes.

### Reinicio tras una recuperación {#restarting-after-a-recovery}

Antes de reiniciar el servidor de Forms después de una recuperación, haga lo siguiente:

1. Inicie el sistema en modo de mantenimiento.
1. AEM Haga lo siguiente para asegurarse de que el administrador de formularios se sincroniza con los formularios de la en el modo de mantenimiento:

   1. Vaya a https://&lt;*server*>:&lt;*puerto*>/lc/fm e inicie sesión con las credenciales de administrador/contraseña.
   1. Haga clic en el nombre del usuario (en este caso, Super Administrator) en la esquina superior derecha.
   1. Clic **Opciones de administración**.
   1. Clic **Inicio** para sincronizar recursos del repositorio.

1. AEM En un entorno agrupado, el nodo principal (con respecto a los nodos de datos) debe estar activo antes que los nodos secundarios.
1. Asegúrese de que no se inician procesos desde orígenes internos o externos como iniciadores de procesos web, SOAP o EJB hasta que se valide el funcionamiento normal del sistema.

AEM AEM Si se mueve o cambia la base de datos de formularios principal de la, consulte las guías de instalación correspondientes a su servidor de aplicaciones para obtener información sobre cómo actualizar la información de conexión de la base de datos para las fuentes de datos de los formularios IDP_DS y EDC_DS de la forma de datos de la forma de la.

>[!NOTE]
> 
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. AEM AEM El reinicio del SDK de la mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de la.

### AEM Cambiar el nombre de host o la dirección IP de los formularios {#changing-the-aem-forms-hostname-or-ip-address}

En un clúster, si utiliza el almacenamiento en caché TCP en lugar de UDP, debe actualizar la configuración del localizador de caché. Consulte &quot;Configuración de los localizadores de almacenamiento en caché (almacenamiento en caché solo mediante TCP)&quot; en la guía de configuración correspondiente a su servidor de aplicaciones.

### AEM Cambio de las rutas del sistema de archivos del nodo de formularios de forma {#changing-the-aem-forms-node-file-system-paths}

AEM Si cambia las rutas del sistema de archivos de un nodo independiente, debe actualizar las referencias adecuadas en las preferencias, otras configuraciones del sistema, aplicaciones personalizadas y aplicaciones de formularios implementadas en el sistema de archivos de forma independiente. Por otro lado, para un clúster, todos los nodos deben utilizar la misma configuración de ruta del sistema de archivos. Establezca el directorio raíz de Global Document Storage (GDS) y asegúrese de que apunta a una copia del GDS recuperado que está sincronizado con la base de datos recuperada. La configuración de la ruta de GDS es importante porque el GDS puede contener datos que pretenden persistir tras los reinicios del servidor de aplicaciones.

En un entorno agrupado, la configuración de la ruta del sistema de archivos del repositorio debe ser la misma para todos los nodos del clúster antes de la copia de seguridad y después de la recuperación.

Utilice el `LCSetGDS`secuencia de comandos en `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` para establecer la ruta de acceso de GDS después de cambiar las rutas del sistema de archivos. Consulte la `ReadMe.txt` en la misma carpeta para obtener más información. Si no se puede utilizar la ruta de acceso al directorio GDS anterior, `LCSetGDS` AEM debe utilizarse una secuencia de comandos para establecer la nueva ruta en el GDS antes de iniciar los formularios de la.

>[!NOTE]
>
>Esta circunstancia es la única en la que debería usar esta secuencia de comandos para cambiar la ubicación de GDS. AEM Para cambiar la ubicación de GDS mientras se está ejecutando el formulario de GDS, utilice la consola de administración. (Consulte [AEM Configurar opciones generales de formularios](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

Después de establecer la ruta de acceso de GDS, inicie el servidor de Forms en modo de mantenimiento y utilice la consola de administración para actualizar las rutas de acceso restantes del sistema de archivos para el nuevo nodo. AEM Después de comprobar que se han actualizado todas las configuraciones necesarias, reinicie y pruebe los formularios de la aplicación de prueba de la aplicación de prueba de la aplicación de.
