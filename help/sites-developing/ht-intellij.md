---
title: Cómo desarrollar AEM proyectos usando IntelliJ IDEA
seo-title: Cómo desarrollar AEM proyectos usando IntelliJ IDEA
description: Uso de IntelliJ IDEA para desarrollar AEM proyectos
seo-description: Uso de IntelliJ IDEA para desarrollar AEM proyectos
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# Cómo desarrollar AEM proyectos usando IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Información general {#overview}

Para comenzar con AEM desarrollo de IntelliJ, se requieren los siguientes pasos.

Cada uno de ellos se explica con más detalle en el resto de este procedimiento.

* Instalar IntelliJ
* Configure el proyecto de AEM en base a Maven
* Preparación de la compatibilidad de JSP con IntelliJ en el POM de Maven
* Importar el proyecto Maven a IntelliJ

>[!NOTE]
>
>Esta guía se basa en IntelliJ IDEA Ultimate Edition 12.1.4 y AEM 5.6.1.

### Instalar IntelliJ IDEA {#install-intellij-idea}

Descargue IntelliJ IDEA de [la página de descargas de JetBrains](https://www.jetbrains.com/idea/download/index.html).

A continuación, siga las instrucciones de instalación de esa página.

### Configure el proyecto de AEM en base a Maven {#set-up-your-aem-project-based-on-maven}

A continuación, configure el proyecto con Maven como se describe en [Cómo crear AEM proyectos con Apache Maven](/help/sites-developing/ht-projects-maven.md).

Para inicio con el trabajo con AEM proyectos en IntelliJ IDEA, la configuración básica de [Introducción en 5 minutos](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) es suficiente.

### Preparar compatibilidad con JSP para IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA también puede proporcionar soporte para trabajar con JSP, por ejemplo

* finalización automática de bibliotecas de etiquetas
* conocimiento de los objetos definidos por `<cq:defineObjects />` y `<sling:defineObjects />`

Para que esto funcione, siga las instrucciones de [Cómo trabajar con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) en [Cómo generar AEM proyectos con Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importar el proyecto Maven {#import-the-maven-project}

1. Abra el cuadro de diálogo **Importar** en IntelliJ IDEA mediante

   * seleccionando **Importar proyecto** en la pantalla de bienvenida si todavía no tiene un proyecto abierto
   * seleccionar **Archivo -> Importar proyecto** en el menú principal

1. En el cuadro de diálogo Importar, seleccione el archivo POM del proyecto.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continúe con la configuración predeterminada como se muestra en el cuadro de diálogo siguiente.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Continúe con los siguientes cuadros de diálogo haciendo clic en **Siguiente** y **Finalizar**.
1. Ahora está configurado para el desarrollo AEM con IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Depuración de JSPs con IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

Los siguientes pasos son necesarios para depurar JSPs con IntelliJ IDEA

* Configuración de una faceta web en el proyecto
* Instalación del complemento de soporte JSR45
* Configuración de un Perfil de depuración
* Configurar AEM para el modo de depuración

#### Configurar una faceta web en el proyecto {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA necesita saber dónde encontrar los JSPs para la depuración. Como IDEA no puede interpretar la configuración `content-package-maven-plugin`, esto debe configurarse manualmente.

1. Vaya a **Archivo -> Estructura del proyecto**
1. Seleccione el módulo **Contenido**
1. Haga clic **+** sobre la lista de módulos y seleccione **Web**
1. Como directorio de recursos Web, seleccione el `content/src/main/content/jcr_root subdirectory` del proyecto como se muestra en la captura de pantalla siguiente.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Instale el complemento de soporte JSR45 {#install-the-jsr-support-plugin}

1. Vaya al panel **Complementos** de la configuración de IntelliJ IDEA
1. Vaya al complemento **Integración de JSR45** y seleccione la casilla de verificación situada junto a él
1. Haga clic en **Aplicar**
1. Reinicie IntelliJ IDEA cuando se le solicite

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configurar un Perfil de depuración {#configure-a-debug-profile}

1. Vaya a **Ejecutar -> Editar configuraciones**
1. Pulse **+** y seleccione **JSR45 Remote**
1. En el cuadro de diálogo de configuración, seleccione **Configurar** junto a **Servidor de aplicaciones** y configure un servidor genérico
1. Configure la página de inicio en una dirección URL apropiada si desea abrir un explorador cuando depure inicios
1. Elimine todas las tareas **antes de iniciar** si utiliza vlt autosync, o configure las tareas Maven apropiadas si no lo hace
1. En el panel **Inicio/Conexión**, ajuste el puerto si es necesario
1. Copiar los argumentos de la línea de comandos que propone IntelliJ IDEA

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Configurar AEM para el modo de depuración {#configure-aem-for-debug-mode}

El último paso requerido es el inicio de AEM con las opciones de JVM propuestas por IntelliJ IDEA.

Puede hacerlo iniciando el archivo jar de AEM directamente y agregando estas opciones, por ejemplo con la siguiente línea de comandos:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

También puede agregar estas opciones a la secuencia de comandos de inicio en `crx-quickstart/bin/start` como se muestra a continuación.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Depuración de inicio {#start-debugging}

Ahora está todo configurado para depurar sus JSP en AEM.

1. Seleccione **Ejecutar -> Depurar -> El Perfil de depuración**
1. Definición de puntos de interrupción en el código de componente
1. Acceso a una página en el explorador

![chlimage_1-52](assets/chlimage_1-52a.png)

### Depuración de paquetes con IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

El código de los paquetes se puede depurar mediante una conexión de depuración remota genérica estándar. Puede seguir la [documentación de JetBrain sobre depuración remota](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html).
