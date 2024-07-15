---
title: Configuración de una cuenta de alias de empresa de Dynamic Media
description: Obtenga información sobre cómo configurar una cuenta de alias de compañía en Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# Acerca de la configuración de una cuenta de alias de empresa de Dynamic Media {#about-dm-alias-acct}

Las direcciones URL de Dynamic Media y el código de incrustación de visor contienen el nombre de cuenta de la empresa. Este nombre de cuenta se creó en el momento del aprovisionamiento de Dynamic Media. Puede haber casos en los que su empresa haya sufrido una adquisición o un cambio de marca, o simplemente desee utilizar un nombre más memorable. En estos casos, no es fácil actualizar manualmente el nombre de la cuenta de su empresa en todas las direcciones URL y el código incrustado de visor que aparece de forma predeterminada. Además, existe la posibilidad de que afecte a su repositorio de Dynamic Media existente o al contenido en directo. Para resolver este problema, puede configurar una cuenta de alias de compañía de Dynamic Media.

Una cuenta de alias de empresa de Dynamic Media garantiza que todas las URL de Dynamic Media y el código incrustado de visualizador integrados en la interfaz de usuario reflejen cualquier actualización realizada en el contexto empresarial, como el cambio de marca. Una cuenta de alias también tiene un impacto positivo en el SEO (optimización del motor de búsqueda), ya que las direcciones URL de Dynamic Media y el código de incrustación de visor reflejan el nuevo nombre de cuenta de la empresa.

Cuando configure una cuenta de alias de compañía de Dynamic Media, tenga en cuenta lo siguiente:

* Cualquier URL de Dynamic Media existente o código incrustado de visor en las propiedades digitales de *live* debe actualizarse manualmente para reflejar el nuevo nombre de alias. Sin embargo, cualquier URL o código incrustado de visualizador con el nombre original de la empresa de Dynamic Media seguirá funcionando para los recursos existentes o nuevos.
* La capacidad de la cuenta de alias de empresa de Dynamic Media se limita al modo de creación y envío de Experience Manager Assets. El nombre del alias de la empresa no funciona con Experience Manager Sites. Los componentes WCM (Web Content Management) no se actualizan para este cambio. Estos componentes siguen funcionando con el nombre de empresa original de Dynamic Media para recuperar los recursos de Dynamic Media.
* Solo puede configurar una cuenta de alias de compañía en la página **[!UICONTROL Editar configuración de Dynamic Media]**. Sin embargo, se pueden crear tantas cuentas de alias de compañía como sea necesario mediante un caso de soporte y reflejar manualmente el nombre de alias necesario en las URL de Dynamic Media o en el código de incrustación de visualizador.
* La funcionalidad predeterminada [Invalidación de caché](/help/assets/invalidate-cdn-cache-dynamic-media.md) de Dynamic Media invalida las direcciones URL con las cuentas de alias de compañía y compañía configuradas en la página Configuración de Dynamic Media en Cloud Service.
* Al configurar una cuenta de alias de compañía en la página **[!UICONTROL Editar configuración de Dynamic Media]**, para que la invalidación de la caché se realice correctamente, debe invalidar las direcciones URL de *tanto* como de la cuenta de **[!UICONTROL Compañía]** y la cuenta de **[!UICONTROL Alias de compañía]** simultáneamente.

Consulte también [Crear una configuración de Dynamic Media en Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configuración de una cuenta de alias de empresa de Dynamic Media {#configure-dm-alias-account}

Para configurar una cuenta de alias de empresa de Dynamic Media, primero debe enviar un caso de asistencia. Este paso es obligatorio.

1. [Use el Admin Console para crear un caso de soporte](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).
1. Proporcione la siguiente información en su caso de asistencia:

   * El nombre de alias de empresa de Dynamic Media que desea utilizar. El nombre debe contener *solamente* letras (se permiten mayúsculas y minúsculas), números, guiones y guiones bajos.
   * Su región.
   * Si se están usando [conjuntos de reglas](/help/assets/using-rulesets-to-transform-urls.md) anteriormente para lograr entregar contenido de Dynamic Media a través de un nombre de cuenta de compañía de Dynamic Media alternativo.

1. Una vez que la asistencia técnica haya creado la cuenta de alias de Dynamic Media, en la instancia de autor as a Cloud Service de Experience Manager, seleccione el logotipo as a Cloud Service de Experience Manager para acceder a la consola de navegación global.
1. A la izquierda de la consola, selecciona el ícono Herramientas y luego ve a **[!UICONTROL Cloud Service > Configuración de Dynamic Media]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]** (no seleccione el icono de carpeta a la izquierda de **[!UICONTROL global]**). Luego selecciona **[!UICONTROL Editar]**.

   ![Campo de texto Alias de compañía de Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. En la página **[!UICONTROL Editar configuración de Dynamic Media]**, en el campo de texto **[!UICONTROL Alias de la compañía]**, escriba el nombre de la cuenta de alias de Dynamic Media que especificó en su caso de soporte técnico anteriormente.
1. En la parte superior derecha de la página, selecciona **[!UICONTROL Guardar]**.
La cuenta de alias de compañía de Dynamic Media ahora está guardada y habilitada; todas las URL y el código incrustado de visualizador de recursos existentes y nuevos ahora reflejan el nuevo nombre de alias de compañía.
