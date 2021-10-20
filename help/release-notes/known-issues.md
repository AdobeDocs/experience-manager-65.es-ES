---
title: Problemas conocidos
description: Notas de versión específicas de problemas conocidos con Adobe Experience Manager 6.5
exl-id: 736037cf-af8c-4ce2-969e-c100a939a038
source-git-commit: e0f024c2e1dc9fc7908382d406844575b4b38363
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 43%

---

# Problemas conocidos {#known-issues}

Esta página contiene una lista de problemas conocidos de Adobe Experience Manager 6.5 que se publicó en abril de 2019.

[Póngase en contacto con el servicio de soporte técnico](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) si necesita más información sobre los problemas conocidos.

## Plataforma {#platform}

* Se informa de un problema en el que CRX-Quickstart y su contenido se eliminan.

   En cada una de estas acciones, asegúrese de que la propiedad `htmllibmanager.fileSystemOutputCacheLocation` no es una cadena vacía:

   1. Llamar a `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Actualización a AEM 6.5.
   3. Ejecutando &quot;migración de contenido diferido&quot; en AEM 6.5.

   A [Base de conocimientos](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) este artículo está disponible con más detalles y la solución para este problema.

* Si utiliza JDK 11 con AEM instancia 6.5, algunas de las páginas podrían aparecer en blanco después de implementar algunos paquetes. El siguiente mensaje de error aparece en el archivo de registro:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Para resolver este error:

1. Detenga la instancia de AEM. Vaya a `<aem_server_path_on_server>crx-quickstart\conf` y abra el `sling.properties` archivo. Adobe recomienda realizar una copia de seguridad de este archivo.

1. Buscar `org.osgi.framework.bootdelegation=`. Agregar `jdk.internal.reflect,jdk.internal.reflect.*` propiedades para mostrar el resultado como.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Guarde el archivo y reinicie la instancia de AEM.

## Assets {#assets}

* **Buscar:** La búsqueda no devuelve ningún resultado si la cadena de búsqueda contiene espacios iniciales ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Esquema de metadatos de carpeta**: después de añadir un botón de opciones, los campos Id. y Valor no se procesan como se esperaba y la funcionalidad de eliminación no funciona. (CQ-4261144)
* Al cambiar el nombre de un recurso, no se puede utilizar un espacio en blanco en el nombre del recurso. (CQ-4266403)

## Forms {#forms}

* Cuando AEM Forms está instalado en el sistema operativo Linux, la firma digital con el módulo de seguridad de hardware no funciona. (CQ-4266721)
* (AEM Forms solo en WebSphere) La opción **Forms Workflow**> **Task Search** (Búsqueda de tareas) no devuelve ningún resultado si se busca un **administrador** con el **nombre de usuario** como criterio de búsqueda. (CQ-4266457)

* AEM Forms no puede convertir archivos TIF y TIFF con compresión de JPEG a documentos PDF. (CQ-4265972)
* Las opciones **AEM Forms Assets Scanner** (Escáner de recursos de AEM Forms) y **Letter to Interactive Communication Migration** (Carta para la migración de comunicaciones interactiva) no funcionan en la página de **migración de AEM Forms**. (CQ-4266572)

* (Solo JBoss 7) Cuando actualiza de una versión anterior a AEM 6.5 Forms y la versión anterior tenía procesos (.lca) que creaban y utilizaban una copia del proceso de envío predeterminado o del procesamiento predeterminado, HTML5 Forms que utilizaba esos procesos (.lca) no realiza las acciones requeridas. (CQ-4243928)
* En un formulario adaptable, cuando se invoca un servicio de modelo de datos de formulario desde el editor de reglas para actualizar dinámicamente los valores del componente de elección de imágenes, los valores del componente de elección de imágenes no se actualizan. (CQ-4254754)
* El instalador de AEM Forms Designer requiere la versión de 32 bits de [Paquete de tiempo de ejecución redistribuible de Visual C++ 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) y [Paquetes de tiempo de ejecución redistribuibles de Visual C++ 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación. (CQ-4265668)

* El Generador de PDF no admite la autenticación basada en tarjetas inteligentes.  Cuando un administrador habilita la directiva de grupo `Interactive Logon: Require Smart card` en un servidor de Windows, todos los usuarios existentes del Generador de PDF se invalidan.

* Cuando se configura un formulario adaptable para actualizar dinámicamente los valores de un componente y se accede a la instancia de publicación que aloja el formulario a través del controlador, la funcionalidad para actualizar dinámicamente los valores de un campo deja de funcionar. Para resolver el problema, en la instancia de publicación, abra CRXDE, vaya a `/libs/fd/af/runtime/clientlibs/guideChartReducer`y cree la propiedad que aparece a continuación.

   * Nombre: allowProxy
   * Tipo: Boolean (booleano)
   * Valor: true (verdadero)
   * Protegido: false (falso)
   * Obligatorio: false (falso)
   * Varios: false (falso)
   * Creación automática: False

   La propiedad permite que las bibliotecas de cliente en la carpeta de ejecución accedan a los proxy. (CQ-4268679)

* Cuando se inicia AEM Forms, la variable `SAX Security Manager could not be setup` aparece la advertencia.
* Al abrir un PDF protegido con AEM Forms Document Security en un Apple iOS o iPadOS que ejecute Adobe Acrobat Reader versión 20.10.00.
* Cuando se envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Apple iOS 15.1 proporciona una solución para el problema.
