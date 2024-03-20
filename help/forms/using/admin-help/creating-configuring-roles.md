---
title: Crear y configurar roles
description: Obtenga información sobre cómo asociar usuarios y grupos con funciones que ya forman parte de la base de datos de administración de usuarios. También puede crear, editar y eliminar roles.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 0%

---

# Crear y configurar roles{#creating-and-configuring-roles}

Mediante las páginas web de Administración de usuarios, puede asociar usuarios y grupos con roles que ya forman parte de la base de datos de Administración de usuarios. También puede crear, editar y eliminar roles.

Administración de usuarios tiene dos tipos de funciones:

**Funciones mutables:** Este tipo de función se puede editar y eliminar, y los permisos de función se pueden agregar y eliminar de estos tipos de funciones. Cualquier función que cree se considerará una función mutable. Puede agregar o quitar usuarios y grupos asignados a funciones mutables.

**Funciones inmutables:** Las funciones predeterminadas que se incluyen con la administración de usuarios son funciones inmutables. Estas funciones no se pueden editar ni eliminar. Sin embargo, puede agregar o quitar usuarios y grupos asignados a funciones inmutables.

AEM Tanto las funciones mutables como las inmutables también se pueden crear mediante las API de formularios de la aplicación de la forma de.

## Funciones predeterminadas {#default-roles}

Las siguientes funciones predeterminadas se incluyen en la base de datos de administración de usuarios.

**usuario de la consola de administración:** Puede acceder a la consola de administración.

**Administrador de aplicaciones:** Puede utilizar todas las funciones de Workbench. Puede utilizar las páginas Aplicaciones y servicios de la consola de administración para configurar las propiedades, los extremos y la seguridad del servicio en tiempo de ejecución.

**AEM Administrador de formularios de:** Puede realizar todas las tareas para todos los servicios instalados.

**Administrador de seguridad:** Controla la configuración de Administración de usuarios y administra los usuarios y grupos asociados a cualquier dominio del Administrador de usuarios

**Usuario de servicios:** Puede ver e invocar cualquier servicio

**Superadministrador:** Tiene acceso a todas las funciones administrativas del sistema, incluidos los servicios

**Administrador de confianza:** Puede administrar la configuración de confianza de PKI y las credenciales de PKI que se administran desde la página Administración del almacén de confianza en la consola de administración

### Funciones predeterminadas adicionales {#additional-default-roles}

AEM Se pueden incluir las siguientes funciones predeterminadas adicionales, en función de los componentes de formularios de la aplicación que haya instalado

**Usuario de aplicación de carga de documento:** Puede cargar documentos mediante Flex Remoting.

**Administrador de Forms:** Puede ver y modificar la configuración desde la página de Forms en la consola de administración

**AEM Administrador de área de contenido de formularios:** Puede ver y modificar la configuración de la página Servicios de contenido (obsoleto) en la consola de administración

**AEM Usuario de ContentSpace de formularios:** Puede iniciar sesión en las páginas web del espacio de contenido (obsoleto)

**Administrador de conectores de Documentum:** Puede ver y modificar la configuración desde la página Connector para Documentum de EMC en la consola de administración

**AEM Administrador del conector FileNet de formularios:** Puede ver y modificar la configuración desde la página Connector for IBM FileNet en la consola de administración

**AEM Administrador del conector de IBM CM de formularios:** Puede ver y modificar la configuración desde la página Conector del administrador de contenido de IBM en la consola de administración

**Rights Management Administrador:** Realiza todas las tareas necesarias para todas las configuraciones de servidor en las páginas relevantes del Rights Management

**Usuario final de Rights Management:** Puede acceder a las páginas web del usuario final Rights Management

**Usuario de invitación de Rights Management:** Puede invitar a usuarios

**Rights Management Administrar usuarios invitados y locales:** Puede realizar las tareas necesarias para administrar todos los usuarios invitados y locales en las páginas relevantes del Rights Management

**Conjunto de directivas de Rights Management Administrador:** Realiza todas las tareas necesarias para todos los conjuntos de directivas en las páginas relevantes del Rights Management

**Rights Management Super Administrator:** Realiza todas las tareas necesarias desde la página del Rights Management

**AEM Administrador de Forms Workspace:** Puede ver y modificar la configuración de la página de Workspace en la consola de administración

***nota **: Flex AEM Workspace está en desuso para la versión de formularios en la que se ha realizado el.*

**Usuario de Workspace:** Puede iniciar sesión en la aplicación para usuarios finales de Workspace

**Administrador de salida:** Puede ver y modificar la configuración desde la página Salida en la consola de administración

**Administrador de PDFG:** Puede ver y modificar la configuración desde la página PDF Generator en la consola de administración

**Usuario de PDFG:** Puede acceder a todas las funciones no administrativas de PDF Generator

**Aplicación web de extensiones de Acrobat Reader DC:** Puede utilizar la aplicación web Acrobat Reader DC extensions

>[!NOTE]
>
>Los usuarios con determinados tipos de privilegios de administrador no pueden acceder a las páginas web de los usuarios finales de Workspace por motivos de seguridad. Dado que estas páginas pueden existir fuera de un cortafuegos, permitir tareas de nivel de administración podría suponer un riesgo para la seguridad. AEM AEM Solo los usuarios que tengan los privilegios de administrador de Forms Workspace o usuario de Forms Workspace de la plantilla de formularios de la aplicación pueden acceder a las páginas web del usuario final de Workspace.

>[!NOTE]
>
>Flex AEM Workspace está en desuso para la versión de formularios en la que se ha realizado un.

## Crear una función {#create-a-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nueva función.
1. En el cuadro Nombre de función, escriba un nombre para la función y, opcionalmente, escriba una descripción de la función y, a continuación, haga clic en Siguiente.

   >[!NOTE]
   >
   >Al utilizar MySQL, no se pueden crear dos funciones que tengan el mismo nombre pero que difieran en el uso de caracteres extendidos. Por ejemplo, si se intenta crear una función denominada abcde cuando ya existe una denominada âbcdè, se producirá un error.

1. Haga clic en Buscar permisos y seleccione los permisos que desea agregar a la función.
1. Haga clic en Aceptar y, a continuación, en Siguiente.
1. Asigne esta función a usuarios y grupos:

   * Haga clic en Buscar usuarios/grupos.
   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * Seleccione Nombre, Correo electrónico o ID de usuario y, a continuación, Usuarios, Grupos o Usuarios y grupos.
   * Seleccione el dominio, seleccione el número de resultados que desea mostrar y haga clic en Buscar.
   * Seleccione las casillas de verificación de los usuarios y grupos a los que desea asignar esta función y haga clic en Aceptar.

1. Para ver los detalles del usuario y del grupo, seleccione la entidad.
1. Haga clic en Aceptar y, a continuación, en Finalizar.

## Editar una función {#edit-a-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. Haga clic en la función que desea editar, edite la configuración general y haga clic en Guardar.
1. Para editar permisos de funciones, haga clic en la pestaña Permisos y realice las siguientes tareas:

   * Para agregar nuevos permisos, haga clic en Buscar permisos, active las casillas de verificación de los permisos que desea agregar, haga clic en Aceptar y, a continuación, haga clic en Guardar.
   * Para eliminar un permiso de la función, active la casilla de verificación del permiso, haga clic en Eliminar y, a continuación, haga clic en Guardar.

1. Para administrar a quién está asignado el rol, haga clic en la ficha Usuarios del rol y realice las tareas siguientes:

   * Para asignar la función a nuevos usuarios y grupos, haga clic en Buscar usuarios/grupos y complete la información de búsqueda. Active la casilla de verificación de cada usuario y grupo al que desee asignar esta función, haga clic en Aceptar y, a continuación, en Guardar.
   * Para quitar la función, active la casilla de verificación de los usuarios o grupos, haga clic en Anular asignación y, a continuación, haga clic en Guardar.

## Eliminar un rol {#delete-a-role}

AEM Puede eliminar cualquiera de las funciones que ha creado, pero no las funciones predeterminadas de los formularios de la aplicación de forma de formulario que se incluyen en el producto.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. Active la casilla de verificación de la función que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Asignar una función a usuarios y grupos {#assign-a-role-to-users-and-groups}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Especifique información para limitar la búsqueda y haga clic en Buscar. Los resultados de la búsqueda se muestran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Seleccione las casillas de verificación situadas junto a los usuarios y grupos que desea asociar a un rol y haga clic en Asignar rol.
1. Seleccione la función que desea asignar al usuario o grupo y haga clic en Aceptar.

También puede asignar funciones mediante la página Administración de funciones.

## Determinar quién está asignado a un rol {#determine-who-is-assigned-to-a-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. En la página Detalles del rol, haga clic en la ficha Usuarios del rol. Se muestra una lista de usuarios y grupos asociados directamente con la función.

## Cambiar permisos de funciones {#change-role-permissions}

Puede cambiar los permisos de cualquiera de las funciones que ha creado. AEM No puede cambiar los permisos de las funciones predeterminadas de los formularios de la que se incluyen en el producto.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. Seleccione la función para la que desea ver los permisos y haga clic en la pestaña Permisos.
1. Para cambiar estos permisos, haga clic en Buscar permisos, active las casillas de verificación de los permisos que desea agregar a la función, haga clic en Aceptar y, a continuación, haga clic en Guardar.
1. Para eliminar un permiso, selecciónelo, haga clic en Eliminar y, a continuación, haga clic en Guardar.

### AEM permisos de formularios de {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Agregar, quitar y modificar extremos de un servicio

**Inicio de sesión de Admin Console:** Ver la consola de administración

**Modificación de certificado:** Modificar la configuración de confianza de cualquier certificado del Almacén de confianza

**Lectura de certificado:** Leer cualquier certificado del almacén de confianza

**Escritura de certificado:** Agregar un certificado al almacén de confianza

**Añadir componente:** Instalar un componente nuevo en el sistema

**Eliminación de componente:** Eliminar cualquier componente del sistema

**Lectura de componente:** Leer cualquier componente del sistema

**Administrador de Contentspace:** Permiso para el administrador de espacio de contenido (obsoleto)

**Inicio de sesión en la consola Contentspace:** Permiso para el inicio de sesión en la consola de Contentspace (obsoleto)

**Control de configuración principal:** Administrar la configuración de la página Configuración del sistema principal en la consola de administración

**CREATE_VERSION_PERM:** Crear una versión de un servicio

**Modificación de credencial:** Modificar cualquier credencial de firma en el almacén de confianza

**Lectura de credencial:** Leer cualquier credencial de firma en el almacén de confianza

**Escritura de credencial:** Agregar una credencial de firma al almacén de confianza

**Modificación de CRL:** Modifique cualquier CRL (Lista de Revocación de Certificados) en el Almacén de Confianza

**Lectura de CRL:** Leer cualquier CRL en el almacén de confianza

**Escritura de CRL:** Agregar una CRL al almacén de confianza

**Delegar:** Establecer una ACL en un recurso

**DELETE_VERSIÓN_PERM:** Eliminar una versión de un servicio

**Carga de documento:** AEM Cargar documentos en formularios de la

**Control de dominio:** Crear, eliminar o modificar la configuración de cualquier dominio de administración de usuarios, incluidos los proveedores de directorios y autenticación

**Editar tipo de evento:** Editar en tipos de eventos

**Control de suplantación de identidad:** Suplantar identidad en el Administrador de usuarios

**INVOKE_PERM:** Invocar todas las operaciones de un servicio

**Control de modelo de datos LCDS:** Leer e implementar modelos de datos en servicios de datos

**Actualización del Administrador de licencias:** Actualizar información de licencia

**MODIFY_CONFIG_PERM:** Modificación de la configuración de un servicio

**TÉRMINO** Modificar la versión de un servicio

**PDFGAdminPermission:** Administrador de PDFG

**PDFGUserPermission:** Usuario de PDFG

**PERM_DCTM_ADMIN:** Administrador de Documentum Connector

**PERM_FILENET_ADMIN:** Administrador del conector FileNet

**PERM_FORMS_ADMIN:** administrador de Forms

**PERM_IBMCM_ADMIN:** Administrador del conector de IBM CM

**PERM_OUTPUT_ADMIN** Administrador de salida

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Uso de la aplicación web Acrobat Reader DC extensions

**PERM_SP_ADMIN:** Administrar configuración del conector de SharePoint

**PERM_WORKSPACE_ADMIN:** Administrar configuración de Workspace

**PERM_WORKSPACE_USER:** Inicie sesión en la aplicación de usuario final de Workspace.

**Control principal:** Administre usuarios y grupos para cualquier dominio y administre asignaciones de funciones para todos los usuarios y grupos de cualquier dominio

**Lectura/Eliminación de grabación de procesos:** Enumeración y recuperación de instancias de auditoría de flujo de trabajo

**PROCESS_OWNER_PERM:** Ver datos de tendencia y realizar acciones administrativas en un servicio creado a partir de un proceso

**Lectura:** Leer el contenido de un recurso

**READ_PERM:** Leer o ver un servicio

**Renovar aserción:** Renovar aserciones en Administración de usuarios

**Delegado de repositorio:** Establecer una ACL en un recurso

**Lectura de repositorio:** Leer el contenido de un recurso

**Recorrido del repositorio:** Incluir un recurso en una solicitud de recursos de lista o leer los metadatos de un recurso

**Escritura en repositorio:** Escribir metadatos y contenido del repositorio

**Propietario de cambio de directiva de Rights Management:** Cambiar propietario de directiva

**Inicio de sesión en la consola de usuario final de Rights Management:** Inicio de sesión en la interfaz de usuario del usuario final de Rights Management

**Configuración de administración del Rights Management:** Administrar configuración del servidor

**Rights Management Administrar usuarios invitados y locales:** Administrar usuarios invitados y locales

**Rights Management Administrar conjuntos de directivas:** Administrar todas las directivas y documentos de cualquier conjunto de directivas

**Conjunto de directivas de Rights Management Agregar coordinador:** Agregar, quitar y cambiar permisos para coordinadores de conjuntos de directivas

**Conjunto de directivas de Rights Management Crear directiva:** Crear una directiva para un conjunto de directivas

**Directiva de Rights Management Establecer directiva de eliminación:** Quitar una directiva de un conjunto de directivas

**Conjunto de directivas de Rights Management Editar directiva:** Editar una directiva en un conjunto de directivas

**Conjunto de directivas de Rights Management Administrar editor de documentos:** Al crear conjuntos de directivas, se asigna a los usuarios la función de editor de documentos. El editor del documento es el usuario que protege el documento con una directiva.

**Conjunto de directivas de Rights Management Quitar coordinador:** Quitar un coordinador de conjunto de directivas de un conjunto de directivas

**Documento de revocación de conjunto de directivas de Rights Management:** Revocar acceso a documentos de un conjunto de directivas

**Directiva de Rights Management Establecer directiva de cambio:** Cambiar directivas para un documento

**Documento sin revocar conjunto de directivas de Rights Management:** Anular la revocación de un documento

**Evento de vista de conjunto de directivas de Rights Management:** Ver los eventos de directivas y documentos de cualquier directiva o documento de un conjunto de directivas

**Eventos del servidor de vista de Rights Management:** Buscar y ver todos los eventos de auditoría

**Control de funciones:** Crear, eliminar y modificar roles en Administración de usuarios

**Activar servicio:** Inicie cualquier servicio, poniéndolo a disposición para su invocación

**Agregar servicio:** Implemente un nuevo servicio en el registro de servicios. Esto incluye añadir nuevos procesos y variantes de proceso

**Desactivación de servicio:** Detener cualquier servicio del sistema

**Eliminación de servicio:** Elimine cualquier servicio del sistema, incluidos los procesos y las variantes de proceso

**Invocación de servicio:** Invocar cualquier servicio del Registro de servicios disponible durante la ejecución

**Modificación del servicio:** Modifique las propiedades de configuración de cualquier servicio del sistema. Esto incluye bloquear y desbloquear un servicio en el IDE, y agregar o quitar extremos de un servicio

**Lectura de servicio:** Lea todos los servicios del sistema. Esto incluye todos los procesos y variantes de procesos

**SERVICE_AGENT_PERM:** Ver datos e interactuar con instancias de proceso para un servicio creado a partir de un proceso

**SERVICE_MANAGER_PERM:** Realizar acciones administrativas y de equilibrio de carga en un servicio creado a partir de un proceso

**START_STOP_PERM:** Iniciar o detener un servicio

**SUPERVISOR_PERM:** Ver datos de instancias de proceso de un servicio creado a partir de un proceso

**Recorrido:** Incluir un recurso en una solicitud de recursos de lista o leer los metadatos de un recurso

**Escribir:** Escribir metadatos y contenido del repositorio

**Abrir archivos en Workbench**

Para ver el contenido de la vista Recursos en Workbench y abrir archivos para verlos, un usuario necesita los siguientes permisos:

* Lectura de repositorio
* Recorrido del repositorio
* Invocación de servicio
* Lectura de servicio

## Quitar un usuario o grupo de una función {#remove-a-user-or-group-from-a-role}

Utilice la página Administración de Roles para eliminar usuarios y grupos de un rol concreto. Si el usuario o grupo heredó la asignación de funciones, no se puede quitar la función en el nivel de usuario o grupo. Quite el usuario o el grupo del árbol de herencia o quite la función del elemento principal.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nombre de la función.

   De forma predeterminada, la página Administración de funciones muestra todas las funciones de la base de datos Administración de usuarios. Si la lista de funciones es grande, utilice el área Buscar de la parte superior de la página para buscar un nombre de función específico.

1. En la lista de funciones, haga clic en el nombre de la función que desea actualizar y, a continuación, haga clic en la ficha Usuarios de la función. Se mostrará una lista de los usuarios y grupos asociados a la función.
1. Seleccione las casillas de verificación de los usuarios y grupos que desea quitar de la función y haga clic en Anular asignación.
1. Haga clic en Guardar y luego en Aceptar.
