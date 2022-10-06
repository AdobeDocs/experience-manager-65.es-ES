---
title: Cómo utilizar la herramienta VLT
seo-title: How to use the VLT Tool
description: La herramienta Jackrabbit FileVault (VLT) es desarrollada por la Apache Foundation que asigna el contenido de una instancia de Jackrabbit/AEM a su sistema de archivos
seo-description: The Jackrabbit FileVault tool (VLT) is developed by The Apache Foundation that maps the content of a Jackrabbit/AEM instance to your file system
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
exl-id: efbba312-9fc8-4670-b8f1-d2a86162d075
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2718'
ht-degree: 2%

---

# Cómo utilizar la herramienta VLT {#how-to-use-the-vlt-tool}

La herramienta Jackrabbit FileVault (VLT) es una herramienta desarrollada por [La Apache Foundation](https://www.apache.org/) que asigna el contenido de una instancia de Jackrabbit/AEM a su sistema de archivos. La herramienta VLT tiene funciones similares a las del cliente del sistema de control de código fuente (como un cliente de Subversion (SVN)), que proporciona operaciones normales de check-in, check-out y administración, así como opciones de configuración para una representación flexible del contenido del proyecto.

La herramienta VLT se ejecuta desde la línea de comandos. En este documento se describe cómo utilizar la herramienta, incluido cómo empezar y obtener ayuda, así como una lista de todas las [comandos](#vlt-commands) y disponibles [opciones](#vlt-global-options).

## Conceptos y arquitectura {#concepts-and-architecture}

Consulte la [Información general de archivo](https://jackrabbit.apache.org/filevault/overview.html) y [Vault FS](https://jackrabbit.apache.org/filevault/vaultfs.html) página del oficial [Documentación de Apache Jackrabbit Filevault](https://jackrabbit.apache.org/filevault/index.html) para obtener una descripción detallada de los conceptos y la estructura de la herramienta Filevault.

## Introducción a VLT {#getting-started-with-vlt}

Para empezar a usar VLT, debe hacer lo siguiente:

1. Instale VLT, actualice las variables de entorno y actualice los archivos de subversión global ignorados.
1. Configure el repositorio de AEM (si aún no lo ha hecho).
1. Consulte el repositorio de AEM.
1. Sincronice con el repositorio.
1. Compruebe si la sincronización funcionó.

### Instalación de la herramienta VLT {#installing-the-vlt-tool}

Para utilizar la herramienta VLT, primero debe instalarla. No está instalado de forma predeterminada, ya que es una herramienta adicional. Además, debe configurar la variable de entorno del sistema.

1. Descargue el archivo FileVault del [Maven el repositorio de artefactos.](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >El origen de la herramienta VLT es [disponible en GitHub.](https://github.com/apache/jackrabbit-filevault)
1. Extraiga el archivo.
1. Agregar `<archive-dir>/vault-cli-<version>/bin` a su entorno `PATH` para que los archivos de comando `vlt` o `vlt.bat` si procede, se accede a ellas. Por ejemplo:

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. Abra un shell de línea de comandos y ejecute `vlt --help`. Asegúrese de que el resultado sea similar a la siguiente pantalla de ayuda:

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

Una vez que lo haya instalado, deberá actualizar los archivos de subversión global ignorados. Edite la configuración de svn y añada lo siguiente:

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### Configuración del carácter de fin de línea {#configuring-the-end-of-line-character}

VLT gestiona automáticamente el fin de línea (EOF) según las siguientes reglas:

* líneas de archivos extraídas en Windows end con un `CRLF`
* líneas de archivos extraídas en Linux/Unix terminan con un `LF`
* líneas de archivos comprometidos con el final del repositorio con un `LF`

Para garantizar que la configuración de VLT y SVN coincida, debe configurar la variable `svn:eol-style` propiedad a `native` para la extensión de los archivos almacenados en el repositorio. Edite la configuración de svn y añada lo siguiente:

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### Extracción del repositorio {#checking-out-the-repository}

Consulte el repositorio utilizando el sistema de control de código fuente. En svn, por ejemplo, escriba lo siguiente (sustituyendo el URI y la ruta con su repositorio):

```shell
svn co https://svn.server.com/repos/myproject
```

### Sincronización con el repositorio {#synchronizing-with-the-repository}

Debe sincronizar filevault con el repositorio. Para ello:

1. En la línea de comandos, vaya a `content/jcr_root`.
1. Consulte el repositorio escribiendo lo siguiente (sustituyendo su número de puerto por **4502** y sus contraseñas de administrador):

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >Las credenciales deben especificarse solo una vez tras el cierre de compra inicial. Luego se almacenan en su directorio de inicio dentro de `.vault/auth.xml`.

### Prueba de si la sincronización funcionó {#testing-whether-the-synchronization-worked}

Después de haber desprotegido el repositorio y sincronizarlo, debe probar para asegurarse de que todo funciona correctamente. Una forma sencilla de hacerlo es editar un **.jsp** y compruebe si los cambios se reflejan después de confirmar los cambios.

Para probar la sincronización:

1. Vaya a `.../jcr_content/libs/foundation/components/text`.
1. Editar algo en `text.jsp`.
1. Consulte los archivos modificados escribiendo `vlt st`
1. Consulte los cambios escribiendo `vlt diff text.jsp`
1. Confirme los cambios: `vlt ci test.jsp`.
1. Vuelva a cargar una página que contenga un componente de texto y compruebe si los cambios están allí.

## Obtención de ayuda con la herramienta VLT {#getting-help-with-the-vlt-tool}

Después de instalar la herramienta VLT, puede acceder a su archivo de ayuda desde la línea de comandos:

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

Para obtener ayuda sobre un comando concreto, escriba el comando help seguido del nombre del comando . Por ejemplo:

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified in order to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## Tareas comunes realizadas en VLT {#common-tasks-performed-in-vlt}

A continuación se indican algunas tareas comunes realizadas en VLT. Para obtener información detallada sobre cada comando, consulte el [comandos](#vlt-commands).

### Extracción de un subárbol {#checking-out-a-subtree}

Si solo desea extraer un subárbol del repositorio, por ejemplo, `/apps/geometrixx`, puede hacerlo escribiendo lo siguiente:

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

Al hacer esto, se crea una nueva raíz de exportación `geo` con un `META-INF` y `jcr_root` y coloca todos los archivos debajo `/apps/geometrixx` en `geo/jcr_root`.

### Realización de una comprobación filtrada {#performing-a-filtered-checkout}

Si tiene un filtro de espacio de trabajo existente y desea utilizarlo para el cierre de compra, puede crear primero la variable `META-INF/vault` y coloque el filtro allí, o especifíquelo en la línea de comandos de la siguiente manera:

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

Un filtro de ejemplo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### Uso de Importar/Exportar en lugar de .vlt Control {#using-import-export-instead-of-vlt-control}

Puede importar y exportar contenido entre un repositorio JCR y el sistema de archivos local sin utilizar archivos de control.

Para importar y exportar contenido sin usar `.vlt` control:

1. Configuración inicial del repositorio:

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. Cambie la copia remota y actualice JCR:

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. Cambie la copia remota y actualice el servidor de archivos:

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## Uso de VLT {#using-vlt}

Para ejecutar comandos en VLT, escriba lo siguiente en la línea de comandos:

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

Las opciones y los comandos se describen detalladamente en las secciones siguientes.

## Opciones globales de VLT {#vlt-global-options}

La siguiente es una lista de opciones de VLT, que están disponibles para todos los comandos. Consulte los comandos individuales para obtener información sobre las opciones disponibles adicionales.

|  |  |
|--- |--- |
| Opción | Descripción |
| `-Xjcrlog <arg>` | Opciones de JcrLog extendidas |
| `-Xdavex <arg>` | Opciones de remoto JCR extendidas |
| `--credentials <arg>` | Las credenciales predeterminadas para usar |
| `--config <arg>` | La configuración JcrFs que se utilizará |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprimir lo menos posible |
| `--version` | Imprime la información de la versión y sale de VLT |
| `--log-level <level>` | Indica el nivel de registro, por ejemplo, el nivel de registro log4j. |
| `-h (--help) <command>` | Imprime la ayuda para ese comando en particular |

## Comandos VLT {#vlt-commands}

La siguiente tabla describe todos los comandos VLT disponibles. Consulte los comandos individuales para obtener información detallada sobre la sintaxis, las opciones disponibles y los ejemplos.

|  |  |  |
|--- |--- |--- |
| Comando | Comando abreviado | Descripción |
| `export` |  | Exporta desde un repositorio JCR (sistema de archivos vault) al sistema de archivos local sin archivos de control. |
| `import` |  | Importa un sistema de archivos local a un repositorio JCR (sistema de archivos vault). |
| `checkout` | `co` | Extrae un sistema de archivos Vault. Utilice esto para un repositorio JCR inicial para el sistema de archivos local. (Nota: Primero debe extraer el repositorio en subversión). |
| `analyze` |  | Analiza los paquetes. |
| `status` | `st` | Imprime el estado de los archivos y directorios de copia de trabajo. |
| `update` | `up` | Importa cambios desde el repositorio a la copia de trabajo. |
| `info` |  | Muestra información sobre un archivo local. |
| `commit` | `ci` | Envía cambios desde la copia de trabajo al repositorio. |
| `revert` | `rev` | Restaura el archivo de copia de trabajo a su estado original y deshace la mayoría de las ediciones locales. |
| `resolved` | `res` | Elimina el estado conflictivo de los archivos o directorios de copia de trabajo. |
| `propget` | `pg` | Imprime el valor de una propiedad en archivos o directorios. |
| `proplist` | `pl` | Imprime las propiedades en archivos o directorios. |
| `propset` | `ps` | Define el valor de una propiedad en archivos o directorios. |
| `add` |  | Coloca los archivos y directorios bajo control de versiones. |
| `delete` | `del` o `rm` | Quita archivos y directorios del control de versiones. |
| `diff` | `di` | Muestra las diferencias entre dos rutas. |
| `console` |  | Ejecuta una consola interactiva. |
| `rcp` |  | Copia un árbol de nodos de un repositorio remoto a otro. |
| `sync` |  | Permite controlar el servicio de sincronización de bóveda. |

### Exportar {#export}

Exporta el sistema de archivos Vault montado en &lt;uri> al sistema de archivos local en &lt;local-path>. Un &lt;jcr-path> se puede especificar para exportar solo un subárbol.

#### Sintaxis {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### Opciones {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada |
| `-t (--type) <arg>` | especifica el tipo de exportación, plataforma o jar. |
| `-p (--prune-missing)` | especifica si los archivos locales que faltan deben eliminarse |
| `<uri>` | uri de punto de montaje |
| `<jcrPath>` | Ruta de JCR |
| `<localPath>` | ruta local |

#### Ejemplos {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### Importar {#import}

Importa el sistema de archivos local (a partir de `<local-path>` al sistema de archivos bóveda en `<uri>`. Puede especificar un `<jcr-path>` como raíz de importación. If `--sync` se especifica, los archivos importados se ponen automáticamente bajo control de almacén.

#### Sintaxis {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### Opciones {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada |
| `-s (-- sync)` | coloca los archivos locales bajo control vault |
| `<uri>` | uri de punto de montaje |
| `<jcrPath>` | Ruta de JCR |
| `<localPath>` | ruta local |

#### Ejemplos {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### Cierre de compra (co) {#checkout-co}

Realiza una comprobación inicial desde un repositorio JCR al sistema de archivos local a partir de &lt;uri> al sistema de archivos local en &lt;local-path>. También puede agregar un &lt;jcrpath> para extraer un subdirectorio del árbol remoto. Se pueden especificar filtros de espacio de trabajo que se copian en el directorio META-INF.

#### Sintaxis {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### Opciones {#options-2}

|  |  |
|--- |--- |
| `--force` | obliga al cierre de compra a sobrescribir los archivos locales si ya existen |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprime lo menos posible |
| `-f (--filter) <file>` | especifica filtros automáticos si ninguno está definido |
| `<uri>` | uri de punto de montaje |
| `<jcrPath>` | (opcional) ruta remota |
| `<localPath>` | (opcional) ruta local |

#### Ejemplos {#examples-2}

Uso de JCR Remoting:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

Con el espacio de trabajo predeterminado:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

Si el URI está incompleto, se expandirá:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### Analizar {#analyze}

Analiza los paquetes.

#### Sintaxis {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### Opciones {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | formato printf para vínculos de correcciones (nombre,id), por ejemplo `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprime lo menos posible |
| `<localPaths> [<localPaths> ...]` | ruta local |

### Estado {#status}

Imprime el estado de los archivos y directorios de copia de trabajo.

If `--show-update` se especifica, cada archivo se marca con la versión remota. A continuación, la segunda letra especifica qué acción se realizará mediante una operación de actualización.

#### Sintaxis {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### Opciones {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprime lo menos posible |
| `-u (--show-update)` | muestra información de actualización |
| `-N (--non-recursive)` | funciona en un solo directorio |
| `<file> [<file> ...]` | archivo o directorio para mostrar el estado |

### Actualizar {#update}

Copia los cambios del repositorio en la copia de trabajo.

#### Sintaxis {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### Opciones {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprime lo menos posible |
| `--force` | fuerza la sobrescritura de archivos locales |
| `-N (--non-recursive)` | funciona en un solo directorio |
| `<file> [<file> ...]` | archivo o directorio para actualizar |

### Información {#info}

Muestra información sobre un archivo local.

#### Sintaxis {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### Opciones {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprime lo menos posible |
| `-R (--recursive)` | opera recursivo |
| `<file> [<file> ...]` | archivo o directorio para mostrar información |

### Transferir {#commit}

Envía cambios desde la copia de trabajo al repositorio.

#### Sintaxis {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### Opciones {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprime lo menos posible |
| `--force` | fuerza la comisión incluso si se modifica la copia remota |
| `-N (--non-recursive)` | funciona en un solo directorio |
| `<file> [<file> ...]` | archivo o directorio para confirmar |

### Revertir {#revert}

Restaura el archivo de copia de trabajo al estado original y deshace la mayoría de las ediciones locales.

#### Sintaxis {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### Opciones {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime lo menos posible |
| `-R (--recursive)` | baja recursivamente |
| `<file> [<file> ...]` | archivo o directorio para confirmar |

### Resuelto {#resolved}

Elimina **conflicted** en archivos de copia de trabajo o directorios.

>[!NOTE]
>
>Este comando no resuelve semánticamente conflictos ni elimina marcadores de conflicto; simplemente elimina los archivos de artefactos relacionados con el conflicto y permite que PATH se vuelva a cometer.

#### Sintaxis {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### Opciones {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime lo menos posible |
| `-R (--recursive)` | baja recursivamente |
| `--force` | resuelve, incluso si hay marcadores de conflicto |
| `<file> [<file> ...]` | archivo o directorio que se va a resolver |

### Proyecto {#propget}

Imprime el valor de una propiedad en archivos o directorios.

#### Sintaxis {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### Opciones {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime lo menos posible |
| `-R (--recursive)` | baja recursivamente |
| `<propname>` | el nombre de la propiedad |
| `<file> [<file> ...]` | archivo o directorio desde el que obtener la propiedad |

### Proveedor {#proplist}

Imprime las propiedades en archivos o directorios.

#### Sintaxis {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### Opciones {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime lo menos posible |
| `-R (--recursive)` | baja recursivamente |
| `<file> [<file> ...]` | archivo o directorio desde el que enumerar las propiedades |

### Gestor de datos {#propset}

Define el valor de una propiedad en archivos o directorios.

>[!NOTE]
>
>VLT reconoce las siguientes propiedades con versiones especiales:
>
>`vlt:mime-type`
>
>El tipo de mimetype del archivo. Se utiliza para determinar si desea combinar el archivo. Un mimetype que comienza con &quot;text/&quot; (o un mimetype ausente) se trata como texto. Cualquier otra cosa se trata como binaria.

#### Sintaxis {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### Opciones {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | imprime lo menos posible |
| `-R (--recursive)` | baja recursivamente |
| `<propname>` | el nombre de la propiedad |
| `<propval>` | el valor de la propiedad |
| `<file> [<file> ...]` | archivo o directorio para establecer la propiedad en |

### Añada {#add}

Coloca los archivos y directorios bajo control de versiones, programándolos para añadirlos al repositorio. Se añadirán en la próxima confirmación.

#### Sintaxis {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### Opciones {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprime lo menos posible |
| `-N (--non-recursive)` | funciona en un solo directorio |
| `--force` | fuerza la ejecución de la operación |
| `<file> [<file> ...]` | archivo local o directorio para agregar |

### Eliminar {#delete}

Quita archivos y directorios del control de versiones.

#### Sintaxis {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### Opciones {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada |
| `-q (--quiet)` | imprime lo menos posible |
| `--force` | fuerza la ejecución de la operación |
| `<file> [<file> ...]` | archivo local o directorio que se va a eliminar |

### Dif. {#diff}

Muestra las diferencias entre dos rutas.

#### Sintaxis {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### Opciones {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | funciona en un solo directorio |
| `<file> [<file> ...]` | para mostrar las diferencias entre |

### Consola {#console}

Ejecuta una consola interactiva.

#### Sintaxis {#syntax-16}

```shell
console -F <file>
```

#### Opciones {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | especifica el archivo de configuración de la consola. El archivo predeterminado es console.properties. |

### Rcp {#rcp}

Copia un árbol de nodos de un repositorio remoto a otro. `<src>` apunta al nodo de origen y `<dst>` especifica la ruta de destino, donde debe existir el nodo principal. Rcp procesa los nodos transmitiendo los datos.

#### Sintaxis {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### Opciones {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | Imprime lo menos posible. |
| `-r (--recursive)` | Desciende recursivamente. |
| `-b (--batchSize) <size>` | Número de nodos que se van a procesar antes de un guardado intermedio. |
| `-t (--throttle) <seconds>` | Número de segundos que hay que esperar después de un guardado intermedio. |
| `-u (--update)` | Sobrescriba o elimine los nodos existentes. |
| `-n (--newer)` | Respete las propiedades lastModified para la actualización. |
| `-e (--exclude) <arg> [<arg> ...]` | Resumen de las rutas de origen excluidas. |
| `<src>` | La dirección del repositorio del árbol de origen. |
| `<dst>` | La dirección del repositorio del nodo de destino. |

#### Ejemplos {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>La variable `--exclude` las opciones deben ir seguidas de otra opción antes de que `<src>` y `<dst>` argumentos. Por ejemplo:
>
>`vlt rcp -e ".*\.txt" -r`

### Sincronización {#sync}

Permite controlar el servicio de sincronización de bóveda. Sin ningún argumento, este comando intenta poner el directorio de trabajo actual bajo control de sincronización. Si se ejecuta dentro de un cierre de compra vlt, utiliza el filtro y host respectivos para configurar la sincronización. Si se ejecuta fuera de un cierre de compra vlt, registra la carpeta actual para la sincronización solo si el directorio está vacío.

#### Sintaxis {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### Opciones {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | salida detallada. |
| `--force` | forzar la ejecución de ciertos comandos. |
| `-u (--uri) <uri>` | especifica el URI del host de sincronización. |
| `<command>` | sincronizar para ejecutar. |
| `<localPath>` | carpeta local que se va a sincronizar. |

### Códigos de estado {#status-codes}

Los códigos de estado utilizados por VLT son:

* &#39; &#39; no hay modificaciones
* &quot;A&quot; Se Ha Añadido
* &#39;C&#39; en conflicto
* &quot;D&quot; eliminado
* &#39;I&#39; ignorado
* &#39;M&#39; modificado
* &quot;R&quot; sustituido
* &#39;?&#39; el elemento no está bajo control de versiones
* &#39;!&#39; falta el elemento (eliminado por el comando no svn) o está incompleto
* Elemento con versiones &#39;~&#39; obstruido por algún elemento de otro tipo

## Configuración de la sincronización de FileVault {#setting-up-filevault-sync}

El servicio de sincronización de vault se utiliza para sincronizar el contenido del repositorio con una representación local del sistema de archivos y viceversa. Esto se logra instalando un servicio OSGi que escuchará los cambios del repositorio y analizará el contenido del sistema de archivos periódicamente. Utiliza el mismo formato de serialización que vault para asignar el contenido del repositorio al disco.

>[!NOTE]
>
>El servicio de sincronización de bóvedas es una herramienta de desarrollo y es muy desaconsejable usarla en un sistema productivo. Tenga en cuenta también que el servicio solo puede sincronizarse con el sistema de archivos local y no puede utilizarse para el desarrollo remoto.

### Instalación del servicio mediante vlt {#installing-the-service-using-vlt}

La variable `vlt sync install` puede utilizarse para instalar automáticamente el paquete y la configuración del servicio de sincronización de vault.

El paquete se instala a continuación `/libs/crx/vault/install` y el nodo de configuración se crea en `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. Inicialmente, el servicio está habilitado, pero no se configuran raíces de sincronización.

El siguiente ejemplo instala el servicio de sincronización en la instancia CRX accesible por el uri dado.

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### Visualización del estado del servicio {#displaying-the-service-status}

La variable `status` puede utilizarse para mostrar información sobre el servicio de sincronización en ejecución. &quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>La variable `status` no recupera ningún dato activo del servicio, sino que lee la configuración en `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### Adición de una carpeta de sincronización {#adding-a-sync-folder}

La variable `register` se utiliza para añadir una carpeta a la configuración.

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>La variable `register` no déclencheur una sincronización hasta que no configure la variable `sync-once` configuración.

### Eliminación de una carpeta de sincronización {#removing-a-sync-folder}

La variable `unregister` se utiliza para quitar una carpeta que sincronizar desde la configuración.

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>Debe anular el registro de una carpeta de sincronización antes de eliminar la propia carpeta.

### Configuración de la sincronización {#configuring-synchronization}

#### Configuración del servicio {#service-configuration}

Una vez que el servicio se está ejecutando, se puede configurar con los siguientes parámetros:

* `vault.sync.syncroots`: Una o varias rutas de filesystem locales que definen las raíces de sincronización.

* `vault.sync.fscheckinterval`: Frecuencia (en segundos) de la cual el sistema de archivos debe ser analizado para detectar cambios. El valor predeterminado es de 5 segundos.
* `vault.sync.enabled`: Indicador general que habilita/deshabilita el servicio.

>[!NOTE]
>
>El servicio se puede configurar con la consola web o con un `sling:OsgiConfig` nodo (con el nombre `com.day.jcr.sync.impl.VaultSyncServiceImpl`) en el repositorio.
>
>Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios; see [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información.

#### Configuración de la carpeta de sincronización {#sync-folder-configuration}

Cada carpeta de sincronización almacena la configuración y el estado en tres archivos:

* `.vlt-sync-config.properties`: archivo de configuración.

* `.vlt-sync.log`: archivo de registro que contiene información sobre las operaciones realizadas durante la sincronización.
* `.vlt-sync-filter.xml`: filtros que definen qué partes del repositorio se sincronizan. El formato de este archivo se describe mediante la variable [Realización de un cierre de compra filtrado](#performing-a-filtered-checkout) para obtener más información.

La variable `.vlt-sync-config.properties` permite configurar las siguientes propiedades:

**disabled** Activa o desactiva la sincronización. De forma predeterminada, este parámetro se establece en false para permitir la sincronización.

**sync-once** Si no está vacío, el siguiente análisis sincronizará la carpeta en la dirección dada, se borrará el parámetro. Se admiten dos valores:

* `JCR2FS`: exporta todo el contenido del repositorio JCR y escribe en el disco local.
* `FS2JCR`: importa todo el contenido del disco en el repositorio JCR.

**sync-log** Define el nombre del archivo de registro. De forma predeterminada, el valor es .vlt-sync.log

### Uso de la sincronización de VLT para el desarrollo {#using-vlt-sync-for-development}

Para configurar un entorno de desarrollo basado en una carpeta de sincronización, siga estos pasos:

1. Cierre el repositorio con la línea de comandos vlt:

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >Puede utilizar filtros para extraer solo las rutas adecuadas. Consulte la [Realización de un cierre de compra filtrado](#performing-a-filtered-checkout) para obtener más información.

1. Vaya a la carpeta raíz de su copia de trabajo:

   ```shell
   $ cd dev/jcr_root/
   ```

1. Instale el servicio de sincronización en el repositorio:

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. Inicialice el servicio de sincronización:

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. Edite el `.vlt-sync-config.properties` archivo oculto y configure la sincronización para sincronizar el contenido del repositorio:

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >Este paso descarga todo el repositorio según la configuración del filtro.

1. Comprobar el archivo de registro `.vlt-sync.log` para ver el progreso:

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

La carpeta local ahora se sincroniza con el repositorio. La sincronización es bidireccional, por lo que la modificación del repositorio se aplicará a la carpeta de sincronización local y viceversa.

>[!NOTE]
>
>La función de sincronización de VLT solo admite archivos y carpetas simples, pero detecta archivos serializados de bóveda especiales (.content.xml, dialog.xml, etc.) y los ignora en silencio. Por lo tanto, es posible utilizar la sincronización de bóveda en un cierre de compra de vlt predeterminado.
