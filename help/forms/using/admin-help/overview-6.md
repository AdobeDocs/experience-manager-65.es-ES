---
title: Información general sobre la configuración de SSL
seo-title: Información general sobre la configuración de SSL
description: Obtenga información sobre cómo mejorar la seguridad de la comunicación mediante la configuración de SSL.
seo-description: Obtenga información sobre cómo mejorar la seguridad de la comunicación mediante la configuración de SSL.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Información general sobre la configuración de SSL {#overview-of-configuring-ssl}

Puede crear credenciales de Capa de sockets seguros (SSL) y configurar SSL en el servidor de aplicaciones para mejorar la seguridad de la comunicación con el servidor de aplicaciones.

Como producto de seguridad, Rights Management requiere la configuración de SSL. Al configurar los certificados SSL, asegúrese de utilizar sólo claves RSA. Los certificados SSL con claves DSA no son compatibles.

La información proporcionada se aplica a las instalaciones llave en mano, automáticas y manuales. Ofrece un ejemplo de un método para configurar SSL. También puede utilizar otros métodos que sean más adecuados para su red u organización.

>[!NOTE]
>
>Se recomienda completar la instalación, configuración e implementación de los módulos de formularios AEM y asegurarse de que los productos se ejecutan correctamente antes de configurar SSL en el servidor de aplicaciones.

>[!NOTE]
>
>Al crear certificados de seguridad SSL y credenciales, utilice los mismos privilegios de cuenta de usuario que utilizó para ejecutar el servidor de aplicaciones. Si el servidor de aplicaciones se ejecuta con otros privilegios de usuario, es posible que el formulario no se procese correctamente en las representaciones de PDFForm cuando ContentRootURI apunta a https.

Si tiene un servidor LDAP habilitado para SSL, configure la Administración de usuarios para que funcione con él. (Consulte [Configuración de la administración de usuarios para un servidor](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)LDAP con SSL habilitado).
