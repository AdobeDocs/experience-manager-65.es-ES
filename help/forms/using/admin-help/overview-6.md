---
title: Información general sobre la configuración de SSL
description: Obtenga información sobre cómo mejorar la seguridad de la comunicación configurando SSL.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 3%

---

# Información general sobre la configuración de SSL {#overview-of-configuring-ssl}

Puede crear credenciales de Secure Sockets Layer (SSL) y configurar SSL en el servidor de aplicaciones para mejorar la seguridad de la comunicación con el servidor de aplicaciones.

Como producto de seguridad, Rights Management requiere la configuración de SSL. Al configurar los certificados SSL, asegúrese de utilizar solo claves RSA. No se admiten certificados SSL con claves DSA.

La información proporcionada se aplica a instalaciones llave en mano, automáticas y manuales. Ofrece un ejemplo de método para configurar SSL. También puede utilizar otros métodos que sean más adecuados para su red u organización.

>[!NOTE]
>
>AEM Se recomienda completar la instalación, la configuración y la implementación de los módulos de formularios de la aplicación y asegurarse de que los productos se ejecutan correctamente antes de configurar SSL en el servidor de aplicaciones.

>[!NOTE]
>
>Al crear certificados y credenciales de seguridad SSL, utilice los mismos privilegios de cuenta de usuario que utilizó para ejecutar el servidor de aplicaciones. Si el servidor de aplicaciones se ejecuta con otros privilegios de usuario, es posible que el formulario no se represente correctamente para representaciones de PDFForm cuando ContentRootURI señala a https.

Si tiene un servidor LDAP habilitado para SSL, configure Administración de usuarios para que funcione con él. (Consulte [Configuración de la administración de usuarios para un servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
