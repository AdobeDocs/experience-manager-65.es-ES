---
title: Revisar información del uso de credenciales
description: Obtenga información sobre cómo revisar la información de uso de las credenciales. Se puede acceder a la información de uso de credenciales, que describe su uso, a través de la extensión de Acrobat Reader.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8e16cf8-f3c8-48ce-87da-2f0de0b10a6e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 4%

---

# Revisar información del uso de credenciales {#review-credential-use-information}

Las credenciales contienen información que describe su uso previsto y a la que se puede acceder mediante la aplicación web de extensiones de Acrobat Reader DC dirigida a usuarios finales. Puede utilizar esta información para determinar el tipo de credencial instalada (ya sea de evaluación o de producción) y sus fechas de validez.

1. Abra un explorador web e introduzca esta dirección URL:

   http://localhost:port/ReaderExtensions (donde *puerto* es el número de puerto del servidor de aplicaciones)

1. Inicie sesión con el nombre de usuario y la contraseña predeterminados:

   Nombre de usuario: administrador

   Contraseña: password

   >[!NOTE]
   >
   >Debe tener privilegios de administrador o superusuario para iniciar sesión con el nombre de usuario y la contraseña predeterminados. Para permitir que otros usuarios accedan a las extensiones de Acrobat Reader DC, cree las cuentas de usuario en Administración de usuarios y otorgue a los usuarios la función Aplicación web de extensiones de Acrobat Reader DC.

1. Seleccione el alias de credencial de la lista Seleccionar credencial y revise la información incluida en Fecha de caducidad y Aviso de uso previsto.

>[!NOTE]
>
>La fecha de caducidad de la credencial también está disponible en la página Configuración > Administración del almacén de confianza > Credenciales locales de la consola de administración, en Fecha de caducidad.
