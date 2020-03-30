---
title: Directorio de almacenamientos de documento global
seo-title: Directorio de almacenamientos de documento global
description: El directorio global de almacenamiento de documento (GDS) es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan en un proceso.
seo-description: El directorio global de almacenamiento de documento (GDS) es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan en un proceso.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Directorio de almacenamientos de documento global{#global-document-storage-directory}

El directorio *global de almacenamiento de documento (GDS)* es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan en un proceso. Estos archivos incluyen archivos PDF, políticas y plantillas de formulario. Los archivos de larga duración son una parte fundamental del estado general de muchas implementaciones de formularios AEM. Si se pierden o dañan algunos o todos los documentos de larga duración, el servidor de formularios puede volverse inestable. Los documentos de entrada para invocaciones de trabajos asincrónicas también se almacenan en el directorio GDS y deben estar disponibles para procesar solicitudes. Es importante que considere la fiabilidad del sistema de archivos que aloja el directorio GDS. Utilice una matriz redundante de discos independientes (RAID) u otra tecnología según sus necesidades de calidad y nivel de servicio.

Los archivos de larga duración pueden contener información confidencial del usuario. Esta información puede requerir credenciales especiales cuando se accede a ella mediante las API de formularios AEM o las interfaces de usuario. Es importante que el directorio GDS esté correctamente asegurado a través del sistema operativo. Solo la cuenta de administrador que se utiliza para ejecutar el servidor de aplicaciones debe tener acceso de lectura y escritura al directorio GDS.

Además de seleccionar un directorio seguro y de alta disponibilidad para GDS, también puede activar el almacenamiento de documento en la base de datos. Tenga en cuenta que, incluso con el uso de la base de datos de formularios AEM para documento almacenamiento, los formularios AEM siguen requiriendo el directorio GDS. (Consulte Opciones [de copia de seguridad cuando se utiliza la base de datos para el almacenamiento](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)de documento).

Los datos de la aplicación de formularios AEM residen en el directorio GDS y en la base de datos de formularios AEM. En la tabla siguiente se describen los datos y sus ubicaciones.

<table>
 <thead>
  <tr>
   <th><p>Datos de formularios de AEM</p></th>
   <th><p>Base de datos</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Datos de la aplicación (usuarios, funciones, procesos, políticas, extremos, eventos, etc.)</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>contenedores de servicio implementados</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Administrador de Documentos </p></td>
   <td><p>No</p></td>
   <td><p>Sí</p></td>
  </tr>
  <tr>
   <td><p>Repositorio de formularios</p></td>
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

La ubicación del directorio GDS se puede configurar manualmente durante el proceso de instalación de formularios AEM. Si la configuración de ubicación permanece vacía durante la instalación, la ubicación predeterminada es un directorio en la instalación del servidor de aplicaciones, como se indica a continuación:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Cambiar la ubicación GDS predeterminada {#change-the-default-gds-location}

Puede cambiar la ubicación de GDS en la consola de administración una vez que se haya completado la instalación de formularios AEM. Debe reubicar manualmente los datos para completar el proceso.

>[!NOTE]
>
>Migrar los datos de la siguiente manera o se producirá la pérdida de datos.

1. Inicie sesión en la consola de administración y haga clic en Configuración > Configuración del sistema principal > Configuraciones.
1. En el cuadro Directorio de Almacenamientos de Documento global, introduzca la ruta completa al nuevo directorio GDS y, a continuación, haga clic en Aceptar.
1. Cierre inmediatamente el servidor de aplicaciones.
1. Mueva todos los archivos desde el directorio GDS anterior a la nueva ubicación, manteniendo la estructura de directorios interna.
1. Reinicie el servidor de aplicaciones.

## Acerca de los archivos de implementación {#about-deployment-files}

Los formularios AEM constan de dos tipos de archivos de implementación: los contenedores de servicio y los archivos EAR de Java 2 Platform, Enterprise Edition (J2EE). Los archivos EAR constan de paquetes de aplicaciones J2EE estándar que contienen la funcionalidad básica de los formularios AEM. Los archivos EAR específicos del servidor de aplicaciones son los siguientes:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

La implementación de formularios AEM implica la implementación de los archivos EAR ensamblados y de los archivos de soporte en el servidor de aplicaciones donde se planea ejecutar la solución de formularios AEM. Si ha configurado y montado varios módulos, los módulos implementables se empaquetan dentro de los archivos EAR implementables. Para implementar estos archivos, cópielos en la página principal de *[appserver]*\server\all\deploy directory.

Los archivos de archivos de módulos y formularios AEM se empaquetan en archivos JAR. Como no son archivos de tipo J2EE, no se implementan en el servidor de aplicaciones. En su lugar, se copian en el directorio GDS y se almacena una referencia a su ubicación en la base de datos de formularios de AEM. Por este motivo, el directorio GDS debe compartirse entre todos los nodos del clúster. Todos los nodos deben tener acceso al directorio de almacenamiento central de los DSC.

>[!NOTE]
>
>Antes de implementar los contenedores de servicio, asegúrese de crear y configurar el directorio GDS. (Consulte [Configuración del directorio](global-document-storage-directory.md#configuring-the-gds-directory)GDS)

