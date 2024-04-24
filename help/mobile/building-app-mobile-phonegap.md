---
title: Creación de aplicaciones móviles
description: Esta página proporciona un artículo paso a paso completo sobre cómo crear una aplicación móvil con el código disponible en GitHub aquí. Cree la aplicación para instalarla en un dispositivo o simulador para probarla o publicarla en tiendas de aplicaciones. Puede crear aplicaciones localmente mediante la interfaz de línea de comandos de PhoneGap o en la nube mediante PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# Creación de aplicaciones móviles{#building-mobile-applications}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran una representación del lado del cliente basada en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Cree la aplicación para instalarla en un dispositivo o simulador para probarla o publicarla en tiendas de aplicaciones. Puede crear aplicaciones localmente mediante la interfaz de línea de comandos de PhoneGap o en la nube mediante PhoneGap Build.

Hay disponible un artículo paso a paso completo sobre cómo crear una aplicación móvil con el código disponible en GitHub [aquí](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Mover la aplicación a la instancia de publicación {#moving-the-application-to-the-publish-instance}

Mueva los archivos de aplicación a la instancia de publicación para que pueda proporcionar actualizaciones de contenido a las instancias instaladas de la aplicación móvil y para generar la aplicación utilizando el contenido publicado. Las aplicaciones constan de dos ramas de nodos en el repositorio:

* `/content/phonegap/apps/<application name>`: Las páginas web que crean y activan los autores.
* `/content/phonegap/content/<application name>`: archivos de configuración de la aplicación y configuraciones de sincronización de contenido.

>[!NOTE]
>
>Si no mueve los archivos de la aplicación a la instancia de publicación, los autores de contenido no podrán actualizar la caché de sincronización de contenido.

Solo es necesario mover los archivos en la `/content/phonegap/content/<application name>` rama a la instancia de publicación. Los archivos en la `/content/phonegap/apps/<application name>` Las ramas se mueven cuando el autor activa las páginas.

AEM proporciona dos métodos para mover contenido masivo a la instancia de publicación:

* [Utilice el comando Activar árbol](/help/sites-authoring/publishing-pages.md) en la consola de replicación.
* [Creación de un paquete](/help/sites-administering/package-manager.md) que contiene el contenido y replicar el paquete.

Por ejemplo, se crea una aplicación móvil llamada phonegapapp. El nodo siguiente debe moverse a la instancia de publicación: /content/phonegap/content/phonegapapp.

**Sugerencia:** Para mover un paquete de la instancia de autor a la instancia de publicación, utilice el comando Replicar en el paquete.

![chlimage_1-16](assets/chlimage_1-16.png)

## Generar mediante la interfaz de línea de comandos de PhoneGap {#building-using-the-phonegap-command-line-interface}

Compile la aplicación PhoneGap en el equipo mediante la interfaz de línea de comandos (CLI) de PhoneGap. AEM AEM Para incluir el contenido de la en la aplicación, crea un archivo ZIP que incluye el contenido de la aplicación móvil, las configuraciones de sincronización de contenido y otros recursos necesarios. Descargue el archivo ZIP e inclúyalo en su compilación.

### Preparación del entorno de compilación {#preparing-your-build-environment}

Para generar utilizando la CLI de PhoneGap, debe instalar Node.js y la utilidad de cliente de PhoneGap. Necesita una conexión a Internet para realizar el siguiente procedimiento.

1. Descargar e instalar [Node.js](https://nodejs.org/en).
1. Abra un terminal o símbolo del sistema e introduzca el siguiente comando de nodo para instalar la utilidad PhoneGap:

   ```shell
   npm install -g phonegap
   ```

   En un sistema UNIX® o Linux®, es posible que deba incluir el prefijo del comando `sudo`.

   El terminal muestra los resultados de una serie de comandos de GET HTTP. Cuando la instalación se realiza correctamente, el terminal muestra dónde están instaladas las bibliotecas de forma similar al siguiente ejemplo:

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. (Opcional) Obtenga el SDK para la plataforma móvil a la que está dirigiendo:

   * Para crear aplicaciones para la plataforma iOS, instale la versión más reciente de [Xcode](https://developer.apple.com/xcode/).
   * Para crear aplicaciones de Android™, instale el [SDK para Android™](https://developer.android.com/).

### Descarga del archivo ZIP de contenido {#downloading-the-content-zip-file}

Mueva el contenido de la aplicación móvil al sistema de archivos.

1. En la página Aplicaciones móviles, seleccione la aplicación.
1. (Opcional) Para crear la aplicación para instalaciones completas, en la barra de herramientas, haga clic en el icono Borrar caché.

   ![Icono Borrar caché indicado por un símbolo de vínculo roto.](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >La caché contiene actualizaciones de contenido para las aplicaciones instaladas. Al borrar la caché, se anularán todas las actualizaciones almacenadas en caché.

1. En la barra de herramientas, haga clic en el icono Descargar recursos CLI.

   ![Descargue el icono Recursos CLI indicado por el símbolo de tableta superpuesto.](do-not-localize/chlimage_1-1.png)

1. Una vez guardado el archivo ZIP, haga clic en Cerrar en el cuadro de diálogo Éxito.
1. Extraiga el contenido del archivo ZIP.

### Uso de la CLI de PhoneGap para la compilación {#using-the-phonegap-cli-to-build}

Utilice la CLI de PhoneGap para compilar e instalar la aplicación. Para obtener información sobre cómo utilizar la CLI de PhoneGap, consulte la interfaz de línea de comandos de PhoneGap (`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`) documentación.

1. Abra un terminal o símbolo del sistema y cambie el directorio actual al archivo ZIP de la aplicación descargada. Por ejemplo, lo siguiente cambia el directorio al archivo ng-app-cli.1392137825303.zip:

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Introduzca el comando phonegap de la plataforma de destino. Por ejemplo, el siguiente comando crea la aplicación para Android™:

   ```shell
   phonegap build android
   ```

## Creación con PhoneGap Build {#building-using-phonegap-build}

Utilice el servicio en la nube de PhoneGap para crear su aplicación. Para realizar este procedimiento, primero debe crear una configuración de PhoneGap Build.

### Conectando con el PhoneGap Build {#connecting-to-phonegap-build}

Cree una configuración de PhoneGap Build para poder utilizar los servicios de PhoneGap Build AEM desde la propia cuenta de. Proporcione el nombre de usuario y la contraseña de la cuenta de PhoneGap Build que utilizará para crear sus aplicaciones móviles.

1. Abra la página Herramientas. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. En el área Operaciones de CQ, haga clic en Cloud Service.
1. Haga clic en el vínculo Configurar ahora para el PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. En el cuadro de diálogo Crear configuración, escriba un valor para la propiedad Título. De forma predeterminada, el valor de la propiedad Name se deriva del título; sin embargo, puede escribir un nombre. Haga clic en Crear.
1. En el cuadro de diálogo Configuración de PhoneGap Build, escriba el nombre de usuario y la contraseña de PhoneGap Build y, a continuación, haga clic en Aceptar.

### Uso del PhoneGap Build {#using-phonegap-build}

Envíe los recursos de su aplicación al PhoneGap Build para que los compile para las distintas plataformas móviles.

1. En la página Aplicaciones móviles, abra la aplicación móvil. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Opcional) Para crear la aplicación para instalaciones completas, seleccione la aplicación y haga clic en el icono Borrar caché.

   ![Icono Borrar caché indicado por un símbolo de vínculo roto.](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >La caché contiene actualizaciones de contenido para las aplicaciones instaladas. Al borrar la caché, se anularán todas las actualizaciones almacenadas en caché.

1. Seleccione la página de inicio y, a continuación, haga clic en el icono Generar remoto.

   ![Icono Generar control remoto indicado por dos engranajes redondos.](do-not-localize/chlimage_1-3.png)

   **Nota:** AEM La versión beta de la versión beta de Beta no crea una notificación de la bandeja de entrada cuando la compilación se completa correctamente.

1. En el cuadro de diálogo Correcto, haga clic en PhoneGap Build para abrir la página de Adobe PhoneGap Build en `https://build.phonegap.com/apps`. Si está esperando a que su aplicación aparezca, puede comprobar el estado del PhoneGap Build en `https://status.build.phonegap.com/`.

   Para obtener información sobre cómo instalar la compilación, consulte [Documentación del PhoneGap Build](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >Las cuentas de PhoneGap Build gratuitas están permitidas en una aplicación privada. Las compilaciones de PhoneGap fallan si crea una aplicación privada adicional.

### Pasos siguientes {#the-next-steps}

El siguiente paso después del proceso de creación es aprender acerca de la [Estructura de una aplicación](/help/mobile/phonegap-structure-an-app.md).
