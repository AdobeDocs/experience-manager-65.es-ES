---
title: Creación y configuración de funciones
seo-title: Creating and configuring roles
description: Obtenga información sobre cómo asociar usuarios y grupos con funciones que ya forman parte de la base de datos de Administración de usuarios. También puede crear, editar y eliminar funciones.
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---

# Creación y configuración de funciones{#creating-and-configuring-roles}

Mediante las páginas web de Administración de usuarios, puede asociar usuarios y grupos con funciones que ya forman parte de la base de datos de Administración de usuarios. También puede crear, editar y eliminar funciones.

La Administración de usuarios tiene dos tipos de funciones:

**Funciones mutables:** Este tipo de rol se puede editar y eliminar, y los permisos de rol se pueden agregar y eliminar de estos tipos de rol. Cualquier función que cree se considerará una función mutable. Puede agregar o eliminar usuarios y grupos asignados a funciones mutables.

**Funciones inmutables:** Las funciones predeterminadas que se incluyen con Administración de usuarios son funciones inmutables. Estas funciones no se pueden editar ni eliminar. Sin embargo, puede agregar o eliminar usuarios y grupos asignados a funciones inmutables.

También se pueden crear funciones mutables e inmutables a través de las API de AEM forms.

## Funciones predeterminadas {#default-roles}

Las siguientes funciones predeterminadas se incluyen en la base de datos de Administración de usuarios.

**usuario de la consola de administración:** Puede acceder a la consola de administración.

**Administrador de aplicaciones:** Puede utilizar todas las funciones de Workbench. Puede utilizar las páginas Aplicaciones y Servicios de la consola de administración para configurar las propiedades, los extremos y la seguridad en tiempo de ejecución del servicio.

**AEM administrador de formularios:** Puede realizar todas las tareas para todos los servicios instalados.

**Administrador de seguridad:** Controla la configuración de Administración de usuarios y administra usuarios y grupos asociados a cualquier dominio de Administrador de usuarios

**Usuario de servicios:** Puede ver e invocar cualquier servicio

**Superadministrador:** Tiene acceso a toda la funcionalidad administrativa del sistema, incluidos los servicios

**Administrador de confianza:** Puede administrar la configuración de confianza de PKI y las credenciales de PKI que se administran desde la página Administración de almacén de confianza en la consola de administración

### Funciones predeterminadas adicionales {#additional-default-roles}

Se pueden incluir las siguientes funciones predeterminadas adicionales, según los componentes de formularios AEM que haya instalado

**Usuario de aplicación de carga de documento:** Puede cargar documentos mediante Flex Remoting.

**Administrador de Forms:** Puede ver y modificar la configuración desde la página de Forms en la Consola de administración

**Administrador de Contentspace de AEM formularios:** Puede ver y modificar la configuración desde la página Servicios de contenido (obsoleto) de la consola de administración

**Usuario de Contentspace de AEM formularios:** Pueden iniciar sesión en las páginas web de Contentspace (obsoleto)

**Administrador de Documentum Connector:** Puede ver y modificar la configuración desde la página Connector for EMC Documentum en la consola de administración

**Administrador del conector de FileNet de formularios AEM:** Puede ver y modificar la configuración desde la página Connector for IBM FileNet en la consola de administración

**Administrador del conector de IBM CM de formularios AEM:** Puede ver y modificar la configuración desde la página Administrador de contenido del conector para IBM en la consola de administración

**Rights Management Administrador:** Realiza todas las tareas necesarias para todas las configuraciones del servidor en las páginas del Rights Management correspondiente

**Usuario final Rights Management:** Pueden acceder a las páginas web del usuario final del Rights Management

**Rights Management Invitar usuario:** Puede invitar a usuarios

**Rights Management Administrar usuarios invitados y locales:** Puede realizar tareas necesarias para administrar todos los usuarios invitados y locales en las páginas de Rights Management relevantes

**Administrador del conjunto de directivas del Rights Management:** Realiza todas las tareas necesarias para todos los conjuntos de directivas en las páginas del Rights Management correspondiente

**Rights Management Super Administrator:** Realiza todas las tareas necesarias desde la página Rights Management

**AEM administrador de Workspace de formularios:** Puede ver y modificar la configuración desde la página de Workspace de la Consola de administración

***nota **: Flex Workspace está en desuso para AEM versión de formularios.*

**Usuario de Workspace:** Puede iniciar sesión en la aplicación de usuario final de Workspace

**Administrador de salida:** Puede ver y modificar la configuración desde la página Salida de la Consola de administración

**Administrador de PDFG:** Puede ver y modificar la configuración desde la página Generador de PDF en la consola de administración

**Usuario PDFG:** Puede acceder a todas las funciones no administrativas del Generador de PDF

**Aplicación web de extensiones de Acrobat Reader DC:** Puede utilizar la aplicación web de extensiones de Acrobat Reader DC

>[!NOTE]
>
>Los usuarios con ciertos tipos de privilegios de administrador no pueden acceder a las páginas web del usuario final del espacio de trabajo por motivos de seguridad. Dado que estas páginas pueden existir fuera de un cortafuegos, permitir tareas de nivel de administración podría suponer un riesgo para la seguridad. Solo los usuarios que tengan los privilegios de administrador de Workspace de formularios AEM o AEM de usuario de Workspace pueden acceder a las páginas web del usuario final de Workspace.

>[!NOTE]
>
>Flex Workspace está en desuso para AEM versión de formularios.

## Crear una función {#create-a-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nueva función.
1. En el cuadro Nombre de función, escriba un nombre para la función y, opcionalmente, escriba una descripción de la función y, a continuación, haga clic en Siguiente.

   >[!NOTE]
   >
   >Al utilizar MySQL, no se pueden crear dos funciones que tengan el mismo nombre pero que difieran en el uso de caracteres extendidos. Por ejemplo, intentar crear una función llamada abcde cuando ya existe una llamada âbcdè provoca un error.

1. Haga clic en Buscar permisos y seleccione los permisos que desea agregar a la función.
1. Haga clic en Aceptar y, a continuación, en Siguiente.
1. Asigne esta función a usuarios y grupos:

   * Haga clic en Buscar usuarios/grupos.
   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * Seleccione Nombre, Correo electrónico o ID de usuario y, a continuación, seleccione Usuarios, Grupos o Usuarios y grupos.
   * Seleccione el dominio, seleccione el número de resultados que desea mostrar y haga clic en Buscar.
   * Seleccione las casillas de verificación de los usuarios y grupos a los que asignar esta función y haga clic en Aceptar.

1. Para ver los detalles del usuario y del grupo, seleccione la entidad.
1. Haga clic en Aceptar y, a continuación, en Finalizar.

## Editar una función {#edit-a-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos de Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de rol específico.

1. Haga clic en la función que desea editar, edite la configuración general y haga clic en Guardar.
1. Para editar los permisos de funciones, haga clic en la ficha Permisos y haga lo siguiente:

   * Para agregar nuevos permisos, haga clic en Buscar permisos, seleccione las casillas de verificación de los permisos que desee agregar, haga clic en Aceptar y, después, haga clic en Guardar.
   * Para eliminar un permiso de la función, active la casilla de verificación del permiso, haga clic en Eliminar y, a continuación, haga clic en Guardar.

1. Para administrar a quién se asigna la función, haga clic en la ficha Usuarios de rol y realice estas tareas:

   * Para asignar la función a nuevos usuarios y grupos, haga clic en Buscar usuarios/grupos y complete la información de búsqueda. Seleccione la casilla de verificación de cada usuario y grupo al que asignar esta función, haga clic en Aceptar y, a continuación, haga clic en Guardar.
   * Para quitar la función, seleccione la casilla de verificación de los usuarios o grupos, haga clic en No asignar y, a continuación, haga clic en Guardar.

## Eliminar una función {#delete-a-role}

Puede eliminar cualquiera de las funciones que ha creado, pero no las funciones AEM formularios predeterminadas incluidas en el producto.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos de Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de rol específico.

1. Seleccione la casilla de verificación de la función que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Asignar una función a usuarios y grupos {#assign-a-role-to-users-and-groups}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Especifique la información para limitar la búsqueda y haga clic en Buscar. Los resultados de la búsqueda se enumeran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Seleccione las casillas de verificación situadas junto a los usuarios y grupos a los que desea asociar una función y haga clic en Asignar función.
1. Seleccione la función que desea asignar al usuario o grupo y haga clic en Aceptar.

También puede asignar funciones mediante la página Administración de funciones .

## Determinar quién está asignado a una función {#determine-who-is-assigned-to-a-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos de Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de rol específico.

1. En la página Detalle de funciones, haga clic en la ficha Usuarios de funciones . Se muestra una lista de usuarios y grupos que están directamente asociados a la función.

## Cambiar permisos de funciones {#change-role-permissions}

Puede cambiar los permisos para cualquiera de las funciones que ha creado. No puede cambiar los permisos para las funciones de formularios AEM predeterminados que se incluyen en el producto.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos de Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de rol específico.

1. Seleccione la función para la que desea ver los permisos y haga clic en la pestaña Permisos .
1. Para cambiar estos permisos, haga clic en Buscar permisos, seleccione las casillas de verificación de los permisos que desea agregar a la función, haga clic en Aceptar y, después, en Guardar.
1. Para eliminar un permiso, selecciónelo, haga clic en Eliminar y, a continuación, haga clic en Guardar.

### AEM permisos de formularios {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Agregar, quitar y modificar puntos finales de un servicio

**Inicio de sesión del Admin Console:** Ver la consola de administración

**Modificación de certificado:** Modificar la configuración de confianza de cualquier certificado del almacén de confianza

**Lectura del certificado:** Lea cualquier certificado del almacén de confianza

**Escritura de certificado:** Agregar un certificado al almacén de confianza

**Agregar componente:** Instalar un componente nuevo en el sistema

**Eliminación de componentes:** Eliminar cualquier componente del sistema

**Lectura de componente:** Leer cualquier componente del sistema

**Administrador de Contentspace:** Permiso para administrador de Contentspace (obsoleto)

**Inicio de sesión en la consola de Contentspace:** Permiso para el inicio de sesión en la consola de Contentspace (obsoleto)

**Control de configuración principal:** Administrar la configuración en la página Configuración del sistema principal de la Consola de administración

**CREATE_VERSION_PERM:** Crear una nueva versión de un servicio

**Modificación de Credencial:** Modificar cualquier credencial de firma en el almacén de confianza

**Credencial Lectura:** Leer cualquier credencial de firma en el almacén de confianza

**Escritura Credencial:** Agregar una credencial de firma al almacén de confianza

**Modificación de CRL:** Modificar cualquier CRL (lista de revocación de certificados) en el almacén de confianza

**Lectura de CRL:** Lea cualquier CRL en el almacén de confianza

**Escritura CRL:** Agregar una CRL al almacén de confianza

**Delegado:** Establecer una ACL en un recurso

**DELETE_VERSION_PERM:** Eliminar una versión de un servicio

**Carga de documento:** Cargar documentos en formularios AEM

**Control de dominio:** Crear, eliminar o modificar la configuración de cualquier dominio de Administración de usuarios, incluidos los proveedores de autenticación y directorios

**Editar tipo de evento:** Editar a tipos de eventos

**Control de suplantación de identidad:** Suplantar identidad en el Administrador de usuarios

**INVOKE_PERM:** Invocar todas las operaciones en un servicio

**Control del modelo de datos LCDS:** Leer e implementar modelos de datos en los servicios de datos

**Actualización del Administrador de licencias:** Actualización de la información de licencia

**MODIFY_CONFIG_PERM:** Modificación de la configuración de un servicio

**TÉRMINO** Modificación de la versión de un servicio

**PDFGAdminPermission:** Administrador de PDFG

**PDFGUserPermiso:** Usuario PDFG

**PERM_DCTM_ADMIN:** Administrador de Documentum Connector

**PERM_FILENET_ADMIN:** Administrador del conector FileNet

**PERM_FORMS_ADMIN:** Administrador de Forms

**PERM_IBMCM_ADMIN:** Administrador del conector IBM CM

**PERM_OUTPUT_ADMIN:** Administrador de salida

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Uso de la aplicación web de extensiones de Acrobat Reader DC

**PERM_SP_ADMIN:** Administrar la configuración del conector de SharePoint

**PERM_WORKSPACE_ADMIN:** Administrar configuración de Workspace

**PERM_WORKSPACE_USER:** Inicio de sesión en la aplicación de usuario final de Workspace

**Control principal:** Administrar usuarios y grupos para cualquier dominio y asignar funciones para todos los usuarios y grupos de cualquier dominio

**Proceso de grabación Lectura/Eliminación:** Enumerar y recuperar instancias de auditoría de flujo de trabajo

**PROCESS_OWNER_PERM:** Ver datos de tendencia y realizar acciones administrativas en un servicio creado a partir de un proceso

**Lea:** Leer el contenido de un recurso

**READ_PERM:** Leer o ver un servicio

**Renovar afirmación:** Renovar aserciones en Administración de usuarios

**Delegado de repositorio:** Establecer una ACL en un recurso

**Lectura del repositorio:** Leer el contenido de un recurso

**Transversal del repositorio:** Incluir un recurso en una solicitud de recursos de lista o leer los metadatos de un recurso

**Escritura del repositorio:** Escribir metadatos y contenido del repositorio

**Propietario de la directiva de cambio de Rights Management:** Cambiar propietario de directiva

**Inicio de sesión en la consola de usuario final del Rights Management:** Inicio de sesión en la interfaz de usuario del usuario final del Rights Management

**Configuración de administración del Rights Management:** Administrar configuración del servidor

**Rights Management Administrar usuarios invitados y locales:** Administrar usuarios invitados y locales

**Rights Management Administrar conjuntos de directivas:** Administrar todas las políticas y documentos dentro de cualquier conjunto de directivas

**Rights Management Conjunto de directivas Agregar Coordinador:** Agregar, quitar y cambiar permisos para los coordinadores de conjuntos de directivas

**Conjunto de directivas de Rights Management Crear directiva:** Crear una directiva nueva para un conjunto de directivas

**Política de eliminación del conjunto de directivas del Rights Management:** Eliminar una directiva de un conjunto de directivas

**Política de edición del conjunto de directivas del Rights Management:** Editar una directiva en un conjunto de directivas

**Conjunto de directivas del Rights Management Administrar el Editor de documentos:** Al crear conjuntos de directivas, se asigna a los usuarios la función de publicador de documentos. El editor del documento es el usuario que protege el documento con una directiva.

**Coordinador para quitar conjunto de directivas del Rights Management:** Quitar un coordinador de conjunto de directivas de un conjunto de directivas

**Conjunto de directivas del Rights Management Revocar documento:** Revocar el acceso a los documentos de un conjunto de directivas

**Política de Rights Management - Configurar directiva de conmutador:** Cambiar directivas de un documento

**Documento sin revocar de conjunto de directivas del Rights Management:** Anular la revocación de un documento

**Evento de vista de conjunto de directivas del Rights Management:** Ver eventos de directivas y documentos para cualquier directiva o documento dentro de un conjunto de directivas

**Eventos del servidor de vista del Rights Management:** Buscar y ver todos los eventos de auditoría

**Control de funciones:** Crear, eliminar y modificar funciones en Administración de usuarios

**Activación del servicio:** Iniciar cualquier servicio, poniéndolo a disposición de la invocación

**Adición de servicio:** Implemente un nuevo servicio en el registro de servicios. Esto incluye agregar nuevos procesos y variantes de proceso

**Desactivación de servicio:** Detenga cualquier servicio en el sistema

**Eliminación de servicio:** Eliminar cualquier servicio del sistema, incluidos los procesos y las variantes de proceso

**Invocación de servicio:** Invocar cualquier servicio en el Registro de servicios disponible durante la ejecución

**Modificación del servicio:** Modifique las propiedades de configuración de cualquier servicio del sistema. Esto incluye bloquear y desbloquear un servicio en el IDE, y agregar o eliminar puntos finales de un servicio

**Lectura del servicio:** Lea los servicios del sistema. Esto incluye todos los procesos y variantes de proceso

**SERVICE_AGENT_PERM:** Ver datos e interactuar con instancias de proceso para un servicio creado a partir de un proceso

**SERVICE_MANAGER_PERM:** Realizar balanceo de carga y otras acciones administrativas en un servicio creado a partir de un proceso

**START_STOP_PERM:** Inicio o parada de un servicio

**SUPERVISOR_PERM:** Ver datos de instancias de proceso para un servicio creado a partir de un proceso

**Reverso:** Incluir un recurso en una solicitud de recursos de lista o leer los metadatos de un recurso

**Escribir:** Escribir metadatos y contenido del repositorio

**Apertura de archivos en Workbench**

Para ver el contenido de la vista Recursos en Workbench y abrir archivos para visualizarlos, un usuario necesita los siguientes permisos:

* Lectura del repositorio
* Transversal del repositorio
* Invocación de servicio
* Lectura del servicio

## Eliminación de un usuario o grupo de una función {#remove-a-user-or-group-from-a-role}

Utilice la página Administración de funciones para eliminar usuarios y grupos de una función en particular. Si el usuario o grupo heredó la asignación de funciones, no puede quitar la función a nivel de usuario o grupo. Elimine el usuario o grupo del árbol de herencia o elimine la función del elemento principal.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos de Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de rol específico.

1. En la lista de funciones, haga clic en el nombre de la función que desea actualizar y, a continuación, haga clic en la ficha Usuarios de funciones . Se muestra una lista de usuarios y grupos asociados con la función .
1. Seleccione las casillas de verificación de los usuarios y grupos que desea quitar de la función y haga clic en No asignar.
1. Haga clic en Guardar y, a continuación, en Aceptar.
