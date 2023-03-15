---
title: Aspectos básicos de la configuración de formularios
seo-title: Basics of configuring forms
description: Obtenga información sobre los distintos servicios de Forms que le ayudan a crear aplicaciones de captura de datos interactivas.
seo-description: Learn about the various forms services that help you create interactive data capture applications.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 3%

---

# Aspectos básicos de la configuración de formularios {#basics-of-configuring-forms}

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y envían formularios normalmente creados en Designer. Los autores de formularios desarrollan un único diseño de formulario que el servicio Forms procesa en varios formatos:

* como PDF en Adobe Reader o en un explorador
* como HTML en varios entornos de explorador, incluido un procesamiento XHTML 1.0 compatible
* como guías de formulario en varios entornos de explorador que admiten el Flash Player de Adobe.

Para obtener más información sobre el servicio Forms, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

Con la página Forms de la consola de administración, puede configurar el comportamiento del servicio de Forms. Esta configuración se aplica a todas las invocaciones del servicio. AEM Cualquier parámetro enviado a través del SDK de formularios de la anula la configuración establecida en la consola de administración; sin embargo, solo afecta a esa invocación en particular.

Después de cambiar la configuración de Forms en la consola de administración, haga clic en Guardar. No es necesario reiniciar el servidor para que los cambios surtan efecto. Sin embargo, es posible que tenga que detener y reiniciar el servicio de Forms al configurar el modo de caché. (Consulte [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
