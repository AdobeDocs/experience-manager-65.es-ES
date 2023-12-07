---
title: Directorio global de almacenamiento de documentos
description: El directorio de almacenamiento global de documentos (GDS) es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan en un proceso.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---

# Directorio global de almacenamiento de documentos{#global-document-storage-directory}

El *almacenamiento global de documentos (GDS)* El directorio es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan dentro de un proceso. Estos archivos incluyen PDF, directivas y plantillas de formulario. AEM Los archivos de larga duración son una parte esencial del estado general de muchas implementaciones de formularios en la forma de un formulario en el que se puede ejecutar un proceso de trabajo. Si se pierden o dañan algunos o todos los documentos de larga duración, el servidor de Forms puede volverse inestable. Los documentos de entrada para invocaciones de trabajo asincrónicas también se almacenan en el directorio GDS y deben estar disponibles para procesar solicitudes. Es importante tener en cuenta la fiabilidad del sistema de archivos que aloja el directorio GDS. Utilice una cabina redundante de discos independientes (RAID) u otra tecnología adecuada para sus necesidades de calidad y nivel de servicio.

Los archivos de larga duración pueden contener información confidencial del usuario. AEM Esta información puede requerir credenciales especiales cuando se accede a ella mediante las API de formularios o las interfaces de usuario de los formularios de la. Es importante que el directorio GDS esté protegido correctamente a través del sistema operativo. Solo la cuenta de administrador utilizada para ejecutar el servidor de aplicaciones debe tener acceso de lectura y escritura al directorio GDS.

Además de seleccionar un directorio seguro y de alta disponibilidad para GDS, también puede optar por habilitar el almacenamiento de documentos en la base de datos. AEM AEM Tenga en cuenta que incluso con el uso de la base de datos de formularios de para el almacenamiento de documentos, los formularios de GDS aún requieren el directorio GDS. (Consulte [Opciones de copia de seguridad cuando se utiliza la base de datos para el almacenamiento de documentos](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM AEM Los datos de la aplicación de formularios de residen en el directorio GDS y en la base de datos de formularios de la aplicación. En la tabla siguiente se describen los datos y sus ubicaciones.

<table>
 <thead>
  <tr>
   <th><p>AEM Datos de formularios</p></th>
   <th><p>Base de datos</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Datos de aplicación (usuarios, funciones, procesos, directivas, extremos, eventos, etc.)</p></td>
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
   <td><p>Carpetas inspeccionadas</p></td>
   <td><p>No</p></td>
   <td><p>Sí</p></td>
  </tr>
 </tbody>
</table>

## Configuración del directorio GDS {#configuring-the-gds-directory}

AEM La ubicación del directorio GDS se puede configurar manualmente durante el proceso de instalación de los formularios de la. Si la configuración de ubicación permanece vacía durante la instalación, la ubicación predeterminada es un directorio en la instalación del servidor de aplicaciones de la siguiente manera:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Cambiar la ubicación predeterminada de GDS {#change-the-default-gds-location}

AEM Puede cambiar la ubicación de GDS en la consola de administración una vez completada la instalación de los formularios de la. Reubicar manualmente los datos para completar el proceso.

>[!NOTE]
>
>Migre los datos de la siguiente manera o se perderán datos.

1. Inicie sesión en la consola de administración y haga clic en Configuración > Configuración del sistema principal > Configuraciones.
1. En el cuadro Directorio global de almacenamiento de documentos, escriba la ruta de acceso completa al nuevo directorio GDS y, a continuación, haga clic en Aceptar.
1. Cierre inmediatamente el servidor de aplicaciones.
1. Mueva todos los archivos del directorio GDS antiguo a la nueva ubicación, conservando la estructura de directorios interna.
1. Reinicie el servidor de la aplicación.

## Acerca de los archivos de implementación {#about-deployment-files}

AEM Los formularios de datos constan de dos tipos de archivos de implementación, los contenedores de servicio y los archivos EAR de Java 2 Platform, Enterprise Edition (J2EE). AEM Los archivos EAR constan de paquetes de aplicaciones J2EE estándar que contienen la funcionalidad principal de los formularios de la aplicación de la versión de la aplicación de la aplicación de la versión de la aplicación de la versión de la aplicación de la versión de. Los archivos EAR específicos del servidor de aplicaciones son los siguientes:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[SO]*.ear

AEM AEM La implementación de formularios requiere implementar los archivos EAR ensamblados y los archivos auxiliares en el servidor de aplicaciones en el que planea ejecutar la solución de formularios de la aplicación de la manera más sencilla. Si ha configurado y ensamblado varios módulos, los módulos implementables se empaquetan dentro de los archivos EAR implementables. Para implementar estos archivos, cópielos en el *[inicio de appserver]* Directorio \server\all\deploy.

AEM Los módulos y los archivos de archivo de formularios de la aplicación se incluyen en archivos JAR. Como no son archivos de tipo J2EE, no se implementan en el servidor de aplicaciones. AEM En su lugar, se copian en el directorio GDS y se almacena una referencia a su ubicación en la base de datos de formularios de la base de datos de la aplicación de formularios de datos de la biblioteca de formularios de la biblioteca de formularios. Por este motivo, el directorio GDS debe compartirse entre todos los nodos del clúster. Todos los nodos deben tener acceso al directorio de almacenamiento central de los DSC.

>[!NOTE]
>
>Antes de implementar los contenedores de servicio, asegúrese de crear y configurar el directorio GDS. (Consulte [Configuración del directorio GDS](global-document-storage-directory.md#configuring-the-gds-directory))
