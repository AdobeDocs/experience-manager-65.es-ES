---
title: Acceso a WebDAV
seo-title: Acceso a WebDAV
description: Obtenga información sobre el acceso a WebDAV en AEM.
seo-description: Obtenga información sobre el acceso a WebDAV en AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Acceso a WebDAV{#webdav-access}

Para conectarse a AEM mediante WebDAV con KDE:

AEM compatibilidad con WebDAV de ofertas que le permite mostrar y editar el contenido del repositorio. La conexión mediante WebDAV le permite acceder directamente al repositorio de contenido a través de su escritorio. Los archivos de texto y PDF que se agregan al repositorio a través de la conexión WebDAV se indexan automáticamente con texto completo y se pueden buscar con las interfaces de búsqueda estándar y a través de las API estándar de Java.

## General {#general}

[En este documento se incluyen instrucciones detalladas por ](/help/sites-administering/webdav-access.md#connecting-via-webdav) sistema operativo, pero básicamente para conectar con el repositorio mediante el protocolo WebDAV, debe señalar el cliente WebDAV a la siguiente ubicación:

```xml
http://localhost:4502
```

![chlimage_1-191](assets/chlimage_1-111a.png)

Esta dirección URL, cuando se conecta desde el nivel de sistema operativo, proporciona acceso WebDAV al espacio de trabajo predeterminado ( `crx.default`). Aunque resulta más sencillo para el usuario, no les proporciona la flexibilidad adicional de especificar nombres de espacio de trabajo, lo que se puede lograr con direcciones URL [WebDAV](/help/sites-administering/webdav-access.md#webdav-urls) adicionales.

AEM muestra el contenido del repositorio de la siguiente manera:

* Un nodo del tipo `nt:folder` se muestra como una carpeta. Los nodos situados debajo del nodo `nt:folder` se muestran como contenido de la carpeta.

* Un nodo del tipo `nt:file` se muestra como archivo. Los nodos situados debajo del nodo `nt:file` no se muestran, pero forman el contenido del archivo.

Cuando se utiliza WebDAV para crear y editar carpetas y archivos, AEM crea y edita los nodos `nt:folder` y `nt:file` necesarios. Si planea utilizar WebDAV para importar y exportar contenido, intente trabajar con tipos de nodos `nt:file` y `nt:folder` tanto como sea posible.

>[!NOTE]
>
>Antes de configurar WebDAV, consulte los [Requisitos técnicos](/help/sites-deploying/technical-requirements.md#webdav-clients).

## Direcciones URL de WebDAV {#webdav-urls}

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
   <td>Host y puerto en el que se ejecuta AEM</td>
   <td>Ruta para la aplicación web del repositorio de AEM</td>
   <td>Ruta a la cual está asignado el servlet WebDAV</td>
   <td>Nombre del espacio de trabajo</td>
  </tr>
 </tbody>
</table>

Al cambiar el elemento de área de trabajo en la ruta, puede asignar espacios de trabajo que no sean los predeterminados ( `crx.default`). Por ejemplo, para asignar un espacio de trabajo denominado `staging`, utilice la siguiente dirección URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Conexión mediante WebDAV {#connecting-via-webdav}

[Como se mencionó anteriormente](/help/sites-administering/webdav-access.md#general), para conectarse al repositorio mediante el protocolo WebDAV, debe señalar el cliente WebDAV a la ubicación del repositorio. Sin embargo, en función del sistema operativo, los pasos necesarios para conectar el cliente son diferentes y puede haber una configuración del sistema operativo necesaria.

Se proporcionan instrucciones sobre cómo conectar los siguientes sistemas operativos:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Para conectar correctamente un sistema de Microsoft Windows 7 (y bueno) a una instancia de AEM que no esté protegida con SSL, la opción de establecer la autenticación básica a través de una red no segura debe estar habilitada explícitamente en Windows. Esto requiere un cambio en el Registro de Windows de WebClient.

Una vez actualizado el Registro, la instancia de AEM se puede asignar como una unidad.

#### Configuración de Windows 7 y Buena {#windows-and-greater-configuration}

Para actualizar el Registro para permitir la autenticación básica a través de una red no segura:

1. Busque la siguiente subclave del Registro:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Establezca la subclave de entrada del Registro `BasicAuthLevel` en un valor de `2` o bueno.

   Si no está presente, agregue la subclave.

1. Debe reiniciar el sistema para que el cambio del Registro surta efecto.

Consulte [Soporte técnico de Microsoft KB 841215](https://support.microsoft.com/default.aspx/kb/841215) para obtener más información sobre este cambio en el Registro.

Consulte [Soporte técnico de Microsoft KB 2445570](https://support.microsoft.com/kb/2445570) para obtener información sobre cómo mejorar la capacidad de respuesta del cliente WebDav en Windows.

>[!NOTE]
>
>Adobe recomienda que cree un usuario de Windows con las mismas credenciales que el usuario del repositorio; de lo contrario, podría encontrar conflictos de permisos.

#### Configuración de Windows 8 {#windows-configuration}

Para Windows 8 también debe cambiar la entrada del Registro [como se describe para Windows 7 y bueno](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Sin embargo, antes de poder hacerlo, Desktop Experience debe estar habilitado para poder ver la entrada del Registro.

Para habilitar la Experiencia de escritorio, abra **Administrador del servidor**, luego **Funciones**, luego **Añadir características** y luego **Experiencia de escritorio**.

Después de reiniciar la entrada del Registro descrita para Windows 7 y bueno, está disponible. Modifíquelo como se describe para Windows 7 y bueno.

#### Conectando en Windows {#connecting-in-windows}

Para conectarse a AEM mediante WebDAV en un entorno de Windows:

1. Abra **Explorador de Windows** o **Explorador de archivos** y haga clic en **Equipo** o **Este equipo**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Haga clic en **Asignar unidad de red** para inicio del asistente.
1. Introduzca los detalles de asignación:

   * **Unidad**: Elegir cualquier carta disponible
   * **Carpeta**:  `http://localhost:4502`
   * Marque **Conectar con credenciales diferentes**

   Haga clic en Finalizar

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Si AEM está ubicado en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, reemplace `localhost` por el nombre de servidor o la dirección IP correspondientes.

1. Escriba el nombre de usuario `admin` y la contraseña `admin`. Adobe recomienda utilizar la cuenta de administrador preconfigurada para realizar pruebas.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. El asistente se cierra y la unidad recién asignada se abre en una ventana del Explorador de Windows o del Explorador de archivos.

   ![chlimage_1-114](assets/chlimage_1-115a.png)

Windows ahora ha asignado AEM como unidad mediante WebDAV y puede utilizarla como cualquier otra unidad.

### macOS {#macos}

No se requieren pasos de configuración para conectarse mediante WebDAV en macOS. Simplemente necesita conectarse al servidor WebDAV.

1. Vaya a cualquier ventana **Finder** y haga clic en **Ir** y **Conectar al servidor**, o presione **Comando+k**.
1. En la ventana **Conectar con el servidor**, introduzca la ubicación AEM:

   * `http://localhost:4502`
   >[!NOTE]
   >
   >Si AEM está ubicado en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, reemplace `localhost` por el nombre de servidor o la dirección IP correspondientes.

1. Cuando se le solicite autenticación, introduzca el nombre de usuario `admin` y la contraseña `admin`. Adobe recomienda utilizar la cuenta de administrador preconfigurada para realizar pruebas.

macOS ahora se ha conectado a AEM mediante WebDAV y puede utilizarla como cualquier otra carpeta en su Mac.

### Linux {#linux}

La conexión a través de WebDAV en Linux no requiere ninguna configuración, pero sí implica algunos pasos para realizar la conexión que varían según el entorno de su escritorio.

#### GNOME {#gnome}

Para conectarse a AEM mediante WebDAV con GNOME:

1. En Nautilus (explorador de archivos), seleccione **Lugares** y seleccione **Conectar al servidor**.
1. En la ventana **Conectar con el servidor**, seleccione WebDAV (HTTP) en Tipo de servicio.

1. En **Servidor**, introduzca `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Si AEM está ubicado en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, reemplace `localhost` por el nombre de servidor o la dirección IP correspondientes.

1. En **Carpeta**, introduzca `/dav`
1. Escriba el nombre de usuario `admin`. Adobe recomienda utilizar la cuenta de administrador preconfigurada para realizar pruebas.
1. Deje el puerto en blanco e introduzca cualquier nombre para la conexión.
1. Haga clic en **Conectar**. AEM su contraseña.
1. Introduzca la contraseña `admin` y haga clic en **Conectar**.

GNOME ahora ha montado AEM como un volumen y usted puede usarlo como cualquier otro volumen.

#### KDE {#kde}

1. Abra el asistente de carpetas de red.
1. Seleccione **WebFolder**(webdav) y haga clic en Siguiente.
1. En **Nombre**, escriba un nombre de conexión.
1. En **Usuario**, escriba `admin.` Adobe recomienda que utilice la cuenta de administrador preconfigurada.
1. En **Servidor**, introduzca `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Si AEM está ubicado en otro puerto, utilice ese número de puerto en lugar de 4502. Además, si no está ejecutando el repositorio de contenido en su equipo local, reemplace `localhost` por el nombre de servidor o la dirección IP correspondientes

1. En **Carpeta**, introduzca `dav`

1. Haga clic en **Guardar y conectar**.
1. Cuando se le pida la contraseña, introduzca la contraseña `admin` y haga clic en **Conectar**.

KDE ya ha montado AEM como un volumen y puede utilizarlo como cualquier otro volumen.
