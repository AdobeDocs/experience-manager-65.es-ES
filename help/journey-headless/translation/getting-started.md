---
title: Introducción a AEM traducción sin encabezado
description: Conozca cómo organizar su contenido sin encabezado y cómo funcionan AEM herramientas de traducción.
index: true
hide: false
hidefromtoc: false
source-git-commit: 7cf68868e0963930bde9fcda647822a03914b61d
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 0%

---

# Introducción a AEM traducción sin encabezado {#getting-started}

Conozca cómo organizar su contenido sin encabezado y cómo funcionan AEM herramientas de traducción.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de traducción sin AEM, [Obtenga información sobre el contenido sin encabezado y cómo traducirlo en AEM](learn-about.md) aprendió la teoría básica de lo que es un CMS sin cabeza y ahora debería:

* Comprender los conceptos básicos de la entrega de contenido sin encabezado.
* Familiarícese con cómo AEM admite la traducción y la eliminación de periféricos.

Este artículo se basa en estos fundamentos para que entienda cómo AEM almacena y administra contenido sin objetivos y cómo puede utilizar AEM herramientas de traducción para traducir ese contenido.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo empezar a traducir contenido sin encabezado en AEM. Después de leer, debe:

* Comprender la importancia de la estructura de contenido para la traducción.
* Comprenda cómo AEM almacena contenido sin encabezado.
* Familiarícese con AEM herramientas de traducción.

## Requisitos y requisitos previos {#requirements-prerequisites}

Antes de empezar a traducir el contenido AEM sin encabezado, existen varios requisitos.

### Conocimiento {#knowledge}

* Experiencia en la traducción de contenido en un CMS
* Experiencia utilizando las funciones básicas de un CMS a gran escala
* Tener un conocimiento práctico de AEM manipulación básica
* Comprensión del servicio de traducción que utiliza
* Tenga una comprensión básica del contenido que está traduciendo

>[!TIP]
>
>Si no está familiarizado con el uso de un CMS a gran escala como AEM, considere la posibilidad de revisar la [Gestión básica](/help/sites-authoring/basic-handling.md) documentación antes de continuar. La documentación de Gestión básica no forma parte del recorrido, por lo que debe volver a esta página cuando haya terminado.

### Herramientas {#tools}

* Acceso a espacio aislado para probar la traducción del contenido
* Credenciales para conectarse al servicio de traducción preferido
* Sea miembro de `project-administrators` grupo en AEM

## La estructura es clave {#content-structure}

AEM contenido, ya sea páginas web tradicionales o sin encabezado, está impulsado por su estructura. AEM impone pocos requisitos a la estructura de contenido, pero tener en cuenta la jerarquía de contenido como parte de la planificación del proyecto puede hacer que la traducción sea mucho más sencilla.

>[!TIP]
>
>Planee la traducción al comienzo del proyecto sin encabezado. Trabaje en estrecha colaboración con el director del proyecto y los arquitectos de contenido desde el principio.
>
>Un administrador de proyectos de internacionalización puede ser una persona independiente, cuya responsabilidad es definir qué contenido debe traducirse y qué no, y qué contenido traducido pueden modificar los productores de contenido regionales o locales.

## Cómo AEM Almacena Contenido Sin Cabeza {#headless-content-in-aem}

Para el especialista en traducción, no es importante comprender en profundidad cómo AEM gestiona el contenido sin encabezado. Sin embargo, familiarizarse con los conceptos básicos y la terminología será útil, ya que más adelante utilizará AEM herramientas de traducción. Lo más importante es que debe comprender su propio contenido y cómo está estructurado para traducirlo de forma eficaz.

### Modelos de contenido {#content-models}

Para que el contenido sin encabezado se envíe de forma coherente entre canales, regiones e idiomas, el contenido debe estar muy estructurado. AEM usa modelos de contenido para aplicar esta estructura. Considere los modelos de contenido como una especie de plantilla o patrón para crear contenido sin encabezado. Dado que cada proyecto tiene sus propias necesidades, cada proyecto define sus propios modelos de fragmento de contenido. AEM no tiene requisitos ni estructura fijos para estos modelos.

El arquitecto de contenido trabaja al principio del proyecto para definir esta estructura. Como especialista en traducción, debe trabajar estrechamente con el arquitecto de contenido para comprender y organizar el contenido.

>[!NOTE]
>
>Es responsabilidad del arquitecto de contenido definir los modelos de contenido. El especialista en traducción solo debe familiarizarse con su estructura como se describe en los pasos siguientes.

Dado que los modelos de contenido definen la estructura del contenido, debe saber qué campos de los modelos se deben traducir. Normalmente, se trabaja con el arquitecto de contenido para definir esto. Para examinar los campos de los modelos de contenido, siga los pasos a continuación.

1. Vaya a **Herramientas** -> **Recursos** -> **Modelos de fragmento de contenido**.
1. Los modelos de fragmento de contenido generalmente se almacenan en una estructura de carpetas. Toque o haga clic en la carpeta de su proyecto.
1. Se muestran los modelos. Toque o haga clic en el modelo para ver los detalles.
   ![Modelos de fragmento de contenido](assets/content-fragment-models.png)
1. La variable **Editor del modelo de fragmento de contenido** se abre.
   1. La columna izquierda contiene los campos del modelo. Esta columna nos interesa.
   1. La columna derecha contiene los campos que se pueden agregar al modelo. Esta columna se puede ignorar.
      ![Editor del modelo de fragmento de contenido](assets/content-fragment-model-editor.png)
1. Toque o haga clic en uno de los campos del modelo. AEM marca y los detalles de ese campo se muestran en la columna derecha.
   ![Detalles del Editor del modelo de fragmento de contenido](assets/content-fragment-model-editor-detail.png)

Tome nota del campo **Nombre de propiedad** para todos los campos que deben traducirse. Necesitará esta información más adelante en el recorrido. Estos **Nombre de propiedad** s son necesarios para informar AEM qué campos del contenido deben traducirse.

>[!TIP]
>
>Por lo general, el arquitecto de contenido proporciona al especialista de traducción la **Nombre de propiedad** de todos los campos requeridos para la traducción. Estos nombres de campo son necesarios para más adelante en el recorrido. Los pasos anteriores se proporcionan para la comprensión del especialista en traducción.

### Fragmentos de contenido {#content-fragments}

Los autores de contenido utilizan los modelos de contenido para crear el contenido sin encabezado real. Los autores de contenido seleccionan en qué modelo basar su contenido y luego crean fragmentos de contenido. Los fragmentos de contenido son instancias de los modelos y representan el contenido real que se va a entregar sin problemas.

Si los modelos de contenido son los patrones para el contenido, los fragmentos de contenido son el contenido real basado en esos patrones. Los fragmentos de contenido representan el contenido que debe traducirse.

Los fragmentos de contenido se administran como recursos en AEM como parte de la administración de recursos digitales (DAM). Esto es importante, ya que todas están situadas debajo de la ruta `/content/dam`.

## Estructura de contenido recomendada {#recommended-structure}

Como se recomendó anteriormente, trabaje con su arquitecto de contenido para determinar la estructura de contenido adecuada para su propio proyecto. Sin embargo, lo siguiente es una estructura probada, simple e intuitiva que es bastante efectiva.

Defina una carpeta base para su proyecto en `/content/dam`.

```text
/content/dam/<your-project>
```

El idioma en el que se crea el contenido se denomina raíz del idioma. En nuestro ejemplo es inglés y debería estar por debajo de este camino.

```text
/content/dam/<your-project>/en
```

Todo el contenido del proyecto que pueda ser necesario localizar debe colocarse bajo la raíz del idioma.

```text
/content/dam/<your-project>/en/<your-project-content>
```

Las traducciones deben crearse como carpetas del mismo nivel a lo largo de la raíz del idioma con su nombre de carpeta que represente el código de idioma ISO-2 del idioma. Por ejemplo, el alemán tendría la siguiente ruta.

```text
/content/dam/<your-project>/de
```

>[!NOTE]
>
>Por lo general, el arquitecto de contenido es responsable de crear estas carpetas de idioma. Si no se crean, AEM podrá crear más adelante trabajos de traducción.

La estructura final puede tener un aspecto similar al siguiente.

```text
/content
    |- dam
        |- your-project
            |- en
                |- some
                |- exciting
                |- headless
                |- content
            |- de
            |- fr
            |- it
            |- ...
        |- another-project
        |- ...
```

Debe tomar nota de la ruta específica del contenido, ya que será necesaria más adelante para configurar la traducción.

>[!NOTE]
>
>Generalmente es responsabilidad del arquitecto de contenido definir la estructura del contenido, pero puede colaborar con el especialista en traducción.
>
>Se detalla aquí para que sea completo.

## AEM herramientas de traducción {#translation-tools}

Ahora que comprende qué son los fragmentos de contenido y la importancia de la estructura de contenido, podemos ver cómo traducir este contenido. Las herramientas de traducción en AEM son bastante poderosas, pero son simples de entender a un alto nivel.

* **Conector de traducción** - El conector es el vínculo entre AEM y el servicio de traducción que utiliza.
* **Reglas de traducción** - Las reglas definen qué contenido bajo rutas particulares se debe traducir.
* **Proyectos de traducción** - Los proyectos de traducción reúnen contenido que debe tratarse como un esfuerzo de traducción único y rastrean el progreso de la traducción, interconectándose con el conector para transmitir el contenido a traducir y recibirlo de nuevo desde el servicio de traducción.

Normalmente, solo se configura un conector una vez para la instancia y las reglas por proyecto sin encabezado. A continuación, utilice proyectos de traducción para traducir su contenido y mantener sus traducciones actualizadas de forma continua.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de traducción sin encabezado, debe:

* Comprender la importancia de la estructura de contenido para la traducción.
* Comprenda cómo AEM almacena contenido sin encabezado.
* Familiarícese con AEM herramientas de traducción.

Aproveche este conocimiento y continúe su recorrido de traducción sin AEM cabeza revisando el documento [Configuración del conector de traducción](configure-connector.md) donde aprenderá a conectar AEM a un servicio de traducción.|

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de traducción sin encabezado revisando el documento [Configuración del conector de traducción](configure-connector.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido sin encabezado.

* [Gestión básica de AEM](/help/sites-authoring/basic-handling.md) : Conozca los conceptos básicos de la interfaz de usuario de AEM para poder navegar cómodamente y realizar tareas esenciales como encontrar el contenido.
* [Identificación del contenido para traducir](/help/sites-administering/tc-rules.md) : Aprenda cómo las reglas de traducción identifican el contenido que necesita traducción.
* [Configuración del marco de integración de traducción](/help/sites-administering/tc-tic.md) - Aprenda a configurar el marco de integración de traducción para integrarlo con servicios de traducción de terceros.
* [Administración de proyectos de traducción](/help/sites-administering/tc-manage.md) - Aprenda a crear y administrar proyectos de traducción automática y humana en AEM.
