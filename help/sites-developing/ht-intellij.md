---
title: AEM Cómo desarrollar proyectos de con IntelliJ IDEA
description: Aprenda a utilizar IntelliJ IDEA para desarrollar proyectos de Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '640'
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

Descargue IntelliJ IDEA desde [la página Descargas en JetBrains](https://www.jetbrains.com/idea/download/).

A continuación, siga las instrucciones de instalación de esa página.

### AEM Configurar el proyecto de en función de Maven {#set-up-your-aem-project-based-on-maven}

AEM A continuación, configure su proyecto mediante Maven tal como se describe en [Cómo crear proyectos de mediante Apache Maven](/help/sites-developing/ht-projects-maven.md).

AEM Para comenzar a trabajar con proyectos de la aplicación de la aplicación IntelliJ IDEA, la configuración básica de [Introducción en 5 minutos](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) es suficiente.

### Preparar compatibilidad con JSP para IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA también puede proporcionar soporte en el trabajo con JSP, por ejemplo:

* finalización automática de bibliotecas de etiquetas
* reconocimiento de objetos definidos por `<cq:defineObjects />` y `<sling:defineObjects />`

AEM Para que esto funcione, siga las instrucciones de [Cómo trabajar con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) en [Cómo crear proyectos de con Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importación del proyecto Maven {#import-the-maven-project}

1. Abrir el cuadro de diálogo **Importar** en IntelliJ IDEA por

   * seleccionando **Importar proyecto** en la pantalla de bienvenida si todavía no tiene ningún proyecto abierto
   * seleccionando **Archivo > Importar proyecto** en el menú principal

1. En el cuadro de diálogo Importar, seleccione el archivo POM del proyecto.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continúe con la configuración predeterminada como se muestra en el cuadro de diálogo siguiente.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Continúe con los siguientes cuadros de diálogo haciendo clic en **Siguiente** y **Finalizar**.
1. AEM Ya está configurado para el desarrollo de la aplicación de desarrollo de la aplicación de desarrollo de IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Depuración de JSP con IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

Los siguientes pasos son necesarios para depurar JSP con IntelliJ IDEA

* Configurar una faceta web en el proyecto
* Instalación del complemento de soporte para JSR45
* Configuración de un perfil de depuración
* AEM Configurar para el modo de depuración

#### Configurar una faceta web en el proyecto {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA debe saber dónde encontrar los JSP para la depuración. Como IDEA no puede interpretar la configuración de `content-package-maven-plugin`, debe configurarse manualmente.

1. Ir a **Archivo > Estructura del proyecto**
1. Seleccione el módulo **Contenido**
1. Haga clic en **+** sobre la lista de módulos y seleccione **Web**
1. Como directorio de recursos web, seleccione el `content/src/main/content/jcr_root subdirectory` del proyecto como se muestra en la captura de pantalla siguiente.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Instalación del complemento de soporte para JSR45 {#install-the-jsr-support-plugin}

1. Vaya al panel **Complementos** en la configuración de IntelliJ IDEA
1. Vaya al complemento **JSR45 Integration** y active la casilla que hay junto a él
1. Haga clic en **Aplicar**
1. Reinicie IntelliJ IDEA cuando se le solicite

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configuración de un perfil de depuración {#configure-a-debug-profile}

1. Vaya a **Ejecutar > Editar configuraciones**
1. Pulse **+** y seleccione **Remoto JSR45**
1. En el cuadro de diálogo de configuración, seleccione **Configurar** junto a **Servidor de aplicaciones** y configure un servidor genérico
1. Establezca la página de inicio en una dirección URL adecuada si desea abrir un explorador al iniciar la depuración
1. Elimine todas las tareas **Antes del inicio** si usa la sincronización automática de vlt, o configure las tareas de Maven adecuadas si no lo hace
1. En el panel **Inicio/Conexión**, ajuste el puerto, si es necesario
1. Copiar los argumentos de la línea de comandos que propone IntelliJ IDEA

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### AEM Configurar para el modo de depuración {#configure-aem-for-debug-mode}

AEM El último paso requerido es comenzar a utilizar las opciones de JVM propuestas por IntelliJ IDEA.

AEM Inicie el archivo jar de directamente y agregue estas opciones, por ejemplo, con la siguiente línea de comandos:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

También puede agregar estas opciones al script de inicio en `crx-quickstart/bin/start`, como se muestra a continuación.

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

1. Seleccione **Ejecutar > Depurar > Su perfil de depuración**
1. Establecer puntos de interrupción en el código del componente
1. Acceder a una página del explorador

![chlimage_1-52](assets/chlimage_1-52a.png)

### Depuración de paquetes con IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

El código de los paquetes se puede depurar mediante una conexión de depuración remota genérica estándar. Puede seguir la [documentación de Jetbrain sobre la depuración remota](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
