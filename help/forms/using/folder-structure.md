---
title: Explicación de la estructura de carpetas
seo-title: Understanding the folder structure
description: Cómo comprender la estructura de carpetas del código fuente del espacio de trabajo de AEM Forms que se va a personalizar.
seo-description: How to understand the folder structure of AEM Forms workspace source code to customize.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Explicación de la estructura de carpetas {#understanding-the-folder-structure}

Los componentes del espacio de trabajo de AEM Forms están diseñados sobre la arquitectura MVC mediante la estructura básica. Cada componente tiene un archivo para:

* Modelo, que contiene lógica empresarial.
* Plantilla, es decir, un archivo HTML que contiene controles de interfaz.
* Ver, que actúa como una clase Controlador a Plantilla.

Los recursos de todos los componentes se colocan en la estructura de carpetas que se describe a continuación. Para acceder a los recursos, inicie sesión en el CRXDE Lite y navegue hasta `/libs/ws/js/runtime/`.

**modelos** Contiene modelos de estructura básica.

**vistas** Contiene vistas de la columna vertebral.

**plantillas** Contiene únicamente las plantillas de HTML de los componentes.

**rutas** Contiene rutas universales. La carpeta Templates dentro de las rutas contiene el código del HTML y las referencias a los componentes.

**servicios** Contiene la interfaz de servicio para llamar a las API de servidor de Adobe Experience Manager en el extremo REST.

**util** Contiene utilidades genéricas que se pueden utilizar en varios componentes.
