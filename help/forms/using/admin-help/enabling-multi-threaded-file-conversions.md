---
title: Activación de las conversiones de archivos con subprocesos múltiples
seo-title: Activación de las conversiones de archivos con subprocesos múltiples
description: Obtenga información sobre cómo habilitar las conversiones de archivos con subprocesos múltiples.
seo-description: Obtenga información sobre cómo habilitar las conversiones de archivos con subprocesos múltiples.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Activación de las conversiones de archivos con subprocesos múltiples {#enabling-multi-threaded-file-conversions}

PDF Generator permite habilitar las conversiones de archivos con subprocesos múltiples para determinados tipos de archivos. La conversión de archivos con subprocesos múltiples mejora el rendimiento de PDF Generator permitiéndole realizar varias conversiones al mismo tiempo.

## Activación de conversiones de archivos con subprocesos múltiples para documentos de OpenOffice, Word y PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

De forma predeterminada, PDF Generator solo puede convertir un documento de OpenOffice, Microsoft Word o PowerPoint a la vez. Si activa las conversiones con varios subprocesos, PDF Generator puede convertir varios documentos al mismo tiempo. PDF Generator iniciará varias instancias de OpenOffice o PDFMaker (se utiliza para realizar las conversiones de Word y PowerPoint).

>[!NOTE]
>
>Las conversiones de archivos con subprocesos múltiples no son compatibles con Microsoft Word 2003 y PowerPoint 2003. Para habilitar las conversiones de archivos con subprocesos múltiples, actualice a Microsoft Word 2007 y PowerPoint 2007 o Microsoft Word 2010 y PowerPoint 2010.

>[!NOTE]
>
>Las conversiones de archivos con subprocesos múltiples no son compatibles con Microsoft Excel, Microsoft Visio, Microsoft Project o Microsoft Publisher.

Cada instancia de OpenOffice o PDFMaker se inicia con una cuenta de usuario independiente. Cada cuenta de usuario que agregue debe ser un usuario válido con privilegios de administrador en el equipo del servidor de formularios. En un entorno agrupado, el mismo conjunto de usuarios debe ser válido para todos los nodos del clúster.

En la página Cuentas de usuario de la consola de administración, puede especificar qué cuentas de usuario utilizar para las conversiones de archivos con subprocesos múltiples. Puede agregar cuentas, eliminarlas o cambiar sus contraseñas. Si está ejecutando PDF Generator en Windows Server 2003 o Windows Server 2008, agregue al menos tres cuentas de usuario con privilegios de administrador.

Al agregar usuarios para OpenOffice, Microsoft Word o Microsoft PowerPoint en Windows Server 2003 o 2008, o para OpenOffice en Linux o Sun™ Solaris™, descarte los cuadros de diálogo de activación iniciales para todos los usuarios.

### Agregue el derecho a reemplazar el token de nivel de proceso {#add-the-right-to-replace-the-process-level-token}

En un sistema operativo Windows, las cuentas de usuario de administrador que se utilizan para la conversión a PDF (usuarios de PDFG) deberán reemplazar los privilegios de token de nivel de proceso. Puede agregar este derecho mediante el Editor de directivas de grupo:

1. En el menú Inicio de Windows, haga clic en Ejecutar y, a continuación, introduzca gpedit.msc.
1. Haga clic en Directiva de equipo local > Configuración de equipo > Configuración de Windows > Configuración de seguridad > Directivas locales > Asignación de derechos de usuario. Edite la directiva de *reemplazo de tokens* de nivel de proceso para incluir el grupo Administradores.
1. Agregue al usuario a la entrada Reemplazar un token de nivel de proceso.

### Se requiere una configuración adicional para OpenOffice, Microsoft Word y Microsoft PowerPoint en Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Si está ejecutando OpenOffice, Microsoft Word o Microsoft PowerPoint en Windows Server 2008, deshabilite UAC para cada usuario agregado.

1. Haga clic en Panel de control > Cuentas de usuario > Activar o desactivar el control de cuentas de usuario.
1. Anule la selección de la casilla &quot;Usar Control de cuentas de usuario (UAC) para ayudar a proteger su equipo&quot; y haga clic en Aceptar.
1. Reinicie el equipo para que la configuración surta efecto.

### Se requiere una configuración adicional para OpenOffice en Linux o Solaris {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Agregar cuentas de usuario. (Consulte [Agregar una cuenta](enabling-multi-threaded-file-conversions.md#add-a-user-account)de usuario).
1. A continuación, realizará cambios en el archivo /etc/sudoers. El permiso predeterminado para este archivo es 440. Cambie el permiso de este archivo a grabable.
1. Agregue entradas para usuarios adicionales (que no sean el administrador que ejecuta el servidor de formularios) en el archivo /etc/sudoers. Por ejemplo, si está ejecutando formularios AEM como un usuario llamado lcadm y un servidor llamado myhost y desea suplantar user1 y user2, agregue las siguientes entradas a /etc/sudoers:

   ```as3
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Esta configuración permite a lcadm ejecutar cualquier comando en el host ‘myhost’ como ‘user1’ o ‘user2’ sin pedir una contraseña.

   >[!NOTE]
   >
   >Asegúrese de que ha asignado las funciones de usuario del sistema y de usuario de PDFG a &quot;user1&quot; y &quot;user2&quot;. Para asignar una función de PDFG a un usuario, consulte [Agregar una cuenta de usuario](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. También en el archivo /etc/sudoers, localice y comente esta línea agregando un signo de número (#) al principio de la línea:

   ```as3
   Defaults requiretty
   ```

   Esto le permite agregar usuarios de Linux.

1. Vuelva a cambiar el permiso del archivo etc/sudoers a 440.
1. Permite que todos los usuarios agregados mediante [Agregar una cuenta](enabling-multi-threaded-file-conversions.md#add-a-user-account) de usuario realicen conexiones con el servidor de formularios. Por ejemplo, para permitir que un usuario local llamado user1 tenga permiso para realizar la conexión con el servidor de formularios, utilice el siguiente comando

   `xhost +local:user1@`

   Para obtener más información, consulte la documentación del comando xhost.

1. Reinicie el servidor.

>[!NOTE]
>
>OpenOffice debe estar instalado en una ubicación de directorio a la que puedan acceder todos los usuarios de PDFG. Puede verificarlo iniciando sesión como usuario de PDFG y comprobando si puede iniciar OpenOffice sin problemas.

### Agregar una cuenta de usuario {#add-a-user-account}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Cuentas de usuario.
1. Haga clic en Agregar e introduzca el nombre de usuario y la contraseña de un usuario que tenga privilegios de administrador en el servidor de formularios. Si va a configurar usuarios para OpenOffice, descarte los cuadros de diálogo de activación iniciales de OpenOffice.

   >[!NOTE]
   >
   >Si está configurando usuarios para OpenOffice, el número de instancias de OpenOffice no puede ser mayor que el número de cuentas de usuario especificado en este paso.

1. Reinicie el servidor de formularios.

### Eliminar un usuario de la lista utilizada para las conversiones de archivos con subprocesos múltiples {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Cuentas de usuario.
1. Haga clic en la casilla de verificación situada junto al usuario que desee eliminar y haga clic en Eliminar.
1. En la página de confirmación, haga clic en Eliminar.
1. Reinicie el servidor de formularios.

### Cambiar la contraseña de una cuenta {#change-the-password-for-an-account}

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Cuentas de usuario.
1. Haga clic en el nombre de usuario y escriba y confirme la nueva contraseña. Esta contraseña debe coincidir con la contraseña del sistema del usuario.

