---
title: Aspectos básicos de la configuración de formularios
description: Obtenga información sobre los distintos servicios de Forms que le ayudan a crear aplicaciones de captura de datos interactivas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 4%

---

# Aspectos básicos de la configuración de formularios {#basics-of-configuring-forms}

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y envían formularios normalmente creados en Designer. Los autores de formularios desarrollan un único diseño de formulario que el servicio Forms procesa en varios formatos:

* como PDF en Adobe Reader o en un explorador
* como HTML en varios entornos de explorador, incluido un procesamiento XHTML 1.0 compatible
* como guías de formulario en varios entornos de explorador que admiten el Flash Player de Adobe.

Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

Con la página Forms de la consola de administración, puede configurar el comportamiento del servicio de Forms. Esta configuración se aplica a todas las invocaciones del servicio. AEM Cualquier parámetro enviado a través del SDK de formularios de la anula la configuración establecida en la consola de administración; sin embargo, solo afecta a esa invocación en particular.

Después de cambiar la configuración de Forms en la consola de administración, haga clic en Guardar. No es necesario reiniciar el servidor para que los cambios surtan efecto. Sin embargo, es posible que tenga que detener y reiniciar el servicio de Forms al configurar el modo de caché. (Consulte [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
