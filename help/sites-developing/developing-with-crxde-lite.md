---
title: Desarrollo con CRXDE Lite
seo-title: Desarrollo con CRXDE Lite
description: CRXDE Lite está integrado en AEM y le permite realizar tareas de desarrollo estándar en el explorador
seo-description: CRXDE Lite está integrado en AEM y le permite realizar tareas de desarrollo estándar en el explorador
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: cb141914428f42a9755b5479ab1652c8ca51f640
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 5%

---


# Desarrollar con CRXDE Lite{#developing-with-crxde-lite}

En esta sección se describe cómo desarrollar su aplicación AEM con CRXDE Lite.

Consulte la documentación general para obtener más información sobre los diferentes entornos de desarrollo disponibles.

CRXDE Lite está integrado en AEM y le permite realizar tareas de desarrollo estándar en el explorador. Con CRXDE Lite, puede crear un proyecto, crear y editar archivos (como .jsp y .java), carpetas, plantillas, componentes, cuadros de diálogo, nodos, propiedades y paquetes durante el registro.
Se recomienda CRXDE Lite cuando no tenga acceso directo al servidor de AEM, cuando desarrolle una aplicación ampliando o modificando los componentes integrados y los paquetes de Java o cuando no necesite un depurador dedicado, la finalización del código y el resaltado de sintaxis.

>[!NOTE]
>
>A partir de AEM 6.5.5.0, el acceso anónimo de CRXDE Lite ya no es posible.
>Los usuarios son redirigidos a la pantalla de inicio de sesión.


>[!NOTE]
>
>Se recomienda utilizar las [Herramientas para desarrolladores de AEM para Eclipse](/help/sites-developing/aem-eclipse.md) y la [Extensión de chapas de AEM HTL](/help/sites-developing/aem-brackets.md) durante el desarrollo del proyecto.

## Introducción a CRXDE Lite {#getting-started-with-crxde-lite}

Para empezar con CRXDE Lite, siga estos pasos:

1. Instale AEM.
1. En el explorador, escriba `https://<host>:<port>/crx/de`. De forma predeterminada, es `https://localhost:4502/crx/de`.
1. Introduzca su **nombre de usuario** y **contraseña**. De forma predeterminada, es `admin` y `admin`.

1. Haga clic en **Aceptar**.

La interfaz de usuario de CRXDE Lite tiene el siguiente aspecto en el explorador:

![chlimage_1-18](assets/crx-interface.jpg)

Ahora puede usar CRXDE Lite para desarrollar su aplicación.

## Información general sobre la interfaz de usuario {#overview-of-the-user-interface}

CRXDE Lite oferta la siguiente funcionalidad:

<table>
 <tbody>
  <tr>
   <td>Barra de conmutación superior</td>
   <td>Permite cambiar rápidamente entre CRXDE Lite, administrador de paquetes y uso compartido de paquetes.</td>
  </tr>
  <tr>
   <td>Widget de ruta de nodo</td>
   <td><p>Muestra la ruta al nodo seleccionado actualmente.</p> <p>También puede utilizarla para saltar a un nodo, introduciendo la ruta a mano o pegándola desde otro lugar y pulsando Intro.</p> <p>También proporciona soporte para buscar nodos con un nombre de nodo específico. Escriba el nombre del nodo que desee encontrar y espere (o pulse el símbolo de búsqueda en el lado derecho). Puede intentar introducir, por ejemplo, la cadena <em>roak</em> en la utilidad para ver cómo funciona. Si un nodo o nodos determinados se cargan en el panel del explorador, se mostrará la lista y podrá seleccionar la ruta y pulsar Intro para desplazarse hasta ella. Tenga en cuenta que solo funciona con los nodos cargados actualmente en la aplicación cliente CRXDE en el navegador. Si desea buscar en todo el repositorio, utilice Herramientas y luego Consulta.</p> </td>
  </tr>
  <tr>
   <td>Panel Explorador</td>
   <td><p>Muestra un árbol de todos los nodos del repositorio.</p> <p>Haga clic en un nodo para mostrar sus propiedades en la ficha <strong>Propiedades</strong>. Después de hacer clic en un nodo, puede seleccionar una acción en la barra de herramientas. Vuelva a hacer clic en el nodo para cambiarle el nombre.</p> <p>Filtro de navegación de árbol (icono binocular): permite filtrar los nodos del repositorio para los que el nombre contiene el texto de entrada. Solo se aplica a los nodos que se han cargado localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Panel Editar</td>
   <td><p><strong></strong> Hometab: le permite buscar contenido y/o documentación y acceder a los recursos del desarrollador (documentación, blog del desarrollador, base de conocimiento) y a la asistencia (página principal de Adobe y centro de asistencia).<br /> </p> <p>Haga clic con el botón doble en un archivo del panel <strong>Explorador</strong> para mostrar su contenido; como, por ejemplo, un archivo .jsp o .java. A continuación, puede modificarlo y guardar los cambios.</p> <p>Una vez que se edita un archivo en el panel <strong>Editar</strong>, las siguientes herramientas están disponibles en la barra de herramientas:<br /> </p> - <strong>Mostrar en árbol: </strong>muestra el archivo en el árbol del repositorio.<br /> -  <strong>Buscar/Reemplazar ...</strong>: realice búsquedas o reemplace.<br /> <br /> Al hacer clic con el doble en la línea de estado del  <strong></strong> panel de edición, se abre el cuadro de diálogo  <strong>Ir a </strong> linedio para que pueda introducir un número de línea específico para ir.<br /> </td>
  </tr>
  <tr>
   <td>Ficha Propiedades<br /> </td>
   <td>Muestra las propiedades del nodo seleccionado. Puede agregar propiedades nuevas o eliminar las existentes.<br /> </td>
  </tr>
  <tr>
   <td>Ficha control de acceso</td>
   <td><p>Mostrar permisos basados en la ruta actual, nivel de repositorio o principal.</p> <p>Los permisos se desglosan en</p> <p>- <strong>Política de Control de acceso aplicable</strong>: Políticas que se pueden aplicar a la selección actual.</p> <p>- <strong>Políticas de Control de acceso local</strong>: Políticas actuales aplicadas localmente a la selección actual.</p> <p>- <strong>Políticas de Control de acceso efectivas</strong>: Las políticas actuales aplicadas a la selección actual pueden establecerse localmente o heredarse de los nodos principales.</p> <p>Nota. Para poder ver la información del Control de acceso, el usuario que ha iniciado sesión en el CRXDE Lite debe tener derechos para leer entradas ACL. El usuario anónimo no puede ver esta información de forma predeterminada: inicie sesión como, por ejemplo, administrador para ver la información.</p> </td>
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
   <td>Información de compilación, ficha<br /> </td>
   <td>Muestra información cuando se está generando un paquete.<br /> </td>
  </tr>
  <tr>
   <td>Actualizar<br /> </td>
   <td>Actualiza la selección actual. Los cambios de otros usuarios se actualizan en la vista del repositorio. Los cambios realizados no se ven afectados.<br /> </td>
  </tr>
  <tr>
   <td>Guardar todos</td>
   <td><p><strong>Guardar todos</strong>:<br /> </p> <p>Guarda todos los cambios realizados. Hasta que haga clic en Guardar, los cambios serán temporales y se perderán al salir de la consola.</p> <p><strong>Revertir</strong>:</p> <p>Desecha todos los cambios realizados en el nodo seleccionado desde la última acción de guardar y, a continuación, vuelve a cargar el estado actual del repositorio para el nodo seleccionado.</p> <p><strong>Revertir todos</strong>:</p> <p>Desecha todos los cambios que ha realizado en todo el repositorio desde la última acción de guardar y, a continuación, vuelve a cargar el estado actual del repositorio.</p> </td>
  </tr>
  <tr>
   <td>Crear ...<br /> </td>
   <td><p>Menú desplegable para crear lo siguiente en el nodo seleccionado:<br /> </p> <p>- <strong>Nodo</strong>: un nodo con un tipo de nodo arbitrario<br /> </p> <p>- <strong>Archivo</strong>: nt:file node y su nt:resource subnode</p> <p>- <strong>Carpeta</strong>: nt:nodo de carpeta</p> <p>- <strong>Plantilla</strong>: Plantilla AEM</p> <p>- <strong>Componente</strong>: Componente AEM</p> <p>- <strong>Diálogo</strong>: Cuadro de diálogo AEM</p> </td>
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
   <td>Mover ...<br /> </td>
   <td>Mueve el nodo seleccionado al nodo definido a través del cuadro de diálogo.</td>
  </tr>
  <tr>
   <td>Cambiar nombre ...<br /> </td>
   <td>Cambia el nombre del nodo seleccionado.<br /> </td>
  </tr>
  <tr>
   <td>Clases...<br /> </td>
   <td>Permite agregar tipos de mezcla al tipo de nodo. Los tipos de mezclas se utilizan principalmente para añadir funciones avanzadas como versiones, controles de acceso, referencias y bloqueo al nodo.</td>
  </tr>
  <tr>
   <td>Herramientas<br /> </td>
   <td><p>Menú desplegable con las siguientes herramientas:</p> <p>- <strong>Configuración del servidor...</strong>: para acceder a la consola Felix.</p> <p>- <strong>Consulta...</strong>: para consulta del repositorio.</p> <p>- <strong>Privilegios...</strong>: para abrir la administración de privilegios, donde puede vista y agregar privilegios.</p> <p>- <strong>Control de acceso de prueba...</strong>: un lugar donde puede probar el permiso para una ruta determinada o principal.</p> <p>- <strong>Tipo de nodo de exportación</strong>: para exportar tipos de nodos en el sistema como notación de código.</p> <p>- <strong>Importar tipo de nodo...</strong>: para importar tipos de nodos mediante notación cnd.</p> <p>- <strong>Instalar SiteCatalyst Debugger...</strong>: instrucciones sobre cómo instalar Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Utilidad de inicio de sesión<br /> </td>
   <td><p>Muestra los usuarios que han iniciado sesión en ese momento y el espacio de trabajo en el que han iniciado sesión, por ejemplo: admin@crx.default.</p> <p>Haga clic en él para iniciar sesión o volver a iniciarla como un usuario específico. Si no especifica un espacio de trabajo en el que iniciar sesión, iniciará sesión en el espacio de trabajo predeterminado, crx.default.</p> <p>Si desea examinar el repositorio como usuario anónimo, utilice <strong>anónimo</strong> como nombre de inicio de sesión y cualquier contraseña (por ejemplo, un espacio o un punto).<br /> </p> <p>Si su autorización ya no es válida (por ejemplo, ha caducado), la utilidad de inicio de sesión muestra "<strong>No autorizado - Inicio de sesión...</strong>". Haga clic en él para volver a iniciar sesión.</p> </td>
  </tr>
 </tbody>
</table>

## Creación de una carpeta {#creating-a-folder}

Para crear una carpeta con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desea crear la nueva carpeta, seleccione **Crear...**, luego **Crear carpeta...**.

1. Introduzca la carpeta **Name** y haga clic en **OK**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de una plantilla {#creating-a-template}

Para crear una plantilla con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en la carpeta donde desee crear la plantilla y seleccione **Crear...**, luego **Crear plantilla...**.

1. Introduzca los valores **Label**, **Title**, **Description**, **Resource Type** y **Ranking** de la plantilla. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca las **Rutas permitidas**. Haga clic en **Siguiente**

1. Este paso es opcional: establezca **Padres permitidos**. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca los **elementos secundarios permitidos**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Crea:

* Un nodo de tipo `cq:Template` con propiedades Template

* Un nodo secundario de tipo `cq:PageContent` con propiedades de contenido de página

Puede agregar propiedades a la plantilla: consulte la sección [Creación de una propiedad](#creating-a-property).

## Creación de un componente {#creating-a-component}

La función descrita aquí solo está disponible si CQ5 está instalado, es decir, si el tipo de nodo `cq:Component` está disponible en el repositorio.

Para crear un componente con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desee crear el componente, seleccione **Crear...**, luego **Crear componente...**.

1. Introduzca los valores **Label**, **Title**, **Description**, **Super Resource Type** y **Group** del componente. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca las propiedades del componente **Es Contenedor,** **Sin decoración**, **Nombre de celda** y **Ruta de diálogo**. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca la propiedad del componente **Padres permitidos**. Haga clic en **Siguiente**. 

1. Este paso es opcional: establezca la propiedad del componente **Elementos secundarios permitidos**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Crea:

* Un nodo de tipo `cq:Component`
* Propiedades del componente
* Un script .jsp de componente

## Creación de un cuadro de diálogo {#creating-a-dialog}

Para crear un cuadro de diálogo con el CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en el componente en el que desea crear el cuadro de diálogo y seleccione **Crear...**, luego **Crear cuadro de diálogo...**.

1. Introduzca la **etiqueta** y el **título**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** l para guardar los cambios en el servidor.

Crea un cuadro de diálogo con la siguiente estructura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Ahora puede adaptar el cuadro de diálogo a sus necesidades modificando propiedades o creando nuevos nodos.

También puede utilizar el Editor de cuadros de diálogo para editar un cuadro de diálogo. Al hacer clic en el nodo de cuadro de diálogo en CRXDE Lite, aparecerá el editor. Encontrará más información sobre el Editor de cuadros de diálogo [aquí](/help/sites-developing/dialog-editor.md).

## Creación de un nodo {#creating-a-node}

Para crear un nodo con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en el nodo donde desee crear el nuevo nodo, seleccione **Crear...**, luego **Crear nodo...**.
1. Introduzca el **Nombre** y el **Tipo**. Haga clic en **Aceptar**.
1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Ahora puede adaptar el nodo a sus necesidades modificando propiedades o creando nuevos nodos.

>[!NOTE]
>
>La mayoría de las operaciones de edición, incluido Crear nodo, mantienen todos los cambios en la memoria y solo los almacena en el repositorio al guardarlos (mediante el botón &quot;Guardar todo&quot;). Sin embargo, algunas operaciones como mover se mantienen automáticamente.
>
>La validación con respecto a si el nuevo nodo creado está permitido por el tipo de nodo del nodo principal también la realiza el repositorio JCR primero al guardar los cambios. Si recibe un mensaje de error al guardar un nodo, compruebe si la estructura de contenido es válida (por ejemplo, no puede crear un nodo `nt:unstructured` como secundario de `nt:folder` nodo).

## Creación de una propiedad {#creating-a-property}

Para crear una propiedad con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, seleccione el nodo en el que desea agregar la nueva propiedad.
1. En la ficha **Propiedades** del panel inferior, introduzca **Nombre**, el **Tipo** y el **Valor**. Haga clic en **Agregar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de una secuencia de comandos {#creating-a-script}

Para crear una nueva secuencia de comandos:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en el componente en el que desea crear la secuencia de comandos, seleccione **Crear...**, luego **Crear archivo...**.

1. Introduzca el archivo **Name**, incluida su extensión. Haga clic en **Aceptar**.

1. El nuevo archivo se abre como una ficha en el panel Editar.
1. Edite el archivo.
1. Haga clic en **Guardar todo** para guardar los cambios.

## Exportación e importación de tipos de nodos {#exporting-and-importing-node-types}

Con CRXDE Lite puede importar y/o exportar definiciones de tipo de nodo en la notación [CND (Área de nombres compacta y definición de tipo de nodo)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar una definición de tipo de nodo:

1. Abra CRXDE Lite en el navegador 
1. Seleccione el nodo requerido.
1. Seleccione **Herramientas** y luego **Exportar tipo de nodo**.

1. La definición, en notación de código, se mostrará en el explorador. Guarde la información si es necesario.

Para importar una definición de tipo de nodo:

1. Abra CRXDE Lite en el navegador 
1. Seleccione **Herramientas** y luego **Importar tipo de nodo...**.

1. Introduzca la notación CND para la definición en el cuadro de texto.
1. Seleccione **Permitir actualización** si está actualizando una definición existente.
1. Haga clic en **Importar**.

## Registro {#logging}

Con CRXDE Lite puede mostrar el archivo `error.log` que se encuentra en el sistema de archivos en `<crx-install-dir>/crx-quickstart/server/logs` y filtrarlo con el nivel de registro adecuado. Proceda de la siguiente manera:

1. Abra CRXDE Lite en el navegador 
1. En la ficha **Consola** de la parte inferior de la ventana, en el menú desplegable de la derecha, seleccione **Registros del servidor**.

1. Haga clic en el icono **Detener** para mostrar los mensajes.

Puede hacer lo siguiente:

* Ajuste los parámetros de registro en la consola Félix haciendo clic en el icono **Configuraciones de registro**.
* Para borrar los mensajes, haga clic en el icono **Pincel**.
* Anclar el mensaje en la selección actual haciendo clic en el icono **Fijar**.
* Habilite o deshabilite la visualización de mensajes haciendo clic en el icono **Detener**.

## Control de acceso {#access-control}

>[!NOTE]
>
>Consulte [Administración de derechos de acceso, grupos y usuarios](/help/sites-administering/user-group-ac-admin.md) para obtener más información.
