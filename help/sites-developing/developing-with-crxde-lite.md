---
title: Desarrollo con CRXDE Lite
seo-title: Developing with CRXDE Lite
description: CRXDE Lite está incrustado en AEM y le permite realizar tareas de desarrollo estándar en el explorador
seo-description: CRXDE Lite is embedded into AEM and enables you to perform standard development tasks in the browser
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 5%

---

# Desarrollo con CRXDE Lite{#developing-with-crxde-lite}

En esta sección se describe cómo desarrollar la aplicación de AEM con CRXDE Lite.

Consulte la documentación de información general para obtener más información sobre los diferentes entornos de desarrollo disponibles.

CRXDE Lite está incrustado en AEM y le permite realizar tareas de desarrollo estándar en el explorador. Con CRXDE Lite, puede crear un proyecto, crear y editar archivos (como .jsp y .java), carpetas, plantillas, componentes, cuadros de diálogo, nodos, propiedades y paquetes durante el registro.
Se recomienda utilizar CRXDE Lite cuando no tenga acceso directo al servidor de AEM, cuando desarrolle una aplicación ampliando o modificando los componentes y paquetes Java predeterminados o cuando no necesite un depurador dedicado, la finalización del código y el resaltado de sintaxis.

>[!NOTE]
>
>A partir de AEM 6.5.5.0, el acceso anónimo de CRXDE Lite ya no es posible.
>Los usuarios se redirigen a la pantalla de inicio de sesión.


>[!NOTE]
>
>Se recomienda usar la variable [AEM herramientas para desarrolladores de Eclipse](/help/sites-developing/aem-eclipse.md) y [Extensión de AEM Brackets HTL](/help/sites-developing/aem-brackets.md) durante el desarrollo del proyecto.

## Introducción a CRXDE Lite {#getting-started-with-crxde-lite}

Para empezar con CRXDE Lite, siga estos pasos:

1. Instalar AEM.
1. En el explorador, introduzca `https://<host>:<port>/crx/de`. De forma predeterminada, es `https://localhost:4502/crx/de`.
1. Escriba la **username** y **password**. De forma predeterminada, es `admin` y `admin`.

1. Haga clic en **Aceptar**.

La interfaz de usuario del CRXDE Lite tiene el siguiente aspecto en el explorador:

![chlimage_1-18](assets/crx-interface.jpg)

Ahora puede utilizar CRXDE Lite para desarrollar su aplicación.

## Descripción general de la interfaz de usuario {#overview-of-the-user-interface}

CRXDE Lite ofrece las siguientes funciones:

<table>
 <tbody>
  <tr>
   <td>Barra de alternador superior</td>
   <td>Permite cambiar rápidamente entre CRXDE Lite, administrador de paquetes y uso compartido de paquetes.</td>
  </tr>
  <tr>
   <td>Widget de rutas de nodos</td>
   <td><p>Muestra la ruta al nodo seleccionado actualmente.</p> <p>También puede utilizarla para saltar a un nodo, introduciendo la ruta manualmente o pegándola desde otro lugar y pulsando Intro.</p> <p>También proporciona soporte para buscar nodos con un nombre de nodo específico. Introduzca el nombre del nodo que desea buscar y espere (o pulse el símbolo de búsqueda en el lado derecho). Puede intentar introducir, por ejemplo, la cadena <em>oak</em> en el widget para ver cómo funciona. Si se carga un nodo o nodos determinados en el panel del explorador, se mostrará la lista y podrá seleccionar la ruta y pulsar Intro para desplazarse hasta ella. Tenga en cuenta que solo funciona para los nodos cargados actualmente en la aplicación cliente CRXDE en el explorador. Si desea buscar en todo el repositorio, utilice Herramientas y, a continuación, Consulta.</p> </td>
  </tr>
  <tr>
   <td>Panel Explorador</td>
   <td><p>Muestra un árbol de todos los nodos del repositorio.</p> <p>Haga clic en un nodo para mostrar sus propiedades en la <strong>Propiedades</strong> pestaña . Después de hacer clic en un nodo, puede seleccionar una acción en la barra de herramientas. Vuelva a hacer clic en el nodo para cambiarle el nombre.</p> <p>Filtro de navegación de árbol (icono binocular): permite filtrar los nodos del repositorio para los que el nombre contiene el texto de entrada. Solo se aplica a los nodos que se han cargado localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Panel Editar</td>
   <td><p><strong>Página principal</strong> pestaña: permite buscar contenido o documentación y acceder a recursos para desarrolladores (documentación, blog para desarrolladores, base de conocimientos) y asistencia (página de inicio y centro de asistencia de Adobe).<br /> </p> <p>Haga doble clic en un archivo de la <strong>Explorer</strong> panel para mostrar su contenido; como, por ejemplo, un archivo .jsp o .java. A continuación, puede modificarlo y guardar los cambios.</p> <p>Una vez que se edita un archivo en la variable <strong>Editar</strong> , las siguientes herramientas están disponibles en la barra de herramientas:<br /> </p> - <strong>Mostrar en el árbol: </strong>muestra el archivo en el árbol del repositorio.<br /> - <strong>Buscar/reemplazar ...</strong>: realice la búsqueda o reemplace.<br /> <br /> Haga doble clic en la línea de estado de la variable <strong>Editar</strong> abre <strong>Ir a la línea</strong> para que pueda introducir un número de línea específico al que ir.<br /> </td>
  </tr>
  <tr>
   <td>Pestaña Propiedades<br /> </td>
   <td>Muestra las propiedades del nodo seleccionado. Puede agregar nuevas propiedades o eliminar las existentes.<br /> </td>
  </tr>
  <tr>
   <td>Ficha Control de acceso</td>
   <td><p>Mostrar permisos basados en la ruta actual, el nivel del repositorio o la entidad principal.</p> <p>Los permisos se desglosan en</p> <p>- <strong>Política de control de acceso aplicable</strong>: Políticas que se pueden aplicar a la selección actual.</p> <p>- <strong>Políticas de control de acceso local</strong>: Las políticas actuales se aplican localmente a la selección actual.</p> <p>- <strong>Políticas de control de acceso efectivas</strong>: Las políticas actuales aplicadas a la selección actual pueden establecerse localmente o heredarse de los nodos principales.</p> <p>Nota. Para poder ver la información de Control de acceso, el usuario que ha iniciado sesión en el CRXDE Lite debe tener derechos para leer entradas de ACL. El usuario anónimo no puede ver esta información de forma predeterminada: inicie sesión como, por ejemplo, administrador para ver la información.</p> </td>
  </tr>
  <tr>
   <td>Pestaña Replicación</td>
   <td><p>Muestra el estado de replicación del nodo actual. Puede replicar y replicar la eliminación del nodo actual.</p> </td>
  </tr>
  <tr>
   <td>Ficha Consola<br /> </td>
   <td><p><strong>Registros de servidor</strong>:</p> <p>Muestra mensajes de registro. Puede configurar el nivel de registro, borrar la consola, fijar en la posición de desplazamiento seleccionada y activar o desactivar la visualización de los mensajes.<br /> </p> <p><strong>Control de versión</strong>:</p> <p>Muestra mensajes de control de versiones.<br /> </p> </td>
  </tr>
  <tr>
   <td>Ficha Información de compilación<br /> </td>
   <td>Muestra información cuando se crea un paquete.<br /> </td>
  </tr>
  <tr>
   <td>Actualizar<br /> </td>
   <td>Actualiza la selección actual. Los cambios de otros usuarios se actualizan en la vista del repositorio. Los cambios realizados no se ven afectados.<br /> </td>
  </tr>
  <tr>
   <td>Guardar todos</td>
   <td><p><strong>Guardar todos</strong>:<br /> </p> <p>Guarda todos los cambios realizados. Hasta que haga clic en guardar, los cambios son temporales y se perderán al salir de la consola.</p> <p><strong>Revertir</strong>:</p> <p>Descarta todos los cambios realizados en el nodo seleccionado desde la última acción de guardado y luego vuelve a cargar el estado actual del repositorio para el nodo seleccionado.</p> <p><strong>Revertir todos</strong>:</p> <p>Descarta todos los cambios realizados en todo el repositorio desde la última acción de guardado y luego vuelve a cargar el estado actual del repositorio.</p> </td>
  </tr>
  <tr>
   <td>Crear ...<br /> </td>
   <td><p>Menú desplegable para crear lo siguiente en el nodo seleccionado:<br /> </p> <p>- <strong>Nodo</strong>: un nodo con un tipo de nodo arbitrario<br /> </p> <p>- <strong>Archivo</strong>: nt:file node y su nt:resource subnode</p> <p>- <strong>Carpeta</strong>: nt:folder node</p> <p>- <strong>Plantilla</strong>: AEM plantilla</p> <p>- <strong>Componente</strong>: AEM componente</p> <p>- <strong>Diálogo</strong>: Cuadro de diálogo AEM</p> </td>
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
   <td>Mueve el nodo seleccionado al nodo configurado a través del cuadro de diálogo.</td>
  </tr>
  <tr>
   <td>Cambiar nombre ...<br /> </td>
   <td>Cambia el nombre del nodo seleccionado.<br /> </td>
  </tr>
  <tr>
   <td>Clases...<br /> </td>
   <td>Permite añadir tipos de mezcla al tipo de nodo. Los tipos de mezcla se utilizan principalmente para añadir funciones avanzadas como versiones, control de acceso, referencia y bloqueo al nodo.</td>
  </tr>
  <tr>
   <td>Herramientas<br /> </td>
   <td><p>Menú desplegable con las siguientes herramientas:</p> <p>- <strong>Configuración del servidor...</strong>: para acceder a la consola Felix.</p> <p>- <strong>Consulta ...</strong>: para consultar el repositorio.</p> <p>- <strong>Privilegios ...</strong>: para abrir la administración de privilegios, donde puede ver y agregar privilegios.</p> <p>- <strong>Probar control de acceso ...</strong>: un lugar en el que se puede probar el permiso para una ruta determinada o principal.</p> <p>- <strong>Exportar tipo de nodo</strong>: para exportar tipos de nodos en el sistema como notación de cnd.</p> <p>- <strong>Importar tipo de nodo ...</strong>: para importar tipos de nodos mediante notación de cnd.</p> <p>- <strong>Instalar SiteCatalyst Debugger ...</strong>: instrucciones sobre cómo instalar Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget de inicio de sesión<br /> </td>
   <td><p>Muestra los usuarios que han iniciado sesión en ese momento y el espacio de trabajo en el que han iniciado sesión, por ejemplo, admin@crx.default.</p> <p>Haga clic en él para iniciar sesión o volver a iniciarla como un usuario específico. Si no especifica un espacio de trabajo en el que iniciar sesión, iniciará sesión en el espacio de trabajo predeterminado, crx.default.</p> <p>Si desea examinar el repositorio como usuario anónimo, utilice <strong>anonymous</strong> como nombre de inicio de sesión y cualquier contraseña (por ejemplo, un espacio o un punto).<br /> </p> <p>Si su autorización ya no es válida (por ejemplo, ha caducado), el widget de inicio de sesión mostrará "<strong>No autorizado - Iniciar sesión..</strong>". Haga clic en él para iniciar sesión de nuevo.</p> </td>
  </tr>
 </tbody>
</table>

## Creación de una carpeta {#creating-a-folder}

Para crear una carpeta con el CRXDE Lite :

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desee crear la nueva carpeta y seleccione **Crear...**, luego **Crear carpeta ...**.

1. Introduzca la carpeta **Nombre** y haga clic en **OK**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de una plantilla {#creating-a-template}

Para crear una plantilla con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en la carpeta donde desee crear la plantilla y seleccione **Crear...**, luego **Crear plantilla ...**.

1. Introduzca la variable **Etiqueta**, **Título**, **Descripción**, **Tipo de recurso** y **Clasificación** de la plantilla. Haga clic en **Siguiente**.

1. Este paso es opcional: configure la variable **Rutas permitidas**. Haga clic en **Siguiente**

1. Este paso es opcional: configure la variable **Principales permitidos**. Haga clic en **Siguiente**.

1. Este paso es opcional: configure la variable **Niños permitidos**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Crea:

* Un nodo de tipo `cq:Template` con propiedades de plantilla

* Un nodo secundario de tipo `cq:PageContent` con propiedades de contenido de página

Puede agregar propiedades a la plantilla: consulte [Creación de una propiedad](#creating-a-property) para obtener más información.

## Creación de un componente {#creating-a-component}

La función descrita aquí solo está disponible si está instalado CQ5, es decir, si el tipo de nodo `cq:Component` está disponible en el repositorio.

Para crear un componente con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en la carpeta donde desee crear el componente y seleccione **Crear...**, luego **Crear componente ...**.

1. Introduzca la variable **Etiqueta**, **Título**, **Descripción**, **Tipo de recurso superior** y **Grupo** del componente. Haga clic en **Siguiente**.

1. Este paso es opcional: establecer las propiedades del componente **Is Container,** **Sin decoración**, **Nombre de celda** y **Ruta de diálogo**. Haga clic en **Siguiente**.

1. Este paso es opcional: establecer la propiedad del componente **Principales permitidos**. Haga clic en **Siguiente**.

1. Este paso es opcional: establecer la propiedad del componente **Niños permitidos**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Crea:

* Un nodo de tipo `cq:Component`
* Propiedades del componente
* Un script .jsp de componente

## Creación de un cuadro de diálogo {#creating-a-dialog}

Para crear un cuadro de diálogo con el CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en el componente donde desee crear el cuadro de diálogo y seleccione **Crear...**, luego **Crear cuadro de diálogo...**.

1. Introduzca la variable **Etiqueta** y **Título**. Haga clic en **Aceptar**.

1. Haga clic en **Guardar todo** l para guardar los cambios en el servidor.

Crea un cuadro de diálogo con la siguiente estructura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Ahora puede adaptar el cuadro de diálogo a sus necesidades modificando propiedades o creando nuevos nodos.

También puede utilizar el Editor de cuadro de diálogo para editar un cuadro de diálogo. Al hacer doble clic en el nodo de diálogo en el CRXDE Lite, aparece el editor. Encontrará más información sobre el Editor de cuadro de diálogo [here](/help/sites-developing/dialog-editor.md).

## Creación de un nodo {#creating-a-node}

Para crear un nodo con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en el nodo en el que desee crear el nuevo nodo, seleccione **Crear...**, luego **Crear nodo ...**.
1. Introduzca la variable **Nombre** y **Tipo**. Haga clic en **Aceptar**.
1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

Ahora puede adaptar el nodo a sus necesidades modificando propiedades o creando nuevos nodos.

>[!NOTE]
>
>La mayoría de las operaciones de edición, incluido Crear nodo, guardan todos los cambios en la memoria y solo los almacenan en el repositorio al guardarlos (mediante el botón Guardar todo). Sin embargo, algunas operaciones como mover se mantienen automáticamente.
>
>La validación con respecto a si el nodo recién creado está permitido por el tipo de nodo del nodo principal también la realiza el repositorio JCR primero al guardar los cambios. Si recibe un mensaje de error al guardar un nodo, compruebe si la estructura de contenido es válida (por ejemplo, no puede crear un `nt:unstructured` como nodo secundario de `nt:folder` nodo ).

## Creación de una propiedad {#creating-a-property}

Para crear una propiedad con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, seleccione el nodo en el que desea agregar la nueva propiedad.
1. En el **Propiedades** en el panel inferior, introduzca la **Nombre**, el **Tipo** y **Valor**. Haga clic en **Agregar**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de una secuencia de comandos {#creating-a-script}

Para crear una nueva secuencia de comandos:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en el componente donde desee crear la secuencia de comandos, seleccione **Crear...**, luego **Crear archivo ...**.

1. Introduzca el archivo **Nombre** incluida su extensión. Haga clic en **Aceptar**.

1. El nuevo archivo se abre como una ficha en el panel Editar.
1. Edite el archivo.
1. Haga clic en **Guardar todo** para guardar los cambios.

## Exportación e importación de tipos de nodo {#exporting-and-importing-node-types}

Con el CRXDE Lite puede importar o exportar definiciones de tipo de nodo en [Anotación CND (espacio de nombres compacto y definición de tipo de nodo)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar una definición de tipo de nodo:

1. Abra CRXDE Lite en el navegador 
1. Seleccione el nodo requerido.
1. Select **Herramientas** then **Exportar tipo de nodo**.

1. La definición, en notación de código, se muestra en el explorador. Guarde la información si es necesario.

Para importar una definición de tipo de nodo:

1. Abra CRXDE Lite en el navegador 
1. Select **Herramientas** then **Importar tipo de nodo...**.

1. Introduzca la notación CND para la definición en el cuadro de texto.
1. Marque **Permitir actualización** si está actualizando una definición existente.
1. Haga clic en **Importar**.

## Registro {#logging}

Con el CRXDE Lite puede mostrar el archivo `error.log` que se encuentra en el sistema de archivos en `<crx-install-dir>/crx-quickstart/server/logs` y filtrarlo con el nivel de registro adecuado. Proceda de la siguiente manera:

1. Abra CRXDE Lite en el navegador 
1. En el **Consola** en la parte inferior de la ventana, en el menú desplegable de la derecha, seleccione **Registros del servidor**.

1. Haga clic en el **Stop** para mostrar los mensajes.

Puede hacer lo siguiente:

* Ajuste los parámetros de registro en la consola Felix haciendo clic en el botón **Configuraciones de registro** icono.
* Para borrar los mensajes, haga clic en el botón **Pincel** icono.
* Para anclar el mensaje a la selección actual, haga clic en el botón **Fijar** icono.
* Para habilitar o deshabilitar la visualización de mensajes, haga clic en el botón **Stop** icono.

## Control de acceso {#access-control}

>[!NOTE]
>
>Consulte [Administración de usuarios, grupos y derechos de acceso](/help/sites-administering/user-group-ac-admin.md) para obtener más información.
