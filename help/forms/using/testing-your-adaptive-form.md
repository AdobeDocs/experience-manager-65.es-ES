---
title: '"Tutorial: Prueba del formulario adaptable"'
seo-title: '"Tutorial: Prueba del formulario adaptable"'
description: Utilice la prueba automatizada para probar varios formularios adaptables a la vez.
seo-description: Utilice la prueba automatizada para probar varios formularios adaptables a la vez.
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 2%

---


# Tutorial: Prueba del formulario adaptable {#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

Este tutorial es un paso en la serie [Crear su primer formulario adaptable](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Una vez que el formulario adaptable esté listo, es importante probar el adaptador antes de extenderlo a los usuarios finales. Puede probar manualmente (pruebas funcionales) cada campo o automatizar la prueba del formulario adaptable. Cuando tiene varios formularios adaptables, la prueba manual de cada campo de todos los formularios adaptables se convierte en una tarea de enormes proporciones.

AEM [!DNL Forms] proporciona un entorno de prueba, Calvin, para automatizar la prueba de los formularios adaptables. Con el marco, las pruebas de interfaz de usuario se escriben y ejecutan directamente en un navegador web. El marco proporciona API de JavaScript para crear pruebas. La prueba automatizada le permite probar la experiencia de cumplimentación previa de un formulario adaptable, enviar la experiencia de un formulario adaptable, reglas de expresión, validaciones, carga diferida e interacciones con la interfaz de usuario. Este tutorial le guía por los pasos para crear y ejecutar pruebas automatizadas en un formulario adaptable. Al final de este tutorial, podrá:

* [Crear un grupo de pruebas para el formulario adaptable](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [Crear pruebas para el formulario adaptable](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [Ejecutar el grupo de pruebas y las pruebas creadas para el formulario adaptable](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## Paso 1: Crear un grupo de pruebas {#step-create-a-test-suite}

Los grupos de pruebas tienen una colección de casos de prueba. Puede tener varios grupos de pruebas. Se recomienda disponer de un grupo de pruebas independiente para cada formulario. Para crear un grupo de pruebas:

1. Inicie sesión en AEM instancia de creación [!DNL Forms] como administrador. Abra [!UICONTROL CRXDE Lite]. Puede tocar AEM logotipo > **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]** o abrir la dirección URL [https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) en un explorador para abrir el CRXDE Lite.

1. Vaya a /etc/clientlibs en [!UICONTROL CRXDE Lite]. Haga clic con el botón derecho en la subcarpeta /etc/clientlibs y haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Crear nodo]**. En el campo **[!UICONTROL Nombre]**, escriba **WeRetailFormTestCases**. Seleccione el tipo como **cq:ClientLibraryFolder** y haga clic en **[!UICONTROL Aceptar]**. Crea un nodo. Puede utilizar cualquier nombre en lugar de `WeRetailFormTestCases`.
1. Añada las siguientes propiedades en el nodo `WeRetailFormTestCases` y toque **[!UICONTROL Guardar TODO]**.

   <table>
    <tbody>
     <tr>
      <td><strong>Propiedad</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Multi</strong></td>
      <td><strong>Value</strong></td>
     </tr>
     <tr>
      <td>categorías</td>
      <td>Cadena</td>
      <td>Activado</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     <tr>
      <td>dependencias</td>
      <td>Cadena</td>
      <td>Activado</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.testrunner <br /> </li>
        <li>granite.testing.calvin <br /> </li>
        <li>apps.testframework.all</li>
       </ul> </td>
     </tr>
    </tbody>
   </table>

   Asegúrese de que cada propiedad se agrega a un cuadro independiente como se muestra a continuación:

   ![dependencias](assets/dependencies.png)

1. Haga clic con el botón derecho en el nodo **[!UICONTROL WeRetailFormTestCases]** y haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Crear archivo]**. En el campo **[!UICONTROL Nombre]**, escriba `js.txt` y haga clic en **[!UICONTROL Aceptar]**.
1. Abra el archivo js.txt para editarlo, añada el siguiente código y guarde el archivo:

   ```text
   #base=.
    init.js
   ```

1. Cree un archivo, init.js, en el nodo `WeRetailFormTestCases`. Añada el código siguiente en el archivo y toque **[!UICONTROL Guardar todo]**.

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm3 = new hobs.TestSuite("We retail - Tests", {
           path: '/etc/clientlibs/WeRetailFormTestCases/init.js',
           register: true
       });
    // window.testsuites.testForm2 = new hobs.TestSuite("testForm2");
   }(window, window.hobs));
   ```

   El código anterior crea un grupo de pruebas denominado **We Retail - Tests**.

1. Abra AEM interfaz de usuario de prueba (AEM > **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Pruebas]**). El grupo de pruebas - **Estamos al por menor - Pruebas** - aparece en la interfaz de usuario.

   ![we-Retail-test-suite](assets/we-retail-test-suite.png)

## Paso 2: Cree un caso de prueba para rellenar previamente los valores en un formulario adaptable {#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}

Un caso de prueba es un conjunto de acciones para probar una funcionalidad específica. Por ejemplo, anteponiendo todos los campos de un formulario y validando algunos campos para asegurarse de que se introducen los valores correctos.

Una acción es una actividad específica de un formulario adaptable, como hacer clic en un botón. Para crear un caso de prueba y acciones para validar los datos introducidos por el usuario para cada campo de formulario adaptable:

1. En [!UICONTROL lista CRXDE], navegue a la carpeta `/content/forms/af/create-first-adaptive-form`. Haga clic con el botón derecho en el nodo de carpeta **[!UICONTROL create-first-adaptive-form]** y haga clic en **[!UICONTROL Crear]** **[!UICONTROL Crear archivo]**. En el campo **[!UICONTROL Nombre]**, escriba `prefill.xml` y haga clic en **[!UICONTROL Aceptar]**. Añada el siguiente código al archivo:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><afData>
     <afUnboundData>
       <data>
         <customer_ID>371767</customer_ID>
         <customer_Name>John Jacobs</customer_Name>
         <customer_Shipping_Address>1657 1657 Riverside Drive Redding</customer_Shipping_Address>
         <customer_State>California</customer_State>
         <customer_ZIPCode>096001</customer_ZIPCode>
        </data>
     </afUnboundData>
     <afBoundData>
       <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"/>
     </afBoundData>
   </afData>
   ```

1. Ir a `/etc/clientlibs`. Haga clic con el botón secundario en la subcarpeta `/etc/clientlibs` y haga clic en **[!UICONTROL Crear]**> **[!UICONTROL Crear nodo]**.

   En el campo **[!UICONTROL Nombre]**, escriba `WeRetailFormTests`. Seleccione el tipo como `cq:ClientLibraryFolder` y haga clic en **[!UICONTROL Aceptar]**.

1. Añada las siguientes propiedades en el nodo **[!UICONTROL WeRetailFormTests]**.

   <table>
    <tbody>
     <tr>
      <td><strong>Propiedad</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Varios</strong></td>
      <td><strong>Valor</strong></td>
     </tr>
     <tr>
      <td>categorías</td>
      <td>Cadena</td>
      <td>Activado</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.hobbes.tests.testForm</li>
       </ul> </td>
     </tr>
     <tr>
      <td>dependencias</td>
      <td>Cadena</td>
      <td>Activado</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. Cree un archivo, js.txt, en el nodo **[!UICONTROL WeRetailFormTests]**. Añada lo siguiente en el archivo:

   ```shell
   #base=.
   prefillTest.js
   ```

   Haga clic en **[!UICONTROL Guardar todo]**.

1. Cree un archivo, `prefillTest.js`, en el nodo **[!UICONTROL WeRetailFormTests]**. Añada el código siguiente en el archivo. El código crea un caso de prueba. El caso de prueba antepone todos los campos de un formulario y valida algunos campos para asegurarse de que se introducen los valores correctos.

   ```javascript
   (function (window, hobs) {
       'use strict';
   
       var ts = new hobs.TestSuite("Prefill Test", {
           path: '/etc/clientlibs/WeRetailFormTests/prefillTest.js',
           register: false
       })
   
       .addTestCase(new hobs.TestCase("Prefill Test")
           // navigate to the testForm which is to be test
           .navigateTo("/content/forms/af/create-first-adaptive-form/shipping-address-add-update-form.html?wcmmode=disabled&dataRef=crx:///content/forms/af/create-first-adaptive-form/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ID").value == 371767;
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ZIPCode").value == 96001;
           })
       );
   
       // register the test suite with testForm
       window.testsuites.testForm3.add(ts);
   
   }(window, window.hobs));
   ```

   El caso de prueba se crea y está listo para ejecutarse. Puede crear casos de prueba para validar varios aspectos de un formulario adaptable, como comprobar la ejecución de la secuencia de comandos de cálculo, validar patrones y validar la experiencia de envío de un formulario adaptable. Para obtener información sobre varios aspectos de la prueba de formularios adaptables, consulte Automatización de la prueba de formularios adaptables.

## Paso 3: Ejecute todas las pruebas en un grupo o en casos de pruebas individuales {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

Un grupo de pruebas puede tener varios casos de prueba. Puede ejecutar todos los casos de prueba en un grupo de pruebas a la vez o individualmente. Al ejecutar una prueba, los iconos indican los resultados:

* Un icono de marca de verificación indica una prueba pasada: ![save_icon](assets/save_icon.svg)
* El icono &quot;X&quot; indica que la prueba ha fallado: ![close-icon](assets/close-icon.svg)

1. Vaya al icono de AEM > **[!UICONTROL Herramientas]** **[!UICONTROL Operaciones]** **[!UICONTROL Pruebas]**
1. Para ejecutar todas las pruebas de Test Suite:

   1. En el panel [!UICONTROL Pruebas], toque **[!UICONTROL Pruebas de venta al por menor - Pruebas (1)]**. Se expande el conjunto para mostrar la lista de la prueba.
   1. Toque el botón **[!UICONTROL Ejecutar pruebas]**. El área en blanco a la derecha de la pantalla se sustituye por un formulario adaptable a medida que se ejecuta la prueba.

      ![run-all-test](assets/run-all-test.png)

1. Para ejecutar una sola prueba desde Test Suite:

   1. En el panel Pruebas, toque **[!UICONTROL We Retail - Tests (1)]**. Se expande el conjunto para mostrar la lista de la prueba.
   1. Toque el botón **[!UICONTROL Prueba de relleno previo]** y toque el botón **[!UICONTROL Ejecutar pruebas]**. El área en blanco a la derecha de la pantalla se sustituye por un formulario adaptable a medida que se ejecuta la prueba.

1. Toque el nombre de la prueba, Prueba de relleno previo, para revisar los resultados del caso de prueba. Abre el panel [!UICONTROL Resultado]. Toque el nombre del caso de prueba en el panel [!UICONTROL Resultado] para vista de todos los detalles de la prueba.

   ![review-results](assets/review-results.png)

Ahora el formulario adaptable está listo para su publicación.
