---
title: Requisitos previos para la integración con Adobe Target
seo-title: Prerequisites for Integrating with Adobe Target
description: Descubra los requisitos previos para la integración con Adobe Target.
seo-description: Find out about the prerequisites for integrating with Adobe Target.
uuid: 55d87a96-5fe7-4f7e-93c1-fdf7fbb7c971
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ae4a6e97-c0d7-472d-a25f-b89b1abf4df3
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 8%

---

# Requisitos previos para la integración con Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Como parte de [AEM integración de los entornos de y Adobe Target](/help/sites-administering/target.md), debe registrarse en Adobe Target, configurar el agente de replicación y asegurar la configuración de actividad en el nodo de publicación.

## Registro en Adobe Target {#registering-with-adobe-target}

AEM Para integrarse con Adobe Target, debe tener una cuenta de Adobe Target válida. Esta cuenta debe tener **aprobador** permisos de nivel como mínimo. Al registrarse en Adobe Target, recibirá un código de cliente. Necesita el código de cliente, el nombre de inicio de sesión de Adobe Target AEM y la contraseña para conectarse de forma directa a la interfaz de usuario de Adobe Target.

El código de cliente identifica la cuenta de cliente de Adobe Target al llamar al servidor de Adobe Target.

>[!NOTE]
>
>El equipo de Target también debe habilitar su cuenta para utilizar la integración.
>
>Si no es el caso, póngase en contacto con [Adobe del Servicio de atención al cliente](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## Activación del agente de replicación de destino {#enabling-the-target-replication-agent}

Prueba y destino [agente de replicación](/help/sites-deploying/replication.md) debe estar habilitado en la instancia de autor. Tenga en cuenta que este agente de replicación no está habilitado de forma predeterminada si ha utilizado el [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) AEM modo de ejecución para la instalación de la. Para obtener más información sobre la seguridad del entorno de producción, consulte la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md).

1. AEM En la página de inicio de la, toque o haga clic en **Herramientas** > **Implementación** > **Replicación**.
1. Haga clic o toque **Agentes en el autor**.
1. Toque o haga clic en **Prueba y destino (prueba y destino)** agente de replicación y toque o haga clic en **Editar**.
1. Seleccione la opción Habilitado y, a continuación, toque o haga clic en **OK**.

   >[!NOTE]
   >
   >Cuando configure el agente de replicación de Test and Target, en la variable **Transporte** , el URI se establece de forma predeterminada en **tnt:///**. No reemplace este URI por **https://admin.testandtarget.omniture.com**.
   >
   >Tenga en cuenta que si intenta probar la conexión con **tnt:///**, se generará un error. Este es el comportamiento esperado, ya que este URI es solo para uso interno y no debe usarse con **Probar conexión**.

## Protección del nodo de configuración de actividad {#securing-the-activity-settings-node}

Debe asegurar el nodo de configuración de actividades **cq:ActivitySettings** de la instancia de publicación, para que los usuarios normales no puedan obtener acceso a él. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.

El **cq:ActivitySettings** El nodo está disponible en CRXDE lite en `/content/campaigns/*nameofbrand*`* *en el nodo activities jcr:content;* *por ejemplo `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Este nodo solo se crea después de establecer como objetivo un componente.

El **cq:ActivitySettings** bajo el jcr:content de la actividad está protegido por las siguientes ACL:

* Denegar todo para todos
* Permitir jcr:read, rep:write para &quot;target-activity-authors&quot; (el autor es miembro de este grupo de forma predeterminada)
* Permitir jcr:read, rep:write para &quot;targetservice&quot;

Esta configuración garantiza que los usuarios normales no tengan acceso a las propiedades del nodo. Utilice las mismas ACL en autor y en publicación. Consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md) para obtener más información.

## AEM Configuración del externalizador de vínculos de la {#configuring-the-aem-link-externalizer}

Al editar una actividad en Adobe Target, la URL apunta a **localhost** AEM a menos que cambie la dirección URL en el nodo de autor de la. AEM Puede configurar el Externalizador de vínculos de si desea que el contenido exportado apunte a un elemento específico *publicar* dominio.

>[!NOTE]
>
>Consulte también [Añadir la configuración de nube](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

AEM Para configurar el externalizador de:

>[!NOTE]
>
>Para obtener más información, consulte [Externalización de direcciones URL](/help/sites-developing/externalizer.md).

1. Vaya a la consola web de OSGi en **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Buscar **Externalizador de vínculos CQ de día** e introduzca el dominio del nodo de creación.

   ![Externalizador de vínculos CQ de día](assets/aem-externalizer-01.png)
