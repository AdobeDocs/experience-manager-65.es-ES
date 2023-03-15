---
title: Configurar SSL en Windows Vista
seo-title: Configuring SSL on Windows Vista
description: Obtenga información sobre cómo configurar SSL en Windows Vista.
seo-description: Learn how to configure SSL on Windows Vista.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 6%

---

# Configurar SSL en Windows Vista {#configuring-ssl-on-windows-vista}

Para configurar SSL en Windows Vista™, necesita un certificado SSL con claves RSA para la autenticación. Puede utilizar la herramienta clave de Java para crear el certificado.

>[!NOTE]
>
>Windows Vista no funciona con claves DSA.

Puede ejecutar keytool con un solo comando que incluya toda la información necesaria para crear el certificado y el repositorio de claves.

**Creación de un certificado SSL**

1. En un símbolo del sistema, vaya a *`[JAVA HOME]`*/bin y escriba el siguiente comando para crear el certificado y el almacén de claves:

   `keytool -genkey -keyalg RSA -dname "CN=`*Nombre de host* `, OU=`*Nombre de grupo* `, O=`*Nombre de empresa* `,L=`*Nombre de ciudad* `, S=`*Estado* `, C=`*Código del país* `" -alias`*&quot;Certificado LC&quot;* `-keypass` `key`*_* *contraseña* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Reemplazar *`[JAVA_HOME]`con el directorio en el que está instalado el JDK y reemplace el texto en cursiva por valores que se correspondan con su entorno.*

1. Tipo `changeit` como contraseña. Esta contraseña es la predeterminada para una instalación de Java y es posible que el administrador del sistema la haya cambiado.
