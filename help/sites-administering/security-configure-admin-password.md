---
title: Configurar la contraseña de administración al realizar la instalación
seo-title: Configurar la contraseña de administración al realizar la instalación
description: Obtenga información sobre cómo cambiar la contraseña de administración en AEM instalación.
seo-description: Obtenga información sobre cómo cambiar la contraseña de administración en AEM instalación.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Configurar la contraseña de administración en la instalación{#configure-the-admin-password-on-installation}

## Información general {#overview}

Desde la versión 6.3, AEM permite que la contraseña de administrador se establezca mediante la línea de comandos al instalar una nueva instancia.

Con versiones anteriores de AEM, la contraseña de la cuenta de administrador, junto con la contraseña de varias otras consolas, tuvieron que cambiarse después de la instalación.

Esta función agrega la posibilidad de configurar una nueva contraseña de administrador para el repositorio y el motor Servlet durante la instalación de una instancia de AEM, eliminando así la necesidad de hacerlo manualmente después.

>[!CAUTION]
>
>Tenga en cuenta que la función no cubre la consola Félix, para la cual la contraseña debe cambiarse manualmente. Para obtener más información, consulte la sección [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts) correspondiente.

## ¿Cómo Lo Utilizo? {#how-do-i-use-it}

Esta función se déclencheur automáticamente si elige instalar AEM a través de la línea de comandos, en lugar de hacer clic en el doble en el JAR desde un explorador del sistema de archivos.

El sintaxis general para ejecutar una instancia de AEM desde la línea de comandos es:

```shell
java -jar aem6.3.jar
```

Al ejecutar la instancia desde la línea de comandos, se le mostrará la opción de cambiar la contraseña de administrador durante el proceso de instalación:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>El mensaje para cambiar la contraseña de administrador solo aparecerá durante la instalación de una nueva instancia de AEM.

## Uso del indicador -nointeractivo {#using-the-nointeractive-flag}

También puede especificar la contraseña de un archivo de propiedades. Esto se realiza mediante el uso del indicador `-nointeractive` combinado con la propiedad del sistema`-Dadmin.password.file`.

A continuación se muestra un ejemplo:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

La contraseña dentro del archivo `passwordfile.properties` debe tener el formato siguiente:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Si simplemente utiliza el parámetro `-nointeractive` sin la propiedad del sistema `-Dadmin.password.file`, AEM utilizará la contraseña de administrador predeterminada sin pedirle que la cambie, básicamente replicando el comportamiento de versiones anteriores. Este modo no interactivo se puede utilizar para instalaciones automatizadas utilizando la línea de comandos en una secuencia de comandos de instalación.

