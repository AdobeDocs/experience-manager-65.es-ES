---
title: Creación de plantillas de página AEM personalizadas con componentes de formulario de Adobe Campaign
seo-title: Creating Custom AEM Page Template with Adobe Campaign Form Components
description: Cree una plantilla de página personalizada que use componentes de Adobe Campaign Form
seo-description: Build a custom page template that uses Adobe Campaign Form components
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 3%

---

# Creación de plantillas de página AEM personalizadas con componentes de formulario de Adobe Campaign{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

Esta página explica cómo crear una plantilla de página personalizada que use [Formulario de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) componentes examinando la plantilla de Geometrixx exterior ( `/apps/geometrixx-outdoors/components/page_campaign_profile`) está implementada y señala a la información importante que puede necesitar al crear su propia plantilla personalizada.

>[!NOTE]
>
>[Los ejemplos de correo electrónico y formulario solo están disponibles en Geometrixx](/help/sites-developing/we-retail.md). Descargue el contenido de ejemplo de Geometrixx de Uso compartido de paquetes.

Para crear una plantilla de página de AEM personalizada con los componentes de formulario de Adobe Campaign, asegúrese de que tiene lo siguiente:

1. **Correcto resourceSuperType**

   Asegúrese de que el componente de página se hereda de `mcm/campaign/components/profile`.

   Esto es necesario para que los servlets obtengan y guarden información

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Configuración de ClientContext**

   Cuando observe la configuración de clientcontext ( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`) puede ver los siguientes ajustes:

   * El ClientContext señala a `/etc/clientcontext/campaign`
   * También hay que pagar un suplemento *config* nodo .

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   En **head.jsp**, verá las siguientes líneas que utilizan la variable **clientcontext-config** y **cloudservice-lock**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   En **body.jsp**, los servicios de nube se cargan en la parte inferior de la página:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Propiedades de la página de Campaign**

   Para poder seleccionar una plantilla de Adobe Campaign, las propiedades de página se amplían con la variable **Campaign** pestaña:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Configuración de plantilla**.

   En la plantilla ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`), verá los siguientes valores predeterminados:

   | **acMapping** | mapRecipient (para Adobe Campaign 6.1), profile (para Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | correo |

   ![chlimage_1-204](assets/chlimage_1-204.png)
