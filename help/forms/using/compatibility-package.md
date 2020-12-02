---
title: Paquete de compatibilidad
seo-title: Paquete de compatibilidad
description: La instalación del paquete de compatibilidad en AEM Forms 6.5 le permite utilizar los recursos de gestión de correspondencia de AEM Forms 6.4 y versiones anteriores, así como las páginas y plantillas de formularios adaptables obsoletos
seo-description: La instalación del paquete de compatibilidad en AEM Forms 6.4 le permite utilizar los recursos de gestión de correspondencia de AEM Forms 6.4 y las páginas y plantillas de formularios adaptables obsoletos
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 6%

---


# Paquete de compatibilidad{#compatibility-package}

## Información general {#overview}

La comunicación interactiva es el método predeterminado y recomendado para crear comunicaciones con clientes en AEM Forms 6.5. Para continuar utilizando letras en AEM Forms 6.5, debe instalar el paquete de compatibilidad [AEMFD más reciente](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).

El paquete de compatibilidad con AEMFD también le permite [utilizar los siguientes recursos de AEM Forms 6.4, 6.3 y 6.2 en AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragmentos de documento
* Cartas
* Diccionarios de datos
* Plantillas y páginas obsoletas de formularios adaptables

Para obtener más información, consulte [Recursos compatibles con AEM Forms 6.5 mediante la instalación del paquete de compatibilidad](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Añada la compatibilidad con los recursos de AEM Forms 6.4, 6.3 y 6.2 en AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Después de realizar una actualización, haga lo siguiente para instalar el paquete de compatibilidad con AEMFD y hacer que sus recursos sean compatibles con 6.5:

Asegúrese de tener [AEM paquete de compatibilidad](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) preinstalado.

1. Instale el paquete de compatibilidad más reciente de 6.5 [](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   Para obtener más información sobre cómo cargar e instalar el paquete, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).

1. Después de estabilizar los registros, reinicie el servidor.
1. Utilice la utilidad de migración para hacer que los recursos sean compatibles con 6.5.

   Para obtener más información, consulte [utilidad de migración](../../forms/using/migration-utility.md).

## Recursos compatibles con AEM Forms 6.5 mediante la instalación del paquete de compatibilidad {#assetsmadecompatible}

Al instalar el paquete Compatibilidad, puede hacer que los siguientes recursos y plantillas sean compatibles con AEM Forms 6.5:

* Recursos de gestión de correspondencia de AEM 6.4 y anteriores:

   * [Cartas](../../forms/using/create-letter.md)
   * [Diccionarios de datos](/help/forms/using/data-dictionary.md)
   * Fragmentos de documento

* Plantillas de formularios adaptables obsoletas:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnregistrationTemplate
   * /libs/fd/af/templates/simpleEnregistrationTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnregistrationTemplate
   * /libs/fd/af/templates/tabbedEnregistrationTemplate2
   * /libs/fd/afaddon/templates/advancedEnregistrationTemplate
   * /libs/fd/afaddon/templates/advancedEnregistrationTemplate2

* Páginas en desuso de formularios adaptables:

   * /libs/fd/af/components/page/encuesta
   * /libs/fd/af/components/page/tabbedenregistration
   * /libs/fd/afaddon/components/page/Advancedenregistration

