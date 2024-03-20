---
title: AEM Creación de plantillas de página de personalizadas con componentes de formulario de Adobe Campaign
description: Crear una plantilla de página personalizada que utilice componentes de formularios Adobe Campaign Forms
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# AEM Creación de plantillas de página de personalizadas con componentes de formulario de Adobe Campaign{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

En esta página se explica cómo crear una plantilla de página personalizada que utilice [Formulario de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) componentes de examinando cómo funciona la plantilla de Geometrixx-outdoors ( `/apps/geometrixx-outdoors/components/page_campaign_profile`) está implementado y le dirige a la información importante que puede necesitar al crear su propia plantilla personalizada.

>[!NOTE]
>
>[Los ejemplos de correo electrónico y formularios solo están disponibles en Geometrixx](/help/sites-developing/we-retail.md). Descargar contenido de Geometrixx de muestra desde Package Share.

AEM Para crear una plantilla de página de personalizada con componentes de formulario de Adobe Campaign, asegúrese de que dispone de lo siguiente:

1. **ResourceSuperType correcto**

   Asegúrese de que el componente de página herede de `mcm/campaign/components/profile`.

   Esto es necesario para que los servlets obtengan y guarden información

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Configuración de ClientContext**

   Cuando observa la configuración de clientcontext ( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`) verá la siguiente configuración:

   * El ClientContext apunta a `/etc/clientcontext/campaign`
   * También hay un suplemento *config* nodo.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   Entrada **head.jsp**, verá las siguientes líneas que utilizan la variable **clientcontext-config** y el **cloudservice-hook**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   Entrada **body.jsp**, los servicios en la nube se cargan en la parte inferior de la página:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Propiedades de página de Campaign**

   Para poder seleccionar una plantilla de Adobe Campaign, las propiedades de página se amplían con la variable **Campaign** pestaña:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Configuración de plantilla**.

   En la plantilla ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) verá los siguientes valores predeterminados:

   | **acMapping** | mapRecipient (para Adobe Campaign 6.1), profile (para Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | correo |

   ![chlimage_1-204](assets/chlimage_1-204.png)
