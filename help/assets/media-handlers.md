---
title: Procesar recursos con controladores de medios y flujos de trabajo
description: Obtenga información sobre los controladores de medios y cómo utilizar los flujos de trabajo para realizar tareas en los recursos digitales.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Procesar recursos con controladores de medios y flujos de trabajo {#processing-assets-using-media-handlers-and-workflows}

Recursos Adobe Experience Manager (AEM) incluye un conjunto de flujos de trabajo predeterminados y controladores de medios para procesar recursos. El flujo de trabajo define las tareas generales que se van a ejecutar en los recursos y, a continuación, delega las tareas específicas a los controladores de medios, como la generación de miniaturas o la extracción de metadatos.

Se puede definir un flujo de trabajo que se ejecutará automáticamente cuando se cargue un recurso de un tipo concreto en el servidor. Los pasos de procesamiento se definen en función de una serie de controladores de medios de AEM Assets. AEM proporciona algunos controladores [integrados,](#default-media-handlers) y otros adicionales se pueden [personalizar, desarrollar](#creating-a-new-media-handler) o definir delegando el proceso en una herramienta [de línea de](#command-line-based-media-handler)comandos.

Los controladores de medios son servicios dentro de Recursos AEM que realizan acciones específicas en los recursos. Por ejemplo, cuando se carga un archivo de audio MP3 en AEM, un flujo de trabajo activa un controlador MP3 que extrae los metadatos y genera una miniatura. Los controladores de medios generalmente se utilizan en combinación con flujos de trabajo. Los tipos MIME más comunes son compatibles con AEM. Se pueden realizar tareas específicas en los recursos ampliando/creando flujos de trabajo, ampliando/creando controladores de medios o deshabilitando/habilitando controladores de medios.

>[!NOTE]
>
>Consulte la página Formatos [admitidos de](assets-formats.md) Recursos para obtener una descripción de todos los formatos admitidos por Recursos AEM, así como de las funciones admitidas para cada formato.

## Controladores de medios predeterminados {#default-media-handlers}

Los siguientes controladores de medios están disponibles en Recursos AEM y controlan los tipos MIME más comunes:

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

| Nombre del controlador | Nombre del servicio (en la consola del sistema) | Tipos MIME admitidos |
|---|---|---|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>aplicación/ilustrador</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | imagen/imagen |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>aplicación/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.xml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | alternativa en caso de que no se encontrara ningún otro controlador para extraer datos de un recurso |

Todos los controladores realizan las siguientes tareas:

* extraer todos los metadatos disponibles del recurso.
* crear una imagen en miniatura a partir del recurso.

Es posible ver los controladores de medios activos:

1. In your browser, navigate to `http://localhost:4502/system/console/components`.
1. Haga clic en el vínculo `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Se muestra una lista con todos los controladores de medios activos. Por ejemplo:

![chlimage_1-437](assets/chlimage_1-437.png)

## Uso de controladores de medios en flujos de trabajo para realizar tareas en recursos {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

Los controladores de medios son servicios que generalmente se utilizan en combinación con flujos de trabajo.

AEM tiene algunos flujos de trabajo predeterminados para procesar recursos. Para verlos, abra la consola Flujo de trabajo y haga clic en la ficha **[!UICONTROL Modelos]** : los títulos de flujo de trabajo que comienzan con Recursos AEM son los específicos de los recursos.

Los flujos de trabajo existentes se pueden ampliar y se pueden crear nuevos para procesar recursos según requisitos específicos.

En el siguiente ejemplo se muestra cómo mejorar el flujo de trabajo de sincronización **[!UICONTROL de recursos de]** AEM para que se generen subrecursos para todos los recursos, excepto para los documentos PDF.

### Deshabilitar o habilitar un controlador de medios {#disabling-enabling-a-media-handler}

Los controladores de medios pueden deshabilitarse o habilitarse a través de la consola de administración web Apache Felix. Cuando el controlador de medios está desactivado, sus tareas no se realizan en los recursos.

Para habilitar/deshabilitar un controlador de medios:

1. In your browser, navigate to `https://<host>:<port>/system/console/components`.
1. Haga clic en **[!UICONTROL Deshabilitar]** junto al nombre del controlador de medios. Por ejemplo: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Actualice la página: se muestra un icono junto al controlador de medios que indica que está deshabilitado.
1. Para habilitar el controlador de medios, haga clic en **[!UICONTROL Habilitar]** junto al nombre del controlador de medios.

### Crear un nuevo controlador de medios {#creating-a-new-media-handler}

Para admitir un nuevo tipo de medio o para ejecutar tareas específicas en un recurso, es necesario crear un nuevo controlador de medios. En esta sección se describe cómo proceder.

#### Clases e interfaces importantes {#important-classes-and-interfaces}

La mejor manera de iniciar una implementación es heredar de una implementación abstracta proporcionada que se ocupa de la mayoría de las cosas y proporciona un comportamiento predeterminado razonable: la `com.day.cq.dam.core.AbstractAssetHandler` clase.

Esta clase ya proporciona un descriptor de servicio abstracto. Si hereda de esta clase y utiliza el complemento maven-sling, asegúrese de establecer el indicador inherit en `true`.

Implemente los siguientes métodos:

* `extractMetadata()`:: extrae todos los metadatos disponibles.
* `getThumbnailImage()`:: crea una imagen en miniatura a partir del recurso pasado.
* `getMimeTypes()`:: devuelve los tipos MIME del recurso.

Esta es un ejemplo de plantilla:

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

La interfaz y las clases incluyen:

* `com.day.cq.dam.api.handler.AssetHandler` interfaz: Esta interfaz describe el servicio que agrega compatibilidad para tipos de MIME específicos. Para implementar esta interfaz es necesario agregar un nuevo tipo de MIME. La interfaz contiene métodos para importar y exportar documentos específicos, para crear miniaturas y extraer metadatos.
* `com.day.cq.dam.core.AbstractAssetHandler` class: Esta clase sirve de base para todas las demás implementaciones de controladores de recursos y proporciona funcionalidad común.
* `com.day.cq.dam.core.AbstractSubAssetHandler` clase:
   * Esta clase sirve de base para todas las demás implementaciones de controladores de recursos y proporciona una funcionalidad común utilizada, además de una funcionalidad común utilizada para la extracción de subrecursos.
   * La mejor manera de iniciar una implementación es heredar de una implementación abstracta proporcionada que se ocupa de la mayoría de las cosas y proporciona un comportamiento predeterminado razonable: la clase com.day.cq.dam.core.AbstractAssetHandler.
   * Esta clase ya proporciona un descriptor de servicio abstracto. Si hereda de esta clase y utiliza el complemento maven-sling, asegúrese de establecer el indicador inherit en true.

Es necesario implementar los siguientes métodos:

* `extractMetadata()`:: este método extrae todos los metadatos disponibles.
* `getThumbnailImage()`:: este método crea una imagen en miniatura a partir del recurso pasado.
* `getMimeTypes()`:: este método devuelve los tipos de MIME de los recursos.

Esta es un ejemplo de plantilla:

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ clase pública MyMediaHandler amplía com.day.cq.dam.core.AbstractAssetHandler { // implementa las partes relevantes }

La interfaz y las clases incluyen:

* `com.day.cq.dam.api.handler.AssetHandler` interfaz: Esta interfaz describe el servicio que agrega compatibilidad para tipos de MIME específicos. Para implementar esta interfaz es necesario agregar un nuevo tipo de MIME. La interfaz contiene métodos para importar y exportar documentos específicos, para crear miniaturas y extraer metadatos.
* `com.day.cq.dam.core.AbstractAssetHandler` class: Esta clase sirve de base para todas las demás implementaciones de controladores de recursos y proporciona funcionalidad común.
* `com.day.cq.dam.core.AbstractSubAssetHandler` class:Esta clase sirve de base para todas las demás implementaciones de controladores de recursos y proporciona una funcionalidad común utilizada, además de una funcionalidad común utilizada para la extracción de subrecursos.

#### Ejemplo: crear un controlador de texto específico {#example-create-a-specific-text-handler}

En esta sección, creará un controlador de texto específico que genere miniaturas con una marca de agua.

Proceda de la siguiente manera:

Consulte Herramientas [de](../sites-developing/dev-tools.md) desarrollo para instalar y configurar Eclipse con un complemento Maven y para configurar las dependencias necesarias para el proyecto Maven.

Después de realizar el siguiente procedimiento, al cargar un archivo de texto en AEM, se extraen los metadatos del archivo y se generan dos miniaturas con una marca de agua.

1. En Eclipse, cree un proyecto `myBundle` Maven:

   1. En la barra de menús, haga clic en **[!UICONTROL Archivo > Nuevo > Otro]**.
   1. En el cuadro de diálogo, expanda la carpeta Maven, seleccione Maven Project y haga clic en **[!UICONTROL Siguiente]**.
   1. Marque la casilla Crear un proyecto simple y la casilla Usar ubicaciones de espacio de trabajo predeterminadas y, a continuación, haga clic en **[!UICONTROL Siguiente]**.
   1. Defina el proyecto Maven:

      * Id Del Grupo: com.day.cq5.myhandler
      * ID del artefacto: myBundle
      * Nombre: Mi paquete AEM
      * Descripción: Este es mi paquete de AEM
   1. Click **[!UICONTROL Finish]**.


1. Establezca el compilador de Java en la versión 1.5:

   1. Haga clic con el botón secundario en el `myBundle` proyecto y seleccione Propiedades.
   1. Seleccione Java Compiler y defina las siguientes propiedades en 1.5:

      * Nivel de cumplimiento del compilador
      * Compatibilidad generada con archivos .class
      * Compatibilidad de origen
   1. Haga clic en **[!UICONTROL Aceptar]**. En la ventana de diálogo, haga clic en Sí.


1. Reemplace el código del archivo pom.xml con el siguiente código:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. Cree el paquete `com.day.cq5.myhandler` que contiene las clases de Java en `myBundle/src/main/java`:

   1. En myBundle, haga clic con el botón derecho `src/main/java`, seleccione Nuevo y, a continuación, Empaquetar.
   1. Asígnele un nombre `com.day.cq5.myhandler` y haga clic en Finalizar.

1. Cree la clase Java `MyHandler`:

   1. En Eclipse, en `myBundle/src/main/java`, haga clic con el botón derecho en el `com.day.cq5.myhandler` paquete, seleccione Nuevo y, a continuación, Clase.
   1. En la ventana de diálogo, asigne un nombre a la clase Java MyHandler y haga clic en Finalizar. Eclipse crea y abre el archivo MyHandler.java.
   1. En `MyHandler.java` sustituya el código existente por el siguiente y, a continuación, guarde los cambios:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile la clase Java y cree el paquete:

   1. Haga clic con el botón secundario en el proyecto myBundle, seleccione **[!UICONTROL Ejecutar como]** y, a continuación, **[!UICONTROL Maven Install]**.
   1. El paquete `myBundle-0.0.1-SNAPSHOT.jar` (que contiene la clase compilada) se crea en `myBundle/target`.

1. En el Explorador de CRX, cree un nuevo nodo en `/apps/myApp`. Nombre = `install`, Tipo = `nt:folder`.
1. Copie el paquete `myBundle-0.0.1-SNAPSHOT.jar` y guárdelo en `/apps/myApp/install` (por ejemplo, con WebDAV). El nuevo controlador de texto ahora está activo en AEM.
1. En el navegador, abra la consola de gestión web Apache Felix. Seleccione la ficha Componentes y desactive el controlador de texto predeterminado `com.day.cq.dam.core.impl.handler.TextHandler`.

## Controlador de medios basado en línea de comandos {#command-line-based-media-handler}

AEM le permite ejecutar cualquier herramienta de línea de comandos dentro de un flujo de trabajo para convertir recursos (como ImageMagick) y añadir la nueva representación al recurso. Solo necesita instalar la herramienta de línea de comandos en el disco que aloja el servidor AEM y agregar y configurar un paso de proceso al flujo de trabajo. El proceso invocado, llamado `CommandLineProcess`, también permite filtrar según tipos MIME específicos y crear varias miniaturas basadas en la nueva representación.

Las siguientes conversiones se pueden ejecutar y almacenar automáticamente en Recursos AEM:

* Transformación de EPS y AI mediante [ImageMagick](https://www.imagemagick.org/script/index.php) y [Ghostscript](https://www.ghostscript.com/)
* Transcodificación de vídeo FLV mediante [FFmpeg](https://ffmpeg.org/)
* Codificación MP3 con [LAME](http://lame.sourceforge.net/)
* Procesamiento de audio mediante [SOX](http://sox.sourceforge.net/)

>[!NOTE]
>
>En sistemas que no son de Windows, la herramienta FFMpeg devuelve un error al generar representaciones para un recurso de vídeo que tiene una sola comilla (&#39;) en el nombre de archivo. Si el nombre del archivo de vídeo incluye una sola cita, elimínelo antes de cargarlo en AEM.

El `CommandLineProcess` proceso realiza las siguientes operaciones en el orden en que aparecen:

* Filtra el archivo según tipos de MIME específicos, si se especifica.
* Crea un directorio temporal en el disco que aloja el servidor AEM.
* Transmite el archivo original al directorio temporal.
* Ejecuta el comando definido por los argumentos del paso. El comando se está ejecutando en el directorio temporal con los permisos del usuario que ejecuta AEM.
* Vuelve a transmitir el resultado a la carpeta de representación del servidor AEM.
* Elimina el directorio temporal.
* Crea miniaturas basadas en esas representaciones, si se especifican. El número y las dimensiones de las miniaturas se definen mediante los argumentos del paso.

### Ejemplo de uso de ImageMagick {#an-example-using-imagemagick}

En el siguiente ejemplo se muestra cómo configurar el paso del proceso de la línea de comandos para que cada vez que se añada un recurso con el tipo mime gif o tiff a /content/dam en el servidor AEM, se cree una imagen volteada del original junto con tres miniaturas adicionales (140 x 100, 48 x 48 y 10 x 250).

Para ello, utilizará ImageMagick. ImageMagick es un conjunto de software libre para crear, editar y componer imágenes de mapa de bits y se utiliza generalmente desde la línea de comandos.

Primera instalación de ImageMagick en el disco que aloja el servidor AEM:

1. Instalar ImageMagick: consulte la documentación [de ImageMagick](https://www.imagemagick.org/script/download.php).
1. Configure la herramienta para que pueda ejecutar la conversión en la línea de comandos.
1. Para ver si la herramienta está instalada correctamente, ejecute el siguiente comando `convert -h` en la línea de comandos.

   Muestra una pantalla de ayuda con todas las opciones posibles de la herramienta de conversión.

   >[!NOTE]
   >
   >En algunas versiones de Windows (por ejemplo, Windows SE), el comando convert puede no ejecutarse porque está en conflicto con la utilidad de conversión nativa que forma parte de la instalación de Windows. En este caso, mencione la ruta completa de la utilidad ImageMagick utilizada para convertir archivos de imagen en miniaturas. Por ejemplo, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Para ver si la herramienta se ejecuta correctamente, agregue una imagen .jpg al directorio de trabajo y ejecute el comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` en la línea de comandos.

   Se agrega una imagen volteada al directorio.

A continuación, agregue el paso del proceso de la línea de comandos al flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM:

1. Vaya a la consola **[!UICONTROL Flujo de trabajo]** .
1. En la ficha **[!UICONTROL Modelos]** , edite el modelo **[!UICONTROL DAM Update Asset]** .
1. Cambie la configuración de la representación **[!UICONTROL habilitada para]** Web de la siguiente manera:

   **Argumentos**:

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. Guarde el flujo de trabajo.

Para probar el flujo de trabajo modificado, agregue un recurso a `/content/dam`.

1. En el sistema de archivos, obtenga una imagen .tiff de su elección. Cambie su nombre `myImage.tiff` y cópielo en `/content/dam`, por ejemplo, mediante WebDAV.
1. Vaya a la consola **[!UICONTROL CQ5 DAM]** , por ejemplo `http://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Abra el recurso **[!UICONTROL myImage.tiff]** y compruebe que se hayan creado la imagen volteada y las tres miniaturas.

#### Configuración del paso del proceso CommandLineProcess {#configuring-the-commandlineprocess-process-step}

En esta sección se describe cómo establecer los argumentos **de** proceso de **CommandLineProcess**.

Los valores de los argumentos **de** proceso deben separarse con una coma y no deben comenzar con un espacio en blanco.

| Argument-Format | Descripción |
|---|---|
| mime:&lt;tipo-mime> | Argumento opcional. El proceso se aplica si el recurso tiene el mismo tipo MIME que el argumento. <br>Se pueden definir varios tipos de MIME. |
| tn:&lt;anchura>:&lt;altura> | Argumento opcional. El proceso crea una miniatura con las dimensiones definidas en el argumento. <br>Se pueden definir varias miniaturas. |
| cmd: &lt;comando> | Define el comando que se ejecutará. La sintaxis depende de la herramienta de línea de comandos. Sólo se puede definir un comando. <br>Se pueden utilizar las siguientes variables para crear el comando:<br>`${filename}`nombre del archivo de entrada, por ejemplo original.jpg <br> `${file}`:: nombre completo de ruta del archivo de entrada, por ejemplo /tmp/cqdam0816.tmp/original.jpg <br> `${directory}`:: directorio del archivo de entrada, por ejemplo /tmp/cqdam0816.tmp <br>`${basename}`: nombre del archivo de entrada sin su extensión, por ejemplo original <br>`${extension}`: extensión del archivo de entrada, por ejemplo jpg |

Por ejemplo, si ImageMagick está instalado en el disco que aloja el servidor AEM y crea un paso de proceso mediante **CommandLineProcess** como Implementación y los siguientes valores como Argumentos **de** proceso:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

a continuación, cuando se ejecuta el flujo de trabajo, el paso solo se aplica a los recursos que tienen tipo mime/gif o mime:image/tiff, crea una imagen al revés del original, la convierte en .jpg y crea tres miniaturas con las dimensiones siguientes: 140 x 100, 48 x 48 y 10 x 250.

Utilice los siguientes argumentos **de proceso** para crear las tres miniaturas estándar con ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Utilice los siguientes argumentos **de proceso** para crear la representación con web habilitada mediante ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>El paso **CommandLineProcess** solo se aplica a los recursos (nodos de tipo `dam:Asset`) o descendientes de un recurso.
