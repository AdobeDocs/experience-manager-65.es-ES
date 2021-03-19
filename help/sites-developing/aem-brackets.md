---
title: Extensión de AEM Brackets
seo-title: Extensión de AEM Brackets
description: Extensión de AEM Brackets
seo-description: nulo
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---


# Extensión de AEM Brackets{#aem-brackets-extension}

## Información general {#overview}

La extensión AEM Brackets proporciona un flujo de trabajo fluido para editar los componentes de AEM y las bibliotecas de cliente, y aprovecha la potencia del editor de código [Brackets](https://brackets.io/), que proporciona acceso desde el editor de código a los archivos y capas de Photoshop. La sencilla sincronización que proporciona la extensión (no se requiere Maven ni File Vault) aumenta la eficacia del desarrollador y también ayuda a los desarrolladores de front-end con conocimientos AEM limitados a participar en proyectos. Esta extensión también proporciona cierta compatibilidad con el [lenguaje de plantilla HTML (HTL)](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html), que elimina la complejidad de JSP para facilitar el desarrollo de componentes y aumentar su seguridad.

![imagen_1-53](assets/chlimage_1-53a.png)

### Características {#features}

Las principales características de la extensión AEM Brackets son:

* Sincronización automatizada de archivos modificados con la instancia de desarrollo de AEM.
* Sincronización bidireccional manual de archivos y carpetas.
* Sincronización completa de paquetes de contenido del proyecto.
* Finalización del código HTL para expresiones y `data-sly-*` instrucciones de bloque.

Además, Brackets incorpora muchas funciones útiles para los desarrolladores de fuentes AEM:

* Compatibilidad con archivos de Photoshop para extraer información de un archivo PSD, como capas, medidas, colores, fuentes, textos, etc.
* Sugerencias de código del PSD para reutilizar fácilmente esta información extraída en el código.
* Compatibilidad con preprocesadores CSS, como LESS y SCSS.
* Y cientos de extensiones adicionales que cubren necesidades más específicas.

## Instalación {#installation}

### Brackets {#brackets}

La extensión AEM Brackets es compatible con Brackets versión 1.0 o buenas.

Descargue la última versión de Brackets de [ackets.io](https://brackets.io/).

### La extensión {#the-extension}

Para instalar la extensión, siga estos pasos:

1. Abrir Brackets. En el menú **Archivo**, seleccione **Extension Manager...**
1. Introduzca **AEM** en la barra de búsqueda y busque **AEM Brackets Extension**.

   ![imagen_1-54](assets/chlimage_1-54a.png)

1. Haga clic en **Instalar**.
1. Cierre el cuadro de diálogo y el Extension Manager una vez completada la instalación.

## Introducción {#getting-started}

### El proyecto Content-Package {#the-content-package-project}

Una vez instalada la extensión, puede empezar a desarrollar componentes de AEM abriendo una carpeta de paquetes de contenido desde el sistema de archivos con Brackets.

El proyecto debe contener al menos:

1. una carpeta `jcr_root` (p. ej. `myproject/jcr_root`)

1. un archivo `filter.xml` (por ejemplo, `myproject/META-INF/vault/filter.xml`); para obtener más información sobre la estructura del archivo `filter.xml`, consulte la [definición del filtro del espacio de trabajo](https://jackrabbit.apache.org/filevault/filter.html).

En el menú **File** de Brackets, elija **Open Folder...** y elija la carpeta `jcr_root` o la carpeta del proyecto principal.

>[!NOTE]
>
>Si no tiene un proyecto propio con un paquete de contenido, puede probar el [HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). En GitHub, haga clic en **Descargar ZIP**, extraiga los archivos localmente y, como se ha indicado anteriormente, abra la carpeta `jcr_root` en Brackets. A continuación, siga los pasos a continuación para configurar la **Configuración del proyecto** y, por último, cargue todo el paquete en la instancia de desarrollo de AEM haciendo un **Paquete de contenido de exportación** como se indica en la sección Sincronización de paquetes de contenido completo .
>
>Después de estos pasos, debe poder acceder a la dirección URL `/content/todo.html` de la instancia de desarrollo de AEM y puede empezar a realizar modificaciones en el código en Brackets y ver cómo, después de hacer una actualización en el explorador web, los cambios se sincronizaron inmediatamente con el servidor de AEM.

### Configuración del proyecto {#project-settings}

Para sincronizar el contenido con y desde una instancia de desarrollo de AEM, debe definir la configuración del proyecto. Para ello, vaya al menú **AEM** y elija **Configuración del proyecto...**

![imagen_1-55](assets/chlimage_1-55a.png)

La Configuración del proyecto permite definir:

1. La URL del servidor (p. ej. `http://localhost:4502`)
1. tolerar servidores que no tengan un certificado HTTPS válido (mantener sin marcar, a menos que sea necesario)
1. El nombre de usuario utilizado para sincronizar contenido (por ejemplo, `admin`)
1. La contraseña del usuario (p. ej. `admin`)

## Sincronización de contenido {#synchronizing-content}

La extensión AEM Brackets proporciona los siguientes tipos de sincronización de contenido para archivos y carpetas permitidos por las reglas de filtrado definidas en `filter.xml`:

### Sincronización automatizada de archivos modificados {#automated-synchronization-of-changed-files}

Esto solo sincroniza los cambios de Brackets a la instancia de AEM, pero nunca al revés.

### Sincronización bidireccional manual {#manual-bidirectional-synchronization}

En el Explorador de proyectos, abra el menú contextual haciendo clic con el botón derecho en cualquier archivo o carpeta y se puede acceder a las opciones **Export to Server** o **Import from Server**.

![imagen_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Si la entrada seleccionada está fuera de la carpeta `jcr_root`, las entradas de menú contextual **Export to Server** y **Import from Server** están desactivadas.

### Sincronización completa de paquetes de contenido {#full-content-package-synchronization}

En el menú **AEM**, las opciones **Exportar paquete de contenido** o **Importar paquete de contenido** permiten sincronizar todo el proyecto con el servidor.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Estado de sincronización {#synchronization-status}

La extensión AEM Brackets incluye un icono de notificación en la barra de herramientas de la derecha de la ventana Brackets, que indica el estado de la última sincronización:

* verde: todos los archivos se han sincronizado correctamente
* azul: una operación de sincronización está en curso
* amarillo: algunos archivos no estaban sincronizados
* rojo: ninguno de los archivos se sincronizó

Al hacer clic en el icono de notificación, se abrirá el cuadro de diálogo del informe Estado de sincronización que enumera todos los estados de cada archivo sincronizado.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Solo se sincronizará el contenido marcado como incluido en las reglas de filtrado de `filter.xml` independientemente del método de sincronización utilizado.
>
>Además, los archivos `.vltignore` son compatibles para excluir el contenido de la sincronización con el repositorio y desde él.

## Edición del código HTL {#editing-htl-code}

La extensión AEM Brackets también incluye algunas funciones de finalización automática para facilitar la escritura de atributos y expresiones HTL.

### Autocompletar atributo {#attribute-auto-completion}

1. En un atributo HTML, escriba `sly`. El atributo se completa automáticamente como `data-sly-`.
1. Seleccione el atributo HTL en la lista desplegable.

### Finalización automática de expresiones {#expression-auto-completion}

Dentro de una expresión `${}`, los nombres de variables comunes se completan automáticamente.

## Más información {#more-information}

La extensión AEM Brackets es un proyecto de código abierto, alojado en GitHub por la organización [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud), en la licencia de Apache, versión 2.0:

* Repositorio de códigos: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licencia de Apache, versión 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

El editor de código Brackets también es un proyecto de código abierto, alojado en GitHub por la organización [Adobe Systems Incorporated](https://github.com/adobe):

* Repositorio de códigos: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

¡Siéntase libre de contribuir!
