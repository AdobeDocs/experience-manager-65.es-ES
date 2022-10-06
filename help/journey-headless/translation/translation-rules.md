---
title: Configuración de las reglas de traducción
description: Aprenda a definir reglas de traducción para identificar el contenido que se va a traducir.
exl-id: 262503af-361b-491c-8639-0bb32f0a4c0e
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 44%

---

# Configuración de las reglas de traducción {#configure-translation-rules}

Aprenda a definir reglas de traducción para identificar el contenido que se va a traducir.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de traducción sin AEM, [Configuración del conector de traducción](configure-connector.md) ha aprendido a instalar y configurar el conector de traducción y ahora debe:

* Comprender los parámetros importantes del marco de trabajo de integración de traducción en AEM.
* Puede configurar su propia conexión con el servicio de traducción.

Ahora que el conector está configurado, este artículo le explica el siguiente paso para identificar qué contenido debe traducir.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo utilizar las reglas de traducción de AEM para identificar el contenido de la traducción. Después de leer este documento, debería poder hacer lo siguiente:

* Comprender lo que hacen las reglas de traducción.
* Poder definir sus propias reglas de traducción.

## Reglas de traducción {#translation-rules}

Los fragmentos de contenido, que representan el contenido sin encabezado, pueden contener mucha información organizada por campos estructurados. Según las necesidades del proyecto, es probable que no se deban traducir todos los campos de un fragmento de contenido.

Las reglas de traducción identifican el contenido que se incluye en los proyectos de traducción o que se excluye de ellos. Cuando se traduce contenido, AEM lo extrae o saca en función de estas reglas. De este modo, solo el contenido que debe traducirse se envía al servicio de traducción.

Las reglas de traducción incluyen la siguiente información:

* Ruta del contenido al que se aplica la regla
   * La regla también se aplica a los descendientes del contenido
* Nombres de las propiedades que contienen el contenido que se va a traducir
   * La propiedad puede ser específica para un tipo de recurso específico o para todos los tipos de recurso

Debido a que los modelos de fragmento de contenido, que definen la estructura de los fragmentos de contenido, son únicos para su propio proyecto, es vital configurar reglas de traducción para AEM sepa qué elementos de los modelos de contenido traducir.

>[!TIP]
>
>Por lo general, el arquitecto de contenido proporciona al especialista de traducción la **Nombre de propiedad** de todos los campos necesarios para la traducción. Estos nombres son necesarios para configurar las reglas de traducción. Como especialista en traducción, usted [puede encontrar estas **Nombre de propiedad** s](getting-started.md#content-models) tal como se ha descrito anteriormente en este recorrido.

## Creación de reglas de traducción {#creating-rules}

Se pueden crear varias reglas para admitir requisitos de traducción complejos. Por ejemplo, un proyecto en el que esté trabajando requiere que se traduzcan todos los campos del modelo, pero en otro solo los campos de descripción deben traducirse mientras los títulos queden sin traducir.

Las reglas de traducción están diseñadas para manejar estos escenarios. Sin embargo, en este ejemplo ilustramos cómo crear reglas centrándose en una configuración simple y única.

Hay una consola de **Configuración de traducción** disponible para configurar las reglas de traducción. Para acceder a ella:

1. Vaya a **Herramientas** -> **General**.
1. Toque o haga clic en **Configuración de traducción**.

En el **Configuración de traducción** En la interfaz de usuario de hay varias opciones disponibles para las reglas de traducción. Aquí resaltamos los pasos más necesarios y típicos necesarios para una configuración de localización básica sin encabezado.

1. Toque o haga clic **Agregar contexto**, que le permite añadir una ruta. Esta es la ruta del contenido que se ve afectado por la regla.
   ![Añadir contexto](assets/add-translation-context.png)
1. Utilice el navegador de rutas para seleccionar la ruta necesaria y toque o haga clic en el botón **Confirmar** para guardar. Recuerde que los fragmentos de contenido, que contienen contenido sin encabezado, generalmente se encuentran debajo de `/content/dam/<your-project>`.
   ![Seleccione la ruta](assets/select-context.png)
1. AEM guarda la configuración.
1. Debe seleccionar el contexto que acaba de crear y, a continuación, tocar o hacer clic en **Editar**. Esto abre el **Editor de reglas de traducción** para configurar las propiedades.
   ![Editor de reglas de traducción](assets/translation-rules-editor.png)
1. De forma predeterminada, todas las configuraciones se heredan de la ruta principal, en este caso `/content/dam`. Desmarque la opción **Heredar de`/content/dam`** para añadir campos adicionales a la configuración.
1. Una vez desmarcado, en la sección **General** de la lista, añada los nombres de propiedad de los modelos de fragmento de contenido que haya [anteriormente identificados como campos para traducción.](getting-started.md#content-models)
   1. Introduzca el nombre de la propiedad en el campo **Nueva propiedad**.
   1. Las opciones **Traducir** y **Heredar** se marcan automáticamente.
   1. Haga clic o pulse **Agregar**.
   1. Repita estos pasos para todos los campos que debe traducir.
   1. Haga clic o pulse **Guardar**.
      ![Agregar propiedad](assets/add-property.png)

Ya ha configurado las reglas de traducción.

## Uso avanzado {#advanced-usage}

Hay varias propiedades adicionales que se pueden configurar como parte de las reglas de traducción. Además, puede especificar las reglas manualmente como XML, lo que permite una mayor especificidad y flexibilidad.

Estas funciones generalmente no son necesarias para empezar a localizar el contenido sin encabezado, pero puede leer más sobre ellas en la sección [Recursos adicionales](#additional-resources) si está interesado.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de traducción sin encabezado, debe:

* Comprender lo que hacen las reglas de traducción.
* Poder definir sus propias reglas de traducción.

Aproveche este conocimiento y continúe su recorrido de traducción sin AEM cabeza revisando el documento [Traducir contenido](translate-content.md) donde aprenderá cómo funcionan juntos sus conectores y reglas para traducir contenido sin encabezado.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de traducción sin encabezado revisando el documento [Traducir contenido](translate-content.md), los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido sin encabezado.

* [Identificación del contenido para traducir](/help/sites-administering/tc-rules.md): aprenda cómo las reglas de traducción identifican el contenido que necesita traducirse.
