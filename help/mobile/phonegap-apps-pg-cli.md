---
title: Desarrollo de aplicaciones con CLI de PhoneGap
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
ht-degree: 1%

---

# Desarrollo de aplicaciones con CLI de PhoneGap{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

En cualquier momento dado, como desarrollador, puede ejecutar la aplicación en un dispositivo o en un emulador, siempre y cuando haya configurado el entorno de desarrollo.

Para ejecutar los siguientes ejemplos necesitará un sistema que ejecute OSx (Mac) con Xcode o un sistema Mac/Win/Linux con el SDK de Android instalado.

## Bootstrap de su entorno de desarrollo {#bootstrap-your-development-environment}

[Configuración de la CLI de PhoneGap](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

Para iOS: Para desarrollar para iPhones y iPads, necesita el IDE Xcode de Apple.

* Descárguelo de forma gratuita [aquí](https://developer.apple.com/xcode/downloads/).
* [Guía de la plataforma PhoneGap iOS](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

Para Android: Para desarrollar para iPhones y iPads, necesita Android Studio IDE de Google.

* Descárguelo de forma gratuita [aquí](https://developer.android.com/sdk/index.html).
* [Guía de la plataforma Android PhoneGap](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## Descargar el origen {#download-the-source}

AEM Una vez que haya arrancado correctamente su entorno de desarrollo, descargue el origen desde el mosaico de creación de la aplicación de la aplicación de la:

* Haga clic en las comillas angulares desplegables de mosaico de PhoneGap Build.

![chlimage_1-45](assets/chlimage_1-45.png)

* Haga clic en Descargar origen.
* Seleccione el origen que desee en el modal Descargar origen.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>La fuente de desarrollo contiene el estado más reciente de la aplicación, aunque incluye cambios sin fases. Utilice la fuente de ensayo para crear candidatos de versión para enviarlos a proveedores de tiendas de aplicaciones.
>
>Si nunca almacena en zona intermedia la aplicación, al seleccionar Ensayo se almacenará en déclencheur el flujo de trabajo de ensayo (sugerencia: esto se mostrará como una aplicación ensayada en la aplicación del visor empresarial de PhoneGap disponible en la AppStore y en la PlayStore de Google).

* Haga clic en Descargar y guarde el archivo ZIP en el equipo.
* Extraiga el archivo zip descargado en el espacio de trabajo.

## Generar y cargar la aplicación (desde el origen) {#build-and-load-the-app-from-source}

La CLI de PhoneGap puede crear un proyecto de plataforma, compilar el origen e implementar la aplicación en un solo comando.

>[!NOTE]
>
>Puede realizar todos estos pasos por separado; consulte [Documentos CLI de PhoneGap](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/).

1. Asegúrese de que ha instalado la CLI de PhoneGap; consulte lo anterior.
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
>1. Crear una carpeta nueva (prueba mkdir)
>1. Vaya a esta nueva carpeta (prueba de CD)
>1. Ejecutar &#39;phonegap create helloWorld&#39;
>1. Navegar a helloWorld (cd helloWorld)
>1. Ejecute &quot;phonegap&quot;, ejecute android (o reemplace android por ios, como se ha indicado anteriormente).
>1. El emulador se abrirá ejecutando la aplicación PhoneGap recién creada, indicando &quot;Dispositivo listo&quot; si el puente JavaScript a nativo está operativo.

>
>Esto comprobará que su entorno de desarrollo de CLI de PhoneGap está funcionando correctamente.

## Depuración de JavaScript con Safari y IOS Debug {#debug-javascripts-with-safari-and-ios-debug}

Puede depurar los JavaScript de su aplicación con las herramientas para desarrolladores de Safari, del mismo modo que lo haría con una aplicación web.

## Habilitar las herramientas para desarrolladores de Safari {#enable-safari-developer-tools}

Para habilitar las herramientas para desarrolladores:

* Abrir las preferencias de Safari

   * Haga clic en Safari en la barra de menús
   * Haga clic en Preferencias

* Haga clic en Avanzadas en la ventana Preferencia

![chlimage_1-47](assets/chlimage_1-47.png)

* Marque &quot;Mostrar el menú Desarrollo en la barra de menús&quot;
* Cierre la ventana Preferencia

## Conexión de Safari a iOS {#connect-safari-to-ios}

Puede conectar Safari a un dispositivo o emulador de iOS.

* En una ventana de la consola, vaya al directorio raíz del origen extraído.
* Introduzca el siguiente comando para iniciar la aplicación en su dispositivo o emulador.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Abrir Safari
* Haga clic en Desarrollo en la barra de menús
* Seleccione el submenú iOS Simulator
* Haga clic en home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## Depurar JavaScript con el inspector web de Safari {#debug-javascript-with-safari-s-web-inspector}

Puede establecer puntos de interrupción en cualquier lugar del origen. Al interactuar con el emulador o el dispositivo, la ejecución de la aplicación se detendrá en esos puntos de interrupción. Puede recorrer paso a paso la ejecución e inspeccionar los valores de las variables.

* Haga clic en Recursos en la ventana Inspector Web
* Navegue por el árbol de origen y haga clic en el archivo de origen deseado
* Haga clic en el número de línea adyacente para agregar un punto de interrupción
* Interactuar con dispositivo o emulador

![chlimage_1-49](assets/chlimage_1-49.png)

* Utilice los botones de control para continuar la ejecución, pasar por encima, entrar y salir de los métodos:

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>Para ver los valores de las variables, en el método actual, pase el ratón por encima.

## Pasos siguientes {#the-next-steps}

Una vez que haya aprendido a desarrollar aplicaciones con la CLI de PhoneGap, consulte [Acceso a funciones del dispositivo](/help/mobile/phonegap-access-device-features.md).
