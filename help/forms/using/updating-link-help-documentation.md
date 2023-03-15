---
title: Actualizar el vínculo a la documentación
seo-title: Updating the link to the documentation
description: Actualizar el destino del vínculo de ayuda del espacio de trabajo en el espacio de AEM Forms para que señale al vínculo de documentación personalizado.
seo-description: How-to update the destination of Workspace Help link in AEM Forms workspace to point to your custom documentation link.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 100%

---

# Actualizar el vínculo a la documentación {#updating-the-link-to-the-documentation}

Puede acceder al contenido de ayuda predeterminado de AEM Forms Workspace al seleccionar **Ayuda > Ayuda del espacio de trabajo**. Señala a la documentación en línea del sitio web de Adobe. Sin embargo, puede actualizarlo para que señale cualquier otra dirección URL.

Tenga en cuenta los siguientes casos de uso en los que puede que desee cambiar la dirección URL de ayuda predeterminada:

* Para proporcionar ayuda localizada en un idioma de su elección.
* Para ofrecer contenido de ayuda personalizado para su espacio de trabajo personalizado.

Para actualizar la URL de la documentación en línea, siga los [Pasos genéricos de personalización](/help/forms/using/generic-steps-html-workspace-customization.md) y luego los siguientes pasos.

1. Copie el archivo `userinfo.html` de `/libs/ws/js/runtime/templates` a `/apps/ws/js/runtime/templates`.
1. Cambiar:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   hasta

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Haga lo siguiente:

   1. Abra /apps/ws/js/registry.js para editarlo.
   1. Busque y reemplace `text!/lc/libs/ws/js/runtime/templates/userinfo.html` con `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
