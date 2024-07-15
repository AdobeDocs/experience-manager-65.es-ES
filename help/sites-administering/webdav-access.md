---
title: Acceso a WebDAV
description: Obtenga información sobre cómo acceder a Experience Manager de Adobe mediante WebDAV.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 0%

---

# Acceso a WebDAV{#webdav-access}

AEM Para conectarse a la red a través de WebDAV con KDE:

AEM ofrece compatibilidad con WebDAV que le permite mostrar y editar el contenido del repositorio. La conexión mediante WebDAV le permite acceder directamente al repositorio de contenido a través de su escritorio. Los archivos de texto y PDF que se agregan al repositorio a través de la conexión WebDAV se indexan automáticamente con texto completo y se pueden buscar con las interfaces de búsqueda estándar y a través de las API estándar de Java™.

## General {#general}

[En este documento se incluyen instrucciones detalladas por sistema operativo](/help/sites-administering/webdav-access.md#connecting-via-webdav), pero básicamente para conectarse al repositorio mediante el protocolo WebDAV, debe apuntar su cliente WebDAV a la siguiente ubicación:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Esta dirección URL, cuando se conecta desde el nivel del sistema operativo, proporciona acceso WebDAV al área de trabajo predeterminada ( `crx.default`). A pesar de ser más sencillo para el usuario, no le proporciona la flexibilidad adicional de especificar nombres de área de trabajo, lo que se puede realizar utilizando [URL de WebDAV](/help/sites-administering/webdav-access.md#webdav-urls) adicionales.

AEM Muestra el contenido del repositorio de la siguiente manera:

* Un nodo del tipo `nt:folder` se muestra como una carpeta. Los nodos situados debajo del nodo `nt:folder` se muestran como el contenido de la carpeta.

* Se muestra un nodo del tipo `nt:file` como archivo. Los nodos situados debajo del nodo `nt:file` no se muestran, sino que forman el contenido del archivo.

AEM Cuando se usa WebDAV para crear y editar carpetas y archivos, se crean y editan los nodos necesarios de `nt:folder` y `nt:file`, y se crean y editan los nodos necesarios. Si planea usar WebDAV para importar y exportar contenido, intente trabajar con `nt:file` y `nt:folder` tipos de nodos tanto como sea posible.

>[!NOTE]
>
>Antes de configurar WebDAV, compruebe los [requisitos técnicos](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URL de WebDAV {#webdav-urls}

La dirección URL del servidor WebDAV tiene la siguiente estructura:

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>Descripción</strong></td>
   <td>AEM Host y puerto en el que se ejecuta la</td>
   <td>AEM Ruta para la aplicación web del repositorio de</td>
   <td>Ruta a la que se asigna el servlet WebDAV</td>
   <td>Nombre del espacio de trabajo</td>
  </tr>
 </tbody>
</table>

Al cambiar el elemento de área de trabajo en la ruta de acceso, puede asignar áreas de trabajo que no sean las predeterminadas ( `crx.default`). Por ejemplo, para asignar un área de trabajo denominada `staging`, utilice la siguiente dirección URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Conexión mediante WebDAV {#connecting-via-webdav}

[Como se mencionó anteriormente](/help/sites-administering/webdav-access.md#general), para conectarse al repositorio mediante el protocolo WebDAV, debe apuntar el cliente WebDAV a la ubicación del repositorio. Sin embargo, según el sistema operativo, los pasos necesarios para conectar al cliente difieren y es posible que se requiera una configuración del sistema operativo.

Se proporcionan instrucciones sobre cómo conectar los siguientes sistemas operativos:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Para conectar correctamente un sistema MicrosoftAEM ® Windows 7 (y posterior) a una instancia de que no esté protegida con SSL, la opción para establecer la autenticación básica en una red no segura debe estar habilitada explícitamente en Windows. Esta capacidad requiere un cambio en el Registro de Windows de WebClient.

AEM Una vez actualizado el registro, la instancia de la instancia de la se puede asignar como una unidad.

#### Configuración de Windows 7 y posterior {#windows-and-greater-configuration}

Para actualizar el Registro para permitir la autenticación básica en una red no segura:

1. Busque la siguiente subclave del Registro:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Establezca la subclave de entrada del Registro `BasicAuthLevel` en un valor de `2` o superior.

   Si no está presente, agregue la subclave.

1. Reinicie el sistema para que el cambio del Registro surta efecto.

>[!NOTE]
>
>El Adobe recomienda crear un usuario de Windows con las mismas credenciales que el usuario del repositorio; de lo contrario, podrían producirse conflictos de permisos.

#### Configuración de Windows 8 {#windows-configuration}

Para Windows 8, cambie la entrada del Registro [tal como se describe para Windows 7 y versiones posteriores](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Sin embargo, antes de realizar esta tarea, la Experiencia de escritorio debe estar habilitada para ver la entrada del Registro.

Para habilitar la experiencia de escritorio, abre **Administrador de servidores**, **Características**, **Agregar características** y **Experiencia de escritorio**.

Después del reinicio, está disponible la entrada del Registro descrita para Windows 7 y posterior. Modifique la configuración tal como se describe para Windows 7 y versiones posteriores.

#### Conexión en Windows {#connecting-in-windows}

AEM Para conectarse a la red a través de WebDAV en un entorno de Windows:

1. Abra **Windows Explorer** o **File Explorer** y haga clic en **Equipo** o **Este equipo**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Para iniciar el asistente, haga clic en **Asignar unidad de red**.
1. Introduzca los detalles de asignación:

   * **Unidad**: elija cualquier carta disponible
   * **Carpeta**: `http://localhost:4502`
   * Comprobar **conexión con credenciales diferentes**

   Haga clic en Finalizar

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >AEM Si está en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, reemplace `localhost` por el nombre del servidor o la dirección IP correspondientes.

1. Escriba el nombre de usuario `admin` y la contraseña `admin`. El Adobe recomienda utilizar la cuenta de administrador preconfigurada para realizar pruebas.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. El asistente se cierra y la unidad recién asignada se abre en una ventana del Explorador de Windows o del Explorador de archivos.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

AEM Windows ahora ha asignado la unidad como una unidad a través de WebDAV y puede utilizarla como cualquier otra unidad.

### macOS {#macos}

No se requieren pasos de configuración para conectarse mediante WebDAV en macOS. Puede conectarse al servidor WebDAV.

1. Vaya a cualquier ventana de **Finder** y haga clic en **Ir** y **Conectarse al servidor**, o bien presione **Comando+k**.
1. AEM En la ventana **Conectarse al servidor**, escriba la ubicación de la:

   * `http://localhost:4502`

   >[!NOTE]
   >
   >AEM Si está en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, reemplace `localhost` por el nombre del servidor o la dirección IP correspondientes.

1. Cuando se le pida autenticación, escriba el nombre de usuario `admin` y la contraseña `admin`. El Adobe recomienda utilizar la cuenta de administrador preconfigurada para realizar pruebas.

macOS AEM ahora se ha conectado a través de WebDAV y se puede usar como cualquier otra carpeta de su Mac.

### Linux® {#linux}

La conexión a través de WebDAV en Linux® no requiere ninguna configuración, pero implica algunos pasos para realizar la conexión que varían según el entorno de escritorio.

#### GNOMO {#gnome}

AEM Para conectarse a la red a través de WebDAV con GNOME:

1. En Nautilus (explorador de archivos), seleccione **Places** y seleccione **Conectar con servidor**.
1. En la ventana **Conectarse al servidor**, seleccione WebDAV (HTTP) en Tipo de servicio.

1. En **Servidor**, escriba `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >AEM Si está en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, reemplace `localhost` por el nombre del servidor o la dirección IP correspondientes.

1. En **carpeta**, escriba `/dav`
1. Escriba el nombre de usuario `admin`. El Adobe recomienda utilizar la cuenta de administrador preconfigurada para realizar pruebas.
1. Deje el puerto en blanco e introduzca cualquier nombre para la conexión.
1. Haga clic en **Conectar**. AEM le pide la contraseña que ha solicitado.
1. Escriba la contraseña `admin` y haga clic en **Conectar**.

AEM GNOME ahora ha montado el volumen como un volumen y usted puede usarlo como cualquier otro volumen.

#### KDE {#kde}

1. Abra el asistente Carpeta de red.
1. Seleccione **WebFolder**(webdav) y haga clic en Siguiente.
1. En **Nombre**, escriba un nombre de conexión.
1. En **Usuario**, escriba `admin.` Adobe recomienda que use la cuenta de administrador preconfigurada.
1. En **Servidor**, escriba `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >AEM Si está en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, reemplace `localhost` por el nombre del servidor o la dirección IP correspondientes

1. En **carpeta**, escriba `dav`

1. Haz clic en **Guardar y conectar**.
1. Cuando se le pida su contraseña, ingrese la contraseña `admin` y haga clic en **Conectar**.

AEM KDE ahora ha montado el volumen como un volumen y puede usarlo como cualquier otro volumen.
