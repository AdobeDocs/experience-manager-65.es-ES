---
title: Información general sobre la configuración de SSL
seo-title: Overview of configuring SSL
description: Obtenga información sobre cómo mejorar la seguridad de la comunicación configurando SSL.
seo-description: Learn about how to enhance security of communication by configuring SSL.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Información general sobre la configuración de SSL {#overview-of-configuring-ssl}

Puede crear credenciales de Secure Sockets Layer (SSL) y configurar SSL en el servidor de aplicaciones para mejorar la seguridad de la comunicación con el servidor de aplicaciones.

Como producto de seguridad, Rights Management requiere la configuración de SSL. Al configurar los certificados SSL, asegúrese de utilizar solo claves RSA. Los certificados SSL con claves DSA no son compatibles.

La información proporcionada se aplica a las instalaciones llave en mano, automáticas y manuales. Ofrece un ejemplo de un método para configurar SSL. También puede utilizar otros métodos que sean más adecuados para su red u organización.

>[!NOTE]
>
>Se recomienda completar la instalación, configuración e implementación de los módulos de formularios AEM y asegurarse de que los productos se ejecutan correctamente antes de configurar SSL en el servidor de aplicaciones.

>[!NOTE]
>
>Al crear certificados de seguridad SSL y credenciales, utilice los mismos privilegios de cuenta de usuario que utilizó para ejecutar el servidor de aplicaciones. Si el servidor de aplicaciones se ejecuta utilizando otros privilegios de usuario, es posible que el formulario no se represente correctamente en las representaciones PDFForm cuando ContentRootURI señala a https.

Si tiene un servidor LDAP habilitado para SSL, configure User Management para que funcione con él. (Consulte [Configuración de la administración de usuarios para un servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
