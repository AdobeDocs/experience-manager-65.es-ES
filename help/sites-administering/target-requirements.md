---
title: Requisitos previos para la integración con Adobe Target
seo-title: Prerequisites for Integrating with Adobe Target
description: Obtenga información sobre los requisitos previos para la integración con Adobe Target.
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 7%

---

# Requisitos previos para la integración con Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Como parte del [integración de AEM y Adobe Target](/help/sites-administering/target.md), debe registrarse con Adobe Target, configurar el agente de replicación y establecer la configuración de actividad segura en el nodo de publicación.

## Registro con Adobe Target {#registering-with-adobe-target}

Para integrar AEM con Adobe Target, debe tener una cuenta de Adobe Target válida. Esta cuenta debe tener **aprobador** nivel de permisos como mínimo. Al registrarse en Adobe Target, recibe un código de cliente. Necesita el código de cliente, el nombre de inicio de sesión y la contraseña de Adobe Target para conectarse AEM Adobe Target.

El código de cliente identifica la cuenta de cliente de Adobe Target al llamar al servidor de Adobe Target.

>[!NOTE]
>
>El equipo de Target también debe habilitar la cuenta para poder usar la integración.
>
>Si no es así, póngase en contacto con [Servicio de atención al cliente de Adobe](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html).

## Habilitar el agente de replicación de Target {#enabling-the-target-replication-agent}

La prueba y el objetivo [agente de replicación](/help/sites-deploying/replication.md) debe estar habilitado en la instancia de autor. Tenga en cuenta que este agente de replicación no está habilitado de forma predeterminada si ha utilizado la variable [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) ejecute el modo para instalar AEM. Para obtener más información sobre la seguridad del entorno de producción, consulte [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md).

1. En la página principal de AEM, toque o haga clic en **Herramientas** > **Implementación** > **Replicación**.
1. Toque o haga clic en **Agentes En Autor**.
1. Toque o haga clic en **Prueba y objetivo (prueba y destino)** agente de replicación y, a continuación, toque o haga clic en **Editar**.
1. Seleccione la opción Activado y, a continuación, toque o haga clic en **OK**.

   >[!NOTE]
   >
   >Cuando configure el agente de replicación de Test y Target, en la variable **Transporte** , el URI se establece de forma predeterminada en **tnt:///**. No reemplace este URI por **https://admin.testandtarget.omniture.com**.
   >
   >Tenga en cuenta que si intenta probar la conexión con **tnt:///**, generará un error. Este comportamiento es esperado, ya que este URI es solo para uso interno y no debe usarse con **Probar conexión**.

## Protección del nodo Configuración de actividades {#securing-the-activity-settings-node}

Debe asegurar el nodo de configuración de actividades **cq:ActivitySettings** de la instancia de publicación, para que los usuarios normales no puedan obtener acceso a él. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.

La variable **cq:ActivitySettings** El nodo está disponible en la lista CRXDE, en `/content/campaigns/*nameofbrand*`* *en el nodo activity jcr:content;* *por ejemplo `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Este nodo solo se crea después de que se dirija a un componente.

La variable **cq:ActivitySettings** bajo el jcr:content de la actividad está protegido por las siguientes ACL:

* Denegar todo para todos
* Permitir jcr:read,rep:write para &quot;target-activity-authors&quot; (el autor es un miembro de este grupo de forma predeterminada)
* Permitir jcr:read,rep:write para &quot;targetservice&quot;

Estos ajustes garantizan que los usuarios normales no tengan acceso a las propiedades del nodo. Utilice las mismas ACL en el autor y en la publicación. Consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md) para obtener más información.

## Configuración del externalizador de vínculos AEM {#configuring-the-aem-link-externalizer}

Al editar una actividad en Adobe Target, la dirección URL señala a **localhost** a menos que cambie la dirección URL en el nodo AEM autor. Puede configurar el AEM externalizador de vínculos si desea que el contenido exportado apunte a un *publicar* dominio.

>[!NOTE]
>
>Consulte también [Añadir la configuración de nube](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Para configurar el externalizador de AEM:

>[!NOTE]
>
>Para obtener más información, consulte [Externalización de direcciones URL](/help/sites-developing/externalizer.md).

1. Vaya a la consola web OSGi en **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Buscar **Externalizador de vínculos de CQ de día** e introduzca el dominio del nodo de creación.

   ![chlimage_1-120](assets/aem-externalizer-01.png)
