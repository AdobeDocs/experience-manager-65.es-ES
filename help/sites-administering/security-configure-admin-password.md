---
title: Configurar la contraseña de administrador durante la instalación
seo-title: Configure the Admin Password on Installation
description: AEM Aprenda a cambiar la contraseña de administrador en la instalación de la.
seo-description: Learn how to change the Admin Password on AEM Installation.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Configurar la contraseña de administrador durante la instalación{#configure-the-admin-password-on-installation}

## Información general {#overview}

AEM Desde la versión 6.3, permite establecer la contraseña de administrador mediante la línea de comandos al instalar una instancia nueva.

AEM Con las versiones anteriores de la cuenta de administrador, la contraseña de la cuenta de administrador, junto con la contraseña de otras consolas, se tenían que cambiar después de la instalación.

AEM Esta función añade la posibilidad de configurar una nueva contraseña de administrador para el repositorio y el motor servlet durante la instalación de una instancia de, lo que elimina la necesidad de hacerlo manualmente posteriormente.

>[!CAUTION]
>
>Tenga en cuenta que esta función no cubre la consola Felix, para la cual es necesario cambiar la contraseña manualmente. Para obtener más información, consulte los [Sección Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## ¿Cómo Lo Uso? {#how-do-i-use-it}

Esta función se almacenará en déclencheur AEM automáticamente si elige instalar los archivos a través de la línea de comandos, en lugar de hacer doble clic en el JAR desde un explorador del sistema de archivos.

AEM La sintaxis general para ejecutar una instancia de desde la línea de comandos es:

```shell
java -jar aem6.3.jar
```

Al ejecutar la instancia desde la línea de comandos, se le ofrecerá la opción de cambiar la contraseña de administrador durante el proceso de instalación:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>AEM La solicitud para cambiar la contraseña de administrador solo aparece durante la instalación de una nueva instancia de la instancia de la instancia de la nueva instancia de la instancia de la.

## Uso del indicador -nointeractive {#using-the-nointeractive-flag}

También puede especificar la contraseña en un archivo de propiedades. Esto se realiza mediante el uso de `-nointeractive` indicador combinado con`-Dadmin.password.file` propiedad del sistema.

A continuación se muestra un ejemplo:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

La contraseña dentro de `passwordfile.properties` el archivo debe tener el siguiente formato:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Si simplemente utiliza la variable `-nointeractive` parámetro sin el parámetro `-Dadmin.password.file` AEM propiedad del sistema, utilizará la contraseña de administrador predeterminada sin pedirle que la cambie, lo que básicamente replicará el comportamiento de versiones anteriores. Este modo no interactivo se puede utilizar para instalaciones automatizadas utilizando la línea de comandos en un script de instalación.
