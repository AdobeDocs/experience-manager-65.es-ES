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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Explicación de la estructura de carpetas {#understanding-the-folder-structure}

Los componentes del espacio de trabajo de AEM Forms están diseñados para la arquitectura MVC mediante la red troncal. Cada componente tiene un archivo para:

* Modelo, que contiene lógica empresarial.
* Plantilla, es decir, un archivo HTML que contiene controles de interfaz.
* Ver, que actúa como una clase Controller de Template.

Los recursos de todos los componentes se colocan en la estructura de carpetas que se describe a continuación. Para acceder a los recursos, inicie sesión en CRXDE Lite y busque `/libs/ws/js/runtime/`.

**modelos** Contiene modelos de red troncal.

**vistas** Contiene vistas de red troncal.

**plantillas** Contiene solo las plantillas HTML para los componentes.

**route** Contiene rutas universales. La carpeta Templates dentro de las rutas contiene el código HTML y las referencias a los componentes.

**services** Contiene una interfaz de servicio para llamar a las API de servidor de Adobe Experience Manager en el extremo REST.

**util** Contiene utilidades genéricas utilizables por varios componentes.

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
