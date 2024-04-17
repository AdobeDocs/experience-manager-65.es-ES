---
title: Desarrollo con CRXDE Lite
description: CRXDE Lite está incrustado en Adobe Experience Manager AEM () y le permite realizar tareas de desarrollo estándar en el explorador
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 4%

---

# Desarrollo con CRXDE Lite{#developing-with-crxde-lite}

En esta sección se describe cómo desarrollar la aplicación de Adobe Experience Manager AEM () mediante CRXDE Lite.

Consulte la documentación general para obtener más información sobre los diferentes entornos de desarrollo disponibles.

CRXDE Lite AEM está incrustado en la interfaz de usuario de y le permite realizar tareas de desarrollo estándar en el explorador. Con CRXDE Lite, puede crear un proyecto, crear y editar archivos (como .jsp y .java), carpetas, plantillas, componentes, cuadros de diálogo, nodos, propiedades y paquetes durante el registro.
Se recomienda utilizar el CRXDE Lite AEM cuando no tenga acceso directo al servidor de la. O bien, cuando desarrolle una aplicación ampliando o modificando los componentes predeterminados y los paquetes Java™, o cuando no necesite un depurador dedicado, la finalización del código y el resaltado de la sintaxis.

>[!NOTE]
>
>AEM A partir de la versión 6.5.5.0, el acceso anónimo del CRXDE Lite ya no es posible.
>Los usuarios se redirigen a la pantalla de inicio de sesión.


>[!NOTE]
>
>El Adobe recomienda que utilice la variable [AEM Herramientas para desarrolladores para Eclipse](/help/sites-developing/aem-eclipse.md) y el [AEM Extensión de corchetes de HTL](/help/sites-developing/aem-brackets.md) durante el desarrollo del proyecto.

## Introducción a CRXDE Lite {#getting-started-with-crxde-lite}

Para empezar a usar CRXDE Lite, siga estos pasos:

1. AEM Instalar.
1. En el explorador, introduzca `https://<host>:<port>/crx/de`. De forma predeterminada, es `https://localhost:4502/crx/de`.
1. Introduzca su **nombre de usuario** y **contraseña**. De forma predeterminada, es `admin` y `admin`.

1. Haz clic en **OK**.

La interfaz de usuario de CRXDE Lite tiene el siguiente aspecto en el explorador:

![chlimage_1-18](assets/crx-interface.jpg)

Ahora puede utilizar CRXDE Lite para desarrollar la aplicación.

## Información general sobre la interfaz de usuario {#overview-of-the-user-interface}

CRXDE Lite ofrece las siguientes funciones:

<table>
 <tbody>
  <tr>
   <td>Barra de conmutación superior</td>
   <td>Cambie rápidamente entre CRXDE Lite, Administrador de paquetes y Uso compartido de paquetes.</td>
  </tr>
  <tr>
   <td>Widget de ruta del nodo</td>
   <td><p>Muestra la ruta al nodo seleccionado.</p> <p>También puede utilizarlo para saltar a un nodo, introduciendo la ruta a mano o pegándola desde otro lugar, y pulsando Intro.</p> <p>También proporciona compatibilidad para buscar nodos con un nombre de nodo específico. Introduzca el nombre del nodo que desea encontrar y espere (o pulse el símbolo de búsqueda en el lado derecho). Puede intentar introducir, por ejemplo, la cadena <em>roble</em> en el widget para ver cómo funciona. Si se carga un nodo o nodos determinados en el panel del explorador, se muestra la lista y puede seleccionar la ruta y pulsar Intro para desplazarse hasta ella. Solo funciona para los nodos cargados en la aplicación cliente CRXDE en el explorador. Si desea buscar en todo el repositorio, utilice Herramientas y luego Consulta.</p> </td>
  </tr>
  <tr>
   <td>Panel del explorador</td>
   <td><p>Muestra un árbol de todos los nodos del repositorio.</p> <p>Haga clic en un nodo para mostrar sus propiedades en la <strong>Propiedades</strong> pestaña. Después de hacer clic en un nodo, puede seleccionar una acción en la barra de herramientas. Vuelva a hacer clic en el nodo para cambiarle el nombre.</p> <p>Filtro de navegación de árbol (icono binocular): permite filtrar los nodos del repositorio para los que el nombre contiene el texto de entrada. Solo se aplica a los nodos que se han cargado localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Panel de edición</td>
   <td><p><strong>Inicio</strong> pestaña: permite buscar contenido o documentación y acceder a recursos para desarrolladores (documentación, blog para desarrolladores, base de conocimiento) y asistencia (página principal de Adobe y centro de asistencia).<br /> </p> <p>Haga doble clic en un archivo de <strong>Explorer</strong> para que pueda mostrar su contenido. Por ejemplo, un archivo .jsp o .java. A continuación, puede modificarla y guardar los cambios.</p> <p>Una vez editado un archivo en la <strong>Editar</strong> , las siguientes herramientas están disponibles en la barra de herramientas:<br /> </p> - <strong>Mostrar en el árbol: </strong>muestra el archivo en el árbol del repositorio.<br /> - <strong>Buscar/Reemplazar...</strong>: buscar o reemplazar.<br /> <br /> Haga doble clic en la línea de estado del <strong>Editar</strong> El panel abre el <strong>Ir a línea</strong> para que pueda introducir un número de línea específico al que ir.<br /> </td>
  </tr>
  <tr>
   <td>Pestaña Propiedades<br /> </td>
   <td>Muestra las propiedades del nodo que ha seleccionado. Puede añadir nuevas propiedades o eliminar las existentes.<br /> </td>
  </tr>
  <tr>
   <td>Pestaña Control de acceso</td>
   <td><p>Mostrar permisos basados en la ruta, el nivel de repositorio o el principal.</p> <p>Los permisos se desglosan en</p> <p>- <strong>Política de control de acceso aplicable</strong>: Las políticas que se pueden aplicar a la selección.</p> <p>- <strong>Políticas de control de acceso local</strong>: Las políticas aplicadas localmente a la selección.</p> <p>- <strong>Políticas de control de acceso efectivas</strong>: las directivas aplicadas para la selección pueden configurarse localmente o heredarse de nodos principales.</p> <p>Nota. Para poder ver la información de control de acceso, el usuario que ha iniciado sesión en el CRXDE Lite debe tener derechos de lectura para las entradas ACL. El usuario anónimo no puede ver esta información de forma predeterminada: inicie sesión como administrador para ver la información, por ejemplo.</p> </td>
  </tr>
  <tr>
   <td>Pestaña Replicación</td>
   <td><p>Mostrar el estado de replicación del nodo. Puede replicar y replicar y eliminar el nodo.</p> </td>
  </tr>
  <tr>
   <td>Pestaña Consola<br /> </td>
   <td><p><strong>Registros de servidor</strong>:</p> <p>Muestra los mensajes de registro. Puede configurar el nivel de registro, borrar la consola, fijar la posición de desplazamiento seleccionada y activar o desactivar la visualización de mensajes.<br /> </p> <p><strong>Control de versiones</strong>:</p> <p>Muestra mensajes de control de versiones.<br /> </p> </td>
  </tr>
  <tr>
   <td>Pestaña Información de compilación<br /> </td>
   <td>Muestra información cuando se está creando un paquete.<br /> </td>
  </tr>
  <tr>
   <td>Actualizar<br /> </td>
   <td>Actualiza la selección. Los cambios de otros usuarios se actualizan en la vista del repositorio. Los cambios que ha realizado no se ven afectados.<br /> </td>
  </tr>
  <tr>
   <td>Guardar todos</td>
   <td><p><strong>Guardar todo</strong>:<br /> </p> <p>Guarda todos los cambios realizados. Hasta que haga clic en Guardar, los cambios son temporales y se pierden al salir de la consola.</p> <p><strong>Revertir</strong>:</p> <p>Descarta todos los cambios realizados en el nodo seleccionado desde la última acción de guardado y vuelve a cargar el estado del repositorio para el nodo seleccionado.</p> <p><strong>Revertir todo</strong>:</p> <p>Descarta todos los cambios realizados en todo el repositorio desde la última acción de guardado y vuelve a cargar el estado del repositorio.</p> </td>
  </tr>
  <tr>
   <td>Crear...<br /> </td>
   <td><p>Menú desplegable para crear lo siguiente en el nodo seleccionado:<br /> </p> <p>- <strong>Nodo</strong>: un nodo con un tipo de nodo arbitrario<br /> </p> <p>- <strong>Archivo</strong>: nodo nt:file y su subnodo nt:resource</p> <p>- <strong>Carpeta</strong>: nt:nodo de carpeta</p> <p>- <strong>Plantilla</strong>AEM : plantilla de</p> <p>- <strong>Componente</strong>AEM : componente</p> <p>- <strong>Diálogo</strong>AEM : cuadro de diálogo</p> </td>
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
   <td>Pega el nodo copiado bajo el nodo seleccionado.<br /> </td>
  </tr>
  <tr>
   <td>Mover...<br /> </td>
   <td>Mueve el nodo seleccionado al nodo definido a través del cuadro de diálogo.</td>
  </tr>
  <tr>
   <td>Cambiar nombre...<br /> </td>
   <td>Cambia el nombre del nodo seleccionado.<br /> </td>
  </tr>
  <tr>
   <td>Mixins...<br /> </td>
   <td>Permite agregar tipos de mezcla al tipo de nodo. Los tipos de mezcla se utilizan principalmente para agregar funciones avanzadas como versiones, control de acceso, referencias y bloqueo al nodo.</td>
  </tr>
  <tr>
   <td>Herramientas<br /> </td>
   <td><p>Menú desplegable con las siguientes herramientas:</p> <p>- <strong>Configuración del servidor...</strong>: para acceder a la consola Felix.</p> <p>- <strong>Consulta...</strong>: para consultar el repositorio.</p> <p>- <strong>Privilegios...</strong>: para abrir la administración de privilegios, donde puede ver y agregar privilegios.</p> <p>- <strong>Probar control de acceso...</strong>: un lugar en el que puede probar el permiso para una ruta o entidad de seguridad determinada.</p> <p>- <strong>Exportar tipo de nodo</strong>: para exportar tipos de nodos en el sistema como notación cnd.</p> <p>- <strong>Importar tipo de nodo...</strong>: para importar tipos de nodos mediante notación cnd.</p> <p>- <strong>Instalar SiteCatalyst Debugger...</strong>: instrucciones sobre cómo instalar Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget de inicio de sesión<br /> </td>
   <td><p>Muestra los usuarios que han iniciado sesión y el espacio de trabajo en el que han iniciado sesión, por ejemplo, admin@crx.default.</p> <p>Haga clic en él para iniciar sesión o volver a iniciar sesión como un usuario específico. Si no especifica un espacio de trabajo en el que iniciar sesión, se iniciará la sesión en el espacio de trabajo predeterminado, crx.default.</p> <p>Si desea examinar el repositorio como un usuario anónimo, utilice <strong>anónimo</strong> como nombre de inicio de sesión y cualquier contraseña (por ejemplo, un espacio o un punto).<br /> </p> <p>Si la autorización ya no es válida (por ejemplo, si ha caducado), se muestra el widget de inicio de sesión "<strong>Sin autorización; inicio de sesión...</strong>". Haga clic en él para volver a iniciar sesión.</p> </td>
  </tr>
 </tbody>
</table>

## Creación de una carpeta {#creating-a-folder}

Para crear una carpeta con el CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el panel de navegación, haga clic con el botón derecho en la carpeta en la que desea crear la carpeta y seleccione **Crear...**, entonces **Crear carpeta...**.

1. Introduzca la carpeta **Nombre** y haga clic en **OK**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de una plantilla {#creating-a-template}

Para crear una plantilla con un CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el panel de navegación, haga clic con el botón derecho en la carpeta donde desee crear la plantilla y seleccione **Crear...**, entonces **Crear plantilla...**.

1. Introduzca el **Etiqueta**, **Título**, **Descripción**, **Tipo de medio**, y **Clasificación** de la plantilla. Haga clic en **Siguiente**.

1. Este paso es opcional: establezca el **Rutas permitidas**. Clic **Siguiente**

1. Este paso es opcional: establezca el **Principales permitidos**. Haga clic en **Siguiente**.

1. Este paso es opcional: establezca el **Elementos secundarios permitidos**. Haz clic en **OK**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Esto crea lo siguiente:

* Un nodo de tipo `cq:Template` con propiedades de plantilla

* Un nodo secundario de tipo `cq:PageContent` con propiedades de contenido de página

Puede añadir propiedades a la plantilla: consulte las [Creación de una propiedad](#creating-a-property) sección.

## Creación de un componente {#creating-a-component}

La función que se describe aquí solo está disponible si está instalado CQ5, es decir, si el tipo de nodo `cq:Component` está disponible en el repositorio.

Para crear un componente con un CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el panel de navegación, haga clic con el botón derecho en la carpeta donde desee crear el componente y seleccione **Crear...**, entonces **Crear componente...**.

1. Introduzca el **Etiqueta**, **Título**, **Descripción**, **Tipo de superrecurso**, y **Grupo** del componente. Haga clic en **Siguiente**.

1. Este paso es opcional: establecer las propiedades del componente **Es un contenedor,** **Sin decoración**, **Nombre de celda**, y **Ruta de diálogo**. Haga clic en **Siguiente**.

1. Este paso es opcional: establecer la propiedad del componente **Principales permitidos**. Haga clic en **Siguiente**.

1. Este paso es opcional: establecer la propiedad del componente **Elementos secundarios permitidos**. Haz clic en **OK**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Esto crea lo siguiente:

* Un nodo de tipo `cq:Component`
* Propiedades del componente
* Un script .jsp de componente

## Creación de un cuadro de diálogo {#creating-a-dialog}

Para crear un cuadro de diálogo con el CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el panel Navegación, haga clic con el botón derecho en el componente donde desee crear el cuadro de diálogo y seleccione **Crear...**, entonces **Crear diálogo...**.

1. Introduzca el **Etiqueta** y el **Título**. Haz clic en **OK**.

1. Clic **Guardar todo** l para guardar los cambios en el servidor.

Crea un cuadro de diálogo con la siguiente estructura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Ahora puede adaptar el cuadro de diálogo a sus necesidades modificando propiedades o creando nodos.

También puede utilizar el Editor de cuadros de diálogo para editar un cuadro de diálogo. Al hacer doble clic en el nodo de diálogo en el CRXDE Lite, aparece el editor. Encontrará más información sobre el Editor de diálogos [aquí](/help/sites-developing/dialog-editor.md).

## Creación de un nodo {#creating-a-node}

Para crear un nodo con un CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el panel de navegación, haga clic con el botón derecho en el nodo en el que desea crear el nodo y seleccione **Crear...**, entonces **Crear nodo...**.
1. Introduzca el **Nombre** y el **Tipo**. Haz clic en **OK**.
1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Ahora puede adaptar el nodo a sus necesidades modificando propiedades o creando nodos.

>[!NOTE]
>
>La mayoría de las operaciones de edición, incluido Crear nodo, conserva todos los cambios en la memoria y solo los almacena en el repositorio al guardarlos (con el botón &quot;Guardar todo&quot;). Sin embargo, algunas operaciones, como mover, persisten automáticamente.
>
>La validación con respecto a si el nodo recién creado está permitido por el tipo de nodo del nodo principal también la realiza primero el repositorio JCR al guardar los cambios. Si recibe un mensaje de error al guardar un nodo, compruebe si la estructura de contenido es válida (por ejemplo, no puede crear un `nt:unstructured` nodo como elemento secundario de `nt:folder` node).

## Creación de una propiedad {#creating-a-property}

Para crear una propiedad con el CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el panel Navegación, seleccione el nodo al que desee agregar la nueva propiedad.
1. En el **Propiedades** en el panel inferior, introduzca la pestaña **Nombre**, el **Tipo**, y el **Valor**. Clic **Añadir**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de una secuencia de comandos {#creating-a-script}

Para crear una secuencia de comandos:

1. Abra el CRXDE Lite en el explorador.
1. En el panel Navegación, haga clic con el botón derecho en el componente donde desee crear el script y seleccione **Crear...**, entonces **Crear archivo...**.

1. Introduzca el archivo **Nombre** incluida su extensión. Haz clic en **OK**.

1. El nuevo archivo se abrirá como una pestaña en el panel de edición.
1. Edite el archivo.
1. Clic **Guardar todo** para guardar los cambios.

## Exportación e importación de tipos de nodo {#exporting-and-importing-node-types}

Con CRXDE Lite, puede importar o exportar definiciones de tipo de nodo en [Notación CND (Compact Namespace y Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar una definición de tipo de nodo:

1. Abra el CRXDE Lite en el explorador.
1. Seleccione el nodo requerido.
1. Seleccionar **Herramientas** entonces **Exportar tipo de nodo**.

1. La definición, en notación cnd, se muestra en el explorador. Guarde la información si es necesario.

Para importar una definición de tipo de nodo:

1. Abra el CRXDE Lite en el explorador.
1. Seleccionar **Herramientas** entonces **Importar tipo de nodo...**.

1. Introduzca la notación CDN para la definición en el cuadro de texto.
1. Marque **Permitir actualización** si está actualizando una definición existente.
1. Haga clic en **Importar**.

## Registro {#logging}

Con CRXDE Lite, puede mostrar el archivo `error.log` que se encuentra en el sistema de archivos en `<crx-install-dir>/crx-quickstart/server/logs` y filtrarlo con el nivel de registro adecuado. Proceda como se indica a continuación:

1. Abra el CRXDE Lite en el explorador.
1. En el **Consola** en la parte inferior de la ventana, en el menú desplegable de la derecha, seleccione **Registros de servidor**.

1. Haga clic en **Detener** para mostrar los mensajes.

Puede hacer lo siguiente:

* Ajuste los parámetros de registro en la consola Felix haciendo clic en el **Configuraciones de registro** icono.
* Borre los mensajes haciendo clic en el **Pincel** icono.
* Anclar el mensaje en la selección haciendo clic en **Fijar** icono.
* Habilite o deshabilite la visualización de mensajes haciendo clic en **Detener** icono.

## Control de acceso {#access-control}

>[!NOTE]
>
>Consulte [Administración de derechos de acceso, grupos y usuarios](/help/sites-administering/user-group-ac-admin.md) para obtener más información.
