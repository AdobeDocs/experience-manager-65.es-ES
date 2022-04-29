---
title: Uso de la herramienta de migración CRX2Oak
seo-title: Using the CRX2Oak Migration Tool
description: Aprenda a utilizar la herramienta de migración CRX2Oak.
seo-description: Learn how to use the CRX2Oak migration tool.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
source-git-commit: 08e7cbe50fbfb301b38c3c36dfa22bfc1024e181
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 0%

---

# Uso de la herramienta de migración CRX2Oak{#using-the-crx-oak-migration-tool}

## Introducción {#introduction}

CRX2Oak es una herramienta diseñada para migrar datos entre diferentes repositorios.

Se puede utilizar para migrar datos de versiones de CQ anteriores basadas en Apache Jackrabbit 2 a Oak, y también se puede utilizar para copiar datos entre repositorios Oak.

Puede descargar la versión más reciente de crx2oak desde el repositorio de Adobe público en esta ubicación:
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

La lista de cambios y correcciones para la versión más reciente se encuentra en la [Notas de la versión CRX2Oak](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/crx2oak.html).

>[!NOTE]
>
>Para obtener más información sobre Apache Oak y los conceptos clave de AEM resistencia, consulte [Introducción a la plataforma AEM](/help/sites-deploying/platform.md).

## Casos de uso de migración {#migration-use-cases}

La herramienta se puede utilizar para:

* Migración de versiones anteriores de CQ5 a AEM 6
* Copia de datos entre varios repositorios Oak
* Conversión de datos entre diferentes implementaciones de Oak MicroKernel.

La compatibilidad con la migración de repositorios utilizando Blob Stores externos (comúnmente conocidos como Data Stores) se proporciona en diferentes combinaciones. Una posible ruta de migración es desde un repositorio CRX2 que está usando un `FileDataStore` a un repositorio de Oak usando un `S3DataStore`.

El diagrama siguiente ilustra todas las combinaciones de migración posibles admitidas por CRX2Oak:

![chlimage_1-151](assets/chlimage_1-151.png)

## Características {#features}

Se llama a CRX2Oak durante AEM actualizaciones de forma que el usuario pueda especificar un perfil de migración predefinido que automatice la reconfiguración de los modos de persistencia. Esto se denomina modo de inicio rápido.

También se puede ejecutar por separado en caso de que requiera más personalización. Sin embargo, tenga en cuenta que en este modo solo se realizan cambios en el repositorio y que cualquier reconfiguración adicional de AEM debe realizarse manualmente. Esto se denomina modo independiente.

Otra cosa a tener en cuenta es que con la configuración predeterminada en modo independiente, solo se migrará el almacén de nodos y el nuevo repositorio reutilizará el antiguo almacenamiento binario.

### Modo de inicio rápido automatizado {#automated-quickstart-mode}

Desde AEM 6.3, CRX2Oak es capaz de gestionar perfiles de migración definidos por el usuario que pueden configurarse con todas las opciones de migración ya disponibles. Esto permite una mayor flexibilidad y la capacidad de automatizar la configuración de AEM funciones que no están disponibles si utiliza la herramienta en modo independiente.

Para cambiar CRX2Oak al modo de inicio rápido, debe definir la ruta a la carpeta crx-quickstart en el directorio de instalación de AEM a través de esta variable ambiental del sistema operativo:

**Para sistemas basados en UNIX y macOS:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Para Windows:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### Reanudar compatibilidad {#resume-support}

La migración se puede interrumpir en cualquier momento, con la posibilidad de reanudarla posteriormente.

#### Lógica de actualización personalizable {#customizable-upgrade-logic}

La lógica personalizada de Java también se puede implementar mediante `CommitHooks`. Personalizado `RepositoryInitializer` se pueden implementar para inicializar el repositorio con valores personalizados.

#### Compatibilidad con operaciones asignadas a memoria {#support-for-memory-mapped-operations}

CRX2Oak también admite operaciones asignadas a memoria de forma predeterminada. La asignación de memoria mejora considerablemente el rendimiento y debe utilizarse siempre que sea posible.

>[!CAUTION]
>
>Sin embargo, tenga en cuenta que las operaciones asignadas a memoria no son compatibles con las plataformas Windows. Por lo tanto, se recomienda añadir la variable **—disable-mmap** al realizar la migración en Windows.

#### Migración selectiva de contenido {#selective-migration-of-content}

De forma predeterminada, la herramienta migra todo el repositorio bajo el `"/"` ruta. Sin embargo, tiene control absoluto sobre qué contenido se debe migrar.

Si hay alguna parte del contenido que no sea necesaria en la nueva instancia, puede usar la variable `--exclude-path` para excluir el contenido y optimizar el procedimiento de actualización.

#### Combinación de rutas {#path-merging}

Si es necesario copiar los datos entre dos repositorios y si tiene una ruta de contenido diferente en ambas instancias, puede definirlos en la variable `--merge-path` parámetro. Una vez que lo haga, CRX2Oak copiará solamente los nuevos nodos en el repositorio de destino y mantendrá los antiguos en su lugar.

![chlimage_1-152](assets/chlimage_1-152.png)

#### Compatibilidad con versiones {#version-support}

De forma predeterminada, AEM creará una versión de cada nodo o página que se modifique y la almacenará en el repositorio. A continuación, se pueden usar las versiones para restaurar la página a un estado anterior.

Sin embargo, estas versiones nunca se depuran aunque se elimine la página original. Cuando se trata de repositorios que han estado en funcionamiento durante mucho tiempo, es posible que la migración necesite procesar muchos datos redundantes causados por versiones huérfanas.

Una característica útil para estos tipos de situaciones es la adición de la variable `--copy-versions` parámetro. Se puede utilizar para omitir los nodos de versión durante la migración o la copia de un repositorio.

También puede elegir si desea copiar versiones huérfanas agregando `--copy-orphaned-versions=true`.

Ambos parámetros también admiten una `YYYY-MM-DD` formato de fecha, en caso de que desee copiar versiones a más tardar en una fecha específica.

![chlimage_1-153](assets/chlimage_1-153.png)

#### Abrir versión de origen {#open-source-version}

Una versión de código abierto de CRX2Oak está disponible en forma de oak-upgrade. Admite todas las funciones excepto:

* Compatibilidad con CRX2
* Compatibilidad con el perfil de migración
* Compatibilidad con la reconfiguración AEM automatizada

Consulte la [Documentación de Apache](https://jackrabbit.apache.org/oak/docs/migration.html) para obtener más información.

## Parámetros {#parameters}

### Opciones del almacén de nodos {#node-store-options}

* `--cache`: Tamaño de caché en MB (el valor predeterminado es `256`)

* `--mmap`: Habilitar el acceso a archivos asignado a memoria para el almacén de segmentos
* `--src-password:` Contraseña de la base de datos RDB de origen

* `--src-user:` Usuario para la RDB de origen

* `--user`: Usuario para la RDB de destino

* `--password`: Contraseña para la RDB de destino.

### Opciones de migración {#migration-options}

* `--early-shutdown`: Cierra el repositorio JCR2 de origen después de que se copien los nodos y antes de que se apliquen los enlaces de confirmación
* `--fail-on-error`: Fuerza un error en la migración si los nodos no se pueden leer desde el repositorio de origen.
* `--ldap`: Migra los usuarios LDAP de una instancia CQ 5.x a una instancia basada en Oak. Para que esto funcione, el proveedor de identidad en la configuración de Oak debe llamarse ldap. Para obtener más información, consulte la [Documentación LDAP](/help/sites-administering/ldap-config.md).

* `--ldap-config:` Utilícelo junto con la variable `--ldap` para repositorios CQ 5.x que usaban varios servidores LDAP para la autenticación. Puede usarlo para apuntar a CQ5.x `ldap_login.conf` o `jaas.conf` archivos de configuración. El formato es `--ldapconfig=path/to/ldap_login.conf`.

### Opciones del almacén de versiones {#version-store-options}

* `--copy-orphaned-versions`: Omite copiar versiones huérfanas. Los parámetros admitidos son: `true`, `false` y `yyyy-mm-dd`. El valor predeterminado es `true`.

* `--copy-versions:` Copia el almacenamiento de la versión. Parámetros: `true`, `false`, `yyyy-mm-dd`. El valor predeterminado es `true`.

#### Opciones de ruta {#path-options}

* `--include-paths:` Lista separada por comas de las rutas que se incluirán durante la copia
* `--merge-paths`: Lista separada por comas de las rutas que se van a combinar durante la copia
* `--exclude-paths:` Lista de rutas de exclusión durante la copia separadas por comas.

### Opciones del almacén de blob de origen {#source-blob-store-options}

* `--src-datastore:` El directorio del almacén de datos que se utilizará como origen `FileDataStore`

* `--src-fileblobstore`: El directorio del almacén de datos que se utilizará como origen `FileBlobStore`

* `--src-s3datastore`: El directorio del almacén de datos que se utilizará para el origen `S3DataStore`

* `--src-s3config`: El archivo de configuración del origen `S3DataStore`.

### Opciones de BlobStore de destino {#destination-blobstore-options}

* `--datastore:` El directorio del almacén de datos que se utilizará como destino `FileDataStore`

* `--fileblobstore:` El directorio del almacén de datos que se utilizará como destino `FileBlobStore`

* `--s3datastore`: El directorio del almacén de datos que se utilizará para el destino `S3DataStore`

* `--s3config`: El archivo de configuración para el destino `S3DataStore`.

### Opciones de ayuda {#help-options}

* `-?, -h, --help:` Muestra información de ayuda.

## Depuración {#debugging}

También puede habilitar la información de depuración para el proceso de migración para solucionar cualquier problema que pueda aparecer durante el proceso. Puede hacerlo de forma diferente en función del modo en el que desee ejecutar la herramienta:

<table>
 <tbody>
  <tr>
   <td><strong>Modo CRX2Oak</strong></td>
   <td><strong>Acción</strong></td>
  </tr>
  <tr>
   <td>Modo de inicio rápido</td>
   <td>Puede añadir la variable <strong>—TRACE de nivel de registro</strong> o <strong>—DEBUG de nivel de registro </strong>al ejecutar CRX2Oak. En este modo, los registros se redirigen automáticamente a la variable <strong>archivo upgrade.log</strong>.</td>
  </tr>
  <tr>
   <td>Modo independiente</td>
   <td><p>Agregue la variable <strong>—trace</strong> opciones a la línea de comandos CRX2Oak para mostrar eventos de TRACE en salida estándar (necesita redirigir los registros usted mismo usando el carácter de redirección: '&gt;' o 'tee' para inspección posterior).</p> </td>
  </tr>
 </tbody>
</table>

## Otras consideraciones {#other-considerations}

Al migrar a un conjunto de réplicas de MongoDB, asegúrese de establecer la variable `WriteConcern` parámetro a `2` en todas las conexiones a las bases de datos de Mongo.

Para ello, agregue la variable `w=2` al final de la cadena de conexión, así:

```xml
java -Xmx4092m -XX:MaxPermSize=1024m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>Para obtener más información, consulte la documentación de la cadena de conexión MongoDB en [Escribir preocupaciones](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).
