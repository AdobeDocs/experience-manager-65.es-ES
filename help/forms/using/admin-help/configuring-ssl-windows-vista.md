---
title: Configuración de SSL en Windows Vista
seo-title: Configuración de SSL en Windows Vista
description: Obtenga información sobre cómo configurar SSL en Windows Vista.
seo-description: Obtenga información sobre cómo configurar SSL en Windows Vista.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# Configuración de SSL en Windows Vista {#configuring-ssl-on-windows-vista}

Para configurar SSL en Windows Vista™, necesita un certificado SSL con claves RSA para la autenticación. Puede utilizar la herramienta de clave de Java para crear el certificado.

>[!NOTE]
>
>Windows Vista no funcionará con las claves DSA.

Puede ejecutar keytool utilizando un único comando que incluya toda la información necesaria para crear el certificado y el almacén de claves.

**Crear un certificado SSL**

1. En un símbolo del sistema, vaya a *`[JAVA HOME]`*/bin y escriba el siguiente comando para crear el certificado y el almacén de claves:

   `keytool -genkey -keyalg RSA -dname "CN=`*Nombre *Host Nombre`, OU=`** Grupo Nombre `, O=`**Empresa Nombre`,L=`** Ciudad Nombre `, S=`**Estado Código`, C=`** `" -alias`**`-keypass``key`** ** `-keystore`**País&quot;LC&quot;Cert&quot;_contraseñaNombreclave`.keystore`

   >[!NOTE]
   >
   >Reemplace *`[JAVA_HOME]`con el directorio en el que está instalado JDK y reemplace el texto en cursiva por valores que correspondan a su entorno.*

1. Escriba `changeit` como contraseña. Esta contraseña es la predeterminada para una instalación de Java y es posible que el administrador del sistema la haya cambiado.

