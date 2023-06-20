---
title: Configuración del Cloud Service de Adobe PhoneGap Build
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: Siga esta página para configurar los servicios en la nube y crear su aplicación con PhoneGap Build.
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: 17d13e9b201629d9d1519fde4740cf651fe89d2c
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Configuración del Cloud Service de Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe SPA recomienda utilizar el Editor de para proyectos que requieran procesamiento del lado del cliente basado en el marco de trabajo de la aplicación de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El **Mosaico de PhoneGap Build** en el panel de aplicaciones se proporciona la capacidad de crear y distribuir la aplicación móvil de PhoneGap a través del servicio de Adobe PhoneGap Build.

Todas las plataformas admitidas definidas dentro de la variable **Administrar aplicación** El mosaico se creará con PhoneGap Build al insertar una compilación remota con el **PhoneGap Build** Mosaico.

Puede insertar una compilación remota en `https://build.phonegap.com` o descargue el origen para compilarlo localmente con la CLI de PhoneGap en `https://docs.phonegap.com/references/phonegap-cli/`.

![Mosaico de PhoneGap Build](assets/chlimage_1-60.png)

## Configuración del Cloud Service {#configuring-the-cloud-service}

Para aprovechar las ventajas del PhoneGap Build AEM, debe configurar el Cloud Service del PhoneGap Build de la con la información de la cuenta de PhoneGap Build.

Si actualmente no tiene una cuenta de, vaya a `https://build.phonegap.com` ¡y regístrate! Si es miembro de Adobe Creative Cloud, puede que admita hasta 25 aplicaciones privadas (aplicaciones de código no abierto).

Una vez que haya comprobado que su cuenta de PhoneGap Build AEM está activa, vaya a la consola de administración de Cloud de, específicamente a [Cloud Service de PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Utilice el **Administración de Cloud Services** mosaico para configurar una nueva configuración de cloud service.

### Uso del mosaico Administrar Cloud Services {#using-manage-cloud-services-tile}

Antes de empezar a crear la aplicación usando **PhoneGap Build** debe configurar los servicios en la nube mediante el icono **Administración de Cloud Services** del tablero de AEM Mobile.

Para configurar los servicios en la nube de su aplicación, siga los pasos a continuación:

1. Haga clic en en la esquina superior derecha de la **Administración de Cloud Services** mosaico.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Elegir **PhoneGap Build** de la opción **Agregar o editar Cloud Service** pantalla.

   Haga clic en **Siguiente**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Introduzca sus credenciales para crear una nueva configuración de nube.

   Una vez verificada, haga clic en **Enviar**. Esta configuración de nube configurada ahora se muestra en la **Administración de Cloud Services** mosaico.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Crear la aplicación con PhoneGap Build {#building-your-application-with-phonegap-build}

Una vez configurados los servicios en la nube de, puede crear la aplicación con **PhoneGap Build** mosaico. Haga clic en en la esquina superior derecha para elegir entre las **Generar remoto** o **Descargar origen** opciones.

![chlimage_1-64](assets/chlimage_1-64.png)

Para invocar una compilación remota con Adobe PhoneGap Build, haga clic en **Generar remoto**.

>[!NOTE]
>
>Si la compilación falla por algún motivo (el icono rojo de iOS a continuación indica que la plataforma ha fallado), puede pasar el ratón sobre el icono para obtener el mensaje de error. También puede hacer clic en el punto triple, &#39;...&#39; en la parte inferior del mosaico para navegar directamente a `https://build.phonegap.com` (debe autenticarse), y ver y administrar su compilación directamente.

### Creación de la aplicación con la CLI de PhoneGap {#building-your-application-with-phonegap-cli}

PhoneGap proporciona una interfaz de línea de comandos para crear la aplicación localmente.

Compile la aplicación PhoneGap en el equipo mediante la Interfaz de línea de comandos (CLI) de PhoneGap. AEM AEM Para incluir el contenido de la en la aplicación, crea un archivo ZIP que incluye el contenido de la aplicación móvil, las configuraciones de sincronización de contenido y otros recursos necesarios. Descargue el archivo ZIP e inclúyalo en su compilación.

Para aprovechar la interfaz de línea de comandos de PhoneGap, deberá configurar su entorno local para incluir lo siguiente:

1. Platform SDK (iOS, Android, Windows Phone, ...) y,
1. CLI de PhoneGap

Puede leer más aquí en `https://docs.phonegap.com/references/phonegap-cli/`.

Una vez instalados los requisitos previos, realice una prueba sencilla creando una aplicación sencilla y ejecutándola en el simulador o, mejor aún, en el dispositivo, desde un terminal. Pruebe lo siguiente:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>agregar: emule al final de esta línea si no desea ejecutarlo en el dispositivo conectado.

Una vez que haya comprobado que lo anterior funciona, utilice el **PhoneGap Build** Mosaico a **Descargar origen**. Guarde y descomprima el archivo en el sistema local. Una vez hecho esto:

* vaya a ese archivo guardado (carpeta)
* ejecute &#39;phonegap run ios&#39; (o android, etc.)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un autor y un desarrollador, consulte los recursos siguientes:

* [Desarrollo para Adobe PhoneGap AEM Enterprise con](/help/mobile/developing-in-phonegap.md)
* [Creación para Adobe PhoneGap AEM Enterprise en](/help/mobile/phonegap.md)
