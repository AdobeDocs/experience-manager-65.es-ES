---
title: Configuración del Cloud Service de Adobe PhoneGap Build
description: Siga esta página para configurar los servicios en la nube y crear su aplicación con PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Configuración del Cloud Service de Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

{{ue-over-mobile}}

El **Mosaico de PhoneGap Build** en el panel de aplicaciones le permite crear y distribuir su aplicación móvil de PhoneGap a través del servicio Adobe PhoneGap Build.

Todas las plataformas admitidas definidas dentro del mosaico **Administrar aplicación** se crean con PhoneGap Build al insertar una compilación remota con el mosaico **PhoneGap Build**.

Puede insertar una compilación remota en `https://build.phonegap.com` o descargar el origen para compilar localmente con la CLI de PhoneGap en `https://docs.phonegap.com/references/phonegap-cli/`.

![Mosaico de PhoneGap Build](assets/chlimage_1-60.png)

## Configuración del Cloud Service {#configuring-the-cloud-service}

Para aprovechar las ventajas del PhoneGap Build AEM, debe configurar el Cloud Service del PhoneGap Build de la con la información de la cuenta de PhoneGap Build.

Si todavía no tiene una cuenta, vaya a `https://build.phonegap.com` y regístrese. Si es miembro de Adobe Creative Cloud, puede que admita hasta 25 aplicaciones privadas (aplicaciones de código no abierto).

Una vez que haya comprobado que su cuenta de PhoneGap Build AEM está activa, vaya a la consola de administración de nube de, específicamente al [Cloud Service de PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Use el mosaico **Administrar Cloud Service** para configurar una nueva configuración de servicio en la nube.

### Uso del mosaico Administrar Cloud Service {#using-manage-cloud-services-tile}

Antes de empezar a crear la aplicación con el mosaico **PhoneGap Build**, debe configurar los servicios en la nube con el mosaico **Administrar Cloud Service** del panel de AEM Mobile.

Para configurar los servicios en la nube de su aplicación, siga los pasos a continuación:

1. Haga clic en la esquina superior derecha del mosaico **Administrar Cloud Service**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Elija la opción **PhoneGap Build** en la pantalla **Agregar o editar Cloud Service**.

   Haga clic en **Siguiente**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Introduzca sus credenciales para poder crear una configuración de nube.

   Una vez verificado, haga clic en **Enviar**. Esta configuración de nube configurada ahora se muestra en el mosaico **Administrar Cloud Service**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Crear la aplicación con PhoneGap Build {#building-your-application-with-phonegap-build}

Una vez que haya configurado los servicios en la nube, puede generar su aplicación con el mosaico **PhoneGap Build**. Haz clic en la esquina superior derecha para elegir entre las opciones **Generar remoto** o **Descargar Source**.

![chlimage_1-64](assets/chlimage_1-64.png)

Para invocar una compilación remota con Adobe PhoneGap Build, haga clic en **Generar remota**.

>[!NOTE]
>
>Si la compilación falla por algún motivo (el icono rojo de iOS a continuación indica que la plataforma ha fallado), puede pasar el ratón sobre el icono para obtener el mensaje de error. También puede hacer clic en el punto triple, &#39;...&#39; en la parte inferior del mosaico para navegar directamente a `https://build.phonegap.com` (debe autenticarse) y ver y administrar su compilación directamente.

### Creación de la aplicación con la CLI de PhoneGap {#building-your-application-with-phonegap-cli}

PhoneGap proporciona una interfaz de línea de comandos para generar la aplicación localmente.

Compile la aplicación PhoneGap en el equipo mediante la interfaz de línea de comandos (CLI) de PhoneGap. AEM AEM Para incluir el contenido de la en la aplicación, crea un archivo ZIP que incluye el contenido de la aplicación móvil, las configuraciones de sincronización de contenido y otros recursos necesarios. Descargue el archivo ZIP e inclúyalo en su compilación.

Para aprovechar la CLI de PhoneGap, debe configurar su entorno local para que incluya lo siguiente:

1. Platform SDK (iOS, Android™, Windows Phone, ...) y,
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
>Añada: emule al final de esta línea si no desea ejecutarlo en el dispositivo conectado.

Una vez que haya comprobado que lo anterior funciona, use el mosaico **PhoneGap Build** para **descargar Source**. Guarde y descomprima el archivo en el sistema local. Una vez hecho esto:

* vaya a ese archivo guardado (carpeta)
* ejecute &#39;phonegap run ios&#39; (o android, etc.)

### Recursos adicionales {#additional-resources}

Para obtener más información sobre las funciones y responsabilidades de un autor y un desarrollador, consulte los recursos siguientes:

* [Desarrollo para Adobe PhoneGap AEM Enterprise con](/help/mobile/developing-in-phonegap.md)
* [Creación para Adobe PhoneGap AEM Enterprise en](/help/mobile/phonegap.md)
