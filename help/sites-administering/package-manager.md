---
title: Cómo trabajar con paquetes
seo-title: Cómo trabajar con paquetes
description: Conozca los aspectos básicos del trabajo con paquetes en AEM.
seo-description: Conozca los aspectos básicos del trabajo con paquetes en AEM.
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
translation-type: tm+mt
source-git-commit: 03967fcdc9685c9a8bf1dead4bd5e389603ff91b
workflow-type: tm+mt
source-wordcount: '3934'
ht-degree: 1%

---


# Cómo trabajar con paquetes{#how-to-work-with-packages}

Los paquetes permiten importar y exportar el contenido del repositorio. Por ejemplo, puede utilizar paquetes para instalar nueva funcionalidad, transferir contenido entre instancias y realizar una copia de seguridad del contenido del repositorio.

Se puede acceder a los paquetes y/o mantenerlos desde las páginas siguientes:

* [Administrador](#package-manager) de paquetes, que se utiliza para administrar los paquetes en la instancia de AEM local.

* [Distribución](#software-distribution) de software, un servidor centralizado que contiene tanto los paquetes disponibles públicamente como los privados para su compañía. Los paquetes públicos pueden contener revisiones, nuevas funcionalidades, documentación, etc.

Puede transferir paquetes entre el administrador de paquetes, la distribución de software y el sistema de archivos.

## ¿Qué son los paquetes? {#what-are-packages}

Un paquete es un archivo zip que contiene el contenido del repositorio en forma de serialización del sistema de archivos (llamada serialización &quot;vault&quot;). Esto proporciona una representación fácil de usar y editar de archivos y carpetas.

Los paquetes incluyen el contenido, tanto de la página como del proyecto, seleccionado con filtros.

Un paquete también contiene información meta de vault, incluidas las definiciones de filtros y la información de configuración de importación. Se pueden incluir en el paquete propiedades de contenido adicionales (que no se utilizan para la extracción de paquetes), como una descripción, una imagen visual o un icono; estas propiedades son para el consumidor del paquete de contenido y solo para fines informativos.

>[!NOTE]
>
>Los paquetes representan la versión actual del contenido en el momento en que se crea el paquete. No incluyen ninguna versión anterior del contenido que AEM en el repositorio.

Puede realizar las siguientes acciones con o con paquetes:

* Crear nuevos paquetes; definir la configuración y los filtros del paquete según sea necesario
* Contenido del paquete de previsualización (antes de la compilación)
* Compilación de paquetes
* Información del paquete de vista
* Contenido del paquete de vista (después de la compilación)
* Modificar la definición de los paquetes existentes
* Reconstruir paquetes existentes
* Volver a ajustar paquetes
* Descargue paquetes de AEM a su sistema de archivos
* Cargar paquetes del sistema de archivos en la instancia de AEM local
* Validar el contenido del paquete antes de la instalación
* Realizar una instalación de ejecución en seco
* Instalación de paquetes (AEM no instala automáticamente los paquetes después de cargarlos)
* Eliminar paquetes
* Descargar paquetes, como revisiones, de la biblioteca de distribución de software
* Cargar paquetes en la sección compañía interna de la biblioteca de distribución de software

## Información del paquete {#package-information}

Una definición de paquete se compone de varios tipos de información:

* [Configuración del paquete](#package-settings)
* [Filtros del paquete](#package-filters)
* [Capturas de pantalla del paquete](#package-screenshots)
* [Iconos de paquete](#package-icons)

### Configuración del paquete {#package-settings}

Puede editar una variedad de opciones de configuración de paquete para definir aspectos como la descripción del paquete, los errores relacionados, las dependencias y la información del proveedor.

El cuadro de diálogo **Configuración del paquete** está disponible mediante el botón **Editar** cuando [crea](#creating-a-new-package) o [edita](#viewing-and-editing-package-information) un paquete y proporciona tres fichas para la configuración. Una vez realizados los cambios, haga clic en **Aceptar** para guardarlos.

![packagesedit](assets/packagesedit.png)

| **Campo** | **Descripción** |
|---|---|
| Nombre | El nombre del paquete. |
| Agrupar | Nombre del grupo al que se va a agregar el paquete, para organizar los paquetes. Escriba el nombre de un grupo nuevo o seleccione un grupo existente. |
| Versión | Texto que se usará para la versión personalizada. |
| Descripción | Breve descripción del paquete. El formato se puede usar con formato HTML. |
| Miniatura    | El icono que aparece con la lista de paquetes. Haga clic en Examinar para seleccionar un archivo local. |

![chlimage_1-108](assets/chlimage_1-108.png)

<table>
 <tbody>
  <tr>
   <th><strong>Campo</strong></th>
   <th><strong>Descripción</strong></th>
   <th><strong>Formato/Ejemplo</strong></th>
  </tr>
  <tr>
   <td>Nombre</td>
   <td>El nombre del proveedor.</td>
   <td><em>Geometrixx AEM<br /> </em></td>
  </tr>
  <tr>
   <td>URL</td>
   <td>Dirección URL del proveedor.</td>
   <td><em>https://www.aem-geometrixx.com</em></td>
  </tr>
  <tr>
   <td>Vínculo</td>
   <td>Vínculo específico del paquete a una página de proveedor.</td>
   <td><em>https://www.aem-geometrixx.com/mypackage.html</em></td>
  </tr>
  <tr>
   <td>Requiere<br /> </td>
   <td>
    <ul>
     <li>Administrador: Seleccione cuándo el paquete solo puede instalarse mediante una cuenta con privilegios de administrador.</li>
     <li>Restart: Seleccione cuándo debe reiniciarse el servidor después de instalar el paquete.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Administración de AC</td>
   <td><p>Especifique cómo se gestiona la información de control de acceso definida en el paquete al importarlo:</p>
    <ul>
     <li><strong>Ignorar</strong></li>
     <li><strong>Sobrescribir</strong></li>
     <li><strong>Combinar</strong></li>
     <li><strong>Borrar</strong></li>
     <li><strong>MergePreserve</strong></li>
    </ul> <p>El valor predeterminado es <strong>Omitir</strong>.</p> </td>
   <td>
    <ul>
     <li><strong>Omitir</strong> : conservar las ACL en el repositorio</li>
     <li><strong>Sobrescribir</strong> : sobrescribir ACL en el repositorio</li>
     <li><strong>Combinar</strong> : combinar ambos conjuntos de ACL</li>
     <li><strong>ACL claras</strong>  y claras</li>
     <li><strong>CombinarConservar</strong> - combinar control de acceso en el contenido con el proporcionado con el paquete agregando las entradas de control de acceso de entidades principales que no están presentes en el contenido</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

![packagesdependencias](assets/packagesdependencies.png)

| **Campo** | **Descripción** | **Formato/Ejemplo** |
|---|---|---|
| Probado con | El nombre del producto y la versión de este paquete son compatibles o están dirigidos a ellos. | *AEM 6* |
| Problemas/errores solucionados | Campo de texto que permite lista de detalles de errores corregidos con este paquete. Lista cada error en una línea separada. | resumen de error-nr |
| Depende de | Lista la información de dependencia que debe respetarse siempre que se necesiten otros paquetes para permitir que el paquete actual se ejecute según lo esperado. Este campo es importante cuando se utilizan revisiones. | groupId:nombre:versión |
| Reemplaza | Una lista de paquetes obsoletos que este paquete reemplaza. Antes de realizar la instalación, compruebe que este paquete incluye todo el contenido necesario de los paquetes obsoletos para que no se sobrescriba ningún contenido. | groupId:nombre:versión |

### Filtros de paquete {#package-filters}

Los filtros identifican los nodos del repositorio que se incluirán en el paquete. Una **Definición de filtro** especifica la siguiente información:

* La **Ruta de raíz** del contenido que se va a incluir.
* **** Reglas que incluyen o excluyen nodos específicos debajo de la ruta raíz.

Los filtros pueden incluir cero o más reglas. Cuando no hay reglas definidas, el paquete contiene todo el contenido debajo de la ruta raíz.

Puede definir una o varias definiciones de filtro para un paquete. Utilice más de un filtro para incluir contenido de varias rutas raíz.

![chlimage_1-109](assets/chlimage_1-109.png)

En la tabla siguiente se describen estas reglas y se proporcionan ejemplos:

<table>
 <tbody>
  <tr>
   <th> Tipo de regla</th>
   <th>Descripción </th>
   <th>Ejemplo </th>
  </tr>
  <tr>
   <td> incluir</td>
   <td>Puede definir una ruta o utilizar una expresión normal para especificar todos los nodos que desee incluir.<br /> <br /> Si se incluye un directorio:
    <ul>
     <li>incluya ese directorio <i>y</i> todos los archivos y carpetas de ese directorio (es decir, todo el subárbol)</li>
     <li><strong>no </strong> incluir otros archivos o carpetas de la ruta raíz especificada</li>
    </ul> </td>
   <td>/libs/sling/install(/.*)? </td>
  </tr>
  <tr>
   <td> excluir</td>
   <td>Puede especificar una ruta o utilizar una expresión normal para especificar todos los nodos que desea excluir.<br /> <br /> Excluir un directorio excluirá ese directorio  <i></i> y todos los archivos y carpetas de ese directorio (es decir, todo el subárbol).<br /> </td>
   <td>/libs/wcm/foundation/components(/.*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Un paquete puede contener varias definiciones de filtro, de modo que los nodos de diferentes ubicaciones se pueden combinar fácilmente en un paquete.

Los filtros del paquete se definen con mayor frecuencia cuando [crea el paquete](#creating-a-new-package) por primera vez, pero también se pueden editar posteriormente (después de lo cual se debe volver a crear el paquete).

### Capturas de pantalla del paquete {#package-screenshots}

Puede adjuntar capturas de pantalla al paquete para proporcionar una representación visual del aspecto del contenido; por ejemplo, proporcionando capturas de pantalla de la nueva funcionalidad.

### Iconos de paquete {#package-icons}

También puede adjuntar un icono al paquete para proporcionar una representación visual de referencia rápida de lo que contiene el paquete. Esto se muestra en la lista del paquete y puede ayudarle a identificar fácilmente el paquete o la clase del paquete.

Como un paquete puede contener un icono, se utilizan las siguientes convenciones para los paquetes oficiales:

>[!NOTE]
>
>Para evitar confusiones, utilice un icono descriptivo para el paquete y no utilice uno de los iconos oficiales.

Paquete de revisión oficial:

![](do-not-localize/chlimage_1-28.png)

Paquete oficial AEM instalación o extensión:

Paquete de funciones oficiales:

![](do-not-localize/chlimage_1-29.png)

## el administrador de paquetes {#package-manager}

El Administrador de paquetes administra los paquetes de la instalación AEM local. Después de [asignar los permisos necesarios](#permissions-needed-for-using-the-package-manager), puede utilizar el Administrador de paquetes para diversas acciones, como configurar, crear, descargar e instalar los paquetes. Los elementos clave que se deben configurar son:

* [Configuración del paquete](#package-settings)
* [Filtros del paquete](#package-filters)

### Permisos necesarios para utilizar el Administrador de paquetes {#permissions-needed-for-using-the-package-manager}

Para otorgar a los usuarios el derecho de crear, modificar, cargar e instalar paquetes, debe darles los permisos adecuados en las siguientes ubicaciones:

* **/etc/packages** (derechos completos excluyendo delete)
* el nodo que contiene el contenido del paquete

Consulte [Configuración de permisos](/help/sites-administering/security.md#setting-page-permissions) para obtener instrucciones sobre cómo cambiar los permisos.

### Creación de un nuevo paquete {#creating-a-new-package}

Para crear una nueva definición de paquete:

1. En la pantalla de bienvenida de AEM, haga clic en **Paquetes** (o en el doble **Herramientas** de la consola, haga clic en **Paquetes**).

1. A continuación, seleccione **Administrador de paquetes**.
1. Haga clic en **Crear paquete**.

   >[!NOTE]
   >
   >Si la instancia tiene muchos paquetes, puede haber una estructura de carpetas en su lugar, por lo que puede desplazarse a la carpeta de destinatario requerida antes de crear el nuevo paquete.

1. En el cuadro de diálogo:

   ![packagesnew](assets/packagesnew.png)

   Introduzca el valor:

   * **Nombre del grupo**

      Nombre del grupo destinatario (o carpeta). Los grupos están pensados para ayudarle a organizar sus paquetes.

      Se creará una carpeta para el grupo si aún no existe. Si deja el nombre del grupo en blanco, creará el paquete en la lista del paquete principal (Inicio > Paquetes).

   * **Nombre del paquete**

      El nombre del nuevo paquete. Seleccione un nombre descriptivo para ayudarle (y a otros) a identificar fácilmente el contenido del paquete.

   * **Versión**

      Campo de texto para indicar una versión. Esto se agregará al nombre del paquete para formar el nombre del archivo zip.
   Haga clic en **Aceptar** para crear el paquete.

1. AEM lista el nuevo paquete en la carpeta de grupo correspondiente.

   ![packagesitem](assets/packagesitem.png)

   Haga clic en el icono o el nombre del paquete para abrirlo.

   ![packagesitemclicked](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >Si es necesario, puede volver a esta página más adelante.

1. Haga clic en **Editar** para editar la [configuración del paquete](#package-settings).

   Aquí puede agregar información y/o definir determinadas opciones de configuración; por ejemplo: una descripción, el [icono](#package-icons), errores relacionados y agregar detalles del proveedor.

   Haga clic en **Aceptar** una vez que haya terminado de editar la configuración.

1. Añada **[Capturas de pantalla](#package-screenshots)** en el paquete según sea necesario. Una instancia está disponible cuando se crea el paquete, agregue más si es necesario mediante **Captura de pantalla del paquete** desde la barra de tareas.

   Añada la imagen real haciendo clic con el doble en el componente de imagen en el área **Capturas de pantalla**, agregando una imagen y haciendo clic en **Aceptar**.

1. Defina los **[Filtros de paquete](#package-filters)** arrastrando las instancias de **Definición de filtro** desde la barra de tareas y, a continuación, haciendo clic con el doble para abrir y editar:

   ![packagesfilter](assets/packagesfilter.png)

   Especifique:

   * **Ruta de**
raízEl contenido que se va a empaquetar; puede ser la raíz de un subárbol.
   * ****
RulesRules son opcionales; para definiciones de paquetes simples, no es necesario especificar reglas de inclusión o exclusión.

      Si es necesario, puede definir [**Incluir** o **Excluir** reglas](#package-filters) para definir exactamente el contenido del paquete.

      Añada las reglas con el símbolo **+**, o bien elimine las reglas con el símbolo **-**. Las reglas se aplican según su orden, por lo que se colocan según sea necesario con los botones **Arriba** y **Abajo**.
   A continuación, haga clic en **Aceptar** para guardar el filtro.

   >[!NOTE]
   >
   >Puede utilizar tantas definiciones de filtro como necesite, aunque debe asegurarse de que no entran en conflicto. Use **Previsualización** para confirmar cuál será el contenido del paquete.

1. Para confirmar lo que contendrá el paquete, puede utilizar **Previsualización**. Esto realiza una ejecución seca del proceso de compilación y lista todo lo que se agregará al paquete cuando se cree realmente.
1. Ahora puede [compilar](#building-a-package) su paquete.

   >[!NOTE]
   >
   >No es obligatorio construir el paquete en este momento, puede hacerse en un momento posterior.

### Generación de un paquete {#building-a-package}

A menudo, un paquete se crea al mismo tiempo que [crea la definición del paquete](#creating-a-new-package), pero puede volver más adelante para crear o volver a compilar el paquete. Esto puede resultar útil si el contenido del repositorio ha cambiado.

>[!NOTE]
>
>Antes de crear el paquete, puede resultar útil la previsualización del contenido del mismo. Para ello, haga clic en **Previsualización**.

1. Abra la definición del paquete desde **Administrador de paquetes** (haga clic en el icono o nombre del paquete).

1. Haga clic en **Generar**. Un cuadro de diálogo solicita confirmación de que desea crear el paquete.

   >[!NOTE]
   >
   >Esto es de especial importancia cuando está reconstruyendo un paquete, ya que se sobrescribirá su contenido.

1. Haga clic en **Aceptar**. AEM creará el paquete, enumerando todo el contenido agregado al paquete tal como lo hace. Cuando se completa la AEM, se muestra una confirmación de que el paquete se creó y (al cerrar el cuadro de diálogo) se actualiza la información de la lista del paquete.

### Reajuste de un paquete {#rewrapping-a-package}

Una vez creado el paquete, se puede volver a ajustar, si es necesario.

Al volver a ajustar se cambia la información del paquete: *sin* cambiar el contenido del paquete. La información del paquete es la miniatura, la descripción, etc., en otras palabras todo lo que puede editar con el cuadro de diálogo **Configuración del paquete** (para abrir este clic **Editar**).

Un caso de uso importante para volver a ajustar es al preparar un paquete. Por ejemplo, puede tener un paquete existente y decidir compartirlo con otros. Para ello, desea agregar una miniatura y una descripción. En lugar de recrear todo el paquete con toda su funcionalidad (lo que puede llevar cierto tiempo y asumir el riesgo de que el paquete ya no sea idéntico al original), puede volver a ajustarlo y simplemente agregar la miniatura y la descripción.

1. Abra la definición del paquete desde **Administrador de paquetes** (haga clic en el icono o nombre del paquete).

1. Haga clic en **Editar** y actualice la **[Configuración del paquete](#package-settings)** según sea necesario. Haga clic en **Aceptar** para guardar.

1. Haga clic en **Volver a ajustar**, un cuadro de diálogo solicitará confirmación.

### Visualización y edición de la información del paquete {#viewing-and-editing-package-information}

Para vista o edición de información sobre una definición de paquete:

1. En el Administrador de paquetes, navegue hasta el paquete que desee vista.
1. Haga clic en el icono de paquete del paquete que desee vista. Esto abrirá la página del paquete con información sobre la definición del paquete:

   ![packagesitemclicked-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >También puede editar y realizar determinadas acciones en el paquete desde esta página.
   >
   >Los botones disponibles dependerán de si el paquete ya se ha creado o no.

1. Si el paquete ya se ha creado, haga clic en **Contenido**, se abrirá una ventana y se lista todo el contenido del paquete:

### Visualización del contenido del paquete y prueba de la instalación {#viewing-package-contents-and-testing-installation}

Después de crear un paquete, puede realizar la vista del contenido:

1. En el Administrador de paquetes, navegue hasta el paquete que desee vista.
1. Haga clic en el icono de paquete del paquete que desee vista. Esto abrirá la página del paquete con información sobre la definición del paquete.

1. Para vista del contenido, haga clic en **Contenido**, se abrirá una ventana y se realizará una lista de todo el contenido del paquete:

   ![packgescontents](assets/packgescontents.png)

1. Para realizar una ejecución seca de la instalación, haga clic en **Probar instalación**. Después de confirmar la acción, se abrirá una ventana y se lista el resultado como si la instalación se hubiera realizado:

   ![packagestestinstall](assets/packagestestinstall.png)

### Descarga de paquetes en el sistema de archivos {#downloading-packages-to-your-file-system}

En esta sección se describe cómo descargar un paquete de AEM a su sistema de archivos mediante **Administrador de paquetes**.

1. En la pantalla de bienvenida de AEM, haga clic en **Paquetes** y, a continuación, seleccione **Administrador de paquetes**.
1. Vaya al paquete que desee descargar.

   ![packagesdownload](assets/packagesdownload.png)

1. Haga clic en el vínculo formado por el nombre del archivo zip (subrayado) del paquete que desea descargar; por ejemplo `export-for-offline.zip`.

   AEM descarga el paquete en el equipo (mediante un cuadro de diálogo de descarga estándar del explorador).

### Carga de paquetes desde el sistema de archivos {#uploading-packages-from-your-file-system}

La carga de paquetes permite cargar un paquete desde el sistema de archivos en el Administrador de paquetes de AEM.
Para cargar un paquete:

1. Vaya al **Administrador de paquetes**. A continuación, vaya a la carpeta de grupo en la que desea que se cargue el paquete.

   ![packagesupload, botón](assets/packagesuploadbutton.png)

1. Haga clic en **Cargar paquete**.

   ![packagesupload addialog](assets/packagesuploaddialog.png)

   * **Archivo**

      Puede escribir el nombre del archivo directamente o utilizar el **Examinar...** para seleccionar el paquete requerido del sistema de archivos local (después de seleccionar **Aceptar**).

   * **Forzar carga**

      Si ya existe un paquete con este nombre, puede hacer clic en él para forzar la carga (y sobrescribir el paquete existente).
   Haga clic en **Aceptar** para que el nuevo paquete se cargue y aparezca en la lista del Administrador de paquetes.

   >[!NOTE]
   >
   >Para que el contenido esté disponible para AEM, asegúrese de [instalar el paquete](#installing-packages).

### Validación de paquetes {#validating-packages}

Antes de instalar un paquete, es posible que desee comprobar su contenido. Dado que los paquetes pueden modificar archivos superpuestos en `/apps` y/o agregar, modificar y eliminar ACL, a menudo resulta útil validar estos cambios antes de instalarlos.

#### Opciones de validación {#validation-options}

El mecanismo de validación puede comprobar las siguientes características del paquete:

* Importaciones de paquetes OSGi
* Superposiciones
* ACL

Estas opciones se detallan a continuación.

* **Validar importaciones de paquetes OSGi**

   **Qué está marcado**

   Esta validación inspecciona el paquete para todos los archivos JAR (paquetes OSGi), extrae su `manifest.xml` (que contiene las dependencias con versiones en las que se basa dicho paquete OSGi) y verifica la AEM instancia exporta dichas dependencias con las versiones correctas.

   **Cómo se informa**

   Todas las dependencias con versiones que no puedan ser satisfechas por la instancia de AEM se enumeran en el **Registro de Actividades** del Administrador de paquetes.

   **Estados de error**

   Si las dependencias no están satisfechas, los paquetes OSGi del paquete con esas dependencias no se inicio. Esto resulta en una implementación de aplicación dañada, ya que todo lo que dependa del paquete OSGi no iniciado no funcionará correctamente.

   **Resolución de errores**

   Para resolver errores debido a paquetes OSGi insatisfechos, es necesario ajustar la versión de dependencia del paquete con importaciones insatisfechas.

* **Validar capas**

   **Qué está marcado**

   Esta validación determina si el paquete que se está instalando contiene un archivo que ya está superpuesto en la instancia de AEM de destino.

   Por ejemplo, dado un overlay existente en `/apps/sling/servlet/errorhandler/404.jsp`, un paquete que contiene `/libs/sling/servlet/errorhandler/404.jsp`, de manera que cambiará el archivo existente en `/libs/sling/servlet/errorhandler/404.jsp`.

   **Cómo se informa**

   Estas superposiciones se describen en el **Registro de Actividades** del Administrador de paquetes.

   **Estados de error**

   Un estado de error significa que el paquete está intentando implementar un archivo que ya está superpuesto, por lo que los cambios en el paquete serán anulados (y por lo tanto &quot;ocultos&quot;) por la superposición y no surtirán efecto.

   **Resolución de errores**

   Para resolver este problema, el mantenedor del archivo de superposición en `/apps` debe revisar los cambios realizados en el archivo superpuesto en `/libs` e incorporar los cambios según sea necesario en la superposición ( `/apps`) y volver a implementar el archivo superpuesto.

   >[!NOTE]
   >
   >Tenga en cuenta que el mecanismo de validación no tiene forma de conciliar si el contenido superpuesto se ha incorporado correctamente en el archivo de superposición. Por lo tanto, esta validación seguirá informando sobre los conflictos incluso después de que se hayan realizado los cambios necesarios.

* **Validar ACL**

   **Qué está marcado**

   Esta validación comprueba qué permisos se agregan, cómo se gestionarán (combinar/reemplazar) y si los permisos actuales se verán afectados.

   **Cómo se informa**

   Los permisos se describen en el **Registro de Actividades** del Administrador de paquetes.

   **Estados de error**

   No se pueden proporcionar errores explícitos. La validación simplemente indica si se agregarán o se verán afectados los nuevos permisos ACL al instalar el paquete.

   **Resolución de errores**

   Utilizando la información proporcionada por la validación, los nodos afectados pueden revisarse en CRXDE y las ACL pueden ajustarse en el paquete según sea necesario.

   >[!CAUTION]
   >
   >Como práctica recomendada, se recomienda que los paquetes no afecten a las ACL proporcionadas por AEM, ya que esto puede provocar un comportamiento inesperado del producto.

#### Realizando validación {#performing-validation}

La validación de los paquetes se puede realizar de dos maneras diferentes:

* Mediante la interfaz de usuario del administrador de paquetes
* A través de una solicitud de POST HTTP como con cURL

>[!NOTE]
>
>La validación debe realizarse siempre después de cargar el paquete, pero antes de instalarlo.

**Validación de paquetes mediante el administrador de paquetes**

1. Abra el Administrador de paquetes en `https://<server>:<port>/crx/packmgr`
1. Seleccione el paquete en la lista y, a continuación, seleccione la lista desplegable **Más** en el encabezado y, a continuación, **Validar** en el menú desplegable.

   >[!NOTE]
   >
   >Esto debe hacerse después de cargar el paquete de contenido, pero antes de instalarlo.

1. En el cuadro de diálogo modal que aparece a continuación, utilice las casillas de verificación para seleccionar los tipos de validación y comenzar la validación haciendo clic en **Validar**. También puede hacer clic en **Cancelar**.

1. Las validaciones elegidas se ejecutan. Los resultados se muestran en el registro de actividades del Administrador de paquetes.

**Validación del paquete mediante solicitud de POST HTTP**

La solicitud de POST tiene el siguiente formato.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>El parámetro `type` puede ser cualquier lista sin ordenar separada por comas que consista en:
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`

>
>
El valor de `type` tiene el valor predeterminado `osgiPackageImports` si no se pasa.

El siguiente es un ejemplo de uso de cURL para ejecutar una validación de paquete.

1. Si utiliza cURL, ejecute una instrucción similar a la siguiente:

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. La validación solicitada se ejecuta y la respuesta se devuelve como un objeto JSON.

>[!NOTE]
>
>La respuesta a una solicitud de POST HTTP de validación será un objeto JSON con los resultados de la validación.

### Instalación de paquetes {#installing-packages}

Después de cargar un paquete, debe instalar el contenido. Para que el contenido del paquete esté instalado y en funcionamiento, es necesario que:

* cargado en AEM (ya sea [cargado desde su sistema de archivos](#uploading-packages-from-your-file-system) o descargado de [Software Distribution](#software-distribution))

* instalen

>[!CAUTION]
>
>La instalación de un paquete puede sobrescribir o eliminar el contenido existente. Cargue un paquete únicamente si está seguro de que no elimina o sobrescribe el contenido que necesita.
>
>Para ver el contenido o el impacto de un paquete, puede:
>
>* Realice una instalación de prueba del paquete sin modificar ningún contenido:
   >  Abra el paquete (haga clic en el icono o nombre del paquete) y haga clic en **Probar instalación**.
   >
   >
* Ver una lista del contenido del paquete:
   >  Abra el paquete y haga clic en **Contenido**.

>



>[!NOTE]
>
>Inmediatamente antes de la instalación del paquete, se crea un paquete de instantánea para que contenga el contenido que se sobrescribirá.
>
>Esta instantánea se reinstalará si desinstala el paquete.

>[!CAUTION]
>
>Si va a instalar recursos digitales, debe:
>
>* En primer lugar, desactive WorkflowLauncher.
   >  Utilice la opción de menú Componentes de la consola OSGi para desactivar `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`.
   >
   >
* A continuación, cuando se complete la instalación, reactive WorkflowLauncher.
>
>
Al desactivar WorkflowLauncher se garantiza que el marco del importador de recursos no manipule los recursos durante la instalación (de forma involuntaria).

1. En el Administrador de paquetes, navegue hasta el paquete que desee instalar.

   Se muestra un botón **Install** en el lado de Packages que todavía no se han instalado.

   >[!NOTE]
   >
   >También puede abrir el paquete haciendo clic en su icono para acceder al botón **Instalar** que se encuentra allí.

1. Haga clic en **Instalar** para inicio de la instalación. Un cuadro de diálogo solicitará confirmación y lista de todos los cambios que se realicen. Cuando termine, haga clic en **Cerrar** en el cuadro de diálogo.

   La palabra **Installed** aparece junto al paquete después de que se haya instalado.

### Carga e instalación basadas en el sistema de archivos {#file-system-based-upload-and-installation}

Hay una forma alternativa de cargar e instalar paquetes en su instancia. En el sistema de archivos, tiene una carpeta `crx-quicksart` junto con el archivo jar y `license.properties`. Debe crear una carpeta con el nombre `install` en `crx-quickstart`. Tendrás algo así: `<aem_home>/crx-quickstart/install`

En esta carpeta de instalación, puede agregar directamente los paquetes. Se cargarán e instalarán automáticamente en su instancia. Cuando haya terminado, podrá ver los paquetes en el Administrador de paquetes.

Si la instancia se está ejecutando, al agregar un paquete a la carpeta `install` se iniciará directamente la carga y la instalación en la instancia. Si su instancia no se está ejecutando, los paquetes que haya colocado en la carpeta `install` se instalarán al inicio en orden alfabético.

>[!NOTE]
>
>También puede hacerlo antes incluso de iniciar la instancia por primera vez. Para ello, debe crear la carpeta `crx-quickstart` manualmente, crear la carpeta `install` y colocar los paquetes allí. A continuación, cuando inicie la instancia por primera vez, los paquetes se instalarán en orden alfabético.

### Desinstalación de paquetes {#uninstalling-packages}

AEM le permite desinstalar paquetes. Esta acción revierte el contenido del repositorio que se ve afectado por la instantánea realizada inmediatamente antes de la instalación del paquete.

>[!NOTE]
>
>Tras la instalación, se crea un paquete de instantánea que contiene el contenido que se sobrescribirá.
>
>Este paquete se reinstalará cuando desinstale el paquete.

1. En el Administrador de paquetes, desplácese hasta el paquete que desee desinstalar.
1. Haga clic en el icono de paquete del paquete que desee desinstalar.
1. Haga clic en **Desinstalar** para eliminar el contenido de este paquete del repositorio. Un cuadro de diálogo solicitará confirmación y lista de todos los cambios que se realicen. Cuando termine, haga clic en **Cerrar** en el cuadro de diálogo.

### Eliminando paquetes {#deleting-packages}

Para eliminar un paquete de las listas del Administrador de paquetes:

>[!NOTE]
>
>Los archivos/nodos instalados del paquete se **no** eliminan.

1. En la consola **Tools**, expanda la carpeta **Packages** para mostrar el paquete en el panel derecho.

1. Haga clic en el paquete que desee eliminar para resaltarlo y, a continuación:

   * Haga clic en **Eliminar** en el menú de la barra de herramientas.
   * Haga clic con el botón derecho y seleccione **Eliminar**.

   ![empaquetesdelete](assets/packagesdelete.png)

1. AEM solicita confirmación de que desea eliminar el paquete. Haga clic en **Aceptar** para confirmar la eliminación.

>[!CAUTION]
>
>Si este paquete ya se ha instalado, se eliminará el contenido *instalado* **no**.

### Replicar paquetes {#replicating-packages}

Repita el contenido de un paquete para instalarlo en la instancia de publicación:

1. En el **Administrador de paquetes**, navegue al paquete que desee replicar.

1. Haga clic en el icono o en el nombre del paquete que desee replicar para expandirlo.
1. En el menú desplegable **Más** de la barra de herramientas, seleccione **Replicar**.

## Uso compartido de paquetes {#package-share}

Package Share era un servidor centralizado que se ponía a disposición del público para compartir Content-Packages.

Se ha reemplazado por [Distribución de software](#software-distribution).

## Distribución de software {#software-distribution}

[La ](https://downloads.experiencecloud.adobe.com) distribución de software es la nueva interfaz de usuario diseñada para simplificar la búsqueda y descarga de paquetes AEM.

Para obtener más información, consulte la [documentación de distribución de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html).

>[!CAUTION]
>
>AEM administrador de paquetes no se puede utilizar con Distribución de software por el momento, usted descarga los paquetes en su disco local.

