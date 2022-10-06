---
title: Acceso a WebDAV
seo-title: WebDAV Access
description: Obtenga información sobre el acceso a WebDAV en AEM.
seo-description: Learn about WebDAV access in AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 0%

---

# Acceso a WebDAV{#webdav-access}

Para conectarse a AEM a través de WebDAV con KDE:

AEM ofrece compatibilidad con WebDAV que le permite mostrar y editar el contenido del repositorio. La conexión mediante WebDAV le permite acceder directamente al repositorio de contenido a través de su escritorio. Los archivos de texto y PDF que se agregan al repositorio a través de la conexión WebDAV se indexan automáticamente con texto completo y se pueden buscar con las interfaces de búsqueda estándar y a través de las API de Java estándar.

## General {#general}

[Instrucciones detalladas por sistema operativo](/help/sites-administering/webdav-access.md#connecting-via-webdav) se incluyen en este documento, pero básicamente para conectarse al repositorio utilizando el protocolo WebDAV, debe señalar al cliente WebDAV a la siguiente ubicación:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Esta URL, cuando se conecta desde el nivel del sistema operativo, proporciona acceso a WebDAV al espacio de trabajo predeterminado ( `crx.default`). Aunque es más sencillo para el usuario, no le ofrece la flexibilidad adicional de especificar nombres de espacio de trabajo, lo que se puede lograr utilizando [URL de WebDAV](/help/sites-administering/webdav-access.md#webdav-urls).

AEM muestra el contenido del repositorio de la siguiente manera:

* Un nodo del tipo `nt:folder` se muestra como una carpeta. Nodos debajo de `nt:folder` se muestran como el contenido de la carpeta.

* Un nodo del tipo `nt:file` se muestra como un archivo. Nodos debajo de `nt:file` no se muestran, sino que forman el contenido del archivo.

Cuando utiliza WebDAV para crear y editar carpetas y archivos, AEM crea y edita los `nt:folder` y `nt:file` nodos. Si planea utilizar WebDAV para importar y exportar contenido, intente trabajar con `nt:file` y `nt:folder` tipos de nodo en la medida de lo posible.

>[!NOTE]
>
>Antes de configurar WebDAV, compruebe el [Requisitos técnicos](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URL de WebDAV {#webdav-urls}

La URL del servidor WebDAV tiene la siguiente estructura:

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
   <td>Host y puerto en el que se ejecuta AEM</td>
   <td>Ruta para la aplicación web del repositorio de AEM</td>
   <td>Ruta a la que está asignado el servlet WebDAV</td>
   <td>Nombre del espacio de trabajo</td>
  </tr>
 </tbody>
</table>

Al cambiar el elemento del espacio de trabajo en la ruta, puede asignar espacios de trabajo que no sean los predeterminados ( `crx.default`). Por ejemplo, para asignar un espacio de trabajo denominado `staging`, utilice la siguiente URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Conexión mediante WebDAV {#connecting-via-webdav}

[Como se ha mencionado anteriormente](/help/sites-administering/webdav-access.md#general), para conectarse al repositorio utilizando el protocolo WebDAV, dirija su cliente WebDAV a su ubicación del repositorio. Sin embargo, en función del sistema operativo, los pasos necesarios para conectar el cliente difieren y puede haber configuración del sistema operativo necesaria.

Se proporcionan instrucciones sobre cómo conectar los siguientes sistemas operativos:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Para conectar correctamente un sistema Microsoft Windows 7 (y bueno) a una instancia AEM que no esté segura con SSL, la opción para establecer la autenticación básica en una red no segura debe estar habilitada explícitamente en Windows. Esto requiere un cambio en el Registro de Windows de WebClient.

Una vez actualizado el registro, la instancia de AEM puede asignarse como una unidad.

#### Configuración de Windows 7 y Buena {#windows-and-greater-configuration}

Para actualizar el registro para permitir la autenticación básica a través de una red no segura:

1. Busque la siguiente subclave del Registro:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Configure las variables `BasicAuthLevel` subclave de entrada de registro a un valor de `2` o buenas.

   Si no está presente, añada la subclave .

1. Debe reiniciar el sistema para que el cambio del registro surta efecto.

Consulte [Compatibilidad con Microsoft KB 841215](https://support.microsoft.com/default.aspx/kb/841215) para obtener más información sobre este cambio en el registro.

Consulte [Compatibilidad con Microsoft KB 2445570](https://support.microsoft.com/kb/2445570) para obtener información sobre cómo mejorar la capacidad de respuesta del cliente WebDav en Windows.

>[!NOTE]
>
>Adobe recomienda crear un usuario de Windows con las mismas credenciales que el usuario del repositorio; de lo contrario, podría encontrar conflictos de permisos.

#### Configuración de Windows 8 {#windows-configuration}

Para Windows 8 también debe cambiar la entrada del Registro [tal como se describe para Windows 7 y bueno](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Sin embargo, antes de poder hacerlo, Desktop Experience debe estar habilitado para poder ver la entrada del registro.

Para habilitar la experiencia de escritorio, abra **Administrador del servidor**, luego **Funciones**, luego **Agregar características**, luego **Experiencia de escritorio**.

Después de reiniciar la entrada del Registro descrita para Windows 7 y bueno está disponible. Modifique como se describe para Windows 7 y buenas.

#### Conexión en Windows {#connecting-in-windows}

Para conectarse a AEM mediante WebDAV en un entorno de Windows:

1. Apertura **Explorador de Windows** o **Explorador de archivos** y haga clic en **Equipo** o **Este PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Haga clic en **Asignar unidad de red** para iniciar el asistente.
1. Introduzca los detalles de asignación:

   * **Unidad**: Elija cualquier carta disponible
   * **Carpeta**: `http://localhost:4502`
   * Marque **Conexión con credenciales diferentes**

   Haga clic en Finalizar

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Si AEM está ubicado en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, sustituya `localhost` con el nombre de servidor o la dirección IP correspondientes.

1. Introducir nombre de usuario `admin` y contraseña `admin`. Adobe recomienda usar la cuenta de administrador preconfigurada para realizar pruebas.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. El asistente se cierra y la unidad recién asignada se abre en una ventana del Explorador de Windows o Explorador de archivos.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows ahora ha asignado AEM como una unidad a través de WebDAV y puede utilizarla como cualquier otra unidad.

### macOS {#macos}

No se requieren pasos de configuración para conectarse mediante WebDAV en macOS. Simplemente debe conectarse al servidor WebDAV.

1. Vaya a cualquier **Buscador** y haga clic en **Ir** y **Conectar con el servidor** o presione **Comando + k**.
1. En el **Conectar con el servidor** , introduzca la ubicación de AEM:

   * `http://localhost:4502`
   >[!NOTE]
   >
   >Si AEM está ubicado en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, sustituya `localhost` con el nombre de servidor o la dirección IP correspondientes.

1. Cuando se le pida autenticación, introduzca el nombre de usuario `admin` y contraseña `admin`. Adobe recomienda usar la cuenta de administrador preconfigurada para realizar pruebas.

macOS ahora se ha conectado a AEM a través de WebDAV y puede utilizarlo como cualquier otra carpeta de su Mac.

### Linux {#linux}

La conexión a través de WebDAV en Linux no requiere ninguna configuración, pero implica algunos pasos para hacer la conexión que varía según el entorno de escritorio.

#### GNOME {#gnome}

Para conectarse a AEM a través de WebDAV con GNOME:

1. En Nautilus (explorador de archivos), seleccione **Lugares** y seleccione **Conectar con el servidor**.
1. En el **Conectar con el servidor** , seleccione WebDAV (HTTP) en Tipo de servicio.

1. En **Servidor**, introduzca `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Si AEM está ubicado en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, sustituya `localhost` con el nombre de servidor o la dirección IP correspondientes.

1. En **Carpeta**, introduzca `/dav`
1. Escriba el nombre de usuario `admin`. Adobe recomienda usar la cuenta de administrador preconfigurada para realizar pruebas.
1. Deje el puerto en blanco e introduzca cualquier nombre para la conexión.
1. Haga clic en **Connect**. AEM le pide su contraseña.
1. Escriba la contraseña `admin` y haga clic en **Connect**.

GNOME ahora ha montado AEM como un volumen y usted puede usarlo como cualquier otro volumen.

#### KDE {#kde}

1. Abra el asistente Carpeta de red .
1. Select **WebFolder**(webdav) y haga clic en Siguiente.
1. En **Nombre**, escriba un nombre de conexión.
1. En **Usuario**, introduzca `admin.` Adobe recomienda usar la cuenta de administrador preconfigurada.
1. En **Servidor**, introduzca `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Si AEM está ubicado en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, sustituya `localhost` con el nombre de servidor o la dirección IP correspondientes

1. En **Carpeta**, introduzca `dav`

1. Haga clic en **Guardar y conectar**.
1. Cuando se le pida la contraseña, introduzca la contraseña `admin` y haga clic en **Connect**.

KDE ahora ha montado AEM como un volumen y puede utilizarlo como cualquier otro volumen.
