---
title: AEM Extensión de corchetes de
description: Aprenda a utilizar la extensión de Adobe Experience Manager para corchetes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# AEM Extensión de corchetes de{#aem-brackets-extension}

## Información general {#overview}

AEM AEM La extensión de brackets proporciona un flujo de trabajo fluido para editar componentes y bibliotecas de cliente, y usa la potencia del editor de código [Brackets](https://brackets.io/), que proporciona acceso desde el editor de código a archivos y capas de Photoshop. AEM La fácil sincronización que proporciona la extensión (no se requiere Maven ni File Vault) aumenta la eficacia del desarrollador y también ayuda a los desarrolladores de front-end con conocimientos limitados a participar en proyectos. Esta extensión también proporciona cierta compatibilidad con el [Lenguaje de HTML de plantillas (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es), que elimina la complejidad de JSP para facilitar el desarrollo de componentes y hacerlos más seguros.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Características {#features}

AEM Las principales características de la extensión de corchetes de la son:

* AEM Sincronización automatizada de los archivos modificados en la instancia de desarrollo de la.
* Sincronización bidireccional manual de archivos y carpetas.
* Sincronización completa del paquete de contenido del proyecto.
* Finalización de código HTL para expresiones e instrucciones de bloque `data-sly-*`.

AEM Además, Brackets incluye muchas funciones útiles para los desarrolladores de front-end de:

* Compatibilidad con archivos Photoshop para extraer información de un archivo de PSD, como capas, medidas, colores, fuentes, textos, etc.
* Sugerencias para el código del PSD para reutilizar fácilmente esta información extraída en el código.
* Compatibilidad con preprocesadores CSS, como LESS y SCSS.
* Y cientos de extensiones adicionales que cubren necesidades más específicas.

## Instalación {#installation}

### Corchetes {#brackets}

AEM La extensión de corchetes de la serie admite corchetes de la versión 1.0 o posterior.

Descargue la versión más reciente de Brackets de [brackets.io](https://brackets.io/).

### La extensión de {#the-extension}

Para instalar la extensión, siga estos pasos:

1. Abra los corchetes. En el menú **Archivo**, seleccione **Extension Manager...**
1. AEM AEM Escriba **&#x200B;**&#x200B;en la barra de búsqueda y busque **Extensión de los corchetes de la**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Haga clic en **Instalar**.
1. Cierre el cuadro de diálogo y el Extension Manager una vez finalizada la instalación.

## Introducción {#getting-started}

### El proyecto del paquete de contenido {#the-content-package-project}

AEM Una vez instalada la extensión, puede empezar a desarrollar componentes de la abriendo una carpeta de paquete de contenido desde el sistema de archivos con corchetes.

El proyecto debe contener al menos:

1. una carpeta `jcr_root` (por ejemplo, `myproject/jcr_root`)

1. un archivo de `filter.xml` (por ejemplo, `myproject/META-INF/vault/filter.xml`); para obtener más detalles acerca de la estructura del archivo de `filter.xml`, vea la [definición del filtro de Workspace](https://jackrabbit.apache.org/filevault/filter.html).

En el menú **Archivo** de Brackets, elija **Abrir carpeta...** y elija la carpeta `jcr_root` o la carpeta del proyecto principal.

>[!NOTE]
>
>Si no dispone de su propio proyecto con un paquete de contenido, puede probar el [Ejemplo de HTL TodoMVC](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). En GitHub, haga clic en **Descargar ZIP**, extraiga los archivos localmente y, como se indica más arriba, abra la carpeta `jcr_root` entre corchetes. AEM A continuación, siga los pasos a continuación para configurar **Configuración del proyecto** y, finalmente, cargue todo el paquete en su instancia de desarrollo de haciendo un **Paquete de contenido de exportación** según se indica más adelante en la sección Sincronización completa del paquete de contenido.
>
>AEM AEM Después de estos pasos, debería poder obtener acceso a la dirección URL `/content/todo.html` en su instancia de desarrollo de y puede empezar a realizar modificaciones en el código entre corchetes y ver cómo, después de realizar una actualización en el explorador web, los cambios se sincronizaron inmediatamente con el servidor de la.

### Configuración de proyecto {#project-settings}

AEM Para sincronizar el contenido con y desde una instancia de desarrollo de, debe definir la Configuración del proyecto. AEM Para ello, vaya al menú **&#x200B;**&#x200B;y elija **Configuración del proyecto...**

![chlimage_1-55](assets/chlimage_1-55a.png)

La Configuración del proyecto permite definir lo siguiente:

1. La dirección URL del servidor (por ejemplo, `http://localhost:4502`)
1. Si se toleran los servidores que no tienen un certificado HTTPS válido (manténgalo sin marcar, a menos que sea necesario)
1. Nombre de usuario utilizado para sincronizar contenido (por ejemplo, `admin`)
1. Contraseña del usuario (por ejemplo, `admin`)

## Sincronización de contenido {#synchronizing-content}

AEM La extensión Brackets proporciona los siguientes tipos de sincronización de contenido para archivos y carpetas permitidos por las reglas de filtrado definidas en `filter.xml`:

### Sincronización Automática De Archivos Cambiados {#automated-synchronization-of-changed-files}

AEM Esto solo sincronizará los cambios de Paréntesis a la instancia de la, pero nunca al revés.

### Sincronización bidireccional manual {#manual-bidirectional-synchronization}

En el Explorador del proyecto, abra el menú contextual haciendo clic con el botón secundario en cualquier archivo o carpeta, y se puede acceder a las opciones **Exportar al servidor** o **Importar desde el servidor**.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Si la entrada seleccionada está fuera de la carpeta `jcr_root`, las entradas de menú contextual **Exportar al servidor** e **Importar del servidor** están deshabilitadas.

### Sincronización completa del paquete de contenido {#full-content-package-synchronization}

AEM En el menú **&#x200B;**, las opciones **Exportar paquete de contenido** o **Importar paquete de contenido** le permiten sincronizar todo el proyecto con el servidor.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Estado de sincronización {#synchronization-status}

AEM La extensión de corchetes de la barra de herramientas de la parte derecha de la ventana Corchetes, que muestra un icono de notificación que indica el estado de la última sincronización, incluye la siguiente información:

* verde: todos los archivos se han sincronizado correctamente
* azul: hay una operación de sincronización en curso
* amarillo: algunos archivos no se sincronizaron
* rojo: no se sincronizó ningún archivo

Al hacer clic en el icono de notificación, se abre el cuadro de diálogo Informe de estado de sincronización que muestra todos los estados de cada archivo sincronizado.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Solo se sincronizará el contenido marcado como incluido por las reglas de filtrado de `filter.xml`, independientemente del método de sincronización utilizado.
>
>Además, se admiten `.vltignore` archivos para excluir contenido de la sincronización con el repositorio y desde él.

## Edición de código HTL {#editing-htl-code}

AEM La extensión Brackets también incluye algunas características de finalización automática para facilitar la escritura de atributos y expresiones HTL.

### Atributo de finalización automática {#attribute-auto-completion}

1. En un atributo de HTML, escriba `sly`. El atributo se completó automáticamente en `data-sly-`.
1. Seleccione el atributo HTL en la lista desplegable.

### Expresión: finalización automática {#expression-auto-completion}

Dentro de una expresión `${}`, los nombres de variables comunes se completan automáticamente.

## Más información {#more-information}

AEM La extensión Brackets es un proyecto de código abierto, alojado en GitHub por la organización [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud), con licencia Apache, versión 2.0:

* Repositorio de códigos: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licencia de Apache, versión 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

El editor de código Brackets también es un proyecto de código abierto, alojado en GitHub por la organización [Adobe Systems Incorporated](https://github.com/adobe):

* Repositorio de códigos: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

¡Siéntase libre de contribuir!
