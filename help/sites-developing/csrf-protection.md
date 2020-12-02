---
title: Marco de protección de la CSRF
seo-title: Marco de protección de la CSRF
description: El marco utiliza tokens para garantizar que la solicitud del cliente sea legítima
seo-description: El marco utiliza tokens para garantizar que la solicitud del cliente sea legítima
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Marco de protección CSRF{#the-csrf-protection-framework}

Además del filtro de Remitente del reenvío Apache Sling, Adobe también proporciona un nuevo marco de protección CSRF para protegerse contra este tipo de ataque.

El marco utiliza tokens para garantizar que la solicitud del cliente es legítima. Los tokens se generan cuando se envía el formulario al cliente y se validan cuando se devuelve el formulario al servidor.

>[!NOTE]
>
>No hay tokens en las instancias de publicación para usuarios anónimos.

## Requisitos {#requirements}

### Dependencias {#dependencies}

Cualquier componente que dependa de la dependencia `granite.jquery` se beneficiará automáticamente del marco de protección del CSRF. Si este no es el caso de ninguno de sus componentes, debe declarar una dependencia a `granite.csrf.standalone` antes de poder usar el marco.

### Replicar la clave de cifrado {#replicating-crypto-keys}

Para utilizar los tokens, debe replicar el binario `/etc/keys/hmac` en todas las instancias de la implementación. Una manera conveniente de copiar la clave HMAC en todas las instancias es crear un paquete que contenga la clave e instalarla a través del Administrador de paquetes en todas las instancias.

>[!NOTE]
>
>Asegúrese también de realizar los cambios necesarios en la configuración de [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para utilizar el marco de protección CSRF.

>[!NOTE]
>
>Si utiliza la caché de manifiesto con la aplicación web, asegúrese de agregar &quot;**&amp;ast;**&quot; al manifiesto para asegurarse de que el token no desconecte la llamada de generación de tokens de CSRF. Para obtener más información, consulte este [vínculo](https://www.w3.org/TR/offline-webapps/).
>
>Para obtener más información sobre los ataques de CSRF y las formas de mitigarlos, consulte la [página OWASP de falsificación de solicitudes entre sitios](https://owasp.org/www-community/attacks/csrf).
