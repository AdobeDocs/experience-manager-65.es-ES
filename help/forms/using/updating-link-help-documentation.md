---
title: Actualización del vínculo a la documentación
seo-title: Actualización del vínculo a la documentación
description: Actualización del destino del vínculo Ayuda de Workspace en el espacio de trabajo de AEM Forms para que apunte al vínculo de documentación personalizada.
seo-description: Actualización del destino del vínculo Ayuda de Workspace en el espacio de trabajo de AEM Forms para que apunte al vínculo de documentación personalizada.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 3%

---


# Actualización del vínculo a la documentación {#updating-the-link-to-the-documentation}

Puede acceder al contenido de ayuda predeterminado del espacio de trabajo de AEM Forms seleccionando **Ayuda > Ayuda del espacio de trabajo**. Señala la documentación en línea en el sitio web de Adobe. Sin embargo, puede actualizarla para que apunte a cualquier otra dirección URL.

Considere los siguientes casos de uso en los que puede que desee cambiar la dirección URL de ayuda predeterminada:

* Para proporcionar ayuda localizada en un idioma de su elección.
* Para proporcionar contenido de ayuda personalizado para su espacio de trabajo personalizado.

Para actualizar la dirección URL de la documentación en línea, siga los [Pasos genéricos de personalización](/help/forms/using/generic-steps-html-workspace-customization.md) y luego los pasos siguientes.

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

   1. Abra /apps/ws/js/registry.js para editar.
   1. Busque y reemplace `text!/lc/libs/ws/js/runtime/templates/userinfo.html` por `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
