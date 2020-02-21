---
title: Desarrollo con CRXDE Lite
seo-title: Desarrollo con CRXDE Lite
description: CRXDE Lite está integrado en AEM y le permite realizar tareas de desarrollo estándar en el navegador
seo-description: CRXDE Lite está integrado en AEM y le permite realizar tareas de desarrollo estándar en el navegador
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# Desarrollo con CRXDE Lite{#developing-with-crxde-lite}

En esta sección se describe cómo desarrollar la aplicación AEM con CRXDE Lite.

Consulte la documentación general para obtener más información sobre los diferentes entornos de desarrollo disponibles.

CRXDE Lite está integrado en AEM y le permite realizar tareas de desarrollo estándar en el navegador. Con CRXDE Lite, puede crear un proyecto, crear y editar archivos (como .jsp y .java), carpetas, plantillas, componentes, cuadros de diálogo, nodos, propiedades y paquetes mientras registra e integra con SVN.
CRXDE Lite se recomienda cuando no tenga acceso directo al servidor AEM, cuando desarrolle una aplicación ampliando o modificando los componentes integrados y los paquetes de Java o cuando no necesite un depurador dedicado, la finalización del código y el resaltado de sintaxis.

>[!NOTE]
>
>De forma predeterminada, todos los usuarios de AEM pueden acceder a CRXDE Lite. Si lo desea, [configure las ACL](/help/sites-administering/security.md#permissions-and-acls) para el nodo siguiente para que solo los desarrolladores puedan acceder a CRX DE Lite:
>
>`/libs/granite/crxde`

>[!NOTE]
>
>Se recomienda utilizar las herramientas de desarrollador de [AEM para Eclipse](/help/sites-developing/aem-eclipse.md) y la extensión de los corchetes HTML de [AEM](/help/sites-developing/aem-brackets.md) durante el desarrollo del proyecto.

## Introducción a CRXDE Lite {#getting-started-with-crxde-lite}

Para comenzar con CRXDE Lite, siga estos pasos:

1. Instale AEM.
1. En el explorador, introduzca `https://<host>:<port>/crx/de`. De forma predeterminada, lo es `https://localhost:4502/crx/de`.
1. Introduzca su **nombre de usuario** y **contraseña**. De forma predeterminada es `admin` y `admin`.

1. Haga clic en **Aceptar**.

La interfaz de usuario de CRXDE Lite tiene el siguiente aspecto en el navegador:

![chlimage_1-18](assets/chlimage_1-18.png)

Ahora puede utilizar CRXDE Lite para desarrollar su aplicación.

## Información general sobre la interfaz de usuario {#overview-of-the-user-interface}

CRXDE Lite ofrece las siguientes funciones:

<table>
 <tbody>
  <tr>
   <td>Barra de conmutación superior</td>
   <td>Permite cambiar rápidamente entre CRXDE Lite, Package Manager y Package Share.</td>
  </tr>
  <tr>
   <td>Widget de ruta de nodo</td>
   <td><p>Muestra la ruta al nodo seleccionado actualmente.</p> <p>También puede utilizarla para saltar a un nodo, introduciendo la ruta a mano o pegándola desde otro lugar y pulsando Intro.</p> <p>También proporciona soporte para buscar nodos con un nombre de nodo específico. Escriba el nombre del nodo que desee encontrar y espere (o pulse el símbolo de búsqueda en el lado derecho). Puede intentar introducir, por ejemplo, el <em>roble</em> de cadena en la utilidad para ver cómo funciona. Si un nodo o nodos determinados se cargan en el panel del explorador, se mostrará la lista y podrá seleccionar la ruta y pulsar Intro para desplazarse hasta ella. Tenga en cuenta que solo funciona con los nodos cargados actualmente en la aplicación cliente CRXDE en el navegador. Si desea buscar en todo el repositorio, utilice Herramientas y, a continuación, Consulta.</p> </td>
  </tr>
  <tr>
   <td>Panel Explorador</td>
   <td><p>Muestra un árbol de todos los nodos del repositorio.</p> <p>Haga clic en un nodo para mostrar sus propiedades en la ficha <strong>Propiedades</strong> . Después de hacer clic en un nodo, puede seleccionar una acción en la barra de herramientas. Vuelva a hacer clic en el nodo para cambiarle el nombre.</p> <p>Filtro de navegación de árbol (icono binocular): permite filtrar los nodos del repositorio para los que el nombre contiene el texto de entrada. Solo se aplica a los nodos que se han cargado localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Panel Editar</td>
   <td><p><strong>Ficha Inicio</strong> : le permite buscar contenido y/o documentación y acceder a los recursos del desarrollador (documentación, blog del desarrollador, base de conocimiento) y a la asistencia técnica (página principal y centro de asistencia de Adobe).<br /> </p> <p>Haga doble clic en un archivo del panel <strong>Explorador</strong> para mostrar su contenido; como, por ejemplo, un archivo .jsp o .java. A continuación, puede modificarlo y guardar los cambios.</p> <p>Una vez que se edita un archivo en el panel <strong>Editar</strong> , las siguientes herramientas están disponibles en la barra de herramientas:<br /> </p> - <strong>Mostrar en árbol: </strong>muestra el archivo en el árbol del repositorio.<br /> - <strong>Buscar/Reemplazar ...</strong>: realice búsquedas o reemplace.<br /> <br /> Al hacer doble clic en la línea de estado del panel <strong>Editar</strong> , se abre el cuadro de diálogo <strong>Ir a la línea</strong> para que pueda introducir un número de línea específico para ir.<br /> </td>
  </tr>
  <tr>
   <td>Ficha Propiedades<br /> </td>
   <td>Muestra las propiedades del nodo seleccionado. Puede agregar nuevas propiedades o eliminar las existentes.<br /> </td>
  </tr>
  <tr>
   <td>Ficha Control de acceso</td>
   <td><p>Mostrar permisos basados en la ruta actual, nivel de repositorio o principal.</p> <p>Los permisos se desglosan en</p> <p>- Directiva <strong>de control de acceso</strong>aplicable: Políticas que se pueden aplicar a la selección actual.</p> <p>- Directivas <strong>de control de acceso</strong>local: Políticas actuales aplicadas localmente a la selección actual.</p> <p>- Políticas <strong></strong>efectivas de control de acceso: Las políticas actuales aplicadas a la selección actual pueden establecerse localmente o heredarse de los nodos principales.</p> <p>Nota. Para poder ver la información del control de acceso, el usuario que ha iniciado sesión en CRXDE Lite debe tener derechos para leer entradas ACL. El usuario anónimo no puede ver esta información de forma predeterminada: inicie sesión como, por ejemplo, administrador para ver la información.</p> </td>
  </tr>
  <tr>
   <td>Ficha Replicación</td>
   <td><p>Muestra el estado de replicación del nodo actual. Puede replicar y replicar la eliminación del nodo actual.</p> </td>
  </tr>
  <tr>
   <td>Ficha Consola<br /> </td>
   <td><p><strong>Registros de servidor</strong>:</p> <p>Muestra mensajes de registros. Puede configurar el nivel de registro, borrar la consola, fijar en la posición de desplazamiento seleccionada y habilitar/deshabilitar la visualización de mensajes.<br /> </p> <p><strong>Control de versión</strong>:</p> <p>Muestra mensajes de control de versiones.<br /> </p> </td>
  </tr>
  <tr>
   <td>Ficha Información de compilación<br /> </td>
   <td>Muestra información cuando se está generando un paquete.<br /> </td>
  </tr>
  <tr>
   <td>Actualizar<br /> </td>
   <td>Actualiza la selección actual. Los cambios de otros usuarios se actualizan en la vista del repositorio. Los cambios realizados no se verán afectados.<br /> </td>
  </tr>
  <tr>
   <td>Guardar todos</td>
   <td><p><strong>Guardar todos</strong>:<br /> </p> <p>Guarda todos los cambios realizados. Hasta que haga clic en Guardar, los cambios serán temporales y se perderán al salir de la consola.</p> <p><strong>Revertir</strong>:</p> <p>Desecha todos los cambios realizados en el nodo seleccionado desde la última acción de guardar y, a continuación, vuelve a cargar el estado actual del repositorio para el nodo seleccionado.</p> <p><strong>Revertir todos</strong>:</p> <p>Desecha todos los cambios que ha realizado en todo el repositorio desde la última acción de guardar y, a continuación, vuelve a cargar el estado actual del repositorio.</p> </td>
  </tr>
  <tr>
   <td>Crear ...<br /> </td>
   <td><p>Menú desplegable para crear lo siguiente en el nodo seleccionado:<br /> </p> <p>- <strong>Nodo</strong>: un nodo con un tipo de nodo arbitrario<br /> </p> <p>- <strong>Archivo</strong>: nt:file node y su nt:resource subnode</p> <p>- <strong>Carpeta</strong>: nt:nodo de carpeta</p> <p>- <strong>Plantilla</strong>: Plantilla de AEM</p> <p>- <strong>Componente</strong>: Componente AEM</p> <p>- <strong>Diálogo</strong>: Cuadro de diálogo AEM</p> </td>
  </tr>
  <tr>
   <td>Eliminar<br /> </td>
   <td>Elimina el nodo seleccionado.<br /> </td>
  </tr>
  <tr>
   <td>Copiar</td>
   <td>Copia el nodo seleccionado.<br /> </td>
  </tr>
  <tr>
   <td>Pegar<br /> </td>
   <td>Pega el nodo copiado debajo del nodo seleccionado.<br /> </td>
  </tr>
  <tr>
   <td>Mover ...<br /> </td>
   <td>Mueve el nodo seleccionado al nodo definido a través del cuadro de diálogo.</td>
  </tr>
  <tr>
   <td>Cambiar nombre ...<br /> </td>
   <td>Cambia el nombre del nodo seleccionado.<br /> </td>
  </tr>
  <tr>
   <td>Clases...<br /> </td>
   <td>Permite agregar tipos de mezcla al tipo de nodo. Los tipos de mezcla se utilizan principalmente para agregar características avanzadas como control de versiones, control de acceso, referencia y bloqueo al nodo.</td>
  </tr>
  <tr>
   <td>Equipo<br /> </td>
   <td><p>Menú desplegable para realizar tareas de control de versiones estándar:</p> <p>- <strong>Actualizar</strong> repositorio desde el servidor SVN</p> <p>- <strong>Confirmar</strong> cambios locales en el servidor SVN</p> <p>- Ver <strong>estado</strong> del nodo actual</p> <p>- Ver estado <strong></strong> recursivo del subárbol del nodo actual</p> <p>- <strong>Cierre de compra</strong> una copia de trabajo del servidor SVN</p> <p>- <strong>Exportar</strong> un proyecto desde el servidor SVN (sin crear una copia de trabajo)</p> <p>- <strong>Importar</strong> un proyecto del repositorio al servidor SVN<br /> </p> <p>Tenga en cuenta que debe iniciar sesión como usuario con permisos suficientes para poder ejecutar algunas de las tareas (especialmente las que escriben en el repositorio local).<br /> </p> </td>
  </tr>
  <tr>
   <td>Herramientas<br /> </td>
   <td><p>Menú desplegable con las siguientes herramientas:</p> <p>- Configuración <strong>del servidor...</strong>: para acceder a la consola Felix.</p> <p>- <strong>Consulta...</strong>: para consultar el repositorio.</p> <p>- <strong>Privilegios ...</strong>: para abrir la administración de privilegios, donde puede ver y agregar privilegios.</p> <p>- Control <strong>de acceso de prueba ...</strong>: un lugar donde puede probar el permiso para una ruta determinada o principal.</p> <p>- <strong>Exportar tipo</strong>de nodo: para exportar tipos de nodos en el sistema como notación de código.</p> <p>- <strong>Importar tipo de nodo...</strong>: para importar tipos de nodos mediante notación cnd.</p> <p>- <strong>Instalar el depurador de SiteCatalyst...</strong>: instrucciones sobre cómo instalar Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Utilidad de inicio de sesión<br /> </td>
   <td><p>Muestra los usuarios que han iniciado sesión en ese momento y el espacio de trabajo en el que han iniciado sesión, por ejemplo: admin@crx.default.</p> <p>Haga clic en él para iniciar sesión o volver a iniciarla como un usuario específico. Si no especifica un espacio de trabajo en el que iniciar sesión, iniciará sesión en el espacio de trabajo predeterminado, crx.default.</p> <p>Si desea examinar el repositorio como usuario anónimo, utilice <strong>anónimo</strong> como nombre de inicio de sesión y cualquier contraseña (por ejemplo, un espacio o un punto).<br /> </p> <p>Si su autorización ya no es válida (por ejemplo, ha caducado), la utilidad de inicio de sesión muestra "<strong>No autorizado - Inicio de sesión...</strong>". Haga clic en él para volver a iniciar sesión.</p> </td>
  </tr>
 </tbody>
</table>

## Creación de un proyecto {#creating-a-project}

Con CRXDE Lite puede crear un proyecto de trabajo con tres clics. El asistente para proyectos crea un nuevo proyecto en `/apps`, contenido debajo de `/conten`t y un paquete que envuelve todo el proyecto en el que se encuentra el contenido `/etc/packages`. El proyecto se puede utilizar de inmediato para procesar una página de muestra con **Hello World**, basada en una secuencia de comandos jsp que procesa una propiedad del repositorio y llama a una clase Java para procesar texto.

Para crear un proyecto con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. **En el panel Navegación, haga clic con el botón derecho en un nodo, seleccione** Crear...**y, a continuación,**Crear proyecto... .
Nota: puede hacer clic con el botón secundario en cualquier nodo de la navegación de árbol, ya que los nuevos nodos de proyecto se crean, por diseño, debajo `/apps,` y `/content` `/etc/packages`.

1. Definir:

   * **Nombre** del proyecto: el nombre del proyecto se utiliza para crear los nuevos nodos y el paquete, por ejemplo `myproject`.

   * **Paquete** Java: el prefijo del nombre del paquete Java, por ejemplo: `com.mycompany`.

1. Haga clic en **Crear**.
1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Para acceder a la página de muestra que muestra **Hola Mundo**, dirija el explorador a:

`https://localhost:4502/content/<project-name>.html`

La página **Hello World** se basa en un nodo de contenido que llama a una secuencia de comandos jsp a través de la `sling:resourceType` propiedad. La secuencia de comandos lee la propiedad del `jcr:title` repositorio y obtiene el contenido del cuerpo llamando a un método de la clase SampleUtil, que está disponible en el paquete de proyectos.

Se crean los siguientes nodos:

* `/apps/<project-name>`:: el contenedor de aplicaciones.
* `/apps/<project-name>/components`:: el contenedor de componentes, que contiene el archivo html.jsp de muestra, utilizado para procesar una página.

* `/apps/<project-name>/src`:: el contenedor de paquetes, que contiene un paquete de proyecto de muestra.

* `/apps/<project-name>/install`:: el contenedor compilado de paquetes, que contiene el paquete de proyectos de muestra compilado.
* `/content/<project-name>`:: el contenedor de contenido.
* /etc/packages/&lt;java-suffix>/&lt;project-name>.zip, un paquete que envuelve toda la aplicación y el contenido del proyecto. Puede utilizarla para reconstruir el proyecto para una mayor implementación (por ejemplo, en otros entornos) o para compartirlo mediante Package Share.

La estructura tiene el siguiente aspecto en CRXDE Lite con un proyecto llamado **myproject** y un sufijo de paquete java llamado **mycompany**:

![chlimage_1-19](assets/chlimage_1-19.png)

![chlimage_1-20](assets/chlimage_1-20.png)

## Creación de una carpeta {#creating-a-folder}

Para crear una carpeta con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. **En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desea crear la nueva carpeta, seleccione** Crear...**y, a continuación,** Crear carpeta... .

1. Introduzca el **nombre** de la carpeta y haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creating a Template {#creating-a-template}

Para crear una plantilla con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. **En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desee crear la plantilla, seleccione** Crear...**y, a continuación,** Crear plantilla... .

1. Introduzca la **etiqueta**, el **título**, la **descripción**, el tipo **de** recurso y la **clasificación** de la plantilla. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca las Rutas **permitidas**. Haga clic en **Siguiente**

1. Este paso es opcional: establezca los Padres **** permitidos. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca los elementos secundarios **permitidos**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Crea:

* Un nodo de tipo `cq:Template` con propiedades Template

* Un nodo secundario de tipo `cq:PageContent` con propiedades de contenido de página

Puede agregar propiedades a la plantilla: consulte la sección [Creación de una propiedad](#creating-a-property) .

## Creación de un componente {#creating-a-component}

La función que se describe aquí solo está disponible si CQ5 está instalado, es decir, si el tipo de nodo `cq:Component` está disponible en el repositorio.

Para crear un componente con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. **En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desea crear el componente, seleccione** Crear...**y, a continuación,** Crear componente... .

1. Introduzca la **etiqueta**, el **título**, la **descripción**, el tipo **** de recurso superior y el **grupo** del componente. Haga clic en **Siguiente**. 

1. Este paso es opcional: defina las propiedades del componente **Es contenedor,** **Sin decoración**, Nombre **de** celda y Ruta **de cuadro de diálogo**. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca la propiedad del componente **Padres** permitidos. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca la propiedad del componente **Permitidos elementos secundarios**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Crea:

* Un nodo de tipo `cq:Component`
* Propiedades del componente
* Un script .jsp de componente

## Creación de un cuadro de diálogo {#creating-a-dialog}

Para crear un cuadro de diálogo con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. **En el panel Navegación, haga clic con el botón derecho en el componente en el que desea crear el cuadro de diálogo, seleccione** Crear...**y, a continuación,** Crear cuadro de diálogo... .

1. Introduzca la **etiqueta** y el **título**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar** todo para guardar los cambios en el servidor.

Crea un cuadro de diálogo con la siguiente estructura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Ahora puede adaptar el cuadro de diálogo a sus necesidades modificando propiedades o creando nuevos nodos.

También puede utilizar el Editor de cuadros de diálogo para editar un cuadro de diálogo. Al hacer doble clic en el nodo de cuadro de diálogo en CRXDE Lite, aparecerá el editor. Puede encontrar más información sobre el Editor de cuadros de diálogo [aquí](/help/sites-developing/dialog-editor.md).

## Creación de un nodo {#creating-a-node}

Para crear un nodo con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. **En el panel Navegación, haga clic con el botón derecho en el nodo en el que desea crear el nuevo nodo, seleccione** Crear...**y, a continuación,** Crear nodo... .
1. Introduzca el **Nombre** y el **Tipo**. Haga clic en **Aceptar**.
1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Ahora puede adaptar el nodo a sus necesidades modificando propiedades o creando nuevos nodos.

>[!NOTE]
>
>La mayoría de las operaciones de edición, incluido Crear nodo, mantienen todos los cambios en la memoria y solo los almacena en el repositorio al guardarlos (mediante el botón &quot;Guardar todo&quot;). Sin embargo, algunas operaciones como mover se mantienen automáticamente.
>
>La validación con respecto a si el nuevo nodo creado está permitido por el tipo de nodo del nodo principal también la realiza el repositorio JCR primero al guardar los cambios. Si recibe un mensaje de error al guardar un nodo, compruebe si la estructura de contenido es válida (por ejemplo, no puede crear un `nt:unstructured` nodo como secundario de `nt:folder` nodo).

## Creación de una propiedad {#creating-a-property}

Para crear una propiedad con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, seleccione el nodo en el que desea agregar la nueva propiedad.
1. En la ficha **Propiedades** del panel inferior, introduzca el **Nombre**, el **Tipo** y el **Valor**. Haga clic en **Agregar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de una secuencia de comandos {#creating-a-script}

Para crear una nueva secuencia de comandos:

1. Abra CRXDE Lite en el navegador 
1. **En el panel Navegación, haga clic con el botón derecho en el componente en el que desea crear la secuencia de comandos, seleccione** Crear ...**y, a continuación,** Crear archivo ... .

1. Introduzca el **nombre** del archivo, incluida su extensión. Haga clic en **Aceptar**.

1. El nuevo archivo se abre como una ficha en el panel Editar.
1. Edite el archivo.
1. Haga clic en **Guardar todo** para guardar los cambios.

## Administración de un paquete {#managing-a-bundle}

Con CRXDE Lite, es sencillo crear un paquete OSGI, agregarle clases Java y compilarlo. El paquete se instala automáticamente y se inicia en el contenedor OSGI.

En esta sección se describe cómo crear un `Test` paquete con una clase `HelloWorld` Java que muestra **Hello World!** en el explorador cuando se solicita el recurso.

### Creación de un paquete {#creating-a-bundle}

Para crear el paquete de prueba con CRXDE Lite:

1. En CRXDE Lite, cree `myapp` un proyecto con el asistente [del](#creating-a-project)proyecto. Entre otros, se crean los siguientes nodos:

   * `/apps/myapp/src`
   * `/apps/myapp/install`

1. `/apps/myapp/src`Haga clic con el botón derecho en la carpeta `Test` que contendrá el **paquete, seleccione** Crear...**y, a continuación,** Crear paquete... .

1. Configure las propiedades del paquete de la siguiente manera:

   * Nombre simbólico del paquete: `com.mycompany.test.TestBundle`

   * Nombre de paquete: `Test Bundle`
   * Descripción del paquete:

      ```
      This is my Test Bundle
      ```

   * Paquete:

      ```
      com.mycompany.test
      ```
   Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

El asistente crea los siguientes elementos:

* El nodo `com.mycompany.test.TestBundle` de tipo `nt:folder.` Es el nodo contenedor del paquete.

* El archivo `com.mycompany.test.TestBundle.bnd`. Actúa como descriptor de implementación para el paquete y consta de un conjunto de encabezados.

* Estructuras de carpetas:

   * `src/main/java/com/mycompany/test`. Contendrá los paquetes y las clases de Java.

   * `src/main/resources`. Contendrá los recursos utilizados dentro del paquete.

* El `Activator.java` archivo. Es la clase de oyente opcional a la que se notificará de los eventos de inicio y parada del paquete.

En la tabla siguiente se enumeran todas las propiedades del archivo .bnd, sus valores y descripciones:

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Valor (en la creación del paquete)<br /> </strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Export-Package:</td>
   <td><p>*</p> <p>Nota: este valor debe adaptarse para reflejar la especificidad del paquete.</p> </td>
   <td>El encabezado Export-Package define los paquetes exportados del paquete (lista de paquetes separados por comas). Los paquetes exportados constituyen la vista pública<br /> del paquete.<br /> </td>
  </tr>
  <tr>
   <td>Import-Package:</td>
   <td><p>*</p> <p>Nota: este valor debe adaptarse para reflejar la especificidad del paquete.</p> </td>
   <td>El encabezado Import-Package define los paquetes importados para el paquete (lista de paquetes separados por comas)</td>
  </tr>
  <tr>
   <td>Paquete privado:</td>
   <td><p>*</p> <p>Nota: este valor debe adaptarse para reflejar la especificidad del paquete.</p> </td>
   <td>El encabezado Private-Package define los paquetes privados para el paquete (lista de paquetes separados por comas). Los paquetes privados constituyen la implementación interna.<br /> </td>
  </tr>
  <tr>
   <td>Nombre del paquete:</td>
   <td>Paquete de prueba</td>
   <td>Define un nombre corto y legible para el paquete</td>
  </tr>
  <tr>
   <td>Descripción del paquete:</td>
   <td>Este es mi paquete de prueba</td>
   <td>Define una descripción breve y legible para el paquete</td>
  </tr>
  <tr>
   <td>Nombre simbólico del paquete:</td>
   <td>com.mycompany.test.TestBundle</td>
   <td>Especifica un nombre único y no localizable para el paquete</td>
  </tr>
  <tr>
   <td>Versión del paquete:</td>
   <td>1.0.0-SNAPSHOT</td>
   <td>Especifica la versión del paquete</td>
  </tr>
  <tr>
   <td>Bundle-Activator:</td>
   <td>com.miempresa.prueba.Activator</td>
   <td>Especifica el nombre de la clase de oyente opcional que se notificará de los eventos de inicio y parada del paquete</td>
  </tr>
 </tbody>
</table>

Para obtener más información sobre el formato de la oferta, consulte la utilidad [de la oferta](https://bndtools.org/) utilizada por CRXDE para crear paquetes OSGI.

### Creación de una clase Java {#creating-a-java-class}

Para crear la clase `HelloWorld` Java dentro del paquete de prueba:

1. Abra CRXDE Lite en el navegador 
1. `Activator.java`En el panel Navegación, haga clic con el botón derecho en el nodo que contiene el `/apps/myapp/src/com.mycompany.test.TestBundle/src/main/java` archivo ( **), seleccione** Crear ...**y, a continuación,** Crear archivo ... .

1. Asigne un nombre al archivo `HelloWorld.java`. Haga clic en **Aceptar**.

1. El `HelloWorld.java` archivo se abre en el panel Editar.
1. Agregue las siguientes líneas a `HelloWorld.java`:

    ```
      package com.mycompany.test;

      public class HelloWorld {
      public String getString(){
      return "Hello World!";
      }
      }
    ```

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

### Creación de un paquete {#building-a-bundle}

Para crear el paquete de prueba:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en el archivo .bnd, seleccione **Herramientas** y, a continuación **, Paquete**.

Asistente de compilación de paquetes:

* Compila las clases de Java.
* Crea el archivo .jar que contiene las clases Java compiladas y los recursos y lo coloca en la `myapp/install` carpeta.
* Instala e inicia el paquete en el contenedor OSGI.

Para ver el efecto del paquete de prueba, cree un componente que utilice el método Java HelloWorld.getString() y un recurso que este componente procese:

1. Cree el componente `mycomp` en `myapp/components`.

1. Edite `mycomp.jsp` y reemplace el código con las siguientes líneas:

   ```
     <%@ page import="com.mycompany.test.HelloWorld"%><%
     %><%@ include file="/libs/foundation/global.jsp"%><%
     %><% HelloWorld hello = new HelloWorld();%><%
     %>
     <html>
     <body>
     <b><%= hello.getString() %></b><br>
     </body>
     </html>
   ```

1. Cree el recurso `test_node` de tipo `nt:unstructured` en `/content`.

1. Para `test_node`, cree la siguiente propiedad: Nombre = `sling:resourceType`, Tipo = `String`, Valor = `myapp/components/mycomp`.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

1. En el explorador, solicite `test_node`: `https://<hostname>:<port>/content/test_node.html`.

1. Se muestra una página con el **Hola Mundo!** message.

## Exportación e importación de tipos de nodos {#exporting-and-importing-node-types}

Con CRXDE Lite puede importar y/o exportar definiciones de tipo de nodo en la notación [](https://jackrabbit.apache.org/jcr/node-type-notation.html)CND (Compact Namespace y Node Type Definition).

Para exportar una definición de tipo de nodo:

1. Abra CRXDE Lite en el navegador 
1. Seleccione el nodo requerido.
1. Seleccione **Herramientas** y luego **Exportar tipo** de nodo.

1. La definición, en notación de código, se mostrará en el explorador. Guarde la información si es necesario.

Para importar una definición de tipo de nodo:

1. Abra CRXDE Lite en el navegador 
1. **Seleccione** Herramientas **y luego** Importar tipo de nodo... .

1. Introduzca la notación CND para la definición en el cuadro de texto.
1. Marque **Permitir actualización** si está actualizando una definición existente.
1. Haga clic en **Importar**.

## Registro {#logging}

Con CRXDE Lite puede mostrar el archivo `error.log` que se encuentra en el sistema de archivos `<crx-install-dir>/crx-quickstart/server/logs` y filtrarlo con el nivel de registro adecuado. Proceda de la siguiente manera:

1. Abra CRXDE Lite en el navegador 
1. En la ficha **Consola** de la parte inferior de la ventana, en el menú desplegable de la derecha, seleccione Registros **del servidor**.

1. Haga clic en el icono **Detener** para mostrar los mensajes.

Puede hacer lo siguiente:

* Ajuste los parámetros de registro en la consola Félix haciendo clic en el icono **Configuración** de registro.
* Para borrar los mensajes, haga clic en el icono **Pincel** .
* Anclar el mensaje en la selección actual haciendo clic en el icono **Anclar** .
* Para activar o desactivar la visualización de mensajes, haga clic en el icono **Detener** .

## Control de acceso {#access-control}

>[!NOTE]
>
>Consulte Administración de [usuarios, grupos y derechos de acceso](/help/sites-administering/user-group-ac-admin.md) para obtener más información.
