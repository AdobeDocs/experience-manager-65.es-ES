---
title: AEM Cómo desarrollar proyectos de con IntelliJ IDEA
description: AEM Uso de IntelliJ IDEA para desarrollar proyectos de
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# AEM Cómo desarrollar proyectos de con IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Información general {#overview}

AEM Para empezar a desarrollar la aplicación de la aplicación en IntelliJ, es necesario realizar los pasos siguientes.

Cada paso se explica con más detalle en el resto de este tema.

* Instalar IntelliJ
* AEM Configurar el proyecto de en función de Maven
* Preparar la compatibilidad con JSP para IntelliJ en el POM de Maven
* Importar el proyecto Maven en IntelliJ

>[!NOTE]
>
>AEM Esta guía se basa en IntelliJ IDEA Ultimate Edition 12.1.4 y en la versión 5.6.1 de la versión en inglés de la versión en inglés de.

### Instalar IntelliJ IDEA {#install-intellij-idea}

Descargar IntelliJ IDEA desde [la página Descargas en JetBrains](https://www.jetbrains.com/idea/download/).

A continuación, siga las instrucciones de instalación de esa página.

### AEM Configurar el proyecto de en función de Maven {#set-up-your-aem-project-based-on-maven}

A continuación, configure el proyecto mediante Maven como se describe en [AEM Creación de proyectos de mediante Apache Maven](/help/sites-developing/ht-projects-maven.md).

AEM Para comenzar a trabajar con Proyectos de la comunidad de la comunidad de IntelliJ IDEA, la configuración básica en [Introducción en 5 minutos](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) es suficiente.

### Preparar compatibilidad con JSP para IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA también puede proporcionar soporte en el trabajo con JSP, por ejemplo:

* finalización automática de bibliotecas de etiquetas
* reconocimiento de objetos definidos por `<cq:defineObjects />` y `<sling:defineObjects />`

Para que esto funcione, siga las instrucciones de [Cómo trabajar con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [AEM Creación de proyectos de mediante Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importación del proyecto Maven {#import-the-maven-project}

1. Abra el **Importar** diálogo en IntelliJ IDEA por

   * selección **Importar proyecto** en la pantalla de bienvenida si todavía no tiene ningún proyecto abierto
   * selección **Archivo -> Importar proyecto** en el menú principal

1. En el cuadro de diálogo Importar, seleccione el archivo POM del proyecto.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continúe con la configuración predeterminada como se muestra en el cuadro de diálogo siguiente.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Siga los siguientes cuadros de diálogo haciendo clic en **Siguiente** y **Finalizar**.
1. AEM Ya está configurado para el desarrollo de la aplicación de desarrollo de la aplicación de desarrollo de IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Depuración de JSP con IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

Los siguientes pasos son necesarios para depurar JSP con IntelliJ IDEA

* Configurar una faceta web en el proyecto
* Instalación del complemento de soporte para JSR45
* Configuración de un perfil de depuración
* AEM Configurar para el modo de depuración

#### Configurar una faceta web en el proyecto {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA debe saber dónde encontrar los JSP para la depuración. Porque IDEA no puede interpretar `content-package-maven-plugin` , debe configurarse manualmente.

1. Ir a **Archivo -> Estructura del proyecto**
1. Seleccione el **Contenido** módulo
1. Clic **+** sobre la lista de módulos y seleccione **Web**
1. Como Directorio de recursos web, seleccione la opción `content/src/main/content/jcr_root subdirectory` del proyecto, como se muestra en la captura de pantalla siguiente.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Instalación del complemento de soporte para JSR45 {#install-the-jsr-support-plugin}

1. Vaya a la **Complementos** panel en la configuración de IntelliJ IDEA
1. Vaya a **Integración de JSR45** Y seleccione la casilla de verificación que hay junto a ella.
1. Haga clic en **Aplicar**
1. Reinicie IntelliJ IDEA cuando se le solicite

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configuración de un perfil de depuración {#configure-a-debug-profile}

1. Ir a **Ejecutar -> Editar configuraciones**
1. Pulse el botón **+** y seleccione **Remoto JSR45**
1. En el cuadro de diálogo de configuración, seleccione **Configurar** junto a **Servidor de aplicaciones** y configurar un servidor genérico
1. Establezca la página de inicio en una dirección URL adecuada si desea abrir un explorador al iniciar la depuración
1. Eliminar todo **Antes del lanzamiento** tareas si utiliza la sincronización automática de vlt o configure las tareas de Maven adecuadas si no lo hace
1. En el **Inicio/Conexión** Panel, ajuste el puerto, si es necesario
1. Copiar los argumentos de la línea de comandos que propone IntelliJ IDEA

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### AEM Configurar para el modo de depuración {#configure-aem-for-debug-mode}

AEM El último paso requerido es comenzar a utilizar las opciones de JVM propuestas por IntelliJ IDEA.

AEM Inicie el archivo jar de directamente y agregue estas opciones, por ejemplo, con la siguiente línea de comandos:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

También puede añadir estas opciones al script de inicio en `crx-quickstart/bin/start` como se muestra a continuación.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Iniciar depuración {#start-debugging}

AEM Ya está todo configurado para depurar los JSP en el modo de depuración de la.

1. Seleccionar **Ejecutar -> Depurar -> Su perfil de depuración**
1. Establecer puntos de interrupción en el código del componente
1. Acceder a una página del explorador

![chlimage_1-52](assets/chlimage_1-52a.png)

### Depuración de paquetes con IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

El código de los paquetes se puede depurar mediante una conexión de depuración remota genérica estándar. Puede seguir las [Documentación de Jetbrain sobre depuración remota](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
