---
title: Personalizar y ampliar [!DNL Assets]
description: Conozca las formas en que puede personalizar y ampliar Asset Share y el Editor de recursos, que presenta a los usuarios una interfaz y un conjunto de funcionalidades específicamente adaptados.
contentOwner: AG
role: Developer
feature: Developer Tools
exl-id: 0271c528-23b0-4a3a-b5e8-5baf6cdeecc7
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Personalizar y ampliar [!DNL Assets] {#customizing-and-extending-assets}

El editor de recursos es el principal punto de acceso que los usuarios de un sitio web de Enterprise Manager de Adobe utilizan para buscar, ver y manipular los recursos digitales del repositorio.

Como un [!DNL Experience Manager] Para los desarrolladores, puede personalizar y ampliar el editor de recursos de varias formas, lo que presenta a los usuarios una interfaz y un conjunto de funcionalidades específicamente adaptados.

Los siguientes aspectos de la funcionalidad se pueden personalizar o mejorar:

* [Ampliar editor de recursos](asseteditorx.md)
* [Ampliar búsqueda de recursos](searchx.md)
* [Procesar recursos mediante controladores de medios y flujos de trabajo](media-handlers.md)
* [Integración de Assets con el flujo de actividad](extending-activity-stream.md)
* [Desarrollo de proxy de activos](proxy.md)
* [Prácticas recomendadas para configurar ImageMagick](best-practices-for-imagemagick.md)

## Personalizar la apariencia {#customizing-the-look-and-feel}

Los siguientes aspectos de la apariencia del editor de recursos son personalizables:

* Logotipo: puede agregar el logotipo de su propia organización a la interfaz.
* Colores y fuentes: puede cambiar los colores y las fuentes utilizados en la interfaz.
* Código de HTML: para una personalización más detallada, puede cambiar el código de HTML subyacente que define las interfaces.

## Personalizar representaciones {#customizing-renditions}

Entrada [!DNL Experience Manager Assets] terminología una representación es la forma en que se presenta un recurso. En general, un recurso concreto puede tener varias representaciones. Por ejemplo, una imagen a todo color puede tener una representación en su tamaño original, otra en tamaño reducido y otra en escala de grises.

Las representaciones en las que está disponible un recurso concreto se pueden personalizar y se pueden crear nuevas representaciones.
