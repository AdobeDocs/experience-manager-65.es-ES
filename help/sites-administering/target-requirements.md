---
title: Requisitos previos para la integración con Adobe Target
seo-title: Requisitos previos para la integración con Adobe Target
description: Descubra los requisitos previos para la integración con Adobe Target.
seo-description: Descubra los requisitos previos para la integración con Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 3%

---


# Requisitos previos para la integración con Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Como parte de la [integración de AEM y Adobe Target](/help/sites-administering/target.md), debe registrarse con Adobe Target, configurar el agente de replicación y proteger la configuración de actividad en el nodo de publicación.

## Registrarse con Adobe Target {#registering-with-adobe-target}

Para integrar AEM con Adobe Target, debe tener una cuenta de Adobe Target válida. Esta cuenta debe tener **permisos de nivel de aprobador** como mínimo. Cuando se registra en Adobe Target, recibe un código de cliente. Necesita el código de cliente, el nombre de inicio de sesión y la contraseña de Adobe Target para conectarse AEM Adobe Target.

El código de cliente identifica la cuenta de cliente de Adobe Target al llamar al servidor de Adobe Target.

>[!NOTE]
>
>El equipo de Destinatario también debe habilitar su cuenta para poder utilizar la integración.
>
>Si no es el caso, póngase en contacto con [Adobe Customer Care](https://docs.adobe.com/content/help/en/target/using/cmp-resources-and-contact-information.html).

## Habilitación del Agente de replicación de Destinatario {#enabling-the-target-replication-agent}

El agente de replicación Test and Destinatario [](/help/sites-deploying/replication.md) debe estar habilitado en la instancia de creación. Tenga en cuenta que este agente de replicación no está habilitado de forma predeterminada si utilizó el modo de ejecución [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) para instalar AEM. Para obtener más información sobre la seguridad del entorno de producción, consulte la [lista de comprobación de seguridad](/help/sites-administering/security-checklist.md).

1. En la página de inicio AEM, toque o haga clic en **Herramientas** > **Implementación** > **Replicación**.
1. Toque o haga clic en **Agentes en el autor**.
1. Toque o haga clic en el **agente de replicación de prueba y Destinatario (prueba y destinatario)** y, a continuación, toque o haga clic en **Editar**.
1. Seleccione la opción Habilitado y, a continuación, toque o haga clic en **Aceptar**.

   >[!NOTE]
   >
   >Al configurar el agente de replicación de Test and Destinatario, en la ficha **Transport**, el URI se establece de forma predeterminada en **tnt:///**. No reemplace este URI por **https://admin.testandtarget.omniture.com**.
   >
   >Tenga en cuenta que si intenta probar la conexión con **tnt:///**, se producirá un error. Este comportamiento es esperado, ya que este URI es solo para uso interno y no debe usarse con **Conexión de prueba**.

## Seguridad del nodo de configuración de Actividad {#securing-the-activity-settings-node}

Debe proteger el nodo de configuración de actividad **cq:ActivitySettings** en la instancia de publicación para que los usuarios normales no puedan acceder a él. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.

El nodo **cq:ActivitySettings** está disponible en la lista CRXDE en `/content/campaigns/*nameofbrand*`* *en el nodo actividades jcr:content;* *por ejemplo `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Este nodo solo se crea tras el destinatario de un componente.

El nodo **cq:ActivitySettings** situado bajo la actividad jcr:content está protegido por las siguientes ACL:

* Denegar todo para todos
* Permitir jcr:read,rep:write para &quot;destinatario-autores-actividades&quot; (el autor es un miembro de este grupo de forma predeterminada)
* Permitir jcr:read,rep:write para &quot;targetservice&quot;

Esta configuración garantiza que los usuarios normales no tengan acceso a las propiedades del nodo. Utilice las mismas ACL en el autor y en la publicación. Consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md) para obtener más información.

## Configuración del AEM Link Externalizer {#configuring-the-aem-link-externalizer}

Al editar una actividad en Adobe Target, la dirección URL apunta a **localhost** a menos que cambie la dirección URL en el nodo de creación de AEM. Puede configurar el AEM Externalizador de vínculos si desea que el contenido exportado apunte a un dominio *de publicación* específico.

>[!NOTE]
>
>Consulte también [Añadir la configuración de la nube](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Para configurar el AEM externalizador:

>[!NOTE]
>
>Para obtener más información, consulte [Externalización de direcciones URL](/help/sites-developing/externalizer.md).

1. Vaya a la consola web OSGi en **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Busque **Day CQ Link Externalizer** e introduzca el dominio para el nodo de creación.

   ![chlimage_1-120](assets/aem-externalizer-01.png)

