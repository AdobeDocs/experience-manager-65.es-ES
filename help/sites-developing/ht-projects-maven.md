---
title: Cómo crear proyectos de AEM con Apache Maven
seo-title: Cómo crear proyectos de AEM con Apache Maven
description: Este documento describe cómo configurar un proyecto de AEM basado en Apache Maven
seo-description: Este documento describe cómo configurar un proyecto de AEM basado en Apache Maven
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: 9d42526ff4c7b7d8a31690ebfb8b45d0e951ebac

---


# Cómo crear proyectos de AEM con Apache Maven{#how-to-build-aem-projects-using-apache-maven}

## Información general {#overview}

Este documento describe cómo configurar un proyecto de AEM basado en [Apache Maven](https://maven.apache.org/).

Apache Maven es una herramienta de código abierto para administrar proyectos de software automatizando las compilaciones y proporcionando información de calidad sobre los proyectos. Es la herramienta de administración de compilación recomendada para los proyectos de AEM.

La creación de un proyecto de AEM basado en Maven le ofrece varias ventajas:

* Un entorno de desarrollo basado en IDE
* Uso de los tipos y artefactos de Maven proporcionados por Adobe
* Uso de conjuntos de herramientas de Apache Sling y Apache Felix para configuraciones de desarrollo basadas en Maven
* Facilidad de importación en un IDE; por ejemplo, Eclipse y/o IntelliJ
* Fácil integración con sistemas de integración continua

### Arquetipos de proyecto de Maven {#maven-project-archetypes}

Adobe proporciona dos tipos de arquetes Maven que pueden servir de referencia para sus proyectos de AEM. Vea más detalles en los vínculos siguientes:

* [arquetipo de proyecto de AEM](https://github.com/adobe/aem-project-archetype)
* [Kit de inicio de arquetipo Maven para aplicaciones de una sola página](https://github.com/adobe/aem-spa-project-archetype)

## Dependencias de la API de Experience Manager {#experience-manager-api-dependencies}

### ¿Qué es UberJar? {#what-is-the-uberjar}

&quot;UberJar&quot; es el nombre informal que se le da al archivo Java Archives (JAR) especial proporcionado por Adobe. Estos archivos JAR contienen todas las API de Java públicas expuestas por Adobe Experience Manager. También incluyen bibliotecas externas limitadas, específicamente todas las API públicas disponibles en AEM que provienen de Apache Sling, Apache Jackrabbit, Apache Lucene, Google Guava y dos bibliotecas utilizadas para el procesamiento de imágenes (la biblioteca CYMK JPEG ImageIO de Werner Randelshofer y la biblioteca de imágenes de DoceMonkeys). Las UberJars solo contienen interfaces y clases de API, lo que significa que solo contienen interfaces y clases que se exportan mediante un paquete OSGi en AEM. También contienen un archivo *MANIFEST.MF* que contiene las versiones correctas de exportación de paquetes para todos estos paquetes exportados, lo que garantiza que los proyectos creados con UberJar tengan los intervalos correctos de importación de paquetes.

### ¿Por qué ha creado Adobe UberJars? {#why-did-adobe-create-the-uberjars}

En el pasado, los desarrolladores tenían que gestionar un número relativamente grande de dependencias individuales a distintas bibliotecas de AEM y, cuando se utilizaba cada nueva API, se debían añadir al proyecto una o varias dependencias individuales. En un proyecto, la introducción de UberJar tuvo como resultado la eliminación de 30 dependencias distintas del proyecto.

A partir de AEM 6.5, Adobe proporciona dos UberJars: una que incluya interfaces obsoletas y una que elimine dichas interfaces obsoletas. Al hacer referencia a uno explícitamente en tiempo de compilación, los clientes pueden comprender si dependen del código obsoleto.

El segundo Uber Jar elimina todas las clases, métodos y propiedades obsoletas para que los clientes puedan compilar en su contra y comprender si el código personalizado es una prueba futura.

### ¿Qué UberJar usar? {#which-uberjar-to-use}

AEM 6.5 viene con dos sabores de Uber Jar:

1. Uber Jar: incluye solo las interfaces públicas que no están marcadas para su desaprobación. Se **recomienda** usar UberJar para ayudar a que la base de código sea resistente en el futuro y no dependa de las API obsoletas.
1. Uber Jar con API obsoletas: incluye todas las interfaces públicas, incluidas las marcadas para su desaprobación en una versión futura de AEM.

### ¿Cómo se usa UberJars? {#how-to-i-use-the-uberjars}

Si utiliza Apache Maven como sistema de compilación (como sucede en la mayoría de los proyectos Java de AEM), deberá añadir uno o dos elementos al archivo *pom.xml* . El primero es un elemento de *dependencia* que agrega la dependencia real al proyecto:

**Dependencia de Uber Jar *(sin API obsoletas)***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**Dependencia de Uber Jar con API obsoletas**

>[!CAUTION]
>
>Adobe recomienda implementar con Uber Jar que ***no* **contiene las API obsoletas para asegurarse de que las aplicaciones se ejecutarán correctamente en futuras versiones de AEM.
>
>Utilice Uber Jar con compatibilidad con API obsoleta solo en caso de que el código que depende de las API obsoletas no pueda modificarse para adaptarse a los cambios.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

Si su empresa ya está utilizando un Administrador de repositorios de Maven como Sontype Nexus, Apache Archiva o JFrog ArtiFactory, agregue la configuración adecuada a su proyecto para hacer referencia a este administrador de repositorios y agregar el repositorio de Maven de Adobe ([https://repo.adobe.com/nexus/content/groups/public/](https://repo.adobe.com/nexus/content/groups/public/)) a su administrador de repositorios.

Si no utiliza un administrador de repositorio, deberá agregar un elemento de *repositorio* al archivo *pom.xml* :

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### ¿Qué puedo hacer con UberJar? {#what-can-i-do-with-the-uberjar}

Con UberJar, puede compilar código de proyecto que depende de las API de AEM (y de las API utilizadas por los proyectos mencionados anteriormente). También puede generar información sobre OSGi Service Component Runtime (SCR) y OSGi Mettype. Con algunas limitaciones, también puede escribir y ejecutar pruebas unitarias.

### ¿Qué no puedo hacer con UberJar? {#what-can-t-i-do-with-the-uberjar}

Dado que UberJar **solo** contiene API, no es ejecutable y no se puede utilizar para **ejecutar** Adobe Experience Manager. Para ejecutar AEM, necesita el formulario AEM Quickstart, independiente o archivo de aplicaciones web (WAR).

### Ha mencionado limitaciones en las pruebas unitarias. Por favor, explique más. {#you-mentioned-limitations-on-unit-tests-please-explain-further}

Las pruebas unitarias generalmente interactúan con las API del producto de tres maneras diferentes, cada una de las cuales se ve afectada de manera ligeramente diferente por UberJar.

#### Caso de uso 1: Código personalizado que llama a una interfaz de API {#use-case-custom-code-which-calls-a-api-interface}

Este caso, que es el más común, incluye algún código personalizado que ejecuta métodos en una interfaz de Java definida por la API de AEM. La implementación de esta interfaz puede proporcionarse directamente o inyectarse utilizando el patrón de inyección de dependencia. **Este caso de uso se puede manejar con UberJar.**

Un ejemplo de lo primero sería:

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

Un ejemplo de esto último sería:

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

Para realizar una prueba unitaria de cualquiera de estos métodos, un desarrollador utilizaría un marco de trabajo burlador como [JMockit](http://jmockit.github.io), [Mockito](https://mockito.org/), [JMock](https://www.jmock.org/)o [Easymock](https://easymock.org/) para crear un objeto de prueba para la API de AEM a la que se hace referencia. Estas muestras utilizan JMockit, pero para este caso de uso en particular, la diferencia entre estos marcos es en gran medida sintética.

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### Caso de uso 2: Código personalizado que llama a una clase de implementación de API {#use-case-custom-code-which-calls-an-api-implementation-class}

Este caso de uso implica llamar a un método estático o de instancia de una clase en la API de AEM donde se hace referencia a una clase concreta, en lugar de a una interfaz como en el caso de uso 1.

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**Este caso de uso se puede manejar con UberJar**. Sin embargo, para las pruebas de rendimiento, se recomienda seguir usando la API en la medida de lo posible.

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### Caso de uso 3: código personalizado que extiende una clase base desde la API {#use-case-custom-code-which-extends-a-base-class-from-the-api}

Al igual que con SCR Generation, si el código amplía una clase base (abstracta o concreta) desde la API de AEM, **debe** utilizar UberJar para probarla.

## Tareas comunes de desarrollo con Maven {#common-development-tasks-with-maven}

### Cómo agregar rutas al módulo de contenido {#how-to-add-paths-to-the-content-module}

El módulo de contenido contiene un archivo src/main/content/META-INF/vault/filter.xml que define los filtros del paquete AEM creado por Maven. El archivo creado por el arquetipo Maven tiene este aspecto:

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Este archivo se utiliza de diferentes maneras:

* por el `content-package-maven-plugin` para determinar qué contenido incluir en el paquete
* mediante la herramienta VLT para determinar qué rutas considerar
* si el paquete se vuelve a crear en el Administrador de paquetes de AEM, también define qué rutas incluir

Según los requisitos de la aplicación, puede que desee agregar a estas rutas para incluir más contenido, como por ejemplo:

* Opciones de configuración del lanzamiento
* Modelos
* Modelos de flujo de trabajo
* Páginas de diseño
* Contenido de muestra

Para agregar a las rutas, agregue más `<filter>` elementos:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/etc/msm/rolloutconfigs/myrolloutconfig"/>
    <filter root="/etc/blueprints/mysite/globalsite"/>
    <filter root="/etc/workflow/models/myproject"/>
    <filter root="/etc/designs/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### Adición de rutas al paquete sin sincronizarlas {#adding-paths-to-the-package-without-syncing-them}

Si tiene archivos que deben agregarse al paquete generado por el content-package-maven-plugin pero que no deben sincronizarse entre el sistema de archivos y el repositorio, puede utilizar `.vltignore` archivos. Estos archivos tienen la misma sintaxis que los archivos [.gitignore](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) .

Por ejemplo, el arquetipo utiliza un `.vltignore` archivo para evitar que el archivo JAR instalado como parte del paquete se sincronice de nuevo con el sistema de archivos:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### Sincronización de rutas sin agregarlas al paquete {#syncing-paths-without-adding-them-to-the-package}

En algunos casos, es posible que desee mantener determinadas rutas sincronizadas entre el sistema de archivos y el repositorio, pero no incluirlas en el paquete que se ha creado para su instalación en AEM.

Un caso típico es la `/libs/foundation` ruta. Para fines de desarrollo, es posible que desee que el contenido de esta ruta esté disponible en el sistema de archivos, de modo que, por ejemplo, su IDE pueda resolver inclusiones JSP que incluyan JSP en `/libs`. Sin embargo, no desea incluir esa parte en el paquete que genera, ya que la parte contiene código de producto que no debe modificarse mediante implementaciones personalizadas. `/libs`

Para conseguirlo, puede proporcionar un archivo `src/main/content/META-INF/vault/filter-vlt.xml`. Si este archivo existe, será utilizado por la herramienta VLT, por ejemplo, cuando realice `vlt up` y `vlt ci`o cuando haya configurado `vlt sync` . El content-package-maven-plugin seguirá usando el archivo `src/main/content/META-INF/vault/filter.xml` al crear el paquete.

Por ejemplo, para que esté `/libs/foundation` disponible localmente para el desarrollo, pero solo incluya `/apps/myproject` en el paquete, utilice los dos archivos siguientes.

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

También deberá volver a configurar el complemento maven-resources-plugin para que no incluya estos archivos en el paquete: el archivo filter.xml no se aplica cuando se instala el paquete, sino solo cuando se vuelve a compilar mediante el administrador de paquetes.

Cambie la `<resources>` sección de la página de contenido en consecuencia:

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### How to Work with JSPs {#how-to-work-with-jsps}

La configuración de Maven descrita hasta ahora crea un paquete de contenido que también puede incluir componentes y sus JSP correspondientes. Sin embargo, Maven los trata como cualquier otro archivo que forme parte del paquete de contenido y ni siquiera los reconoce como JSP.

Los componentes resultantes funcionan en AEM de la misma manera, pero hacer que Maven esté al tanto de los JSP tiene dos ventajas principales

* permite que Maven falle si los JSP contienen errores, de modo que éstos se muestren en el momento de la creación y no cuando se compilen por primera vez en AEM
* Para los IDE que pueden importar proyectos de Maven, esto también habilita la finalización de código y la compatibilidad con la biblioteca de etiquetas en los JSP

Se requieren dos cosas para habilitar esta configuración:

1. agregar dependencias de biblioteca de etiquetas
1. compilar los JSP como parte del proceso de compilación de Maven

#### Adición de dependencias de la biblioteca de etiquetas {#adding-tag-library-dependencies}

Debajo es necesario agregar dependencias al POM de los `content` módulos.

>[!NOTE]
>
>A menos que importe las dependencias del producto tal como se describe en [Importación de dependencias](#importingaemproductdependencies) del producto de AEM más arriba, también es necesario agregarlas al POM principal junto con la versión que coincida con la configuración de AEM, tal como se describe en [Adición de dependencias](#addingdependencies) más arriba. Los comentarios de cada entrada a continuación muestran el paquete que buscar en el Buscador de dependencias.

>[!NOTE]
>
>El `com.adobe.granite.xssprotection` artefacto no se incluye en el POM cq-quickstart-product-dependencias y requiere coordenadas completas de Maven, tal como se obtiene del Buscador de dependencias.

#### Compilación de JSP como parte de la fase de compilación de Maven {#compiling-jsps-as-part-of-the-maven-compile-phase}

Para compilar JSPs en la `compile` fase de Maven, utilizamos el complemento [JspC](https://sling.apache.org/documentation/development/jspc.html) Maven de Apache Sling como se muestra a continuación:

* configuramos una ejecución para el `jspc` objetivo (que de forma predeterminada se enlaza a la `compile` fase, por lo que no necesitamos especificar la fase explícitamente)

* le decimos que recopile cualquier JSP en `${project.build.directory}/jsps-to-compile`
* y generar el resultado en `${project.build.directory}/ignoredjspc` (que se traduce como `myproject/content/target/ignoredjspc`)

* configuramos maven-resources-plugin para copiar los JSP a `${project.build.directory}/jsps-to-compile` en la fase de generación-orígenes y configurarlo para que no copie la `libs/` carpeta (porque es código de producto de AEM y no queremos incurrir en dependencias para la compilación de nuestro proyecto, ni necesitamos validar que compila.

Nuestro objetivo principal, como se ha indicado anteriormente, es validar los JSP y asegurarse de que el proceso de compilación falla si contienen errores. Es por eso que los compilamos en un directorio separado que se ignora (y de hecho se elimina inmediatamente después, como se verá en un minuto).

El resultado del complemento JspC de Maven también se puede agrupar e implementar como parte de un paquete OSGi, pero esto tiene otras implicaciones y efectos secundarios y va más allá de nuestro objetivo de validar los JSPs.

Para lograr la eliminación de las clases compiladas desde los JSP, configuramos el complemento Maven Clean como se muestra a continuación. Si desea inspeccionar el resultado del complemento JspC de Maven, ejecute `mvn compile` en `myproject/content` — después de eso, encontrará el resultado en `myproject/content/target/ignoredjspc`).

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>Dependiendo de si realmente utiliza el código JSP en `/libs` (es decir, incluya JSP desde allí), deberá precisar qué JSP se copian para la compilación.
>
>Por ejemplo: si incluye `/libs/foundation/global.jsp`, puede utilizar la siguiente configuración para el `maven-resources-plugin` en lugar de la configuración anterior, que se salta por completo `/libs`.
>
>```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```
>

### Cómo trabajar con sistemas SCM {#how-to-work-with-scm-systems}

Cuando trabaje con Administración de configuración de origen (SCM), asegúrese de que

* El VCS ignora los artefactos que no son de origen en el sistema de archivos
* VLT ignora los artefactos del VCS y no los protege en el repositorio

>[!NOTE]
>
>Esta descripción no explica cómo configurar Maven para que funcione con su SCM, que se describe exhaustivamente en la referencia [de](https://maven.apache.org/pom.html#SCM) Maven POM y en la documentación [del complemento](https://maven.apache.org/scm/)Maven SCM.

#### Patrones para excluir de SCM {#patterns-to-exclude-from-scm}

A continuación se muestra una lista típica de patrones que se incluirán desde SCM. Por ejemplo: si está utilizando git, puede agregarlos al `.gitignore` archivo del proyecto.

#### sample.gitignore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### Ignorar archivos de control SCM en VLT {#ignoring-scm-control-files-in-vlt}

En algunos casos, es posible que tenga archivos de control SCM en el árbol de fuentes de contenido que no desee que se registren en el repositorio.

Piense en la siguiente situación:

El arquetipo ya creó un archivo .vltignore para evitar que el archivo jar del paquete instalado se vuelva a sincronizar con el sistema de archivos:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

Obviamente, tampoco desea este archivo en su SCM, por lo que si, por ejemplo, está usando git, agregaría un archivo correspondiente . `gitignore` archivo:

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

Como . `gitignore` no debe ir al repositorio tampoco, el . `vltignore` debe ampliarse para incluir el . `gitignore` archivo:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### Cómo trabajar con perfiles de implementación {#how-to-work-with-deployment-profiles}

Si el proceso de compilación es parte de una configuración de administración del ciclo de vida de desarrollo más grande, como un proceso de integración continuo, a menudo debe implementar en otros equipos que no sean sólo la instancia local del desarrollador.

Para estos escenarios, puede agregar fácilmente nuevos perfiles [de](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) Maven Build al POM del proyecto.

El ejemplo siguiente agrega un perfil `integrationServer`, que redefine los nombres de host y los puertos para las instancias de autor y publicación. Puede implementar en estos servidores ejecutando maven desde la raíz del proyecto, como se muestra a continuación.

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### Cómo trabajar con comunidades AEM {#how-to-work-with-aem-communities}

Si dispone de una licencia para la función AEM Communities, se necesita un tarro de API adicional.

Para obtener más información, consulte [Uso de Maven para comunidades](/help/communities/maven.md)
