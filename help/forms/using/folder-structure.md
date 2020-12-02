---
title: Explicación de la estructura de carpetas
seo-title: Explicación de la estructura de carpetas
description: Cómo comprender la estructura de carpetas del código fuente del espacio de trabajo de AEM Forms que se va a personalizar.
seo-description: Cómo comprender la estructura de carpetas del código fuente del espacio de trabajo de AEM Forms que se va a personalizar.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Explicación de la estructura de carpetas {#understanding-the-folder-structure}

Los componentes del espacio de trabajo de AEM Forms están diseñados para la arquitectura MVC mediante la red troncal. Cada componente tiene un archivo para:

* Modelo, que contiene lógica empresarial.
* Plantilla, es decir, un archivo HTML que contiene controles de interfaz.
* Vista, que actúa como una clase Controller de Template.

Los recursos de todos los componentes se colocan en la estructura de carpetas que se describe a continuación. Para acceder a los recursos, inicie sesión en CRXDE Lite y vaya a `/libs/ws/js/runtime/`.

**** modelosContiene modelos de red troncal.

**** viewsContiene vistas de red troncal.

**** templatesContiene solamente las plantillas HTML para los componentes.

**** routeContiene rutas universales. La carpeta Templates dentro de las rutas contiene el código HTML y las referencias a los componentes.

**** servicesContiene una interfaz de servicio para llamar a las API de servidor de Adobe Experience Manager en el extremo REST.

**** utilContiene utilidades genéricas utilizables por varios componentes.
