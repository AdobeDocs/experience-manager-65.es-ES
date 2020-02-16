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
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Tutorial: Prueba del formulario adaptable{#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

Este tutorial es un paso de la serie [Crear su primer formulario](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) adaptable. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

Una vez que el formulario adaptable esté listo, es importante probar el adaptador antes de extenderlo a los usuarios finales. Puede probar manualmente (pruebas funcionales) cada campo o automatizar la prueba del formulario adaptable. Cuando tiene varios formularios adaptables, la prueba manual de cada campo de todos los formularios adaptables se convierte en una tarea de enormes proporciones.

AEM Forms proporciona un marco de pruebas, Calvin, para automatizar las pruebas de los formularios adaptables. Con el marco, las pruebas de interfaz de usuario se escriben y ejecutan directamente en un navegador web. El marco proporciona API de JavaScript para crear pruebas. La prueba automatizada le permite probar la experiencia de cumplimentación previa de un formulario adaptable, enviar la experiencia de un formulario adaptable, las reglas de expresión, las validaciones, la carga diferida y las interacciones con la interfaz de usuario. Este tutorial le guía por los pasos para crear y ejecutar pruebas automatizadas en un formulario adaptable. Al final de este tutorial, podrá:

* [Crear un grupo de pruebas para el formulario adaptable](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [Crear pruebas para el formulario adaptable](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [Ejecutar el grupo de pruebas y las pruebas creadas para el formulario adaptable](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## Paso 1: Crear un grupo de pruebas {#step-create-a-test-suite}

Los grupos de pruebas tienen una colección de casos de prueba. Puede tener varios grupos de pruebas. Se recomienda disponer de un grupo de pruebas independiente para cada formulario. Para crear un grupo de pruebas:

1. Inicie sesión en la instancia de creación de AEM Forms como administrador. Abra CRXDE Lite. Puede tocar Logotipo de AEM > **Herramientas** > **General** > **CRXDE Lite** o abrir la [https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) URL en un navegador para abrir CRXDE Lite.

1. Vaya a /etc/clientlibs en CRXDE Lite. Haga clic con el botón derecho en la subcarpeta /etc/clientlibs y haga clic en **Crear** > **Crear nodo.** En el campo Nombre, escriba **WeRetailFormTestCases**. Seleccione el tipo como **cq:ClientLibraryFolder** y haga clic en **Aceptar**. Crea un nodo. Puede utilizar cualquier nombre en lugar de WeRetailFormTestCases.
1. Agregue las siguientes propiedades al nodo WeRetailFormTestCases y toque **Guardar todo**.

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
     <li>granite.testing.hobbes.testing<br /> </li>
     <li>granite.testing.calvin.testing</li>
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

1. Haga clic con el botón derecho en el nodo **[!UICONTROL WeRetailFormTestCases]** y haga clic en **Crear** > **Crear archivo**. En el campo Nombre, escriba `js.txt` y haga clic en **Aceptar**.
1. Abra el archivo js.txt para editarlo, añada el siguiente código y guarde el archivo:

   ```
   #base=.
    init.js
   ```

1. Cree un archivo, init.js, en el `WeRetailFormTestCases`nodo. Agregue el código siguiente al archivo y toque **[!UICONTROL Guardar todo]**.

   ```
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

   El código anterior crea un grupo de pruebas llamado **We Retail - Tests**.

1. Abra la interfaz de usuario de AEM Testing (AEM > Herramientas > Operaciones > Pruebas). El grupo de pruebas - **We Retail - Tests** - aparece en la interfaz de usuario.

   ![we-Retail-test-suite](assets/we-retail-test-suite.png)

## Paso 2: Crear un caso de prueba para rellenar previamente los valores en un formulario adaptable {#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}

Un caso de prueba es un conjunto de acciones para probar una funcionalidad específica. Por ejemplo, anteponiendo todos los campos de un formulario y validando algunos campos para asegurarse de que se introducen los valores correctos.

Una acción es una actividad específica de un formulario adaptable, como hacer clic en un botón. Para crear un caso de prueba y acciones para validar los datos introducidos por el usuario para cada campo de formulario adaptable:

1. En la lista CRXDE, vaya a la `/content/forms/af/create-first-adaptive-form` carpeta. Haga clic con el botón derecho en el nodo de la carpeta **[!UICONTROL create-first-adaptive-form]** y haga clic en **[!UICONTROL Crear]**> **[!UICONTROL Crear archivo]**. En el campo Nombre, escriba `prefill.xml` y haga clic en **[!UICONTROL Aceptar]**. Agregue el siguiente código al archivo:

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

1. Ir a `/etc/clientlibs`. Haga clic con el botón secundario en la `/etc/clientlibs` subcarpeta y haga clic en **[!UICONTROL Crear]**> **[!UICONTROL Crear nodo]**.

   En el campo **[!UICONTROL Nombre]** , escriba `WeRetailFormTests`. Seleccione el tipo como `cq:ClientLibraryFolder` y haga clic en **[!UICONTROL Aceptar]**.

1. Agregue las siguientes propiedades al nodo **[!UICONTROL WeRetailFormTests]** .

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
     <li>granite.testing.hobbes.testing<br /> </li>
     <li>granite.testing.hobbes.testing.testForm</li>
    </ul> </td>
  </tr>
  <tr>
   <td>dependencias</td>
   <td>Cadena</td>
   <td>Activado</td>
   <td>
    <ul>
     <li>granite.testing.calvin.testing</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

1. Cree un archivo, js.txt, en el nodo **[!UICONTROL WeRetailFormTests]** . Agregue lo siguiente al archivo:

   ```shell
   #base=.
   prefillTest.js
   ```

   Haga clic en **[!UICONTROL Guardar todo]**.

1. Cree un archivo `prefillTest.js`en el nodo **[!UICONTROL WeRetailFormTests]** . Agregue el código siguiente al archivo. El código crea un caso de prueba. El caso de prueba antepone todos los campos de un formulario y valida algunos campos para asegurarse de que se introducen los valores correctos.

   ```
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

## Paso 3: Ejecutar todas las pruebas en un grupo o en casos de pruebas individuales {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

Un grupo de pruebas puede tener varios casos de prueba. Puede ejecutar todos los casos de prueba en un grupo de pruebas a la vez o individualmente. Al ejecutar una prueba, los iconos indican los resultados:

* Un icono de marca de verificación indica una prueba pasada: ![](https://helpx.adobe.com/content/dam/help/icons/Checkmark.png)
* El icono &quot;X&quot; indica que la prueba ha fallado: ![](https://helpx.adobe.com/content/dam/help/icons/Cross.png)

1. Vaya al icono de AEM > **[!UICONTROL Herramientas]**> **[!UICONTROL Operaciones]**> **[!UICONTROL Pruebas]**
1. Para ejecutar todas las pruebas de Test Suite:

   1. En el panel Pruebas, toque **[!UICONTROL We Retail - Tests (1)]**. Se expande el grupo para mostrar la lista de pruebas.
   1. Puntee en el botón **[!UICONTROL Ejecutar pruebas]** . El área en blanco a la derecha de la pantalla se sustituye por un formulario adaptable a medida que se ejecuta la prueba.
   ![run-all-test](assets/run-all-test.png)

1. Para ejecutar una sola prueba desde Test Suite:

   1. En el panel Pruebas, toque **[!UICONTROL We Retail - Tests (1)]**. Se expande el grupo para mostrar la lista de pruebas.
   1. Toque la **[!UICONTROL Prueba]** de relleno previo y toque el botón **[!UICONTROL Ejecutar pruebas]** . El área en blanco a la derecha de la pantalla se sustituye por un formulario adaptable a medida que se ejecuta la prueba.

1. Toque el nombre de la prueba, Prueba de relleno previo, para revisar los resultados del caso de prueba. Se abre el panel Resultado. Toque el nombre del caso de prueba en el panel Resultado para ver todos los detalles de la prueba.

   ![review-results](assets/review-results.png)

Ahora el formulario adaptable está listo para su publicación.
