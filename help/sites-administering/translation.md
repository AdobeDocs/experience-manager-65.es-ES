---
title: Traducción de contenido para sitios multilingües
seo-title: Traducción de contenido para sitios multilingües
description: Aprenda a traducir contenido para sitios multilingües.
seo-description: Aprenda a traducir contenido para sitios multilingües.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: Copiar idioma
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# Traducción de contenido para sitios multilingües {#translating-content-for-multilingual-sites}

Automatice la traducción del contenido de la página, los recursos y el contenido generado por el usuario para crear y mantener sitios web multilingües. Para automatizar los flujos de trabajo de traducción, se integran los proveedores de servicios de traducción con AEM y se crean proyectos para traducir contenido a varios idiomas. AEM admite flujos de trabajo de traducción automática y humana.

* Traducción humana: El contenido se envía a su proveedor de traducción y lo traducen traductores profesionales. Cuando se completa, el contenido traducido se devuelve e importa en AEM. Cuando el proveedor de traducción está integrado con AEM, el contenido se envía automáticamente entre AEM y el proveedor de traducción.
* Traducción automática: El servicio de traducción automática traduce inmediatamente su contenido.

La traducción de contenido implica los siguientes pasos:

1. [Conecte AEM con su ](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) proveedor de servicios de traducción y  [cree configuraciones](/help/sites-administering/tc-tic.md) del marco de integración de traducción.
1. [Asocie las páginas del ](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) maestro de idioma con el servicio de traducción y las configuraciones del marco.
1. [Identifique el tipo de ](/help/sites-administering/tc-rules.md) contenido que desea traducir.
1. [Prepare el contenido para la ](/help/sites-administering/tc-prep.md) traducción creando el maestro de idioma y las páginas raíz de las copias de idioma.
1. [Cree ](/help/sites-administering/tc-manage.md) proyectos de traducción para recopilar el contenido que desea traducir y preparar el proceso de traducción.
1. Utilice los proyectos de traducción para [administrar el proceso de traducción de contenido](/help/sites-administering/tc-manage.md).

Si el proveedor de servicios de traducción no proporciona un conector para la integración con AEM, AEM admite la extracción manual y la reinserción del contenido de traducción en formato XML.

>[!NOTE]
>
>El usuario debe ser miembro del grupo de administradores de proyectos para utilizar las funciones de copia de idioma.

## Prácticas recomendadas   {#best-practices}

La página [Prácticas recomendadas de traducción](/help/sites-administering/tc-bp.md) contiene información importante sobre la implementación.
