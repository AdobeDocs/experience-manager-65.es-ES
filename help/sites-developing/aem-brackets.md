---
title: AEM Extensión de corchetes de
seo-title: AEM Brackets Extension
description: AEM Extensión de corchetes de
seo-description: null
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---

# AEM Extensión de corchetes de{#aem-brackets-extension}

## Información general {#overview}

AEM AEM La extensión de brackets proporciona un flujo de trabajo fluido para editar componentes de y bibliotecas de cliente, y aprovecha la potencia de la [Corchetes](https://brackets.io/) editor de código, que proporciona acceso desde el editor de código a los archivos y capas de Photoshop. AEM La fácil sincronización que proporciona la extensión (no se requiere Maven ni File Vault) aumenta la eficacia del desarrollador y también ayuda a los desarrolladores de front-end con conocimientos limitados a participar en proyectos. Esta extensión también proporciona cierta compatibilidad con el [Lenguaje de plantilla de HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es), que elimina la complejidad de JSP para que el desarrollo de componentes sea más fácil y seguro.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Características {#features}

AEM Las principales características de la extensión de corchetes de la son:

* AEM Sincronización automatizada de los archivos modificados en la instancia de desarrollo de la.
* Sincronización bidireccional manual de archivos y carpetas.
* Sincronización completa del paquete de contenido del proyecto.
* Finalización de código HTL para expresiones y `data-sly-*` instrucciones de bloque.

AEM Además, Brackets incluye muchas funciones útiles para los desarrolladores de front-end de:

* Compatibilidad con archivos Photoshop para extraer información de un archivo PSD, como capas, medidas, colores, fuentes, textos, etc.
* Sugerencias para el código del PSD para reutilizar fácilmente esta información extraída en el código.
* Compatibilidad con preprocesadores CSS, como LESS y SCSS.
* Y cientos de extensiones adicionales que cubren necesidades más específicas.

## Instalación {#installation}

### Corchetes {#brackets}

AEM La extensión de corchetes de la admite corchetes de la versión 1.0 o buena.

Descargue la última versión de Brackets de [paréntesis.io](https://brackets.io/).

### La extensión de {#the-extension}

Para instalar la extensión, siga estos pasos:

1. Abra los corchetes. En el menú **Archivo**, seleccione **Extension Manager...**
1. Entrar **AEM** en la barra de búsqueda y busque **AEM Extensión de corchetes de**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Clic **Instalar**.
1. Cierre el cuadro de diálogo y el Extension Manager una vez finalizada la instalación.

## Introducción {#getting-started}

### El proyecto del paquete de contenido {#the-content-package-project}

AEM Una vez instalada la extensión, puede empezar a desarrollar componentes de la abriendo una carpeta de paquete de contenido desde el sistema de archivos con corchetes.

El proyecto debe contener al menos:

1. a `jcr_root` carpeta (por ejemplo, `myproject/jcr_root`)

1. a `filter.xml` (por ejemplo, `myproject/META-INF/vault/filter.xml`); para obtener más detalles acerca de la estructura del `filter.xml` por favor, consulte el [Definición del filtro de Workspace](https://jackrabbit.apache.org/filevault/filter.html).

Entre paréntesis **Archivo** menú, elija **Abrir carpeta...** y elija la `jcr_root` o la carpeta del proyecto principal.

>[!NOTE]
>
>Si no tiene un proyecto propio con un paquete de contenido, puede probar el [Ejemplo de HTL TodoMVC](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). En GitHub, haga clic en **Descargar ZIP**, extraiga los archivos localmente y, como se indica más arriba, abra el `jcr_root` carpeta en Corchetes. A continuación, siga los pasos a continuación para configurar el **Configuración de proyecto** AEM y, finalmente, cargue todo el paquete en la instancia de desarrollo de su haciendo un **Exportar paquete de contenido** como se indica más adelante en la sección Sincronización completa del paquete de contenido.
>
>Después de estos pasos, debe poder acceder a las `/content/todo.html` AEM AEM En la URL de la instancia de desarrollo de la puede empezar a realizar modificaciones en el código de Brackets y ver cómo, después de realizar una actualización en el explorador web, los cambios se sincronizan inmediatamente con el servidor de la.

### Configuración de proyecto {#project-settings}

AEM Para sincronizar el contenido con y desde una instancia de desarrollo de, debe definir la Configuración del proyecto. Esto se puede hacer accediendo a la **AEM** menú y elegir **Configuración del proyecto...**

![chlimage_1-55](assets/chlimage_1-55a.png)

La Configuración del proyecto permite definir lo siguiente:

1. La URL del servidor (por ejemplo, `http://localhost:4502`)
1. Si se toleran los servidores que no tienen un certificado HTTPS válido (no marcar, a menos que sea necesario)
1. El nombre de usuario utilizado para sincronizar contenido (por ejemplo, `admin`)
1. La contraseña del usuario (por ejemplo, `admin`)

## Sincronización de contenido {#synchronizing-content}

AEM La extensión Brackets proporciona los siguientes tipos de sincronización de contenido para archivos y carpetas permitidos por las reglas de filtrado definidas en `filter.xml`:

### Sincronización Automática De Archivos Cambiados {#automated-synchronization-of-changed-files}

AEM Esto solo sincronizará los cambios de Paréntesis a la instancia de la, pero nunca al revés.

### Sincronización bidireccional manual {#manual-bidirectional-synchronization}

En el Explorador del proyecto, abra el menú contextual haciendo clic con el botón secundario en cualquier archivo o carpeta y, a continuación, seleccione **Exportar a servidor** o **Importar desde servidor** se puede acceder a las opciones.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Si la entrada seleccionada está fuera de `jcr_root` carpeta, la **Exportar a servidor** y **Importar desde servidor** las entradas del menú contextual están desactivadas.

### Sincronización completa del paquete de contenido {#full-content-package-synchronization}

En el **AEM** , el menú **Exportar paquete de contenido** o **Importar paquete de contenido** Las opciones de permiten sincronizar todo el proyecto con el servidor.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Estado de sincronización {#synchronization-status}

AEM La extensión de corchetes de la barra de herramientas de la parte derecha de la ventana Corchetes, que muestra un icono de notificación que indica el estado de la última sincronización, incluye la siguiente información:

* verde: todos los archivos se han sincronizado correctamente
* azul: hay una operación de sincronización en curso
* amarillo: algunos archivos no se sincronizaron
* rojo: no se sincronizó ningún archivo

Al hacer clic en el icono de notificación, se abrirá el cuadro de diálogo del informe Estado de sincronización que enumera todos los estados de cada archivo sincronizado.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Solo el contenido marcado como incluido por las reglas de filtrado de `filter.xml` se sincronizarán, independientemente del método de sincronización utilizado.
>
>Además, `.vltignore` Los archivos de se admiten para excluir el contenido de la sincronización con el repositorio y desde él.

## Edición de código HTL {#editing-htl-code}

AEM La extensión Brackets también incluye algunas características de finalización automática para facilitar la escritura de atributos y expresiones HTL.

### Atributo de finalización automática {#attribute-auto-completion}

1. En un atributo de HTML, escriba `sly`. El atributo se completa automáticamente en `data-sly-`.
1. Seleccione el atributo HTL en la lista desplegable.

### Expresión: finalización automática {#expression-auto-completion}

Dentro de una expresión `${}`, los nombres de variables comunes se completan automáticamente.

## Más información {#more-information}

AEM La extensión de Brackets es un proyecto de código abierto, alojado en GitHub por el [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) organización, bajo la licencia de Apache, versión 2.0:

* Repositorio de códigos: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licencia de Apache, versión 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

El editor de código Brackets también es un proyecto de código abierto, alojado en GitHub por el [Adobe Systems Incorporated](https://github.com/adobe) organización:

* Repositorio de códigos: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

¡Siéntase libre de contribuir!
