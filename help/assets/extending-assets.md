---
title: Personalizar y ampliar [!DNL Assets]
description: Conozca las formas en que puede personalizar y ampliar Asset Share y Asset Editor, que presentan a los usuarios una interfaz y un conjunto de funciones específicos.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Personalizar y ampliar [!DNL Assets] {#customizing-and-extending-assets}

El Editor de recursos es el punto de acceso principal que los usuarios de un sitio web de Enterprise Manager de Adobe utilizarán para encontrar, ver y manipular los recursos digitales de su repositorio.

Como [!DNL Experience Manager] desarrollador, puede personalizar y ampliar el Editor de recursos de varias formas, ofreciendo a los usuarios una interfaz y un conjunto de funciones específicos.

Se pueden personalizar o mejorar los siguientes aspectos de la funcionalidad:

* [Ampliar editor de recursos](asseteditorx.md)
* [Ampliar búsqueda de recursos](searchx.md)
* [Procesamiento de recursos con controladores de medios y flujos de trabajo](media-handlers.md)
* [Integración de recursos con el flujo de actividad](extending-activity-stream.md)
* [Desarrollo de proxy de recursos](proxy.md)
* [Prácticas recomendadas para configurar ImageMagick](best-practices-for-imagemagick.md)

## Personalizar el aspecto {#customizing-the-look-and-feel}

Los siguientes aspectos del aspecto del Editor de recursos se pueden personalizar:

* Logotipo: Puede añadir el logotipo de su propia organización a la interfaz.
* Colores y fuentes: Puede cambiar los colores y las fuentes utilizados en la interfaz.
* Código de HTML: Para una personalización más completa, puede cambiar el código de HTML subyacente que define las interfaces.

## Personalizar representaciones {#customizing-renditions}

En [!DNL Experience Manager Assets] terminología: una representación es la forma en que se presenta un recurso. En general, un recurso concreto puede tener varias representaciones. Por ejemplo, la imagen de color completo puede tener una representación en su tamaño original, otra en un tamaño reducido y otra que se reduzca y se convierta a escala de grises.

Las representaciones en las que está disponible un recurso en particular se pueden personalizar y crear nuevas representaciones.
