---
title: 'Pasos adicionales para obtener el correo electrónico con los archivos adjuntos '
description: 'Pasos adicionales para obtener el correo electrónico con los archivos adjuntos   '
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# No se puede obtener el correo electrónico con los archivos adjuntos para AEM Forms en plataformas JEE{#unable-to-get-email-with-attachments}

El problema se aplica a la siguiente versión:
* Experience Manager 6.5 Forms

## Problema   {#issue}

El usuario no puede realizar operaciones como Enviar PDF por correo electrónico o Incluir archivos adjuntos con la configuración de envío.

## Solución {#solution}

1. Descargar jar como [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) y descomprima el archivo jar descargado para obtener el archivo de manifiesto.

1. Utilice el archivo de manifiesto de `java.mail-1.0.jar` se ha recuperado del paso 1 para crear un nuevo archivo jar personalizado, como `java.mail-1.5.jar`.

1. Abra el archivo de manifiesto y reemplace todas las ocurrencias de `1.5.0` con `1.5.6` y `Bundle-Version: 1.0` con `Bundle-Version:1.5`

1. Crear un nuevo jar personalizado (`java.mail-1.5.jar`) utilizando el siguiente comando en `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` como:
   `jar -cfm java.mail-1.5.jar manifest.mf`

   En el comando anterior, *manifest.mf* es el nombre del archivo de manifiesto y *java.mail-1.5.jar* es el nombre del archivo que se crearía después de ejecutar el comando anterior.

1. Descargar [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. Vaya a `http://<server name>:<port>/lc/system/console/bundles`y elimine el paquete con un nombre como `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. Instalar `java.mail-1.5.jar` obtenido del paso 3.  Este paso reinicia las propiedades sling de la implementación JEE. Espere a que se instalen los paquetes en `http://<server name>:<port>/lc/system/console/bundles` para mostrar el estado como **Activo**.

   >Nota: En caso de que el estado siga siendo **InActive**, reiniciar   **JBoss** de la variable **Consola Servicios**.


1. Instalar `javax.mail-1.5.6.redhat-1.jar`archivo descargado mediante el paso 5.

1. Stop **JBoss** de la variable **Consola Servicios** y anexe las siguientes propiedades a **Sling.properties** archivo:
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. Restart **JBoss**.