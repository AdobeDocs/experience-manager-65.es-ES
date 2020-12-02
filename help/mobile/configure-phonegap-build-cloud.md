---
title: Configurar su Cloud Service de Adobe PhoneGap Build
seo-title: Configurar su Cloud Service de Adobe PhoneGap Build
description: Siga esta página para configurar los servicios en la nube y crear la aplicación con la compilación de PhoneGap.
seo-description: Siga esta página para configurar los servicios en la nube y crear la aplicación con la compilación de PhoneGap.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---


# Configure su Cloud Service de Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe recomienda el uso del Editor de SPA para proyectos que requieren una representación de cliente basada en el marco de aplicaciones de una sola página (por ejemplo, React). [Más información](/help/sites-developing/spa-overview.md).

El **icono de PhoneGap Build** en el panel de la aplicación proporciona la capacidad de crear y distribuir la aplicación móvil PhoneGap a través del servicio Adobe PhoneGap Build.

Todas las plataformas admitidas definidas en el mosaico **Administrar aplicación** se generarán con PhoneGap Build al impulsar una compilación remota con el icono **PhoneGap Build**.

Puede insertar una compilación remota en [https://build.phonegap.com](https://build.phonegap.com) o descargar la fuente para compilarla localmente con [CLI de PhoneGap](https://docs.phonegap.com/references/phonegap-cli/).

![Mosaico de PhoneGap Build](assets/chlimage_1-60.png)

## Configuración del Cloud Service {#configuring-the-cloud-service}

Para aprovechar el PhoneGap Build, debe configurar el Cloud Service del PhoneGap Build AEM con la información de su cuenta de PhoneGap Build.

Si actualmente no tiene una cuenta, navegue a [https://build.phonegap.com](https://build.phonegap.com) y regístrese. Si está abonado a Adobe Creative Cloud, es posible que tenga soporte para un máximo de 25 aplicaciones privadas (aplicaciones de código abierto).

Una vez que haya comprobado que la cuenta de PhoneGap Build está activa, navegue hasta la consola de administración de la nube de AEM, específicamente el [Cloud Service de PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Utilice el mosaico **Administrar Cloud Services** para configurar una nueva configuración de servicio en la nube.

### Uso del mosaico Administrar Cloud Services {#using-manage-cloud-services-tile}

Antes de empezar a compilar la aplicación con el mosaico **PhoneGap Build**, debe configurar los servicios en la nube mediante el mosaico **Administrar Cloud Services** del panel de AEM Mobile.

Para configurar los servicios en la nube para su aplicación, siga los pasos a continuación:

1. Haga clic en la esquina superior derecha del mosaico **Administrar Cloud Services**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Elija la opción **PhoneGap Build** en la pantalla **Añadir o editar Cloud Service**.

   Haga clic en **Siguiente**. 

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Introduzca sus credenciales para crear una nueva configuración de nube.

   Una vez verificada, haga clic en **Enviar**. Esta configuración de nube configurada ahora se muestra en el mosaico **Administrar Cloud Services**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Creación de la aplicación con PhoneGap Build {#building-your-application-with-phonegap-build}

Una vez configurados los servicios en la nube, puede crear la aplicación con **mosaico de PhoneGap Build**. Haga clic en la esquina superior derecha para elegir entre las opciones **Generar remoto** o **Descargar origen**.

![chlimage_1-64](assets/chlimage_1-64.png)

Para invocar una compilación remota con Adobe PhoneGap Build, haga clic en **Generar remoto**.

>[!NOTE]
>
>Si la compilación falla por cualquier motivo (el icono rojo de iOS que aparece a continuación indica que la plataforma ha fallado), puede pasar el ratón sobre el icono para obtener el mensaje de error. También puede hacer clic en el punto triple, &#39;...&#39; en la parte inferior del mosaico para desplazarse directamente a https://build.phonegap.com (debe autenticarse) y ver y administrar la compilación directamente.

### Generación de la aplicación con la CLI de PhoneGap {#building-your-application-with-phonegap-cli}

PhoneGap proporciona una interfaz de línea de comandos para crear la aplicación localmente.

Compile la aplicación PhoneGap en su equipo mediante la interfaz de línea de comandos (CLI) de PhoneGap. Para incluir el contenido AEM en la aplicación, AEM crea un archivo ZIP que contiene el contenido de la aplicación móvil, las configuraciones de sincronización de contenido y otros recursos necesarios. Descargue el archivo ZIP e inclúyalo en la compilación.

Para aprovechar la interfaz de línea de comandos de PhoneGap, deberá configurar el entorno local para que incluya:

1. SDK de plataforma (iOS, Android, WindowsPhone, ...) y
1. CLI de PhoneGap

Puede leer más [aquí](https://docs.phonegap.com/references/phonegap-cli/).

Una vez que haya instalado los requisitos previos, realice una prueba sencilla creando una aplicación sencilla y ejecutándola en el simulador o, mejor aún, en el dispositivo, desde un intento de terminal:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>agregar —emular al final de esta línea si no desea ejecutarlo en el dispositivo conectado.

Una vez verificado que lo anterior funciona, utilice el icono **PhoneGap Build** para **Descargar fuente**. Guarde y descomprima el archivo en su sistema local. Una vez hecho esto:

* desplazarse a ese archivo guardado (carpeta)
* ejecutar &#39;phonegap run ios&#39; (o android, etc.)

### Recursos adicionales {#additional-resources}

Para obtener información sobre las funciones y responsabilidades de un autor y desarrollador, consulte los siguientes recursos:

* [Desarrollo para Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Creación para Adobe PhoneGap Enterprise en AEM](/help/mobile/phonegap.md)
