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

---


# Marco de protección de la CSRF{#the-csrf-protection-framework}

Además del filtro de referente Sling de Apache, Adobe también proporciona un nuevo marco de protección CSRF para protegerse contra este tipo de ataques.

El marco utiliza tokens para garantizar que la solicitud del cliente es legítima. Los tokens se generan cuando se envía el formulario al cliente y se validan cuando se devuelve el formulario al servidor.

>[!NOTE]
>
>No hay tokens en las instancias de publicación para usuarios anónimos.

## Requisitos {#requirements}

### Dependencias {#dependencies}

Cualquier componente que dependa de la `granite.jquery` dependencia se beneficiará automáticamente del Marco de Protección del CSRF. Si este no es el caso de ninguno de los componentes, debe declarar una dependencia a `granite.csrf.standalone` antes de poder usar la estructura.

### Replicar la clave de cifrado {#replicating-crypto-keys}

Para utilizar los tokens, debe replicar el `/etc/keys/hmac` binario en todas las instancias de la implementación. Una manera conveniente de copiar la clave HMAC en todas las instancias es crear un paquete que contenga la clave e instalarla a través del Administrador de paquetes en todas las instancias.

>[!NOTE]
>
>Asegúrese también de realizar los cambios [necesarios en la configuración de](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) Dispatcher para utilizar el marco de protección CSRF.

>[!NOTE]
>
>Si utiliza la caché de manifiesto con la aplicación web, asegúrese de agregar &quot;**&amp;ast;**&quot; al manifiesto para asegurarse de que el token no desconecte la llamada de generación de tokens de CSRF. Para obtener más información, consulte este [vínculo](https://www.w3.org/TR/offline-webapps/).
>
>Para obtener más información sobre los ataques de CSRF y las formas de mitigarlos, consulte la página [OWASP de falsificación de solicitudes](https://owasp.org/www-community/attacks/csrf)entre sitios.
