---
title: Explicación de la estructura de carpetas
description: Obtenga más información sobre la estructura de carpetas del código fuente de AEM Forms Workspace que se va a personalizar.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 100%

---

# Explicación de la estructura de carpetas {#understanding-the-folder-structure}

Los componentes de AEM Forms Workspace han sido diseñados sobre arquitectura MVC mediante Backbone. Cada componente tiene un archivo para:

* El modelo, que contiene lógica empresarial.
* La plantilla, es decir, un archivo HTML que contiene controles de interfaz.
* La vista, que actúa como una clase de controlador para la plantilla.

Los archivos de todos los componentes se colocan en la estructura de carpetas que se describe a continuación. Para acceder a los archivos, inicie sesión en CRXDE Lite y desplácese hasta `/libs/ws/js/runtime/`.

**models** Contiene modelos de Backbone.

**views** Contiene vistas de Backbone.

**templates** Contiene únicamente las plantillas HTML de los componentes.

**routes** Contiene rutas universales. La carpeta templates dentro de routes contiene el código HTML y las referencias a los componentes.

**services** Contiene la interfaz de servicio para llamar a las API del servidor de Adobe Experience Manager en el extremo REST.

**util** Contiene utilidades genéricas que se pueden utilizar en varios componentes.
