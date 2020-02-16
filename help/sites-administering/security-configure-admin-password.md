---
title: Configurar la contraseña de administración al realizar la instalación
seo-title: Configurar la contraseña de administración al realizar la instalación
description: Obtenga información sobre cómo cambiar la contraseña de administración en la instalación de AEM.
seo-description: Obtenga información sobre cómo cambiar la contraseña de administración en la instalación de AEM.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Configurar la contraseña de administración al realizar la instalación{#configure-the-admin-password-on-installation}

## Información general {#overview}

Desde la versión 6.3, AEM permite establecer la contraseña de administrador mediante la línea de comandos al instalar una nueva instancia.

Con versiones anteriores de AEM, la contraseña de la cuenta de administrador, junto con la contraseña de varias otras consolas, tuvieron que cambiarse después de la instalación.

Esta función agrega la posibilidad de configurar una nueva contraseña de administrador para el repositorio y el motor Servlet durante la instalación de una instancia de AEM, eliminando así la necesidad de hacerlo manualmente posteriormente.

>[!CAUTION]
>
>Tenga en cuenta que la función no cubre la consola Félix, para la cual la contraseña debe cambiarse manualmente. Para obtener más información, consulte la sección [correspondiente Lista de comprobación](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)de seguridad.

## ¿Cómo Lo Utilizo? {#how-do-i-use-it}

Esta función se activará automáticamente si decide instalar AEM a través de la línea de comandos, en lugar de hacer doble clic en JAR desde un explorador de sistemas de archivos.

La sintaxis general para ejecutar una instancia de AEM desde la línea de comandos es:

```shell
java -jar aem6.3.jar
```

Al ejecutar la instancia desde la línea de comandos, se le mostrará la opción de cambiar la contraseña de administrador durante el proceso de instalación:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>El mensaje para cambiar la contraseña de administrador solo aparecerá durante la instalación de una nueva instancia de AEM.

## Uso del indicador -nointeractive {#using-the-nointeractive-flag}

También puede especificar la contraseña de un archivo de propiedades. Esto se realiza mediante el uso del `-nointeractive` indicador combinado con la propiedad del`-Dadmin.password.file` sistema.

A continuación se muestra un ejemplo:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

La contraseña dentro del `passwordfile.properties` archivo debe tener el formato siguiente:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Si simplemente utiliza el `-nointeractive` parámetro sin la propiedad `-Dadmin.password.file` del sistema, AEM utilizará la contraseña de administrador predeterminada sin pedirle que la cambie, básicamente replicando el comportamiento de versiones anteriores. Este modo no interactivo se puede utilizar para instalaciones automatizadas utilizando la línea de comandos en una secuencia de comandos de instalación.

