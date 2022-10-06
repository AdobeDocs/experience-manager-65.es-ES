---
title: Directorio global de almacenamiento de documentos
seo-title: Global document storage directory
description: El directorio global de almacenamiento de documentos (GDS) es un directorio utilizado para almacenar archivos de larga duración que se utilizan dentro de un proceso.
seo-description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# Directorio global de almacenamiento de documentos{#global-document-storage-directory}

La variable *almacenamiento global de documentos (GDS)* es un directorio utilizado para almacenar archivos de larga duración que se utilizan en un proceso. Estos archivos incluyen PDF, políticas y plantillas de formulario. Los archivos de larga duración son una parte fundamental del estado general de muchas implementaciones de formularios AEM. Si se pierden o dañan algunos o todos los documentos de larga duración, el servidor de formularios puede volverse inestable. Los documentos de entrada para invocaciones asincrónicas de trabajos también se almacenan en el directorio GDS y deben estar disponibles para procesar solicitudes. Es importante que considere la fiabilidad del sistema de archivos que aloja el directorio GDS. Utilice una matriz redundante de discos independientes (RAID) u otra tecnología adecuada para sus necesidades de calidad y nivel de servicio.

Los archivos de larga duración pueden contener información confidencial del usuario. Esta información puede requerir credenciales especiales cuando se accede a ella mediante las API de formularios AEM o interfaces de usuario. Es importante que el directorio GDS esté correctamente protegido mediante el sistema operativo. Solo la cuenta de administrador que se utiliza para ejecutar el servidor de aplicaciones debe tener acceso de lectura y escritura al directorio GDS.

Además de seleccionar un directorio seguro y altamente disponible para GDS, también puede elegir habilitar el almacenamiento de documentos en la base de datos. Observe que, incluso con el uso de la base de datos de formularios AEM para el almacenamiento de documentos, AEM formularios aún requieren el directorio GDS. (Consulte [Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM datos de la aplicación de formularios se encuentran en el directorio GDS y en la base de datos de AEM forms. En la tabla siguiente se describen los datos y sus ubicaciones.

<table>
 <thead>
  <tr>
   <th><p>Datos de formularios AEM</p></th>
   <th><p>Base de datos</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Datos de aplicación (usuarios, funciones, procesos, políticas, extremos, eventos, etc.)</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Contenedores de servicio implementados</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Administrador de documentos </p></td>
   <td><p>No</p></td>
   <td><p>Sí</p></td>
  </tr>
  <tr>
   <td><p>Repositorio de Forms</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Configuración del sistema</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Carpetas vigiladas</p></td>
   <td><p>No</p></td>
   <td><p>Sí</p></td>
  </tr>
 </tbody>
</table>

## Configuración del directorio GDS {#configuring-the-gds-directory}

La ubicación del directorio GDS se puede configurar manualmente durante el proceso de instalación de los formularios AEM. Si la configuración de ubicación permanece vacía durante la instalación, la ubicación predeterminada es un directorio en la instalación del servidor de aplicaciones de la siguiente manera:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Cambiar la ubicación predeterminada de GDS {#change-the-default-gds-location}

Puede cambiar la ubicación de GDS en la consola de administración una vez completada la instalación de los formularios AEM. Debe reubicar manualmente los datos para completar el proceso.

>[!NOTE]
>
>Migrar los datos de la siguiente manera o se producirá la pérdida de datos.

1. Inicie sesión en la consola de administración y haga clic en Configuración > Configuración del sistema principal > Configuraciones.
1. En el cuadro Directorio global de almacenamiento de documentos, introduzca la ruta completa al nuevo directorio GDS y, a continuación, haga clic en Aceptar.
1. Cierre inmediatamente el servidor de aplicaciones.
1. Mueva todos los archivos del antiguo directorio GDS a la nueva ubicación, manteniendo la estructura de directorio interna.
1. Reinicie el servidor de aplicaciones.

## Acerca de los archivos de implementación {#about-deployment-files}

AEM formularios consta de dos tipos de archivos de implementación, los contenedores de servicio y los archivos EAR de Java 2 Platform, Enterprise Edition (J2EE). Los archivos EAR constan de paquetes de aplicaciones J2EE estándar que contienen la funcionalidad básica de AEM formularios. Los archivos EAR específicos del servidor de aplicaciones son los siguientes:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[Sistema operativo]*.ear

La implementación de AEM formularios implica la implementación de los archivos EAR ensamblados y los archivos auxiliares en el servidor de aplicaciones donde planee ejecutar la solución de formularios AEM. Si ha configurado y montado varios módulos, los módulos implementables se empaquetan dentro de los archivos EAR implementables. Para implementar estos archivos, cópielos en la *[inicio de appserver]*\server\all\deploy directory.

Los módulos y AEM archivos de archivo de formularios están empaquetados en archivos JAR. Como no son archivos de tipo J2EE, no se implementan en el servidor de aplicaciones. En su lugar, se copian en el directorio GDS y se almacena una referencia a su ubicación en la base de datos de formularios AEM. Por este motivo, el directorio GDS debe compartirse entre todos los nodos del clúster. Todos los nodos deben tener acceso al directorio de almacenamiento central de los DSC.

>[!NOTE]
>
>Antes de implementar los contenedores de servicio, asegúrese de que ha creado y configurado el directorio GDS. (Consulte [Configuración del directorio GDS](global-document-storage-directory.md#configuring-the-gds-directory))
