---
title: Extracción de cadenas para traducir
seo-title: Extracción de cadenas para traducir
description: Utilice xgettext-maven-plugin para extraer cadenas del código fuente que necesiten traducir
seo-description: Utilice xgettext-maven-plugin para extraer cadenas del código fuente que necesiten traducir
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Extracción de cadenas para traducir{#extracting-strings-for-translating}

Utilice xgettext-maven-plugin para extraer cadenas del código fuente que necesiten traducir. El complemento Maven extrae cadenas en un archivo XLIFF que envía para su traducción. Las cadenas se extraen de las siguientes ubicaciones:

* Archivos de origen Java
* Archivos de origen Javascript
* Representaciones XML de recursos SVN (nodos JCR)

## Configuración de la Extracción de cadena {#configuring-string-extraction}

Configure cómo la herramienta xgettext-maven-plugin extrae cadenas para el proyecto.

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| Sección | Descripción |
|---|---|
| /filter | Identifica los archivos analizados. |
| /parsers/vaultxml | Configura el análisis de los archivos Vault. Identifica los nodos JCR que contienen cadenas y sugerencias de localización externalizadas. También identifica los nodos JCR que se deben ignorar. |
| /parsers/javascript | Identifica las funciones de Javascript que externalizan cadenas. No es necesario cambiar esta sección. |
| /parsers/regexp | Configura el análisis de los archivos de plantilla Java, JSP y ExtJS. No es necesario cambiar esta sección. |
| /potenciales | Fórmula para detectar cadenas que se van a internacionalizar. |

### Identificación de los archivos que analizar {#identifying-the-files-to-parse}

La sección /filter del archivo i18n.any identifica los archivos que analiza la herramienta xgettext-maven-plugin. Añada varias reglas de inclusión y exclusión que identifican los archivos analizados e ignorados, respectivamente. Debe incluir todos los archivos y luego excluir los archivos que no desee analizar. Normalmente, excluye los tipos de archivo que no contribuyen a la interfaz de usuario o los archivos que definen la interfaz de usuario pero que no se están traduciendo. Las reglas de inclusión y exclusión tienen el siguiente formato:

```
{ /include "pattern" }
{ /exclude "pattern" }
```

La parte de patrón de una regla se utiliza para coincidir con los nombres de los archivos que se van a incluir o excluir. El prefijo de patrón indica si está haciendo coincidir un nodo JCR (su representación en Vault) o el sistema de archivos.

| Prefijo | Efecto |
|---|---|
| / | Indica una ruta JCR. Por lo tanto, este prefijo coincide con los archivos situados debajo del directorio jcr_root. |
| &amp;ast; | Indica un archivo normal en el sistema de archivos. |
| ninguno | Ningún prefijo, o patrón que comience por un nombre de archivo o carpeta, indica un archivo normal en el sistema de archivos. |

Cuando se utiliza dentro de un patrón, el carácter / indica un subdirectorio y el &amp;ast; coincide con todos. La tabla siguiente lista varias reglas de ejemplo.

<table>
 <tbody>
  <tr>
   <th>Regla de ejemplo</th>
   <th>Efecto</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>Incluir todos los archivos.</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>Excluya todos los archivos PDF.</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>Excluir archivos POM.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>Excluya todos los archivos situados debajo del nodo /content.</p> <p>Incluya el nodo /content/catalogs/geometrixx/templatepages.</p> <p>Incluya todos los nodos secundarios de /content/catalogs/geometrixx/templatepages.</p> </td>
  </tr>
 </tbody>
</table>

### Extracción de cadenas {#extracting-the-strings}

sin POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

Con POM: Añada esto a POM:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

el comando:

```shell
mvn xgettext:extract
```

### Archivos de salida {#output-files}

* `raw.xliff`:: cadenas extraídas
* `warn.log`:: advertencias (si las hay), si  `CQ.I18n.getMessage()` la API se utiliza incorrectamente. Siempre necesitan una corrección y luego una repetición.

* `parserwarn.log`:: advertencias del analizador (si las hay), por ejemplo problemas con el analizador de js
* `potentials.xliff`:: Los candidatos &quot;potenciales&quot; que no se extraen, pero que pueden ser cadenas legibles por el hombre que necesitan traducción (se puede ignorar, y aun así produce una gran cantidad de falsos positivos)
* `strings.xliff`:: archivo xliff acoplado, que se importará en ALF
* `backrefs.txt`:: permite una búsqueda rápida de ubicaciones de código fuente para una cadena determinada

