---
title: Desarrollo de aplicaciones con la CLI de PhoneGap
seo-title: Developing Apps with PhoneGap CLI
description: Siga esta página para obtener más información sobre el desarrollo de aplicaciones con la CLI de PhoneGap.
seo-description: Follow this page to learn about developing apps with PhoneGap CLI.
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Desarrollo de aplicaciones con la CLI de PhoneGap{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>Adobe recomienda utilizar el Editor de SPA para proyectos que requieren una representación del lado del cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

Como desarrollador, puede ejecutar la aplicación en un dispositivo o en un emulador en cualquier momento, siempre que haya configurado el entorno de desarrollo.

Para ejecutar los siguientes ejemplos necesitará un sistema que ejecute OSx (Mac) con Xcode o un sistema Mac/Win/Linux con el SDK para Android instalado.

## Bootstrap del entorno de desarrollo {#bootstrap-your-development-environment}

[Configuración de la CLI de PhoneGap](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

Para iOS: Para desarrollar para iPhone y iPads, necesita Apple Xcode IDE.

* Descárguelo gratis [here](https://developer.apple.com/xcode/downloads/).
* [Guía de la plataforma de PhoneGap iOS](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

Para Android: Para desarrollar iPhone y iPads, necesita el Android Studio IDE de Google.

* Descárguelo gratis [here](https://developer.android.com/sdk/index.html).
* [Guía de la plataforma de PhoneGap para Android](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## Descargar la fuente {#download-the-source}

Una vez que haya mejorado correctamente su entorno de desarrollo, descargue la fuente desde el mosaico de la versión de la aplicación AEM:

* Haga clic en la cadena desplegable de mosaicos del PhoneGap Build.

![chlimage_1-45](assets/chlimage_1-45.png)

* Haga clic en Descargar fuente.
* Seleccione la fuente que desee en el modal Descargar origen .

![imagen_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>La fuente de desarrollo contiene el estado más reciente de la aplicación, al tiempo que incluye cambios no escalonados. Utilice la fuente de ensayo para crear candidatos para enviar a proveedores de tiendas de aplicaciones.
>
>Si nunca realiza la fase de la aplicación, la selección de Ensayo déclencheur el flujo de trabajo de ensayo (sugerencia: esto se mostrará como una aplicación provisional en la aplicación de visor empresarial PhoneGap (disponible en App Store y Google PlayStore).

* Haga clic en Descargar y guarde el ZIP en su equipo.
* Extraiga el archivo zip descargado en su espacio de trabajo.

## Generar y cargar la aplicación (desde el origen) {#build-and-load-the-app-from-source}

La CLI de PhoneGap puede crear un proyecto de plataforma, compilar el origen e implementar la aplicación en un único comando.

>[!NOTE]
>
>Puede realizar todos estos pasos por separado; consulte [Documentos CLI de PhoneGap](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/).

1. Asegúrese de haber instalado la CLI de PhoneGap, consulte más arriba.
1. En una ventana de consola (o terminal), vaya al directorio raíz del origen extraído.
1. Introduzca el siguiente comando:

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>Si tiene problemas en este punto, vuelva a lo básico para solucionar problemas:
>
>1. Crear una nueva carpeta (prueba mkdir)
>1. Vaya a esta nueva carpeta (prueba cd)
>1. Ejecutar &#39;phonegap create helloWorld&#39;
>1. Vaya a helloWorld (cd helloWorld)
>1. Ejecute &#39;phonegap run android (o reemplace android con ios como se ha indicado anteriormente).
>1. El emulador se abrirá ejecutando la aplicación PhoneGap recién creada, diciendo &quot;Preparado para el dispositivo&quot; si el puente de JavaScript a nativo está en funcionamiento.

>
>Esto comprobará que su entorno de desarrollo de CLI de PhoneGap está funcionando correctamente.

## Depurar JavaScript con la depuración de Safari y IOS {#debug-javascripts-with-safari-and-ios-debug}

Puede depurar los JavaScript de la aplicación con las herramientas para desarrolladores de Safari, del mismo modo que lo haría con una aplicación web.

## Habilitar las herramientas para desarrolladores de Safari {#enable-safari-developer-tools}

Para habilitar las herramientas para desarrolladores:

* Abrir las preferencias de Safari

   * Haga clic en Safari en la barra de menús
   * Haga clic en Preferencias

* Haga clic en Avanzadas en la ventana Preferencias

![chlimage_1-47](assets/chlimage_1-47.png)

* Marque &quot;Mostrar menú Desarrollo en la barra de menús&quot;
* Cierre de la ventana Preferencias

## Conexión de Safari a iOS {#connect-safari-to-ios}

Puede conectar Safari a un dispositivo iOS o emulador.

* En una ventana de la consola, vaya al directorio raíz del origen extraído.
* Introduzca el siguiente comando para iniciar la aplicación en su dispositivo o emulador.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Abrir Safari
* Haga clic en Desarrollo en la barra de menús
* Seleccione el submenú Simulador de iOS
* Haga clic en home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## Depurar JavaScript con el inspector web de Safari {#debug-javascript-with-safari-s-web-inspector}

Puede establecer puntos de interrupción en cualquier lugar del origen. Cuando interactúe con su emulador o dispositivo, la ejecución de su aplicación se detendrá en esos puntos de interrupción. Puede pasar por la ejecución e inspeccionar los valores en las variables.

* Haga clic en Recursos en la ventana Inspector Web
* Navegue por el árbol de origen y haga clic en el archivo de origen deseado
* Haga clic en el número de línea adyacente para agregar un punto de interrupción.
* Interaccione con el dispositivo o emulador

![imagen_1-49](assets/chlimage_1-49.png)

* Utilice los botones de control para continuar la ejecución, dar un paso más allá, entrar en los métodos y salir de ellos:

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>Para ver los valores de las variables, en el método actual, pase el ratón.

## Pasos siguientes {#the-next-steps}

Una vez que sepa cómo desarrollar aplicaciones con la CLI de PhoneGap, consulte [Acceso a las funciones del dispositivo](/help/mobile/phonegap-access-device-features.md).
