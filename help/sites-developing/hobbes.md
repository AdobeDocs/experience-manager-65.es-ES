---
title: Prueba de la interfaz de usuario
seo-title: Testing Your UI
description: AEM proporciona un marco para automatizar pruebas para la interfaz de usuario de AEM
seo-description: AEM provides a framework for automating tests for your AEM UI
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 2%

---

# Prueba de la interfaz de usuario{#testing-your-ui}

>[!NOTE]
>
>A partir de AEM 6.5, el marco de pruebas de la interfaz de usuario de hobbes.js quedará obsoleto. Adobe no tiene previsto realizar más mejoras y recomienda a los clientes que utilicen la automatización de Selenium.
>
>Consulte [Funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

AEM proporciona un marco para automatizar pruebas para la interfaz de usuario de AEM. Con el marco, se escriben y ejecutan pruebas de IU directamente en un explorador web. El marco de trabajo proporciona una API de javascript para la creación de pruebas.

El marco de AEM prueba utiliza Hobbes.js, una biblioteca de pruebas escrita en JavaScript. El marco Hobbes.js se desarrolló para probar AEM como parte del proceso de desarrollo. El marco de trabajo ya está disponible para uso público para probar las aplicaciones AEM.

>[!NOTE]
>
>Consulte Hobbes.js [documentación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html) para obtener más información sobre la API.

## Estructura de las pruebas {#structure-of-tests}

Cuando se utilizan pruebas automatizadas en AEM, es importante entender los términos siguientes:

| Acción | Un **Acción** es una actividad específica de una página web, como hacer clic en un vínculo o en un botón. |
|---|---|
| Caso de prueba | A **Caso de prueba** es una situación específica que puede estar formada por uno o más **Acciones**. |
| Grupo de pruebas | A **Grupo de pruebas** es un grupo relacionado **Casos de prueba** que juntos prueban un caso de uso específico. |

## Ejecución de pruebas {#executing-tests}

### Visualización de grupos de pruebas {#viewing-test-suites}

Abra la Consola de pruebas para ver los grupos de pruebas registrados. El panel Pruebas contiene una lista de grupos de pruebas y sus casos de prueba.

Vaya a la consola Herramientas a través de **Navegación global -> Herramientas > Operaciones -> Pruebas**.

![imagen_1-63](assets/chlimage_1-63.png)

Al abrir la consola, los grupos de pruebas se muestran a la izquierda junto con una opción para ejecutarlos de forma secuencial. El espacio a la derecha que se muestra con un fondo marcado es un marcador de posición para mostrar el contenido de la página mientras se ejecutan las pruebas.

![imagen_1-64](assets/chlimage_1-64.png)

### Ejecución de un único grupo de pruebas {#running-a-single-test-suite}

Los grupos de pruebas se pueden ejecutar individualmente. Cuando ejecuta un grupo de pruebas, la página cambia a medida que se ejecutan los casos de prueba y sus acciones y los resultados aparecen después de completar la prueba. Los iconos indican los resultados.

Un icono de marca de verificación indica una prueba pasada:

![](do-not-localize/chlimage_1-2.png)

El icono &quot;X&quot; indica una prueba fallida:

![](do-not-localize/chlimage_1-3.png)

Para ejecutar un grupo de pruebas:

1. En el panel Pruebas, toque o haga clic en el nombre del caso de prueba que desea ejecutar para expandir los detalles de las acciones.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Toque o haga clic en **Ejecutar prueba** botón.

   ![](do-not-localize/chlimage_1-4.png)

1. El marcador de posición se reemplaza por el contenido de la página a medida que se ejecuta la prueba.

   ![imagen_1-66](assets/chlimage_1-66.png)

1. Revise los resultados del caso de prueba tocando o haciendo clic en la descripción para abrir el **Resultado** panel. Toque o haga clic en el nombre del caso de prueba en la sección **Resultado** muestra todos los detalles.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Ejecución de varias pruebas {#running-multiple-tests}

Los grupos de pruebas se ejecutan secuencialmente en el orden en que aparecen en la consola. Puede explorar en profundidad una prueba para ver los resultados detallados.

![chlimage_1-68](assets/chlimage_1-68.png)

1. En el panel Pruebas , toque o haga clic en las **Ejecutar todas las pruebas** o **Ejecutar pruebas** debajo del título del grupo de pruebas que desea ejecutar.

   ![](do-not-localize/chlimage_1-5.png)

1. Para ver los resultados de cada caso de prueba, toque o haga clic en el título del caso de prueba. Toque o haga clic en el nombre de la prueba en la sección **Resultado** muestra todos los detalles.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Creación y uso de un grupo de pruebas simple {#creating-and-using-a-simple-test-suite}

El siguiente procedimiento lo guía durante la creación y ejecución de un grupo de pruebas [Contenido de We.Retail](/help/sites-developing/we-retail.md), pero puede modificar fácilmente la prueba para utilizar una página web diferente.

Para obtener más información sobre cómo crear sus propios grupos de pruebas, consulte la [Documentación de la API de Hobbes.js](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html).

1. Abra CRXDE Lite. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. Haga clic con el botón derecho en el `/etc/clientlibs` carpeta y haga clic en **Crear > Crear carpeta**. Tipo `myTests` para el nombre y haga clic en **OK**.
1. Haga clic con el botón derecho en el `/etc/clientlibs/myTests` carpeta y haga clic en **Crear > Crear nodo**. Utilice los siguientes valores de propiedad y haga clic en **OK**:

   * Nombre: `myFirstTest`
   * Tipo: `cq:ClientLibraryFolder`

1. Agregue las siguientes propiedades al nodo myFirstTest :

   | Nombre | Tipo | Valor |
   |---|---|---|
   | `categories` | Cadena[] | `granite.testing.hobbes.tests` |
   | `dependencies` | Cadena[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**Solo AEM Forms**
   >
   >
   >Para probar los formularios adaptables, agregue los siguientes valores a las categorías y dependencias. Por ejemplo:
   >
   >
   >**categories**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**dependencias**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. Haga clic en **Guardar todo**.
1. Haga clic con el botón derecho en el `myFirstTest` nodo y haga clic en **Crear > Crear archivo**. Asigne un nombre al archivo `js.txt` y haga clic en **OK**.
1. En el `js.txt` , escriba el siguiente texto:

   ```
   #base=.
   myTestSuite.js
   ```

1. Haga clic en **Guardar todo** y luego cierre el `js.txt` archivo.
1. Haga clic con el botón derecho en el `myFirstTest` nodo y haga clic en **Crear > Crear archivo**. Asigne un nombre al archivo `myTestSuite.js` y haga clic en **OK**.
1. Copie el siguiente código en la `myTestSuite.js` y guarde el archivo:

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. Vaya a la **Pruebas** para probar el grupo de pruebas.
