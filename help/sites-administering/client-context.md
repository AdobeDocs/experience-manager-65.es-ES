---
title: ClientContext
seo-title: Client Context
description: Aprenda a utilizar Client Context en AEM.
seo-description: Learn how to use the Client Context in AEM.
uuid: 82b2f976-cb41-42f8-ad4b-3a5cd23cc5f5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7a3322fe-554e-479e-a27c-4259cdd3ba2e
docset: aem65
exl-id: 69c66c82-fbd6-406e-aefd-b85480a62109
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---

# ClientContext{#client-context}

>[!NOTE]
>
>Context del cliente ha sido reemplazado por ContextHub. Para obtener más información, consulte las [configuración]ch-configuring.md) y [desarrollador](/help/sites-developing/contexthub.md) documentación.

Client Context es un mecanismo que proporciona cierta información sobre la página y el visitante actuales. Se puede abrir mediante **Ctrl-Alt-C** (windows) o **control-opción-c** (Mac):

![](assets/clientcontext_alisonparker.png)

En ambas [entorno de publicación y creación que muestra información](#propertiesavailableintheclientcontext) acerca de:

* El visitante; según la instancia, se solicita o deriva cierta información.
* Etiquetas de página y el número de veces que el visitante actual ha accedido a estas etiquetas (esto se muestra cuando mueve el ratón sobre una etiqueta específica) .
* Información de la página.
* Información sobre el entorno técnico; como la dirección IP, el navegador y la resolución de pantalla.
* Cualquier segmento que esté resuelto actualmente.

Los iconos (solo disponibles en el entorno de creación) le permiten configurar los detalles de ClientContext:

![](do-not-localize/clientcontext_icons.png)

* **Editar**
Se abrirá una nueva página que le permitirá [editar, añadir o quitar una propiedad de perfil](#editingprofiledetails).

* **Cargar**
Puede [seleccione entre una lista de perfiles y cargue el perfil](#loading-a-new-user-profile) desea probar.

* **Restablecer**
Puede [restablecer el perfil](#resetting-the-profile-to-the-current-user) al del usuario actual.

## Componentes de Client Context disponibles {#available-client-context-components}

Client Context puede mostrar las siguientes propiedades ([según lo que se haya seleccionado mediante Editar](#adding-a-property-component)):

**Información del internauta** Muestra la siguiente información del lado del cliente:

* el **Dirección IP**
* **keywords** se usa para referencia de motores de búsqueda
* el **explorador** en uso
* el **Sistema operativo** (sistema operativo) en uso
* la pantalla **resolution**
* el **mouse X** position
* el **mouse Y** position

**Flujo de actividad** Proporciona información sobre la actividad social del usuario en varias plataformas; por ejemplo, los foros de AEM, blogs, clasificaciones, etc.

**Campaign** Permite a los autores simular una experiencia específica para una campaña. Este componente anula la resolución de campaña normal y la selección de experiencias para permitir la prueba de varias permutaciones.

La resolución de la campaña se basa normalmente en la propiedad priority de la campaña. La experiencia se selecciona normalmente en función de la segmentación.

**Carro de compras** Muestra la información del carro de compras, incluidas las entradas de productos (título, cantidad, precioCon formato, etc.), las promociones resueltas (título, mensaje, etc.) y cupones (código, descripción, etc.).

El almacén de sesiones del carro de compras también notifica al servidor de los cambios de promoción resueltos (según los cambios de segmentación) mediante ClientContextCartServlet.

**Almacén genérico** Es un componente genérico que muestra el contenido de una tienda. Es una versión de nivel inferior del componente Propiedades genéricas del almacén.

El almacén genérico debe configurarse con un procesador JS que muestre los datos de forma personalizada.

**Propiedades de almacén genéricas** Es un componente genérico que muestra el contenido de una tienda. Es una versión de nivel superior del componente Tienda genérica .

El componente Propiedades genéricas de la tienda incluye un procesador predeterminado que enumera las propiedades configuradas (junto con una miniatura).

**Geolocalización** Muestra la latitud y la longitud del cliente. Utiliza la API de geolocalización de HTML5 para consultar el explorador para la ubicación actual. Esto hace que se muestre una ventana emergente al visitante, donde el explorador le pregunta si está de acuerdo con compartir su ubicación.

Cuando se muestra en Context Cloud, el componente utiliza una API de Google para mostrar un mapa como miniatura. El componente está sujeto a la API de Google [límites de uso](https://developers.google.com/maps/documentation/staticmaps/intro#Limits).

>[!NOTE]
>
>En AEM 6.1, el almacén de geolocalización ya no proporciona la función de geocodificación inversa. Por lo tanto, el almacén de geolocalización ya no recupera detalles sobre la ubicación actual, como el nombre de la ciudad o el código de país. Los segmentos que utilicen estos datos de almacenamiento no funcionarán correctamente. El almacén de geolocalización solo contiene la latitud y la longitud de una ubicación.

**Tienda JSONP** Componente que muestra el contenido que depende de la instalación.

El estándar JSONP es un complemento de JSON que permite evitar la misma política de origen (lo que hace imposible que una aplicación web se comunique con servidores que están en otro dominio). Consiste en ajustar el objeto JSON en una llamada de función para poder cargarlo como un `<script>` del otro dominio (que es una excepción permitida a la misma directiva de origen).

La tienda JSONP es como cualquier otra tienda, pero carga información que proviene de otro dominio sin necesidad de tener un proxy para esa información en el dominio actual. Consulte el ejemplo en [Almacenamiento de datos en Client Context mediante JSONP](/help/sites-administering/client-context.md#storing-data-in-client-context-via-jsonp).

>[!NOTE]
>
>La tienda JSONP no almacena en caché la información de la cookie, pero recupera esos datos en cada carga de página.

**Datos de perfil** Muestra información recopilada en el perfil del usuario. Por ejemplo, sexo, edad, dirección de correo electrónico, entre otros.

**Segmentos resueltos** Muestra qué segmentos se resuelven actualmente (a menudo dependen de otra información mostrada en ClientContext). Esto es de interés al configurar una campaña.

Por ejemplo, si el ratón está actualmente sobre la parte izquierda o derecha de la ventana. Este segmento se utiliza principalmente para pruebas, ya que los cambios se pueden ver inmediatamente.

**Gráfico social** Muestra el gráfico social de los amigos y seguidores del usuario.

>[!NOTE]
>
>Actualmente, se trata de una función de demostración que se basa en conjuntos de datos preconfigurados en los nodos de perfil de nuestros usuarios de demostración. Por ejemplo, consulte:
>
>`/home/users/geometrixx/aparker@geometrixx.info/profile` => propiedad friends

**Nube de etiquetas** Muestra las etiquetas establecidas en la página actual y las recopiladas al navegar por el sitio. Al mover el ratón sobre una etiqueta se muestra el número de veces que el usuario actual ha accedido a páginas que contienen esa etiqueta específica.

>[!NOTE]
Las etiquetas establecidas en los recursos DAM que se muestran en las páginas visitadas no se contarán.

**Almacenamiento tecnográfico** Este componente depende de la instalación.

**Productos vistos** Realiza un seguimiento de los productos que el comprador ha visto. Se puede consultar el producto que se ha visto más recientemente o el producto que se ha visto más recientemente y que no está ya en el carro de compras.

Este almacén de sesiones no tiene un componente de contexto de cliente predeterminado.

Para obtener más información, consulte [Client Context en detalle](/help/sites-developing/client-context.md).

>[!NOTE]
Los datos de página ya no están en ClientContext como componente predeterminado. Si es necesario, puede agregarlo editando el contexto del cliente y añadiendo la variable **Propiedades de almacén genéricas** y, a continuación, configurarlo para definir la variable **Tienda** como `pagedata`.

## Cambio del perfil de contexto de cliente {#changing-the-client-context-profile}

Client Context le permite cambiar detalles de forma interactiva:

* Si cambia el perfil que se utiliza en Client Context, podrá ver las diferentes experiencias que verán los distintos usuarios en la página actual.
* Además de cambiar el perfil de usuario, puede cambiar algunos detalles del perfil para ver cómo difiere la experiencia de la página en diversas condiciones.

### Carga de un nuevo perfil de usuario {#loading-a-new-user-profile}

Puede cambiar el perfil mediante:

* [uso del icono de carga](#loading-a-new-visitor-profile-with-the-load-profile-icon)
* [uso del control deslizante de selección](#loadinganewvisitorprofilewiththeselectionslider)

Cuando haya terminado, puede [restablecer el perfil](#resetting-the-profile-to-the-current-user).

#### Cargar un nuevo perfil del visitante con el icono Cargar perfil {#loading-a-new-visitor-profile-with-the-load-profile-icon}

1. Haga clic en el icono Cargar perfil :

   ![](do-not-localize/clientcontext_loadprofile.png)

1. Se abrirá el cuadro de diálogo, donde puede seleccionar el perfil que desea cargar:

   ![](assets/clientcontext_profileloader.png)

1. Haga clic en **OK** para cargar.

#### Carga de un nuevo perfil de usuario con el control deslizante de selección {#loading-a-new-user-profile-with-the-selection-slider}

También puede seleccionar un perfil con el control deslizante de selección:

1. Haga doble clic en el icono que representa al usuario actual. Se abrirá el selector, utilice las flechas para navegar y ver los perfiles disponibles:

   ![](assets/clientcontext_profileselector.png)

1. Haga clic en el perfil que desee cargar. Cuando se hayan cargado los detalles, haga clic fuera del selector para cerrar.

#### Restablecer el perfil al usuario actual {#resetting-the-profile-to-the-current-user}

1. Utilice el icono de restablecimiento para devolver el perfil de Client Context al del usuario actual:

   ![](do-not-localize/clientcontext_resetprofile.png)

### Cambio de la plataforma del explorador {#changing-the-browser-platform}

1. Haga doble clic en el icono que representa la plataforma del explorador. Se abrirá el selector, utilizará las flechas para navegar y verá las plataformas/navegadores disponibles:

   ![](assets/clientcontext_browserplatform.png)

1. Haga clic en el explorador de la plataforma que desee cargar. Cuando se hayan cargado los detalles, haga clic fuera del selector para cerrar.

### Cambio de la geolocalización {#changing-the-geolocation}

1. Haga doble clic en el icono de geolocalización. Se abrirá un mapa expandido, donde puede arrastrar el marcador a una nueva ubicación:

   ![](assets/clientcontext_geomocationrelocate.png)

1. Haga clic fuera del mapa para cerrar.

### Cambio de la selección de etiquetas {#changing-the-tag-selection}

1. Haga doble clic en la sección Nube de etiquetas de Client Context. Se abrirá el cuadro de diálogo, donde puede seleccionar etiquetas:

   ![](assets/clientcontext_tagselection.png)

1. Haga clic en Aceptar para cargar en Client Context.

## Edición de Client Context {#editing-the-client-context}

La edición de un contexto de cliente se puede utilizar para establecer (o restablecer) los valores de ciertas propiedades, agregar una nueva propiedad o quitar una que ya no sea necesaria.

### Edición de detalles de propiedades {#editing-property-details}

La edición de un contexto de cliente se puede utilizar para establecer (o restablecer) los valores de ciertas propiedades. Esto le permite probar escenarios específicos (especialmente útil para [segmentación](/help/sites-administering/campaign-segmentation.md) y [campañas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)).

![](assets/clientcontext_alisonparker_edit.png)

### Adición de un componente de propiedad {#adding-a-property-component}

Una vez que haya abierto el **página de diseño del ClientContext**, también puede **Agregar** una propiedad completamente nueva que utilice los componentes disponibles (los componentes aparecen en la barra de tareas o en la barra de tareas **Insertar nuevo componente** que se abre después de hacer doble clic en el botón **Arrastrar componentes o recursos aquí** ):

![](assets/clientcontext_alisonparker_new.png)

### Eliminación de un componente de propiedad {#removing-a-property-component}

Una vez que haya abierto el **página de diseño del ClientContext**, también puede **Eliminar** una propiedad si ya no es necesaria. Esto incluye las propiedades proporcionadas de forma predeterminada; **Restablecer** se restablecerán si se han eliminado.

## Almacenamiento de datos en Client Context mediante JSONP {#storing-data-in-client-context-via-jsonp}

Siga este ejemplo para utilizar el componente de almacén de contexto de la tienda JSONP para añadir datos externos a Client Context. A continuación, cree un segmento basado en la información de esos datos. El ejemplo utiliza el servicio JSONP que proporciona WIPmania.com. El servicio devuelve información de geolocalización basada en la dirección IP del cliente web.

Este ejemplo utiliza el sitio web de muestra de Geometrixx Outdoors para acceder a Client Context y probar el segmento creado. Puede utilizar un sitio web diferente siempre que la página haya habilitado Client Context. (Consulte [Adición de contexto de cliente a una página](/help/sites-developing/client-context.md#adding-client-context-to-a-page).)

### Añadir el componente de la tienda JSONP {#add-the-jsonp-store-component}

Agregue el componente Tienda JSONP a Client Context y utilícelo para recuperar y almacenar información de geolocalización sobre el cliente web.

1. Abra la página de inicio en inglés del sitio de Geometrixx Outdoors en la instancia de autor de AEM. ([https://localhost:4502/content/geometrixx-outdoors/en.html](https://localhost:4502/content/geometrixx-outdoors/en.html)).
1. Para abrir Client Context, pulse Ctrl-Alt-c (windows) o control-opción-c (Mac).
1. Haga clic en el icono de edición en la parte superior de Client Context para abrir Client Context Designer.

   ![](do-not-localize/chlimage_1.png)

1. Arrastre el componente Tienda JSONP a Client Context.

   ![](assets/chlimage_1-4.jpeg)

1. Haga doble clic en el componente para abrir el cuadro de diálogo de edición.
1. En el cuadro URL del servicio JSONP, introduzca la siguiente URL y, a continuación, haga clic en Buscar almacén:

   `https://api.wipmania.com/jsonp?callback=${callback}`

   El componente llama al servicio JSONP y enumera todas las propiedades que contienen los datos devueltos. Las propiedades que están en la lista son las que estarán disponibles en Client Context.

   ![](assets/chlimage_1-40.png)

1. Haga clic en Aceptar.
1. Vuelva a la página de inicio de Geometrixx Outdoors y actualice la página. Client Context ahora incluye la información del componente Tienda JSONP.

   ![](assets/chlimage_1-41.png)

### Creación del segmento {#create-the-segment}

Utilice los datos del almacén de sesiones que ha creado con el componente de almacén JSONP. El segmento utiliza la latitud del almacén de sesiones y la fecha actual para determinar si es invierno en la ubicación del cliente.

1. Abra la consola Herramientas en el explorador web (`https://localhost:4502/miscadmin#/etc`).
1. En el árbol de carpetas, haga clic en la carpeta Herramientas/Segmentación y, a continuación, haga clic en Nuevo > Nueva carpeta. Especifique los siguientes valores de propiedad y haga clic en Crear:

   * Nombre: mysegments
   * Título: Mis segmentos

1. Seleccione la carpeta Mis segmentos y haga clic en Nuevo > Nueva página:

   1. Para el Título, escriba Invierno.
   1. Seleccione la plantilla Segmento .
   1. Haga clic en Crear.

1. Haga clic con el botón derecho en el segmento Invierno y haga clic en Abrir.
1. Arrastre la propiedad de almacén genérico al contenedor AND predeterminado.

   ![](assets/chlimage_1-5.jpeg)

1. Haga doble clic en el componente para abrir el cuadro de diálogo de edición, especifique los siguientes valores de propiedad y, a continuación, haga clic en Aceptar:

   * Tienda: wipmania
   * Nombre de propiedad: latitude
   * Operador: es bueno que
   * Valor de propiedad: 30

1. Arrastre el componente Script al mismo contenedor AND y abra su cuadro de diálogo de edición. Agregue la siguiente secuencia de comandos y haga clic en Aceptar:

   `3 < new Date().getMonth() < 12`
