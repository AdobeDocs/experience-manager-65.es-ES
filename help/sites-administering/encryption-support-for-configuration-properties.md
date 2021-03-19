---
title: Compatibilidad con cifrado para propiedades de configuración
seo-title: Compatibilidad con cifrado para propiedades de configuración
description: Compatibilidad con cifrado para propiedades de configuración
seo-description: nulo
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Compatibilidad con cifrado para propiedades de configuración{#encryption-support-for-configuration-properties}

## Información general {#overview}

Esta función permite almacenar todas las propiedades de configuración de OSGi en una forma cifrada protegida en lugar de en un texto claro. El formulario de la interfaz de usuario de la consola web se utiliza para crear texto cifrado a partir de texto sin formato utilizando la clave maestra de cifrado de todo el sistema.

Se agregó compatibilidad con el complemento de configuración OSGi para descifrar la propiedad antes de que la utilice un servicio.

>[!NOTE]
>
>Los servicios que esperan un valor cifrado deben utilizar la comprobación IsProtection para ver si el valor está cifrado antes de intentar descifrarlo, ya que es posible que ya se haya descifrado.

## Habilitación de la compatibilidad con cifrado {#enabling-encryption-support}

Estos pasos muestran cómo cifrar la contraseña SMTP para el servicio de correo. Puede completar estos pasos para una propiedad OSGI que desee codificar.

1. Vaya a la consola web de AEM en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. En la esquina superior izquierda, vaya a **Principal - Compatibilidad con cifrado**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. Se muestra la página **Compatibilidad con criptografía de la consola web de Adobe Experience Manager**.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. En el campo **Texto sin formato**, introduzca el texto de los datos confidenciales que desea proteger.
1. Seleccione **Protect**. El texto protegido se muestra como texto cifrado.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copie el Texto protegido del paso 5 y péguelo en el valor del formulario OSGI. En este ejemplo, la **contraseña SMTP** cifrada se agrega al *Servicio de correo de CQ de día*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Guarde las propiedades de Day CQ Mail Service. La contraseña SMTP ahora se envía como valor cifrado.

## Compatibilidad con descifrado {#decryption-support}

AEM ahora proporciona un complemento de configuración para descifrar las propiedades de configuración. Este complemento de AEM descifrará automáticamente y recuperará las propiedades de texto limpio.
