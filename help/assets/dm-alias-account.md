---
title: Configurar una cuenta de alias de empresa de Dynamic Media
description: Obtenga información sobre cómo configurar una cuenta de alias de empresa en Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# Acerca de la configuración de una cuenta de alias de empresa de Dynamic Media {#about-dm-alias-acct}

Las direcciones URL de Dynamic Media y el código incrustado del visor contienen el nombre de cuenta de la empresa. Este nombre de cuenta se creó en el momento del aprovisionamiento de Dynamic Media. Puede haber escenarios en los que su empresa haya pasado por una adquisición o un cambio de marca, o simplemente desee utilizar un nombre más memorable. En estos casos, no es fácil actualizar manualmente el nombre de la cuenta de la empresa en todas las direcciones URL y el código incrustado del visor que salen de la caja. Además, existe la posibilidad de que afecte al repositorio de Dynamic Media existente o al contenido en directo. Para resolver este problema, puede configurar una cuenta de alias de empresa de Dynamic Media.

Una cuenta de alias de empresa de Dynamic Media garantiza que todas las direcciones URL de Dynamic Media y el código incrustado del visor integrados en la interfaz de usuario reflejen cualquier actualización realizada en su contexto empresarial, como el cambio de marca. Una cuenta de alias también tiene un impacto positivo en su SEO (Optimización de motores de búsqueda) porque las URL de Dynamic Media y el código incrustado del visor reflejan el nuevo nombre de cuenta de la empresa.

Al configurar una cuenta de alias de empresa de Dynamic Media, tenga en cuenta lo siguiente:

* Cualquier URL de Dynamic Media existente o código incrustado del visor en su *live* las propiedades digitales deben actualizarse manualmente para reflejar el nuevo nombre de alias. Sin embargo, las direcciones URL o los visores incrustan código con el nombre de empresa original de Dynamic Media siguen funcionando para los recursos existentes o nuevos.
* La capacidad de cuenta de alias de la empresa de Dynamic Media se limita al modo y la entrega de creación de Experience Manager Assets. El nombre de alias de la empresa no funciona con Experience Manager Sites. Los componentes WCM (Web Content Management) no se actualizan para este cambio. Estos componentes siguen funcionando con el nombre de empresa original de Dynamic Media para recuperar recursos de Dynamic Media.
* Solo puede configurar una cuenta de alias de compañía en la variable **[!UICONTROL Editar configuración de Dynamic Media]** página. Sin embargo, puede crear tantas cuentas de alias de empresa como desee mediante un caso de compatibilidad y reflejar manualmente el nombre de alias necesario en las direcciones URL de Dynamic Media o en el código incrustado del visor.
* La solución predeterminada [Invalidación de caché](/help/assets/invalidate-cdn-cache-dynamic-media.md) Dynamic Media invalida las direcciones URL con cuentas de alias de empresa y de empresa configuradas en la página Configuración de Dynamic Media en Cloud Services.
* Al configurar una cuenta de alias de empresa en la variable **[!UICONTROL Editar configuración de Dynamic Media]** para que la invalidación de la caché se realice correctamente, debe invalidar las direcciones URL de *both* el **[!UICONTROL Empresa]** y **[!UICONTROL Alias de empresa]** cuenta, simultáneamente.

Consulte también [Crear una configuración de Dynamic Media en Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configurar una cuenta con alias de empresa de Dynamic Media {#configure-dm-alias-account}

Comience a configurar una cuenta de alias de empresa de Dynamic Media enviando primero un caso de asistencia. Este paso es necesario.

1. [Utilice el Admin Console para crear un caso de asistencia](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. Proporcione la siguiente información en su caso de asistencia:

   * El nombre de alias de empresa de Dynamic Media que desea usar. El nombre debe contener *only* letras (se permiten mayúsculas y minúsculas), números, guiones y guiones bajos.
   * Su región.
   * Si alguna [conjuntos de reglas](/help/assets/using-rulesets-to-transform-urls.md) se están utilizando anteriormente para lograr la entrega de contenido de Dynamic Media mediante un nombre de cuenta de empresa alternativo de Dynamic Media.

1. Una vez creada la cuenta de alias de Dynamic Media por la asistencia, en la instancia de Autor as a Cloud Service de Experience Manager, seleccione el logotipo as a Cloud Service de Experience Manager para acceder a la consola de navegación global.
1. En la parte izquierda de la consola, seleccione el icono Herramientas y vaya a **[!UICONTROL Cloud Services > Configuración de Dynamic Media]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]** (no seleccione el icono de carpeta a la izquierda de **[!UICONTROL global]**). A continuación, seleccione **[!UICONTROL Editar]**.

   ![Campo de texto Alias de empresa de Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. En el **[!UICONTROL Editar configuración de Dynamic Media]** en la **[!UICONTROL Alias de empresa]** campo de texto, escriba el nombre de cuenta de alias de Dynamic Media que especificó anteriormente en su caso de soporte.
1. En la parte superior derecha de la página, seleccione **[!UICONTROL Guardar]**.
La cuenta de alias de la empresa de Dynamic Media ahora se guarda y se activa; ahora, todas las direcciones URL y el código incrustado del visor para recursos nuevos y existentes reflejan el nuevo nombre de alias de la empresa.
