---
title: Trabajar con el modelo de datos de formulario
seo-title: Trabajar con el modelo de datos de formulario
description: La integración de datos proporciona un editor de modelos de datos de formulario para configurar y trabajar con modelos de datos de formulario.
seo-description: La integración de datos proporciona un editor de modelos de datos de formulario para configurar y trabajar con modelos de datos de formulario.
uuid: ed78f7f7-8123-4778-9252-89924cec09d6
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c47ef627-261e-4b4b-8846-873d3d84234b
docset: aem65
translation-type: tm+mt
source-git-commit: ba42f1e85216f6be4ae0dd90891e1b2d1d559bd8
workflow-type: tm+mt
source-wordcount: '4148'
ht-degree: 0%

---


# Trabajar con el modelo de datos de formulario{#work-with-form-data-model}

![integración de datos](do-not-localize/data-integeration.png)

El editor del modelo de datos de formulario proporciona una interfaz de usuario intuitiva y herramientas para editar y configurar un modelo de datos de formulario. Con el editor, puede agregar y configurar objetos, propiedades y servicios del modelo de datos desde orígenes de datos asociados en el modelo de datos de formulario. Además, le permite crear objetos y propiedades del modelo de datos sin orígenes de datos y enlazarlos posteriormente con objetos y propiedades del modelo de datos respectivos. También puede generar y editar datos de ejemplo para propiedades de objeto del modelo de datos que puede utilizar para rellenar formularios adaptables y comunicaciones interactivas durante la vista previa. Puede probar los objetos y servicios del modelo de datos configurados en un modelo de datos de formulario para asegurarse de que está correctamente integrado con los orígenes de datos.

Si es nuevo en la integración de datos de Forms y no ha configurado un origen de datos o creado un modelo de datos de formulario, consulte los siguientes temas:

* [Integración de datos de AEM Forms](/help/forms/using/data-integration.md)
* [Configurar orígenes de datos](/help/forms/using/configure-data-sources.md)
* [Crear modelo de datos de formulario](/help/forms/using/create-form-data-models.md)

Continúe leyendo para obtener más información sobre las distintas tareas y configuraciones que puede realizar con el editor del modelo de datos de formulario.

>[!NOTE]
>
>Debe ser miembro de los grupos **fdm-author** y **form-user** para poder crear y trabajar con el modelo de datos de formulario. Póngase en contacto con el administrador de AEM para convertirse en miembro de los grupos.

## Añadir objetos y servicios del modelo de datos {#add-data-model-objects-and-services}

Si ha creado un modelo de datos de formulario con orígenes de datos, puede utilizar el editor del modelo de datos de formulario para agregar objetos y servicios del modelo de datos, configurar sus propiedades, crear asociaciones entre objetos del modelo de datos y probar el modelo y los servicios de datos de formulario.

Puede agregar objetos y servicios del modelo de datos a partir de orígenes de datos disponibles en el modelo de datos de formulario. Cuando los objetos del modelo de datos agregados aparecen en la ficha Modelo, los servicios agregados aparecen en la ficha Servicios.

Para agregar objetos y servicios del modelo de datos:

1. Inicie sesión en la instancia de creación de AEM, vaya a **[!UICONTROL Forms > Integraciones de datos]** y abra el modelo de datos de formulario en el que desee agregar objetos de modelo de datos.
1. En el panel Fuentes de datos, expanda las fuentes de datos para vista de los objetos y servicios del modelo de datos disponibles.
1. Seleccione los objetos y servicios del modelo de datos que desee agregar al modelo de datos de formulario y toque **[!UICONTROL Añadir seleccionados]**.

   ![selected-Objects](assets/selected-objects.png)

   Objetos y servicios del modelo de datos seleccionado

   La ficha Modelo muestra una representación gráfica de todos los objetos del modelo de datos y sus propiedades agregadas al modelo de datos de formulario. Cada objeto del modelo de datos se representa mediante un cuadro en el modelo de datos de formulario.

   ![model-tab](assets/model-tab.png)

   La ficha Modelo muestra los objetos del modelo de datos agregados

   >[!NOTE]
   >
   >Puede mantener y arrastrar cuadros de objetos del modelo de datos para organizarlos en el área de contenido. Todos los objetos del modelo de datos agregados en el modelo de datos de formulario aparecen atenuados en el panel Fuentes de datos.

   La ficha Servicios lista los servicios agregados.

   ![services-tab](assets/services-tab.png)

   La ficha Servicios muestra los servicios del modelo de datos

   >[!NOTE]
   >
   >Además de los objetos y servicios del modelo de datos, el documento de metadatos del servicio OData incluye propiedades de navegación que definen la asociación entre dos objetos del modelo de datos. Para obtener más información, consulte [Uso de las propiedades de navegación de los servicios OData](#work-with-navigation-properties-of-odata-services).

1. Toque **[!UICONTROL Guardar]** para guardar el objeto del modelo de formulario.

   >[!NOTE]
   >
   >Puede invocar servicios configurados en la ficha Servicios de un modelo de datos de formulario mediante las reglas de formulario adaptables. Los servicios configurados están disponibles en la acción Invocar servicios del editor de reglas. Para obtener más información sobre el uso de estos servicios en reglas de formularios adaptables, consulte Invocar servicios y establecer valor de reglas en [editor de reglas](/help/forms/using/rule-editor.md).

## Crear objetos de modelo de datos y propiedades secundarias {#create-data-model-objects-and-child-properties}

### Crear objetos de modelo de datos {#create-data-model-objects}

Aunque puede agregar objetos de modelo de datos desde orígenes de datos configurados, también puede crear objetos o entidades de modelo de datos sin orígenes de datos. Resulta especialmente útil si no ha configurado orígenes de datos en el modelo de datos de formulario.

Para crear un objeto de modelo de datos sin orígenes de datos:

1. Inicie sesión en la instancia de creación de AEM, vaya a **[!UICONTROL Forms > Integraciones de datos]** y abra el modelo de datos de formulario en el que desee crear una entidad u objeto del modelo de datos.
1. Toque **[!UICONTROL Crear entidad]**.
1. En el cuadro de diálogo Crear modelo de datos, especifique un nombre para el objeto del modelo de datos y toque **[!UICONTROL Añadir]**. Se agrega un objeto de modelo de datos al modelo de datos de formulario. Tenga en cuenta que el objeto del modelo de datos recientemente agregado no está enlazado a un origen de datos y no tiene ninguna propiedad, como se muestra en la siguiente imagen.

   ![new-entity](assets/new-entity.png)

A continuación, puede agregar propiedades secundarias en objetos del modelo de datos independientes.

### Añadir propiedades secundarias {#child-properties}

El editor del modelo de datos de formulario permite crear propiedades secundarias en un objeto del modelo de datos. La propiedad cuando se crea no está enlazada a ninguna propiedad de un origen de datos. Posteriormente, puede enlazar la propiedad secundaria con otra propiedad del objeto del modelo de datos que la contiene.

Para crear una propiedad secundaria:

1. En un modelo de datos de formulario, seleccione un objeto de modelo de datos y toque **[!UICONTROL Crear propiedad secundaria]**.
1. En el cuadro de diálogo **[!UICONTROL Crear propiedad secundaria]**, especifique un nombre y un tipo de datos para la propiedad en los campos **[!UICONTROL Nombre]** y **[!UICONTROL Tipo]**, respectivamente. Opcionalmente, puede especificar un título y una descripción para la propiedad.
1. Active Calculado si la propiedad es una propiedad calculada. El valor de una propiedad calculada se evalúa en función de una regla o una expresión. Para obtener más información, consulte [Editar propiedades](#edit-properties).
1. Si el objeto del modelo de datos está enlazado a un origen de datos, la propiedad secundaria agregada se enlazará automáticamente a la propiedad del objeto del modelo de datos principal con el mismo nombre y tipo de datos.

   Para enlazar manualmente una propiedad secundaria con una propiedad de objeto de modelo de datos, toque el icono Examinar situado junto al campo **[!UICONTROL Referencia de enlace]**. El cuadro de diálogo **[!UICONTROL Seleccionar objeto]** lista todas las propiedades del objeto del modelo de datos principal. Seleccione una propiedad con la que enlazar y toque el icono de visto. Tenga en cuenta que sólo puede seleccionar una propiedad del mismo tipo de datos que la propiedad secundaria.

1. Toque **[!UICONTROL Listo]** para guardar la propiedad secundaria y toque **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario. La propiedad secundaria ahora se agrega al objeto del modelo de datos.

Una vez creados los objetos y las propiedades del modelo de datos, puede seguir creando formularios adaptables y comunicaciones interactivas basadas en el modelo de datos de formulario. Posteriormente, cuando tenga orígenes de datos disponibles y configurados, puede enlazar el modelo de datos de formulario con orígenes de datos. El enlace se actualizará automáticamente en formularios adaptables y comunicaciones interactivas asociados. Para obtener más información sobre la creación de formularios adaptables y comunicaciones interactivas mediante el modelo de datos de formulario, consulte [Uso del modelo de datos de formulario](/help/forms/using/using-form-data-model.md).

### Enlazar objetos y propiedades del modelo de datos {#bind-data-model-objects-and-properties}

Cuando los orígenes de datos que desea integrar con el modelo de datos de formulario están disponibles, puede agregarlos al modelo de datos de formulario como se describe en [Actualizar orígenes de datos](/help/forms/using/create-form-data-models.md#update). A continuación, haga lo siguiente para enlazar los objetos y las propiedades del modelo de datos sin enlazar:

1. En el modelo de datos de formulario, seleccione el origen de datos independiente que desea enlazar con un origen de datos.
1. Toque **[!UICONTROL Editar propiedades]**.
1. En el panel **[!UICONTROL Editar propiedades]**, toque el icono de exploración situado junto al campo **[!UICONTROL Enlace]**. Abre el cuadro de diálogo **[!UICONTROL Seleccionar objeto]** que lista los orígenes de datos agregados en el modelo de datos de formulario.

   ![select-object](assets/select-object.png)

1. Expanda el árbol de orígenes de datos y seleccione un objeto de modelo de datos para enlazar y tocar el icono de visto.
1. Toque **[!UICONTROL Listo]** para guardar las propiedades y, a continuación, toque **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario. El objeto del modelo de datos ahora está enlazado con un origen de datos. Observe que el objeto del modelo de datos ya no está marcado como Sin enlazar.

   ![bound-model-object](assets/bound-model-object.png)

## Configurar servicios {#configure-services}

Para leer y escribir datos para un objeto de modelo de datos, haga lo siguiente para configurar los servicios de lectura y escritura:

1. Seleccione la casilla de verificación situada en la parte superior de un objeto de modelo de datos para seleccionarlo y toque **[!UICONTROL Editar propiedades]**.

   ![edit-properties](assets/edit-properties.png)

   Editar propiedades para configurar servicios de lectura y escritura para un objeto de modelo de datos

   Se abre el cuadro de diálogo Editar propiedades.

   ![edit-properties-2](assets/edit-properties-2.png)

   Cuadro de diálogo Editar propiedades

   >[!NOTE]
   >
   >Además de los objetos y servicios del modelo de datos, el documento de metadatos del servicio OData incluye propiedades de navegación que definen la asociación entre dos objetos del modelo de datos. Cuando se agrega un origen de datos del servicio OData a un modelo de datos de formulario, hay un servicio disponible en el modelo de datos de formulario para todas las propiedades de navegación de un objeto de modelo de datos. Puede utilizar este servicio para leer las propiedades de navegación del objeto del modelo de datos correspondiente.
   >
   >
   >Para obtener más información sobre el uso del servicio, consulte [Uso de las propiedades de navegación de los servicios OData](#work-with-navigation-properties-of-odata-services).

1. Cambie **[!UICONTROL Objeto de nivel superior]** para especificar si el objeto del modelo de datos es un objeto de modelo de nivel superior.

   Los objetos del modelo de datos configurados en un modelo de datos de formulario están disponibles para su uso en la ficha Objetos del modelo de datos del navegador de contenido de un formulario adaptable basado en el modelo de datos de formulario. Cuando se agrega una asociación entre dos objetos del modelo de datos, el objeto del modelo de datos con el que se asocia se anida en el objeto del modelo de datos que se asocia en la ficha Objetos del modelo de datos. Si el modelo de datos anidado es un objeto de nivel superior, también aparecerá por separado en la ficha Objetos del modelo de datos. Por lo tanto, verá dos entradas del mismo, una dentro y otra fuera de la jerarquía anidada, lo que podría confundir a los autores de formularios. Para que el objeto del modelo de datos asociado aparezca solo en la jerarquía anidada, desactive la propiedad Objeto de nivel superior.

1. Seleccione Servicios de lectura y escritura para los objetos del modelo de datos seleccionado. Aparecen los argumentos de los servicios.

   ![read-write-services](assets/read-write-services.png)

   Servicios de lectura y escritura configurados para la fuente de datos de empleados

1. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) para que el argumento de servicio de lectura [enlace el argumento a un atributo de Perfil de usuario, atributo de solicitud o valor literal](#bindargument) y especifique el valor de enlace.
1. Toque **[!UICONTROL Listo]** para guardar el argumento, **[!UICONTROL Listo]** para guardar las propiedades y, a continuación, **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.

### Enlazar argumentos de servicio de lectura {#bindargument}

Enlace el argumento de servicio de lectura a un atributo de Perfil de usuario, un atributo de solicitud o un valor literal basado en un valor de enlace. El valor se pasa al servicio como un argumento para recuperar los detalles asociados con el valor especificado del origen de datos.

#### Valor literal {#literal-value}

Seleccione **[!UICONTROL Literal]** en el menú desplegable **[!UICONTROL Enlace a]** e introduzca un valor en el campo **[!UICONTROL Valor de enlace]**. Los detalles asociados con el valor se recuperan del origen de datos. Utilice esta opción para recuperar detalles asociados a un valor estático.

En este ejemplo, los detalles asociados con **4367655678**, como valor para el argumento `mobilenum`, se recuperan del origen de datos. Los detalles asociados si pasa el valor de un argumento de número móvil pueden incluir propiedades como nombre de cliente, dirección de cliente y ciudad.

![Valor literal](assets/fdm_binding_literal_new.png)

#### Atributo de perfil de usuario {#user-profile-attribute}

Seleccione **[!UICONTROL Atributo de Perfil de usuario]** en el menú desplegable **[!UICONTROL Enlace a]** e introduzca el nombre del atributo en el campo **[!UICONTROL Valor de enlace]**. Los detalles del usuario que ha iniciado sesión en la instancia de AEM se recuperan del origen de datos en función del nombre del atributo.

El nombre de atributo especificado en el campo **[!UICONTROL Valor de enlace]** debe incluir la ruta de enlace completa hasta el nombre de atributo del usuario. Abra la siguiente URL para acceder a los detalles del usuario en CRXDE:

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![Perfil de usuario](assets/binding_crxde_user_profile_new.png)

En este ejemplo, especifique `profile.empid` en el campo **[!UICONTROL Valor de enlace]** para el usuario `grios`.

![Editar argumento](assets/edit_argument_user_profile_new.png)

El argumento `id` toma el valor del atributo `empid` del perfil del usuario y lo pasa como argumento al servicio de lectura. Lee y devuelve valores de propiedades asociadas desde el objeto del modelo de datos de empleado para el `empid` asociado al usuario que ha iniciado sesión.

#### Solicitar atributo {#request-attribute}

Utilice el atributo request para recuperar las propiedades asociadas del origen de datos.

1. Seleccione **[!UICONTROL Solicitar atributo]** en el menú desplegable **[!UICONTROL Enlace a]** e introduzca el nombre del atributo en el campo **[!UICONTROL Valor de enlace]**.

1. Cree una [superposición](../../../help/sites-developing/overlays.md) para head.jsp. Para crear la superposición, abra CRX DE y copie el archivo `https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp` en `https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp`

   >[!NOTE]
   >
   > * Si utiliza una plantilla estática, superponga head.jsp en:
      >   `/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`
   > * Si utiliza una plantilla editable, superponga el archivo aftemplatedpage.jsp en:
      >   `/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp`


1. Establezca [!DNL paramMap] para el atributo de solicitud. Por ejemplo, incluya el siguiente código en el archivo .jsp de la carpeta de aplicaciones:

   ```javascript
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);
   ```

   Por ejemplo, utilice el código siguiente para recuperar el valor de petid del origen de datos:


   ```javascript
   <%Map paraMap = new HashMap();
   paraMap.put("petId",request.getParameter("petId"));
   request.setAttribute("paramMap",paraMap);%>
   ```

Los detalles se recuperan del origen de datos en función del nombre de atributo especificado en la solicitud.

Por ejemplo, si se especifica atributo como `petid=100` en la solicitud, se recuperarán las propiedades asociadas al valor de atributo del origen de datos.

## Añadir asociaciones {#add-associations}

Normalmente, hay asociaciones creadas entre objetos de modelo de datos en un origen de datos. La asociación puede ser uno a uno o uno a varios. Por ejemplo, puede haber varios dependientes asociados a un empleado. Se denomina asociación de uno a varios y `1:n` se describe en la línea que conecta los objetos del modelo de datos asociados. Sin embargo, si una asociación devuelve un nombre de empleado único para un ID de empleado determinado, se denomina asociación uno a uno.

Cuando se agregan objetos de modelo de datos asociados en un origen de datos a un modelo de datos de formulario, sus asociaciones se conservan y se muestran como conectadas por líneas de flecha. Puede agregar asociaciones entre objetos del modelo de datos en distintos orígenes de datos en un modelo de datos de formulario.

>[!NOTE]
>
>Las asociaciones predefinidas en un origen de datos JDBC no se conservan en el modelo de datos de formulario. Debe crearlos manualmente.

Para agregar una asociación:

1. Seleccione la casilla de verificación situada en la parte superior de un objeto de modelo de datos para seleccionarlo y toque **[!UICONTROL Añadir asociación]**. Se abre el cuadro de diálogo Añadir asociación.

   ![complemento-asociación](assets/add-association.png)

   >[!NOTE]
   >
   >Además de los objetos y servicios del modelo de datos, el documento de metadatos del servicio OData incluye propiedades de navegación que definen la asociación entre dos objetos del modelo de datos. Puede utilizar estas propiedades de navegación al agregar asociaciones en el Modelo de datos de formulario. Para obtener más información, consulte [Uso de las propiedades de navegación de los servicios OData](#work-with-navigation-properties-of-odata-services).

   Se abre el cuadro de diálogo Añadir asociación.

   ![add-union-2](assets/add-association-2.png)

   Cuadro de diálogo añadir asociación

1. En el panel Añadir asociación:

   * Especifique un título para la asociación.
   * Seleccione el tipo de asociación — Uno a Uno o Uno a Muchos.
   * Seleccione el objeto del modelo de datos con el que se va a asociar.
   * Seleccione el servicio de lectura para leer datos del objeto de modelo seleccionado. Se abre el argumento del servicio de lectura. Edite para cambiar el argumento, si es necesario, y enlace el argumento a la propiedad del objeto del modelo de datos que se va a asociar.

   En el ejemplo siguiente, el argumento predeterminado para el servicio de lectura del objeto del modelo de datos Dependents es `dependentid`.

   ![add-collection-example](assets/add-association-example.png)

   El argumento predeterminado para el servicio de lectura de dependientes depende

   Sin embargo, el argumento debe ser una propiedad común entre el objeto del modelo de datos asociado, que en este ejemplo es `Employeeid`. Por lo tanto, el argumento `Employeeid` debe enlazarse a la propiedad `id` del objeto del modelo de datos Empleado para recuperar los detalles de dependientes asociados del objeto del modelo de datos Dependientes.

   ![add-collection-example-2](assets/add-association-example-2.png)

   Argumento y enlace actualizados

   Toque **[!UICONTROL Listo]** para guardar el argumento.

1. Toque **[!UICONTROL Listo]** para guardar la asociación y luego **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.
1. Repita los pasos para crear más asociaciones según sea necesario.

>[!NOTE]
>
>La asociación agregada aparece en el cuadro de objetos del modelo de datos con el título especificado y una línea que conecta los objetos del modelo de datos asociados.
>
>Puede editar una asociación si selecciona la casilla de verificación correspondiente y toca **[!UICONTROL Editar asociación]**.

![added-union](assets/added-association.png)

## Editar propiedades {#properties}

Puede editar las propiedades de los objetos del modelo de datos, sus propiedades y los servicios agregados en el modelo de datos de formulario.

Para editar las propiedades:

1. Active la casilla de verificación situada junto a un objeto de modelo de datos, una propiedad o un servicio en el modelo de datos de formulario.
1. Toque **[!UICONTROL Editar propiedades]**. Se abre el panel **[!UICONTROL Editar propiedades]** para el objeto, la propiedad o el servicio del modelo seleccionado.

   * **Objeto** del modelo de datos: Especifique los servicios de lectura y escritura y edite los argumentos.
   * **Propiedad**: Especifique el tipo, subtipo y formato de la propiedad. También puede especificar si la propiedad seleccionada es la clave principal del objeto del modelo de datos.
   * **Servicio**: Especifique el objeto del modelo de entrada, el tipo de salida y los argumentos del servicio. Para un servicio Get, puede especificar si se espera que devuelva una matriz.

   ![edit-properties-service](assets/edit-properties-service.png)

   Cuadro de diálogo Editar propiedades para obtener un servicio

1. Toque **[!UICONTROL Listo]** para guardar las propiedades y luego **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.

### Crear propiedades calculadas {#computed}

Una propiedad calculada es aquella cuyo valor se calcula en función de una regla o una expresión. Mediante una regla, puede establecer el valor de una propiedad calculada en una cadena literal, un número, un resultado de una expresión matemática o el valor de otra propiedad en el modelo de datos de formulario.

Por ejemplo, puede crear una propiedad calculada **FullName** cuyo valor sea el resultado de la concatenación de las propiedades **FirstName** y **LastName** existentes. Para ello:

1. Cree una nueva propiedad con el nombre `FullName` cuyo tipo de datos sea String.
1. Habilite **[!UICONTROL Calculado]** y toque **[!UICONTROL Listo]** para crear la propiedad.

   ![computado](assets/computed.png)

   Se crea la propiedad calculada FullName. Observe el icono situado junto a la propiedad para mostrar una propiedad calculada.

   ![computed-prop](assets/computed-prop.png)

1. Seleccione la propiedad FullName y toque **[!UICONTROL Editar regla]**. Se abre una ventana del editor de reglas.
1. En la ventana del editor de reglas, toque **[!UICONTROL Crear]**. Se abre una ventana de regla **[!UICONTROL Establecer valor]**.

   En la lista desplegable Seleccionar opción, seleccione **[!UICONTROL Expresión matemática]**. Otras opciones disponibles son **[!UICONTROL Objeto del modelo de datos de formulario]** y **[!UICONTROL Cadena]**.

1. En la expresión matemática, seleccione **[!UICONTROL FirstName]** y **[!UICONTROL LastName]** en los objetos primero y segundo, respectivamente. Seleccione **[!UICONTROL plus]** como operador.

   Toque **[!UICONTROL Listo]** y luego toque **[!UICONTROL Cerrar]** para cerrar la ventana del editor de reglas. La regla tiene un aspecto similar al siguiente.

   ![regla](assets/rule.png)

1. En el modelo de datos de formulario, toque **[!UICONTROL Guardar]**. La propiedad calculada está configurada.

## Trabajar con las propiedades de navegación de los servicios de OData {#work-with-navigation-properties-of-odata-services}

En los servicios OData, las propiedades de navegación se utilizan para definir asociaciones entre dos objetos del modelo de datos. Estas propiedades se definen en un tipo de entidad o un tipo complejo. Por ejemplo, en el siguiente extracto del archivo de metadatos de los servicios de muestra [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData, la entidad persona contiene tres propiedades de navegación: Amigos, BestFriend y Viajes.

Para obtener más información sobre las propiedades de navegación, consulte [documentación de OData](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536).

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

Al configurar un servicio OData en un modelo de datos de formulario, todas las propiedades de navegación de un contenedor de entidad están disponibles a través de un servicio en el modelo de datos de formulario. En este ejemplo del servicio TripPin OData, las tres propiedades de navegación del contenedor de entidad `Person` se pueden leer utilizando un servicio `GET LINK` en el Modelo de datos de formulario.

A continuación se resalta el servicio `GET LINK of Person /People` en el Modelo de datos de formulario, que es un servicio combinado para las tres propiedades de navegación en la entidad `Person` del servicio OData de TripPin.

![nav-prop-service](assets/nav-prop-service.png)

Una vez agregado el servicio `GET LINK` a la ficha Servicios del Modelo de datos de formulario, puede editar las propiedades para elegir el objeto del modelo de salida y la propiedad de navegación que se va a utilizar en el servicio. Por ejemplo, el siguiente servicio `GET LINK of Person /People` del ejemplo siguiente utiliza el viaje como objeto del modelo de salida y la propiedad navigation como Viajes.

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>Los valores disponibles en el campo **Valor predeterminado** del argumento **NavigationPropertyName** dependen del estado de la matriz **Return?** botón de alternancia. Cuando está activado, muestra las propiedades de navegación del tipo Colección.

En este ejemplo, también puede elegir el objeto del modelo de salida como argumento de propiedad Persona y navegación como Amigos o BestFriend (en función de si **Matriz de devolución?** está habilitado o deshabilitado).

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

Del mismo modo, puede elegir un servicio `GET LINK` y configurar sus propiedades de navegación al agregar asociaciones en el Modelo de datos de formulario. Sin embargo, para poder seleccionar una propiedad de navegación, asegúrese de que el campo **[!UICONTROL Enlace a]** está establecido en **Literal**.

![add-collection-nav-prop](assets/add-association-nav-prop.png)

## Generar y editar datos de muestra {#sample}

El editor del modelo de datos de formulario permite generar datos de ejemplo para todas las propiedades de objeto del modelo de datos, incluidas las propiedades calculadas, en un modelo de datos de formulario. Es un conjunto de valores aleatorios que cumplen el tipo de datos configurado para cada propiedad. También puede editar y guardar datos, que se conservan aunque vuelva a generar los datos de ejemplo.

Para generar y editar datos de ejemplo, haga lo siguiente:

1. Abra un modelo de datos de formulario y toque **[!UICONTROL Editar datos de ejemplo]**. Genera y muestra los datos de ejemplo en la ventana Editar datos de muestra.

   ![Generar datos de muestra](assets/form_data_model_generate_sample_data_new.png)

1. En la ventana **[!UICONTROL Editar datos de ejemplo]**, edite los datos según sea necesario y toque **[!UICONTROL Guardar]**.

A continuación, puede utilizar los datos de ejemplo para rellenar previamente y probar comunicaciones interactivas basadas en el modelo de datos de formulario. Para obtener más información, consulte [Uso del modelo de datos de formulario](/help/forms/using/using-form-data-model.md).

## Probar los objetos y servicios del modelo de datos {#test-data-model-objects-and-services}

El modelo de datos de formulario está configurado pero, antes de ponerlo en uso, es posible que desee probar si los objetos y servicios configurados del modelo de datos funcionan correctamente. Para probar los objetos y servicios del modelo de datos:

1. Seleccione un objeto de modelo de datos o un servicio en el modelo de datos de formulario y toque **[!UICONTROL Test Model Object]** o **[!UICONTROL Test Service]**, respectivamente.

   Se abre la ventana Probar modelo de datos de formulario.

   ![test-data-model](assets/test-data-model.png)

1. En la ventana Probar modelo de datos de formulario, seleccione el objeto o servicio del modelo de datos que se va a probar en el panel Entrada.

1. Especifique un valor de argumento en el código de prueba y toque **[!UICONTROL Prueba]**. Una prueba correcta devuelve el resultado en el panel Salida.

   ![Resultados de la prueba](assets/test_results_form_data_model_new.png)

Del mismo modo, se pueden probar otros objetos y servicios del modelo de datos en el modelo de datos de formulario.

## Validación automatizada de datos de entrada {#automated-validation-of-input-data}

El modelo de datos de formulario valida los datos recibidos como entrada al invocar la API DermisBridge (según los criterios de validación disponibles en el modelo de datos de formulario). La validación se basa en el indicador `ValidationOptions` establecido en el objeto de consulta que se utiliza para invocar la API.

El indicador se puede establecer en cualquiera de los siguientes valores:

* **COMPLETO**: FDM realiza la validación en función de todas las restricciones
* **DESACTIVADO**: Sin validación
* **BÁSICO**: FDM realiza la validación basándose en las restricciones &quot;requeridas&quot; y &quot;rellenables&quot;

Si no se establece ningún valor para el indicador `ValidationOptions`, la validación **BASIC** se realiza en los datos de entrada.

A continuación se muestra un ejemplo de cómo establecer el indicador de validación en **FULL**:

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>El valor que proporcione para un atributo en los datos de entrada debe coincidir con el tipo de datos definido para el atributo en el documento de metadatos.\
>Si el valor no coincide con el tipo de datos definido para el atributo, la API DermisBridge muestra una excepción independientemente del valor del indicador `ValidationOptions`. Si el nivel de registro está establecido en Debug, se registra un error en el archivo **error.log**.

El modelo de datos de formulario valida los datos de entrada en función de una lista de restricciones de tipo de datos. La lista de restricciones para los datos de entrada puede variar en función del origen de datos.

La siguiente tabla lista las restricciones de los datos de entrada en función del origen de datos:

<table>
 <tbody> 
  <tr> 
   <td>Restricciones</td> 
   <td>Descripción</td> 
   <td>Origen de datos de entrada</td> 
  </tr> 
  <tr> 
   <td>required</td> 
   <td>Si es true, el parámetro debe incluirse en los datos de entrada.</td> 
   <td>Swagger, WSDL y base de datos</td> 
  </tr> 
  <tr> 
   <td>NULL</td> 
   <td>Si es true, el valor del parámetro se puede establecer en Null en los datos de entrada.</td> 
   <td>WSDL, Odata y base de datos</td> 
  </tr> 
  <tr> 
   <td>máximo</td> 
   <td>Especifica el límite superior de los valores numéricos. El valor máximo especificado como límite superior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>mínimo</td> 
   <td>Especifica el límite inferior de los valores numéricos. El valor mínimo especificado como límite inferior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueMaximum</td> 
   <td>Especifica el límite superior de los valores numéricos. El valor máximo especificado como límite superior no debe asignarse al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueMinimum</td> 
   <td>Especifica el límite inferior de los valores numéricos. El valor mínimo especificado como límite inferior no debe asignarse al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>Especifica el límite inferior del número de caracteres incluidos en una cadena. El valor mínimo especificado como límite inferior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>Especifica el límite superior del número de caracteres incluidos en una cadena. El valor máximo especificado como límite superior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger, WSDL, Odata y base de datos</td> 
  </tr> 
  <tr> 
   <td>pattern</td> 
   <td>Especifica una secuencia fija de caracteres. La cadena de entrada solo se valida correctamente si los caracteres se ajustan al patrón especificado.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>Especifica el número mínimo de elementos de una matriz. El valor mínimo especificado como límite inferior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>Especifica el número máximo de elementos de una matriz. El valor máximo especificado como límite superior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>Si es true, todos los elementos de la matriz deben ser únicos en los datos de entrada.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>enum (cadena)<br /> <br /> </td> 
   <td>Restringe el valor de un parámetro en los datos de entrada a un conjunto fijo de valores de cadena. Debe ser una matriz con al menos un elemento, donde cada elemento es único.</td> 
   <td>Swagger, WSDL y Odata</td> 
  </tr> 
  <tr> 
   <td>enum (número)<br /> <br /> </td> 
   <td>Restringe el valor de un parámetro en los datos de entrada a un conjunto fijo de valores numéricos. Debe ser una matriz con al menos un elemento, donde cada elemento es único.</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

En este ejemplo, los datos de entrada se validan según las restricciones máxima, mínima y requerida definidas en el archivo Swagger. Los datos de entrada cumplen los criterios de validación solo si el identificador de pedido está presente y su valor está entre 1 y 10.

```json
   parameters: [
   {
   name: "orderId",
   in: "path",
   description: "ID of pet that needs to be fetched",
   required: true,
   type: "integer",
   maximum: 10,
   minimum: 1,
   format: "int64"
   }
   ]
```

Se muestra una excepción si los datos de entrada no cumplen los criterios de validación. Si el nivel de registro está establecido en **Depurar**, se registra un error en el archivo **error.log**. Por ejemplo,

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## Próximos pasos {#next-steps}

Tiene un modelo de datos de formulario que ya está listo para su uso en formularios adaptables y flujos de trabajo de comunicaciones interactivos. Para obtener más información, consulte [Uso del modelo de datos de formulario](/help/forms/using/using-form-data-model.md).
