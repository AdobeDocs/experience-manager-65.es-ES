---
title: Marco de protección del CSRF
seo-title: The CSRF Protection Framework
description: El marco de trabajo utiliza tokens para garantizar que la solicitud del cliente sea legítima
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Marco de protección del CSRF{#the-csrf-protection-framework}

Además del filtro de referente de Apache Sling, Adobe también proporciona un nuevo marco de protección CSRF para protegerse contra este tipo de ataque.

El marco utiliza tokens para garantizar que la solicitud del cliente sea legítima. Los tokens se generan cuando el formulario se envía al cliente y se validan cuando se devuelve el formulario al servidor.

>[!NOTE]
>
>No hay tokens en las instancias de publicación para usuarios anónimos.

## Requisitos  {#requirements}

### Dependencias {#dependencies}

Cualquier componente que dependa del `granite.jquery` dependencia se beneficiará automáticamente del marco de protección CSRF. Si este no es el caso de ninguno de sus componentes, debe declarar una dependencia a `granite.csrf.standalone` antes de poder usar el marco.

### Duplicación de la clave criptográfica {#replicating-crypto-keys}

Para utilizar los tokens, debe replicar la variable `/etc/keys/hmac` binario a todas las instancias de la implementación. Una forma cómoda de copiar la clave HMAC en todas las instancias es crear un paquete que contenga la clave e instalarla a través del Administrador de paquetes en todas las instancias.

>[!NOTE]
>
>Asegúrese de que también hace lo necesario [Cambios en la configuración de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para utilizar el marco de protección del CSRF.

>[!NOTE]
>
>Si utiliza la caché de manifiesto con la aplicación web, asegúrese de agregar &quot;**&amp;ast;**&quot; al manifiesto para asegurarse de que el token no desconecte la llamada de generación de tokens de CSRF. Para obtener más información, consulte esta [vínculo](https://www.w3.org/TR/offline-webapps/).
>
>Para obtener más información sobre los ataques de CSRF y las formas de mitigarlos, consulte la [Página ASP de falsificación de solicitudes entre sitios](https://owasp.org/www-community/attacks/csrf).
