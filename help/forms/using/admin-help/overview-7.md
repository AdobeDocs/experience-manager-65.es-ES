---
title: Fundamentos de la configuración de formularios
seo-title: Fundamentos de la configuración de formularios
description: Obtenga información sobre los distintos servicios de formularios que le ayudan a crear aplicaciones interactivas de captura de datos.
seo-description: Obtenga información sobre los distintos servicios de formularios que le ayudan a crear aplicaciones interactivas de captura de datos.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Fundamentos de la configuración de formularios {#basics-of-configuring-forms}

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y entregan formularios creados normalmente en Designer. Los creadores de formularios desarrollan un único diseño de formulario que el servicio de Forms procesa en varios formatos:

* como PDF en Adobe Reader o en un navegador
* como HTML en varios entornos del navegador, incluida una representación XHTML 1.0 compatible
* como guías de formulario en varios entornos de explorador que admiten el Flash Player de Adobe.

Para obtener información adicional sobre el servicio Forms, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

Mediante la página Forms de la consola de administración, puede configurar el comportamiento del servicio Forms. Esta configuración se aplica a todas las invocaciones del servicio. Los parámetros enviados a través del SDK de formularios AEM anulan la configuración establecida en la consola de administración; sin embargo, sólo afectan a esa invocación en particular.

Después de cambiar la configuración de Forms en la consola de administración, haga clic en Guardar. No es necesario reiniciar el servidor para que los cambios surtan efecto. Sin embargo, es posible que tenga que detener y reiniciar el servicio Forms al configurar los ajustes del modo de caché. (Consulte [Inicio y parada de servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
