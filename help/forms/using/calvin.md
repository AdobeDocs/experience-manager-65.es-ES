---
title: Automatización de pruebas de formularios adaptables
seo-title: Automatización de pruebas de formularios adaptables
description: Con Calvin puede crear casos de prueba en CRXDE y ejecutar pruebas de interfaz de usuario directamente en el navegador web para probar exhaustivamente los formularios adaptables.
seo-description: Con Calvin puede crear casos de prueba en CRXDE y ejecutar pruebas de interfaz de usuario directamente en el navegador web para probar exhaustivamente los formularios adaptables.
uuid: 7bf4fc8f-96df-4407-8d10-cf18880518bd
contentOwner: gtalwar
content-type: reference
topic-tags: adaptive_forms, develop
discoiquuid: 1cb54c8a-9322-4b5a-b5a7-0eef342cee54
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 1%

---


# Automatizar la prueba de formularios adaptables{#automate-testing-of-adaptive-forms}

## Información general {#overview}

Los formularios adaptables son esenciales para las interacciones con los clientes. Es importante probar los formularios adaptables con todos los cambios que realice en ellos, como cuando se despliega un nuevo paquete de correcciones o se cambia una regla del formulario. Sin embargo, la prueba funcional de los formularios adaptables y de todos los campos de los mismos puede resultar tediosa.

Calvin le permite automatizar la prueba de sus formularios adaptables en el navegador web. Calvin utiliza la interfaz de usuario de [Hobbes](/help/sites-developing/hobbes.md) para ejecutar las pruebas y proporciona las siguientes herramientas:

* Una API de JavaScript para crear pruebas.
* Una interfaz de usuario para ejecutar pruebas.

Con Calvin, puede crear casos de prueba en CRXDE y ejecutar pruebas de interfaz de usuario directamente en el navegador web para probar a fondo los siguientes aspectos de los formularios adaptables:

<table>
 <tbody>
  <tr>
   <td><strong>Aspecto de formulario adaptable para probar</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Experiencia de cumplimentación previa de un formulario adaptable</td>
   <td>
    <ul>
     <li>¿El formulario se rellena previamente según lo esperado en función del tipo de modelo de datos?</li>
     <li>¿Los valores predeterminados de los objetos de formulario se van a rellenar previamente según lo esperado?</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Enviar experiencia de un formulario adaptable</td>
   <td>
    <ul>
     <li>¿Se generan datos correctos al enviar?</li>
     <li>¿Se está revalidando el formulario en el servidor durante el envío?</li>
     <li>¿Está configurada la acción de envío para el formulario que se está ejecutando?</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Reglas de expresión</p> <p> </p> </td>
   <td>
    <ul>
     <li>¿Las expresiones asociadas con objetos de formulario, como calculate, visible, ejecutan secuencias de comandos después de salir de un campo, y se ejecutan después de realizar las operaciones de IU relevantes?<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Validaciones</td>
   <td>
    <ul>
     <li>¿Las validaciones de campo se ejecutan según lo esperado después de realizar las operaciones?</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Carga diferida</p> <p> </p> </td>
   <td>
    <ul>
     <li>Al hacer clic en las fichas (o en cualquier elemento de navegación de un panel), ¿se está recuperando el HTML del servidor según la configuración de carga diferida?</li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Interacción de la interfaz de usuario</p> </td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html#toc2__anchor" target="_blank">Prueba de la interacción de la interfaz de usuario con objetos de formulario adaptable</a></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Requisitos previos {#prerequisites}

Antes de utilizar este artículo para crear los casos de prueba, debe saber lo siguiente:

* Creación de grupos de pruebas y ejecución de casos de prueba mediante [Hobbes](https://docs.adobe.com/docs/en/aem/6-3/develop/components/hobbes.html)
* [Hobbes JavaScript API](https://docs.adobe.com/docs/en/aem/6-2/develop/ref/test-api/index.html)
* [API de JavaScript de Calvin](https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html)

## Ejemplo: Crear un grupo de pruebas para un formulario adaptable usando Hobbes como marco de pruebas {#example-create-a-test-suite-for-an-adaptive-form-using-hobbes-as-testing-framework}

El siguiente ejemplo lo acompaña durante la creación de un grupo de pruebas para probar varios formularios adaptables. Debe crear un caso de prueba independiente para cada formulario que necesite probar. Si sigue pasos similares a los siguientes y modifica el código JavaScript en el paso 11, puede crear su propio grupo de pruebas para probar los formularios adaptables.

1. Vaya a CRXDE Lite en el navegador web: `https://'[server]:[port]'/crx/de`.
1. Haga clic con el botón derecho en la subcarpeta /etc/clientlibs y haga clic en **Crear** > **Crear nodo**. Escriba un nombre (aquí afTestRegistration), especifique el tipo de nodo como cq:ClientLibraryFolder y haga clic en **Aceptar.**

   La carpeta clientlibs contiene el aspecto de registro de la aplicación (JS e Init). Se recomienda registrar todos los objetos de los grupos de pruebas Hobbes específicos de un formulario en la carpeta clientlibs.

1. Especifique los siguientes valores de propiedad en el nodo recién creado (aquí afTestRegistration) y haga clic en **Guardar todo**. Estas propiedades ayudan a Hobbes a reconocer la carpeta como una prueba. Para reutilizar esta biblioteca de cliente como una dependencia en otras bibliotecas de cliente, asígnele el nombre granite.testing.calvin.testing.

<table>
 <tbody>
  <tr>
   <td>Propiedad</td>
   <td>Tipo</td>
   <td>Value</td>
  </tr>
  <tr>
   <td><p>categorías</p> </td>
   <td><p>Cadena[]</p> </td>
   <td><p>granite.testing.hobbes.testing, granite.testing.calvin.testing</p> </td>
  </tr>
  <tr>
   <td><p>dependencias</p> </td>
   <td><p>Cadena[]</p> </td>
   <td><p>granite.testing.hobbes.testrunner, granite.testing.calvin, apps.testframework.all</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>La clientlib granite.testing.calvin.af contiene todas las API de formularios adaptables. Estas API forman parte de la Área de nombres de cálculo.

![1_post_registration](assets/1_aftestregistration.png)

1. Haga clic con el botón secundario en el nodo de prueba (aquí **afTestRegistration)** y, a continuación, haga clic en **Crear** > **Crear archivo**. Asigne un nombre al archivo js.txt y haga clic en **Aceptar**.
1. En el archivo js.txt, agregue el siguiente texto:

   ```javascript
   #base=.
   js.txt
   ```

1. Haga clic en **Guardar todo** y cierre el archivo js.txt.
1. Haga clic con el botón derecho en el nodo de prueba (aquí **afTestRegistration)** y haga clic en **Crear** > **Crear archivo**. Asigne un nombre al archivo init.js y haga clic en **Aceptar**.
1. Copie el siguiente código en el archivo init.js y haga clic en **Guardar todo**:

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm = new hobs.TestSuite("Adaptive Form - Demo Test", {
           path: '/etc/clientlibs/afTestRegistration/init.js',
           register: true
       });
    // window.testsuites.testForm1 = new hobs.TestSuite("testForm1");
   }(window, window.hobs));
   ```

   El código anterior crea un grupo de pruebas denominado **Formulario adaptable - Prueba de demostración**. Para crear un grupo de pruebas con un nombre diferente, cambie el nombre según corresponda.

1. Haga clic en **Crear** > **Crear nodo** para crear un nodo en la carpeta clientlib para cada formulario que desee probar. En este ejemplo se utiliza un nodo denominado **testForm** para probar un formulario adaptable denominado **testForm**. Especifique las siguientes propiedades y haga clic en **Aceptar**:

   * Nombre: testForm (su nombre de formulario)
   * Tipo: cq:ClientLibraryFolder

1. Añada las siguientes propiedades en el nodo recién creado (aquí testForm) para probar un formulario adaptable:

   | **Propiedad** | **Tipo** | **Value** |
   |---|---|---|
   | categorías | Cadena[] | granite.testing.hobbes.testing, granite.testing.hobbes.testing.testForm |
   | dependencias | Cadena[] | granite.testing.calvin.tests |

   >[!NOTE]
   >
   >En este ejemplo se utiliza una dependencia de la biblioteca de cliente granite.testing.calvin.testing para una mejor administración. En este ejemplo también se agrega una categoría de biblioteca de cliente, &quot;granite.testing.hobbes.testing.testForm&quot;, para reutilizar esta biblioteca de cliente, si es necesario.

   ![2_testformproperties](assets/2_testformproperties.png)

1. Haga clic con el botón derecho en la carpeta que ha creado para el formulario de prueba (aquí testForm) y seleccione **Crear** > **Crear archivo**. Asigne un nombre al archivo scriptingTest.js y agregue el siguiente código al archivo y haga clic en **Guardar todo.**

   Para utilizar el siguiente código para probar otro formulario adaptable, cambie la ruta y el nombre del formulario en **navigateTo** (líneas 11, 36 y 62) y los respectivos casos de prueba. Para obtener más información sobre las API para probar diferentes aspectos de formularios y objetos de formulario, consulte [API de Calvin](https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html).

   ```javascript
   (function(window, hobs) {
       'use strict';
   
    var ts = new hobs.TestSuite("Script Test", {
           path: '/etc/clientlibs/testForm/scriptingTest.js',
     register: false
    })
   
       .addTestCase(new hobs.TestCase("Checking execution of calculate script")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/testForm.html?wcmmode=disabled")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel1.textbox1");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel1.textbox", "5");
           })
           // if the calculate expression was setting "textbox1" value to "5", let's also check that
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel1.textbox1", "Calculate");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel1.textbox1");
           })
           .asserts.isTrue(function () {
               return calvin.model("panel1.textbox1").value == "5"
           })
       )
   
       .addTestCase(new hobs.TestCase("Calculate script Test")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/cal/demoform.html?wcmmode=disabled&dataRef=crx:///content/forms/af/cal/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
   
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel2.panel1488218690733.downPayment");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel2.panel1488218690733.priceProperty", "1000000");
           })
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel2.panel1488218690733.downPayment", "Calculate");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel2.panel1488218690733.downPayment");
           })
           .asserts.isTrue(function () {
               // if the calculate expression was setting "downPayment" value to "10000", let's also check that
      return calvin.model("panel2.panel1488218690733.downPayment").value == 10000
           })
       )
   
       .addTestCase(new hobs.TestCase("Checking execution of Value commit script")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/cal/demoform.html?wcmmode=disabled&dataRef=crx:///content/forms/af/cal/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
   
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel2.panel1488218690733.priceProperty");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel2.panel1488218690733.priceProperty", "100");
           })
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel2.panel1488218690733.priceProperty", "Value Commit");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel2.panel1488218690733.priceProperty");
           })
           .asserts.isTrue(function () {
            // if the value commit expression was setting "textbox1488215618594" value to "0", let's also check that
               return calvin.model("panel2.panel1488218690733.textbox1488215618594").value == 0
           })
       );
   
    // register the test suite with testForm
     window.testsuites.testForm.add(ts);
   
    }(window, window.hobs));
   ```

   Se crea el caso de prueba. Proceda a ejecutar el caso de prueba para probar los formularios adaptables a través de Hobbes. Para ver los pasos para ejecutar los casos de prueba, consulte [Ejecución de pruebas en la prueba de la interfaz de usuario mediante pruebas automatizadas](/help/sites-developing/hobbes.md).

También puede instalar el paquete en el archivo adjunto SampleTestPackage.zip para obtener los mismos resultados que con los pasos explicados en Ejemplo: Cree un grupo de pruebas para un formulario adaptable utilizando Hobbes como marco de prueba.

[Obtener archivo](assets/sampletestpackage.zip)

## Prueba de la interfaz de usuario mediante pruebas automatizadas {#testing-your-ui-using-automated-tests}

### Ejecución de un único grupo de pruebas {#running-a-single-test-suite}

Los grupos de pruebas se pueden ejecutar de forma individual. Al ejecutar un grupo de pruebas, la página cambia a medida que se ejecutan los casos de prueba y sus acciones y los resultados aparecen una vez finalizada la prueba. Los iconos indican los resultados.

Un icono de marca de verificación indica una prueba pasada: ![marca de verificación](assets/checkmark.png)

El icono &quot;X&quot; indica que la prueba ha fallado: ![cross](assets/cross.png)

Para ejecutar un grupo de pruebas:

1. En el panel Pruebas, toque o haga clic en el nombre del caso de prueba que desee ejecutar para expandir los detalles de las acciones.

   ![1_tapnameoftestcase](assets/1_tapnameoftestcase.png)

1. Toque o haga clic en el botón Ejecutar pruebas. ![runtestcase](assets/runtestcase.png)

   ![2_clickrun](assets/2_clickrun.png)

1. El marcador de posición se reemplaza por el contenido de la página a medida que se ejecuta la prueba.

   ![3_pagecontent](assets/3_pagecontent.png)

1. Revise los resultados del caso de prueba tocando o haciendo clic en la descripción para abrir el panel Resultado. Al tocar o hacer clic en el nombre del caso de prueba en el panel Resultado se muestran todos los detalles.

   ![4_reviewresults](assets/4_reviewresults.png)

Los pasos para probar los formularios adaptables AEM son similares a los pasos para probar la IU AEM. Para obtener más información sobre la prueba de los formularios adaptables, consulte los siguientes temas en [Prueba de la interfaz de usuario](https://helpx.adobe.com//experience-manager/6-3/help/sites-developing/hobbes.html):

* Visualización de grupos de pruebas
* Ejecución de varias pruebas

## Glosario {#glossary}

<table>
 <tbody>
  <tr>
   <td><strong>Término</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><p>Conjunto de pruebas</p> </td>
   <td><p>Un grupo de pruebas es una colección de casos de prueba relacionados.</p> </td>
  </tr>
  <tr>
   <td><p>Caso de prueba</p> </td>
   <td><p>Un caso de prueba representa una tarea que un usuario realiza mediante su interfaz de usuario. Añada casos de prueba a su grupo de pruebas para probar las actividades que realizan los usuarios.</p> </td>
  </tr>
  <tr>
   <td><p>Acciones</p> </td>
   <td><p>Las acciones son métodos que realizan un gesto en la interfaz de usuario, como hacer clic en un botón o rellenar un cuadro de entrada con un valor.</p> <p>Los métodos de las clases hobs.actions.Asserts, hobs.actions.Core y hobs.utils.af son acciones que se pueden utilizar en las pruebas. Todas las acciones se ejecutan sincrónicamente.</p> </td>
  </tr>
  <tr>
   <td><p>Crear o publicar entorno</p> </td>
   <td><p>En general, los formularios se pueden probar en el entorno de creación o publicación. En caso de publicación, de forma predeterminada, el acceso para ejecutar la prueba está restringido. Esto se debe a que todas las bibliotecas de cliente relacionadas con el ejecutor de pruebas se encuentran dentro de /libs en la estructura JCR.</p> </td>
  </tr>
 </tbody>
</table>

