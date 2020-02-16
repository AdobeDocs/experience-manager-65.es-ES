---
title: Extensión de corchetes AEM
seo-title: Extensión de corchetes AEM
description: nulo
seo-description: nulo
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# Extensión de corchetes AEM{#aem-brackets-extension}

## Información general {#overview}

La extensión de corchetes AEM proporciona un flujo de trabajo suave para editar los componentes y las bibliotecas de cliente de AEM, y aprovecha la potencia del editor de código de [corchetes](https://brackets.io/) , que proporciona acceso desde el editor de código a los archivos y capas de Photoshop. La sencilla sincronización que proporciona la extensión (no se requiere Maven ni File Vault) aumenta la eficacia del desarrollador y también ayuda a los desarrolladores de front-end con conocimientos limitados de AEM a participar en los proyectos. Esta extensión también ofrece cierta compatibilidad con el lenguaje de plantilla [HTML (HTL)](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), que elimina la complejidad de JSP para facilitar y aumentar la seguridad del desarrollo de componentes.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Características {#features}

Las principales funciones de la extensión de los soportes AEM son:

* Sincronización automatizada de los archivos modificados con la instancia de desarrollo de AEM.
* Sincronización bidireccional manual de archivos y carpetas.
* Sincronización completa del paquete de contenido del proyecto.
* Finalización del código HTL para expresiones y sentencias de `data-sly-*` bloque.

Además, los corchetes incluyen muchas funciones útiles para los desarrolladores de fuentes AEM:

* Compatibilidad con archivos de Photoshop para extraer información de un archivo PSD, como capas, medidas, colores, fuentes, textos, etc.
* Sugerencias de código del PSD para reutilizar fácilmente esta información extraída en el código.
* Compatibilidad con preprocesadores CSS, como LESS y SCSS.
* Y cientos de extensiones adicionales que cubren necesidades más específicas.

## Instalación {#installation}

### Corchetes {#brackets}

La extensión de los corchetes AEM admite los corchetes de la versión 1.0 o superior.

Descargue la versión más reciente de los corchetes de [corchetes.io](https://brackets.io/).

### La extensión {#the-extension}

Para instalar la extensión, siga estos pasos:

1. Abra Corchetes. En el menú **Archivo**, seleccione **Extension Manager...**
1. Introduzca **AEM** en la barra de búsqueda y busque Extensión de corchetes **AEM**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Haga clic en **Instalar**.
1. Cierre el cuadro de diálogo y Extension Manager una vez finalizada la instalación.

## Introducción {#getting-started}

### El proyecto Content-Package {#the-content-package-project}

Una vez instalada la extensión, puede empezar a desarrollar los componentes de AEM abriendo una carpeta de paquetes de contenido desde el sistema de archivos con paréntesis.

El proyecto debe contener al menos:

1. una `jcr_root` carpeta (p. ej. `myproject/jcr_root`)

1. un `filter.xml` archivo (p. ej. `myproject/META-INF/vault/filter.xml`); para obtener más información sobre la estructura del `filter.xml` archivo, consulte la definición [Filtro](https://jackrabbit.apache.org/filevault/filter.html)de espacio de trabajo.

En el menú **Archivo** de corchetes, elija **Abrir carpeta...** y elija la `jcr_root` carpeta o la carpeta del proyecto principal.

>[!NOTE]
>
>Si no tiene un proyecto propio con un paquete de contenido, puede probar el Ejemplo [](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)HTL TodoMVC. En GitHub, haga clic en **Descargar ZIP**, extraiga los archivos localmente y, como se ha indicado anteriormente, abra la `jcr_root` carpeta entre corchetes. A continuación, siga los pasos que se describen a continuación para configurar la configuración **del** proyecto y, finalmente, cargue todo el paquete en su instancia de desarrollo de AEM realizando un paquete **de** exportación de contenido como se indica en la sección Sincronización de contenido completo y paquete.
>
>Después de estos pasos, debe poder acceder a la `/content/todo.html` URL en la instancia de desarrollo de AEM y puede empezar a realizar modificaciones en el código entre corchetes y ver cómo, tras realizar una actualización en el navegador web, los cambios se sincronizaron inmediatamente con el servidor AEM.

### Configuración del proyecto {#project-settings}

Para sincronizar el contenido con y desde una instancia de desarrollo de AEM, debe definir la configuración del proyecto. Para ello, vaya al menú de **AEM** y elija Ajustes **del proyecto...**

![chlimage_1-55](assets/chlimage_1-55a.png)

La Configuración del proyecto permite definir:

1. La dirección URL del servidor (p. ej. `http://localhost:4502`)
1. Si desea tolerar servidores que no tengan un certificado HTTPS válido (mantenga la opción sin marcar, a menos que sea necesario)
1. Nombre de usuario utilizado para sincronizar contenido (p. ej. `admin`)
1. La contraseña del usuario (p. ej. `admin`)

## Sincronización de contenido {#synchronizing-content}

La extensión de corchetes AEM proporciona los siguientes tipos de sincronización de contenido para archivos y carpetas permitidos por las reglas de filtrado definidas en `filter.xml`:

### Sincronización Automática De Archivos Cambiados {#automated-synchronization-of-changed-files}

Esto solo sincronizará los cambios de los corchetes a la instancia de AEM, pero nunca al revés.

### Sincronización bidireccional manual {#manual-bidirectional-synchronization}

En el Explorador de proyectos, abra el menú contextual haciendo clic con el botón derecho en cualquier archivo o carpeta, y se puede acceder a las opciones de **Exportar al servidor** o **Importar desde el servidor** .

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Si la entrada seleccionada está fuera de la `jcr_root` carpeta, se desactivan las entradas del menú contextual **Exportar a servidor** e **Importar desde servidor** .

### Sincronización de paquetes de contenido completo {#full-content-package-synchronization}

En el menú **AEM** , las opciones **Exportar paquete** de contenido o **Importar paquete** de contenido permiten sincronizar todo el proyecto con el servidor.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Estado de sincronización {#synchronization-status}

La Extensión de corchetes AEM incluye un icono de notificación en la barra de herramientas de la derecha de la ventana Corchetes, que indica el estado de la última sincronización:

* verde: todos los archivos se sincronizaron correctamente
* azul: una operación de sincronización está en curso
* amarillo: algunos archivos no se sincronizaron
* rojo: no se sincronizó ninguno de los archivos

Al hacer clic en el icono de notificación, se abrirá el cuadro de diálogo de informe Estado de sincronización, que enumera todos los estados de cada archivo sincronizado.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Solo se sincronizará el contenido marcado como incluido por las reglas de filtrado desde `filter.xml` , independientemente del método de sincronización utilizado.
>
>Además, `.vltignore` los archivos son compatibles para excluir el contenido de la sincronización con el repositorio y desde éste.

## Edición de código HTML {#editing-htl-code}

La extensión de corchetes AEM también incluye algunas funciones de finalización automática para facilitar la escritura de atributos y expresiones HTML.

### Finalización automática de atributos {#attribute-auto-completion}

1. En un atributo HTML, escriba `sly`. El atributo se rellena automáticamente en `data-sly-`.
1. Seleccione el atributo HTL en la lista desplegable.

### Finalización automática de expresiones {#expression-auto-completion}

Dentro de una expresión `${}`, los nombres de variables comunes se completan automáticamente.

## Más información {#more-information}

La extensión de los corchetes de AEM es un proyecto de código abierto, alojado en GitHub por la organización de [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) , bajo la licencia de Apache, versión 2.0:

* Repositorio de códigos: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licencia de Apache, versión 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

El editor de código de soportes también es un proyecto de código abierto, alojado en GitHub por la organización [Adobe Systems Incorporated](https://github.com/adobe) :

* Repositorio de códigos: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

¡Siéntase libre de contribuir!
