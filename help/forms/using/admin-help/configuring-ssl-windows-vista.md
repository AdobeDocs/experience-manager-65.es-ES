---
title: Configurar SSL en Windows Vista
description: Obtenga información sobre cómo configurar SSL en Windows Vista. Utilice y ejecute la herramienta Java Keytool para generar el certificado SSL con claves RSA para la autenticación.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

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
