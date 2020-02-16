---
title: Personalización y ampliación de Recursos AEM
description: Conozca las formas en que puede personalizar y ampliar el uso compartido de recursos y el editor de recursos, que ofrece a los usuarios una interfaz y un conjunto de funciones específicos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Personalización y ampliación de recursos {#customizing-and-extending-assets}

El editor de recursos es el principal punto de acceso que los usuarios de un sitio web de Adobe Enterprise Manager (AEM) utilizarán para buscar, ver y manipular los recursos digitales de su repositorio.

Como desarrollador de AEM, puede personalizar y ampliar el Editor de recursos de varias formas, ofreciendo a los usuarios una interfaz y un conjunto de funciones específicos.

Se pueden personalizar o mejorar los siguientes aspectos de la funcionalidad:

* [Ampliar editor de recursos](asseteditorx.md)
* [Ampliar búsqueda de recursos](searchx.md)
* [Procesar recursos con controladores de medios y flujos de trabajo](media-handlers.md)
* [Integrar recursos con flujo de actividades](extending-activity-stream.md)
* [Desarrollo de proxy de recursos](proxy.md)
* [Prácticas recomendadas para configurar ImageMagick](best-practices-for-imagemagick.md)

## Personalización del aspecto {#customizing-the-look-and-feel}

Se pueden personalizar los siguientes aspectos del aspecto del Editor de recursos:

* Logotipo: Puede agregar el logotipo de su propia organización a la interfaz.
* Colores y fuentes: Puede cambiar los colores y las fuentes utilizados en la interfaz.
* Código HTML: Para una personalización más completa, puede cambiar el código HTML subyacente que define las interfaces.

## Personalización de representaciones {#customizing-renditions}

En la terminología de Recursos AEM, una representación es la forma en que se presenta un recurso. En general, un recurso concreto puede tener varias representaciones. Por ejemplo, la imagen a color completo puede tener una representación en su tamaño original, otra en un tamaño reducido y otra que se reduzca y se convierta a escala de grises.

Las representaciones en las que está disponible un recurso concreto se pueden personalizar y crear nuevas representaciones.
