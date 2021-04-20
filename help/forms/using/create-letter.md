---
title: Crear carta
seo-title: Crear carta
description: 'En este tema se explican los pasos para crear una carta, agregar módulos de datos y archivos adjuntos y previsualizarla en Gestión de Correspondencia. '
seo-description: 'En este tema se explican los pasos para crear una carta, agregar módulos de datos y archivos adjuntos y previsualizarla en Gestión de Correspondencia. '
uuid: b5cdbf01-db85-4ff8-9fda-1489542bffef
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: 6cef0bcf-e2f0-4a5a-85a1-6d8a5dd9bd01
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4008'
ht-degree: 2%

---


# Crear carta {#create-letter}

## Flujo de trabajo de Gestión de Correspondencia {#correspondence-management-workflow}

El flujo de trabajo de Gestión de correspondencia consta de cuatro fases:

1. Creación de plantillas
1. Creación de fragmentos de documento
1. Creación de cartas
1. Postprocesamiento

### Creación de plantilla {#template-creation}

El siguiente gráfico muestra un flujo de trabajo típico para crear una plantilla de correspondencia.

![Flujo de trabajo para crear una plantilla de correspondencia](assets/01.png)

En este flujo de trabajo:

1. Los diseñadores de formularios crean diseños y diseños de fragmento utilizando Adobe Forms Designer y los cargan en un repositorio CRX. Los diseños contienen campos de formulario típicos, funciones de presentación como encabezado y pie de página, y &quot;áreas de destino&quot; vacías para la colocación de contenido. Posteriormente, los especialistas en aplicaciones asignan el contenido necesario para estas áreas de destino. Más información sobre [diseño](/help/forms/using/layout-design-details.md).
1. Expertos en materia de asuntos de los departamentos jurídicos, financieros o de marketing crean y cargan contenido, como cláusulas de texto, términos y condiciones, e imágenes como logotipos, que se reutilizan en varias plantillas de correspondencia.
1. Los especialistas en aplicaciones crean plantillas de correspondencia. El especialista en solicitudes

   * Asigna cláusulas de texto e imágenes a áreas de destino en plantillas de diseño
   * Define condiciones/reglas para la inclusión de contenido
   * Enlaza campos y variables de diseño con modelos de datos subyacentes

1. El autor obtiene una vista previa de la carta y la envía para su procesamiento posterior. Más información sobre [post processing](/help/forms/using/submit-letter-topostprocess.md).

#### Uso de plantillas de carta proporcionadas con la Administración de correspondencia {#using-letter-templates-provided-with-correspondence-management}

En lugar de crear una plantilla de diseño desde cero, puede elegir modificar y reutilizar las plantillas que proporciona la Gestión de Correspondencia. Puede utilizar designer para modificar rápidamente la marca y los campos de datos y contenido de las plantillas a fin de adaptarlos a las necesidades de su organización. Para obtener más información sobre las plantillas de Gestión de Correspondencia, consulte [Plantillas de carta de referencia](/help/forms/using/reference-cm-layout-templates.md).

### Creación de fragmentos de documento {#document-fragment-creation}

Los fragmentos de documento son partes reutilizables\componentes de una correspondencia mediante los cuales puede componer cartas\correspondencia.

Los fragmentos del documento son de los siguientes tipos:

#### Texto {#text}

Un recurso de texto es un fragmento de contenido que consta de uno o más párrafos de texto. Un párrafo puede ser estático o dinámico. Un párrafo dinámico contiene referencias a elementos de datos, cuyos valores se proporcionan durante la ejecución.

#### Lista {#list}

Lista es una serie de fragmentos de documento, incluidos texto, listas (la misma lista no se puede &quot;añadir en sí misma), condiciones e imágenes. El orden de los elementos de la lista puede ser fijo o editable. Al crear una carta, puede utilizar algunos o todos los elementos de la lista para replicar un patrón de elementos reutilizable.

#### Condición {#condition}

Las condiciones permiten definir qué contenido se incluye en el momento de la creación de la correspondencia, según los datos suministrados. La condición se describe en términos de variables de control. Las variables pueden ser un elemento de diccionario de datos o un marcador de posición. Cuando agregue una condición, puede elegir incluir un recurso en función del valor que tenga la variable de control. Las condiciones tienen una sola salida basada en una expresión. La primera expresión se encuentra como verdadera, en función de la variable de condición actual. Su valor se convierte en el resultado de la condición.

#### Fragmento de diseño {#layout-fragment}

Un fragmento de diseño es un diseño que se puede utilizar en una o varias letras. Un fragmento de diseño se utiliza para crear patrones repetibles, especialmente tablas dinámicas. La presentación puede contener campos de formulario típicos, como &quot;Dirección&quot; y &quot;Número de referencia&quot;. También contiene subformularios vacíos que denotan áreas de destino. Los diseños (XDP) se crean en Designer y luego se [cargan en Forms y Documents](/help/forms/using/get-xdp-pdf-documents-aem.md).

### Creación de letras {#letter-creation}

Existen dos maneras de generar la correspondencia que se envía a sus clientes: impulsado por el usuario y por el sistema.

#### {#user-driven} impulsado por el usuario

Los empleados orientados al cliente, como los reguladores de reclamaciones o los trabajadores de casos, pueden crear correspondencia personalizada. Con una interfaz sencilla e intuitiva de cumplimentación de cartas, los usuarios empresariales pueden añadir texto opcional a la correspondencia, personalizar el contenido editable y previsualizar la correspondencia en tiempo real. Luego pueden enviar la correspondencia personalizada a un proceso back-end.

![Correspondencia personalizada, dirigida por el usuario](assets/02.png)

#### Sistema controlado {#system-driven}

La generación de correspondencia está automatizada, impulsada por déclencheur de eventos. Por ejemplo, un aviso recordatorio enviado a una ciudadana pidiéndole que registre impuestos por adelantado, se genera combinando la plantilla predefinida con datos ciudadanos. La carta final puede enviarse por correo electrónico, imprimirse, enviarse por fax o archivarse.

![Correspondencia basada en el sistema](assets/us_cm_generate.png)

### Procesamiento posterior {#post-processing}

La correspondencia final se puede enviar a un proceso back-end para el posprocesamiento. La correspondencia puede ser:

1. Procesado para correo electrónico, fax o impresión por lotes, o colocado en una carpeta para imprimir o enviar por correo electrónico.
1. Presentado para su examen y aprobación.
1. Garantizado mediante la aplicación de firmas digitales, certificación, cifrado o administración de derechos.
1. Se convierte en un documento PDF en el que se pueden buscar y que contiene todos los metadatos necesarios para fines de archivo y auditoría.
1. Se incluye en un Portfolio PDF que incluye más documentos, como material de marketing. El Portfolio PDF se puede enviar como correspondencia final.

### Arquitectura de la solución de administración de correspondencia {#correspondence-management-solution-architecture}

El siguiente gráfico proporciona información general sobre una arquitectura de ejemplo de la solución Letras.

![Arquitectura de la solución de letras](assets/us_cm_architecture_es3.png)

## Desestructurar una letra {#deconstructing-a-letter}

Este documento de Aviso de Cancelación es un ejemplo de correspondencia típica:

![Ejemplo de carta de cancelación](assets/5_deconstructingaletter.png)

<table> 
 <tbody> 
  <tr> 
   <td><strong>Elementos de carta</strong></td> 
   <td><strong>Descripción</strong></td> 
   <td><strong>Formado con</strong></td> 
  </tr> 
  <tr> 
   <td>Datos de sistemas empresariales back-end</td> 
   <td>Datos procedentes de sistemas empresariales back-end. Los datos se combinan dinámicamente con la plantilla de correspondencia.</td> 
   <td>El archivo de datos<br /> creado en función de un diccionario de datos</td> 
  </tr> 
  <tr> 
   <td>Datos<br /> introducidos por el empleado de primera línea</td> 
   <td>Datos que puede proporcionar un empleado de primera línea que está personalizando la carta antes de enviarla.<br /> </td> 
   <td><p>Elementos DD no protegidos<br /> Párrafos de texto editables<br /> Variables/marcadores de posición<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Párrafos de texto aprobados previamente<br /></td> 
   <td>Contenido de texto preaprobado. Los expertos en Asuntos Jurídicos, Finanzas o una línea de negocios que comprenden el contexto empresarial de la carta suelen crear el contenido del texto. El contenido, como el encabezado, el pie de página, las exenciones de responsabilidad y el saludo, sería común en la mayoría de las letras. Sin embargo, el contenido como "motivo de la rescisión" sería específico de la carta en cuestión.</td> 
   <td><p>Text\Lists\<br /> Condiciones\Diseño</p> <p> </p> </td> 
  </tr> 
  <tr> 
   <td>Datos<br /> basados en la lógica personalizada ?</td> 
   <td>En el caso de algunas cartas, como una carta para solicitar más información sobre una reclamación, los usuarios, como el Ajuste de reclamaciones, pueden agregar contenido de texto personalizado.</td> 
   <td>Documento<br /> Fragmento de tipo Condición </td> 
  </tr> 
  <tr> 
   <td>Imágenes almacenadas<br /> del repositorio central</td> 
   <td>Imágenes como logotipos e imágenes de firma. Imágenes como logotipos corporativos aparecerían en la mayoría o en toda la correspondencia. Las imágenes de firma son específicas de la carta y de la persona en cuyo nombre se envía la carta.</td> 
   <td><p>Imágenes almacenadas en AEM assets (DAM)<br /> </p> <p> </p> </td> 
  </tr> 
 </tbody> 
</table>

## Analice una carta antes de crearla {#analyze-a-letter-before-you-construct-it}

Analice cada carta para descubrir las distintas partes que la componen. El especialista en aplicaciones analiza las correspondencias que se generan.

* Qué partes de la correspondencia son estáticas y cuáles son dinámicas. Las variables que se rellenan desde fuentes de datos back-end o por usuarios finales.
* El orden en que aparecen los distintos párrafos de texto en la correspondencia, como si un usuario empresarial puede cambiar de párrafo durante la creación de la correspondencia.
* ¿Se genera el sistema de correspondencia o se requiere que un usuario final edite la correspondencia? ¿Cuántas correspondencias se generan a partir del sistema y cuántas requieren la intervención del usuario?
* ¿Con qué frecuencia cambia la plantilla de correspondencia? ¿Se actualizará anualmente, trimestralmente o solo cuando cambie una legislación en particular? ¿Qué tipo de cambios se esperan? ¿Se trata de un cambio para corregir errores tipográficos, un cambio de diseño, agregar más campos, agregar más párrafos, etc.?
* Al planificar sus necesidades de correspondencia, prepare la lista de nuevas plantillas de correspondencia. Para cada plantilla de correspondencia, necesita:

   * Cláusulas de texto, imágenes y tablas
   * Valores de datos de sistemas back-end
   * El diseño y los diseños de fragmento de la correspondencia
   * El orden en el que aparece el contenido en la carta y las reglas para la inclusión y exclusión de contenido

* Condiciones en las que los usuarios comerciales, como los reguladores de reclamaciones o los trabajadores de casos, modifican el contenido o partes de la carta.
* Los escenarios son narrativas que describen la experiencia del usuario, los requisitos y los beneficios de utilizar la solución de cartas.
* Los escenarios también proporcionan: los conjuntos de habilidades y herramientas que necesita para su proyecto.
* Prácticas recomendadas para planificar la implementación. &quot;Descripción general de la implementación de alto nivel.

## Ventajas de realizar el análisis {#benefits-of-performing-the-analysis}

**Reutilización de** contenidoTiene una lista consolidada del nuevo contenido necesario para generar correspondencia. Gran parte del contenido, como encabezados, pies de página, exenciones de responsabilidad e introducciones, es común a muchas letras y se puede reutilizar en varias letras. Todos estos contenidos comunes pueden ser creados y aprobados por expertos una vez y luego reutilizados en muchos fragmentos de correspondencia.

**Creación del** diccionario de datosHabrá valores de datos como &quot;ID de cliente&quot; y &quot;Nombre de cliente&quot; que son comunes a muchas letras. Puede preparar una lista consolidada de todos estos valores de datos. Normalmente, se consulta a alguien del equipo de middleware empresarial al planificar la estructura. Esto forma la base para crear el diccionario de datos.

**Abastecimiento de datos de** sistemas empresariales back-endTambién conocerá todos los valores de datos necesarios y desde dónde se obtienen los datos del sistema empresarial. A continuación, puede crear la implementación para extraer los datos del sistema empresarial y alimentarlos con la solución Letters .

**Calcular la complejidad de las** cartasEs importante determinar lo complejo que será crear una correspondencia en particular. Este análisis ayuda a determinar la cantidad de tiempo y conjuntos de habilidades que se necesitarán para crear las plantillas de letras. Esto, a su vez, ayudará a estimar los recursos y el coste de la implementación de la solución Letters.

## Complejidad de correspondencia {#correspondence-complexity}

La complejidad de la correspondencia puede determinarse analizando los siguientes parámetros:

**Complejidad del** diseño ¿Qué tan complejo es el diseño? Las cartas como Aviso de cancelación tienen diseños simples. Mientras que las letras como Confirmación de Cobertura de Reclamaciones tienen un diseño complejo con varias tablas y más de 60 campos de formulario. La creación de diseños complejos lleva más tiempo y requiere conjuntos de habilidades de diseño avanzado.

**Número de párrafos de texto y** condicionesUn contrato de préstamo puede tener 10 páginas y contener más de 40 cláusulas de texto. Muchas de estas cláusulas dependerían de &quot;parámetros de préstamo&quot;. Sobre la base de las condiciones exactas, las cláusulas se incluirían o excluirían del contrato. La creación de esas cartas requiere una planificación minuciosa y una definición cuidadosa de las condiciones complejas.

En esta tabla se proporcionan algunas directrices que puede utilizar para clasificar las cartas:

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Nivel de complejidad</strong></p> </td> 
   <td><p><strong>Complejidad de diseño (subjetivo)</strong></p> </td> 
   <td><p><strong>Número de párrafos de texto</strong></p> </td> 
   <td><p><strong>Número de textos o imágenes condicionales</strong></p> </td> 
   <td><p><strong>Conjunto de habilidades requerido</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Baja complejidad</p> </td> 
   <td><p>Baja. La presentación tiene pocos campos de formulario (&lt;15).</p> <p>Normalmente una página<span class="acrolinxCursorMarker"></span>.</p> </td> 
   <td><p>8</p> </td> 
   <td><p>1</p> </td> 
   <td><p>Capacidades de Diseñador medio.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Complejidad media</p> </td> 
   <td><p>Diseño de complejidad medio. Incluye estructuras como tablas. Normalmente, más de una página de longitud.</p> </td> 
   <td><p>16</p> </td> 
   <td><p>2</p> </td> 
   <td><p>Capacidades de Diseñador medio.</p> <p> </p> <p>Capacidad para crear expresiones complejas mediante interfaces de usuario.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Complejidad</p> </td> 
   <td><p>Diseño complejo. Puede tener buenas tres páginas. Contiene tablas y más de 60 campos de formulario.</p> </td> 
   <td><p>40</p> </td> 
   <td><p>8</p> </td> 
   <td><p>Capacidades de Diseñador experto.</p> <p> </p> <p>Capacidad para crear expresiones complejas mediante interfaces de usuario.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Información general sobre la creación de una carta {#overview-of-creating-a-letter}

1. Seleccione el diseño adecuado que sirve como base de la carta y cree una carta.
1. Agregue módulos de datos o fragmentos de diseño a la carta y configúrelos.
1. Elija para obtener una vista previa de la correspondencia.
1. Edite y configure los campos, variables, contenido y archivos adjuntos.

### Requisitos previos {#prerequisites}

Primero necesita lo siguiente para crear una correspondencia:

* [Paquete de compatibilidad](compatibility-package.md). Instale el paquete de compatibilidad para ver la opción **Letters** en la página **Forms**.
* La letra XDP ([layout](/help/forms/using/document-fragments.md)).
* Otros XDP ([fragmentos de diseño](document-fragments.md#document-fragments)) que forman partes de la carta. Los XDP\Diseños se crean en [Designer](https://help.adobe.com/en-US/AEMForms/6.1/DesignerHelp/).
* El [diccionario de datos](/help/forms/using/data-dictionary.md) correspondiente (opcional).
* Los [módulos de datos](/help/forms/using/document-fragments.md) que desea utilizar en la correspondencia.
* [Los ](/help/forms/using/data-dictionary.md#p-working-with-test-data-p) datos de prueba son el archivo XML con los datos de prueba incorporados. Los datos de prueba son necesarios si utiliza un diccionario de datos.

## Crear una plantilla de carta {#create-a-letter-template}

### Seleccione un diseño e introduzca las propiedades de la letra {#select-a-layout-and-enter-the-letter-properties}

1. Seleccione **Forms** > **Letras**.

1. Seleccione **Crear > Carta**. La gestión de correspondencia muestra los diseños disponibles (XDP). Estos diseños proceden de Designer. Los diseños también incluyen las plantillas de letras que la Gestión de Correspondencia proporciona de forma predeterminada. Para obtener más información sobre las plantillas de Gestión de Correspondencia, consulte [Plantillas de carta de referencia](/help/forms/using/reference-cm-layout-templates.md). Para añadir sus propios diseños, cree archivos XDP (layout) en Designer y, a continuación, [cárguelos en AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md).

   ![create-letter](assets/create-letter.png)

1. Para seleccionar un diseño, toque o haga clic en **Next**.

   ![Seleccionar diseño para crear una carta](assets/selectlayout.png)

1. Introduzca las propiedades de la correspondencia y pulse **Guardar:**

   * **Título (opcional):** introduzca el título de la carta. El título no tiene que ser único y puede tener caracteres especiales y caracteres que no sean de inglés.
   * **Nombre:** el nombre exclusivo de la carta. No puede haber dos letras en ningún estado con el mismo nombre. En el campo Nombre, solo se pueden introducir caracteres, números y guiones en inglés. El campo Nombre se rellena automáticamente en función del campo Título . Los caracteres especiales, espacios, números y caracteres que no sean de inglés introducidos en el campo Título se sustituyen por guiones en el campo Nombre. Aunque el valor del campo Título se copia automáticamente en el Nombre, puede editarlo.
   * **Descripción (opcional):** describa la carta para su referencia.
   * **Diccionario de datos (opcional)**: El diccionario de datos se puede asociar a la correspondencia. Los recursos que inserte posteriormente en esta correspondencia deben tener el mismo diccionario de datos que el que elija para la correspondencia aquí o ningún diccionario de datos.
   * **Etiquetas (opcional):** seleccione las etiquetas que desee aplicar a la correspondencia. También puede escribir un nombre de etiqueta nuevo/personalizado y pulsar Intro para crearlo.
   * **Proceso de anuncio (opcional):** seleccione el proceso de anuncio que se aplicará a la plantilla de carta. Existen procesos de publicación predeterminados y los que ha creado mediante AEM, como correo electrónico e impresión.

   ![Propiedades de correspondencia](assets/createcorrespondenceproperties.png)

1. El sistema muestra un mensaje: &quot;Carta creada correctamente&quot;. (en el mensaje de alerta) Toque **Open** para configurar los módulos de datos y los fragmentos de diseño en él. O pulse **Listo** para volver a la página anterior.

   ![Mensaje de alerta: carta creada correctamente](assets/createcorrespondencecreated.png)

   **Siguiente**: Al pulsar  **Abrir**, Gestión de correspondencia muestra una representación del diseño con todos los componentes del diseño (XDP) enumerados. Continúe insertando los [Módulos de datos y fragmentos de diseño y configurándolos](/help/forms/using/create-letter.md#p-insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them-p).

### Inserte módulos de datos y fragmentos de diseño en una carta y configúrelos {#insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them}

Cuando después de crear una correspondencia, pulse Abrir, la Gestión de correspondencia muestra una representación de la presentación con todas las áreas de subformularios/destino de la presentación (XDP) enumeradas. En cada una de las áreas de destino, puede elegir insertar un módulo de datos o un fragmento de diseño (y luego módulos de datos en el fragmento de diseño).

>[!NOTE]
>
>También puede pulsar Editar icono para una carta en la página Letras para Insertar módulos de datos y fragmentos de diseño en una carta y configurarlos.

1. Pulse **Insertar** para cada uno de los subformularios y seleccione Módulos de datos o un fragmento de diseño para insertar en cada uno de los subformularios.

   ![Insertar módulos de datos y fragmentos de diseño](assets/insertdmandlf.png)

1. Seleccione Módulo de datos o Fragmento de diseño para estas opciones para cada uno de los subformularios y, a continuación, elija los módulos de datos o los fragmentos de diseño que desea insertar. Un fragmento de diseño le permite insertar más módulos de datos o fragmentos de diseño según su diseño (hasta cuatro niveles).

   ![nestedlf](assets/nestedlf.png)

1. Si inserta un fragmento de presentación, el nombre del fragmento de presentación aparecerá en el subformulario. Y según el fragmento seleccionado, los subformularios anidados aparecen en el subformulario.
1. Una vez insertados los módulos de datos seleccionados en el diseño, puede pulsar el modo de configuración y definir lo siguiente después de pulsar el icono Editar para cada uno de los módulos:

   1. **Editable**: Cuando se selecciona esta opción, el contenido se puede editar en la interfaz de usuario Crear correspondencia . Marque el contenido como editable solo si requiere que el usuario del negocio (como un ajuste de reclamaciones) lo modifique.
   1. **Obligatorio**: Cuando se selecciona esta opción, el contenido es necesario en la interfaz de usuario Crear correspondencia .
   1. **Seleccionado**: Cuando se selecciona esta opción, el contenido se selecciona de forma predeterminada en la interfaz de usuario Crear correspondencia .
   1. **Sangría**: Aumente o disminuya la sangría del módulo/contenido de la carta. La sangría se especifica en términos de niveles, comenzando por 0. Cada nivel sangra 36 puntos. Para obtener más información sobre la personalización de formularios, consulte **[!UICONTROL Correspondence Management Configurations]** en [Forms workflow](submit-letter-topostprocess.md#formsworkflow).
   1. **Salto de página antes** de: Si establece el salto de página antes de que se active, el contenido de ESTE módulo siempre se mostrará en una nueva página.
   1. **Salto de página después** de: Si establece el valor de Salto de página después de para un módulo específico, el contenido del módulo NEXT siempre se muestra en una página nueva.

   ![Módulos de datos insertados y fragmentos de diseño](assets/insertdmandlf2.png)

1. Para editar un módulo, pulse el icono Editar que hay junto a él. Después de editar los módulos, pulse **Guardar**.

   En esta página, también puede hacer lo siguiente para los subformularios:

   1. **Permitir texto** libre: Si la opción Permitir texto libre está activada, el usuario puede añadir texto en línea en letra en la vista CCR. En la vista CCR, se habilita una acción &#39;T&#39; para las áreas de destino que tienen habilitada la opción Permitir texto libre y cuando el usuario la toca, se solicita el nombre y la descripción del texto y, al pulsar Aceptar, se abre el texto en modo de edición, donde el usuario puede agregar texto. Esto funciona como otros módulos de texto
   1. **Orden** de bloqueo: Bloquea el orden de los subformularios de la carta. No se permite al autor reordenar los subformularios o componentes al crear la carta.

   En esta página, también puede hacer lo siguiente para cada uno de los recursos de los subformularios:

   1. **Cambie el orden de los recursos**: arrastre y suelte un recurso que contenga el icono de reordenar de un recurso (  ![arrastrar y soltar](assets/dragndrop.png)).
   1. **Eliminar recursos**: Pulse el icono Eliminar situado junto a un recurso para eliminarlo.
   1. **Vista previa de recursos**: Pulse el icono mostrar vista previa (  ![showpreview](assets/showpreview.png)) situado junto a un recurso.


1. Toque **Siguiente**.
1. La página Datos detalla cómo se utilizan los campos de datos y las variables en la plantilla. Los datos se pueden vincular a fuentes de datos como un diccionario de datos o entradas del usuario. Cada campo define propiedades desde las que el diccionario de datos asigna datos o qué rótulo se muestra para los campos de entrada del usuario.

   Vinculación:

   * Los elementos **field** se pueden vincular a un literal, a un elemento de diccionario de datos, a un recurso o a un valor especificado por el usuario. También puede ignorar un elemento de campo enlazándolo a la opción Ignore .
   * Los elementos **variable** se pueden vincular a un literal, a un elemento de diccionario de datos, a un campo, a una variable, a un recurso o a un valor especificado por el usuario.

   A continuación, se muestran algunos campos principales en el vínculo :

   * **Multilínea**: Puede especificar si la entrada de datos de un campo o variable es multilínea. Si selecciona esta opción, el cuadro de entrada del campo o variable se muestra como cuadro de entrada multilínea en la vista Edición de datos. El campo o variable también se muestra como multilínea en las vistas Datos y contenido de la interfaz de usuario Crear correspondencia . El campo de entrada multilínea es similar al campo para introducir un comentario en un TextModule. La opción multilínea solo está disponible para campos y variables con tipo de vínculo Usuario o Elementos de diccionario de datos no protegidos.
   * **Opcional**: Puede especificar si el valor del campo o la variable es opcional o no. La opción de campo opcional está disponible para campos y variables con tipo de vínculo Usuario o elementos de diccionario de datos no protegidos.

   * **Validación** de campos/variables: Para proporcionar una validación mejorada del valor de un campo o variable, puede asignar un validador al campo o variable. Esta opción solo está disponible para campos y variables con tipo de vínculo Usuario o elementos de diccionario de datos no protegidos.
   * **** Pie de ilustración e  **información del objeto**: Rótulo es la etiqueta del campo que aparece antes del campo en la interfaz de usuario de CCR. Esta opción está disponible para campos y variables con tipo de vínculo Usuario o elementos de diccionario de datos no protegidos.

   A continuación se indican los tipos de validación que puede utilizar para los campos:

   * **Validador** de cadenas: Utilice el validador de cadenas para especificar una longitud mínima y máxima de la cadena introducida en el campo o la variable. Cuando cree un validador de cadenas, asegúrese de especificar parámetros de validación válidos. Introduzca una longitud válida para los valores mínimo y máximo. Para el validador de cadenas, puede especificar la longitud mínima y máxima del valor que se puede introducir. Si el valor introducido no está de acuerdo con el mínimo y el máximo especificados, el campo correspondiente en la interfaz de usuario de CCR se marca en color rojo.

   * **Validador** de número: Utilice el Validador de números para especificar el valor numérico mínimo y máximo introducido en un campo o variable. Cuando cree un Validador de números, asegúrese de especificar parámetros de validación válidos. Introduzca valores numéricos para los valores mínimo y máximo.

   * **Validador** de expresiones regulares: Utilice el validador de expresiones regulares para definir una expresión regular que se utilice para validar el valor de un campo o variable. Además, puede personalizar el mensaje de error. Cuando cree un validador de expresiones regulares, asegúrese de especificar una expresión regular válida.
   >[!NOTE]
   >
   >Los validadores de campos y variables solo están disponibles en campos o variables con tipo de vínculo Usuario o Elementos de diccionario de datos no protegidos.

   ![vínculos](assets/linkages.png)

1. Después de especificar el vínculo, pulse **Siguiente**. Gestión de Correspondencia muestra la pantalla Anexos.

### Configurar los archivos adjuntos {#set-up-the-attachments}

1. Seleccione **Agregar recurso**.
1. En la pantalla Seleccionar recurso, pulse los recursos que desea adjuntar a la carta y pulse **Listo**. Debe tener los recursos cargados primero en Assets. Se recomienda adjuntar sólo documentos PDF y Microsoft Office, pero también adjuntar imágenes. Para obtener más información sobre la carga de recursos en DAM, consulte [Carga de recursos](/help/assets/manage-assets.md).
1. Para bloquear el orden de los recursos en la lista de modo que el ajuste de reclamaciones no pueda cambiar el orden, pulse **Bloquear orden**. Si no selecciona esta opción, el Ajuste de Reclamaciones puede cambiar el orden de los artículos de la lista.
1. Para cambiar el orden de los recursos, arrastre y suelte un recurso que contenga el icono de reordenar de un recurso ( ![arrastrar](assets/dragndrop.png)).
1. Pulse **Editar** delante de un archivo adjunto y especifique un archivo adjunto como obligatorio si no desea que el autor pueda eliminarlo. Especifique un archivo adjunto como Seleccionado si desea que se preseleccione en la interfaz de CCR.
1. Seleccione **Acceso a biblioteca** para dar acceso a la biblioteca. Si el acceso a la biblioteca está habilitado, el ajuste de reclamaciones puede acceder a la biblioteca de contenido al crear una carta e insertar archivos adjuntos.
1. Seleccione **Attachments Configuration** y especifique el número máximo de archivos adjuntos.

1. Toque **Guardar**. La correspondencia se crea y aparece en la página Letras .

Después de crear una plantilla de carta en Gestión de Correspondencia, el usuario/agente/ajustador de reclamaciones final puede abrir la carta en la interfaz de usuario de CCR y crear una correspondencia introduciendo datos, configurando contenido y administrando archivos adjuntos. Para obtener más información, consulte [Crear correspondencia](/help/forms/using/create-correspondence.md).

## Tipos de vinculación disponibles para cada uno de los campos {#types-of-linkage-available-for-each-of-the-fields}

La siguiente tabla describe qué tipos de vínculos están disponibles para varios tipos de campos.

Los valores siguientes de la tabla

* **Sí**: El tipo de campo de la columna situada más a la izquierda admite ese tipo de asignación
* **No**: El tipo de campo de la columna situada más a la izquierda no admite ese tipo de asignación
* **N/D**: El tipo de campo de la columna situada más a la izquierda no es aplicable

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td><strong>Literal</strong></td> 
   <td><strong>Recurso</strong></td> 
   <td><strong>Diccionario de datos</strong></td> 
   <td><strong>Ignorar</strong></td> 
   <td><strong>Usuario</strong></td> 
   <td><strong>Campo</strong></td> 
   <td><strong>Variable</strong></td> 
  </tr> 
  <tr> 
   <td><strong>date</strong></td> 
   <td>Sí</td> 
   <td>No</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>time</strong></td> 
   <td>Sí</td> 
   <td>No</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>datetime</strong></td> 
   <td>Sí</td> 
   <td>No</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>integer</strong></td> 
   <td>Sí</td> 
   <td>No</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>Sí<br /> </td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>float</strong></td> 
   <td>Sí</td> 
   <td>No</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>Sí<br /> </td> 
   <td>N/D</td> 
   <td>N/D<br /> </td> 
  </tr> 
  <tr> 
   <td><strong>richtext</strong></td> 
   <td>Sí</td> 
   <td>solo texto</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong></strong> <strong>texto sin formato</strong></td> 
   <td>Sí</td> 
   <td>solo texto</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>Sí</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>image</strong></td> 
   <td>No</td> 
   <td>solo imagen</td> 
   <td>No</td> 
   <td>Sí</td> 
   <td>No</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>signature</strong></td> 
   <td>No</td> 
   <td>No</td> 
   <td>No<br /> </td> 
   <td>Sí</td> 
   <td>No</td> 
   <td>N/D</td> 
   <td>N/D<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Crear copia de una plantilla de carta {#createcopylettertemplate}

Puede utilizar una plantilla de carta existente para crear rápidamente una plantilla de carta con propiedades, contenido y recursos heredados similares, como fragmentos de documento y diccionario de datos. Para ello, copie y pegue una carta.

1. En la página Letras, seleccione una o varias letras. La interfaz de usuario muestra el icono Copiar .
1. Pulse Copiar. La interfaz de usuario muestra el icono Pegar . También puede elegir ir dentro de una carpeta antes de pegar. Las distintas carpetas pueden contener recursos con los mismos nombres. Para obtener más información sobre las carpetas, consulte [Carpetas y organización de recursos](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets).
1. Pulse Pegar. Aparecerá el cuadro de diálogo Pegar. Si está copiando y pegando las letras en el mismo lugar, el sistema asigna automáticamente nombres y títulos a las nuevas copias de las letras, pero puede editar los títulos y nombres de las letras.
1. Si es necesario, edite el Título y el Nombre con los que desea guardar la copia de la carta.
1. Pulse Pegar. Se crea la copia de la carta. Ahora puede realizar los cambios necesarios en la carta recién creada.

