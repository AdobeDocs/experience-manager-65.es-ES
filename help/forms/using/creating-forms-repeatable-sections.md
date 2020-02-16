---
title: Creación de formularios con secciones repetibles
seo-title: Creación de formularios con secciones repetibles
description: Las secciones repetibles son paneles que se pueden agregar o quitar dinámicamente a un formulario.
seo-description: Las secciones repetibles son paneles que se pueden agregar o quitar dinámicamente a un formulario.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# Creación de formularios con secciones repetibles {#creating-forms-with-repeatable-sections}

Las secciones repetibles son paneles que se pueden agregar o eliminar dinámicamente a un formulario.

Por ejemplo, mientras solicita un trabajo, el buscador de trabajo proporciona detalles de trabajo anteriores, como el nombre de la empresa, la función, el proyecto y otra información. La información de todos los empleadores requiere secciones diferentes pero similares. En ese caso, el formulario de empleo proporciona una sección de empleadores y también ofrece la opción de agregar dinámicamente más secciones de ese tipo. Estas secciones, que se agregan dinámicamente, se denominan secciones repetibles.

Puede utilizar uno de los siguientes métodos para crear paneles repetitivos:

## Uso del Administrador de instancias mediante secuencias de comandos {#using-instance-manager-via-scripts-nbsp}

1. En el modo de edición, seleccione un panel y toque ![cmppr](assets/cmppr.png). En la barra lateral, en Propiedades, habilite **Hacer que el panel sea repetible**. Especifique los valores de los campos **[!UICONTROL Máximo]** y **[!UICONTROL Mínimo]** .

   El campo Máximo especifica el número máximo de veces que puede aparecer un panel en la página. Puede especificar -1 en el campo Número máximo para permitir que el panel aparezca por un número infinito de veces.

   El campo Mínimo especifica el número mínimo de veces que aparece un panel en el formulario. Si establece el campo Recuento mínimo en cero, más adelante puede eliminar todas las instancias mediante secuencias de comandos una vez finalizada la representación.

   >[!NOTE]
   >
   >Para crear un panel no repetible, defina el valor del campo Máximo y Mínimo en uno. El diseño de acordeón no admite -1 en el campo Número máximo. Puede especificar un número elevado para dar la noción de valor infinito.

1. El elemento principal del panel, que se va a repetir, debe contener botones de adición y eliminación para administrar las instancias de los paneles repetibles. Siga los pasos siguientes para insertar botones en el elemento principal y activar secuencias de comandos en los botones:

   1. Desde la barra lateral, arrastre y suelte un componente de botón en el elemento principal del panel. Seleccione el componente y toque ![edit-rules](assets/edit-rules.png). Las reglas del botón se abren en el editor de reglas.
   1. En la ventana Editor de reglas, haga clic en **Crear**.

      Seleccione Editor **visual** en la fila Objetos y funciones de formulario.

      1. En el área de regla, en CUÁNDO, seleccione el estado en el que **se hace clic**.
      1. En ENTONCES:

         * Para crear un botón de añadir panel, seleccione **Agregar instancia** y arrastre y suelte el panel mediante el panel ![de](assets/toggle-side-panel.png) alternancia o selecciónelo con el objeto **Colocar o selecciónelo aquí.**
         * Para crear un botón del panel Eliminar, seleccione **Quitar instancia** y arrastre y suelte el panel mediante el panel ![de](assets/toggle-side-panel.png) alternancia o selecciónelo con el objeto **Colocar o seleccione aquí.**
      Seleccione Editor **de código** en la fila Objetos y funciones de formulario. Haga clic en **Editar reglas** y en el área de código:

      * Para crear un botón de adición de panel, especifique `this.panel.instanceManager.addInstance()`
      * Para crear un botón del panel Eliminar, especifique `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`
      Haga clic en **Finalizado**.

      >[!NOTE]
      >
      >Si un campo pertenece a un panel repetible, no podrá acceder a él directamente utilizando su nombre en las secuencias de comandos. Para acceder al campo, especifique la instancia repetible a la que pertenece el campo mediante la `instances` API en `InstanceManager`. La sintaxis para utilizar la `instances` API en `InstanceManager` es:
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >Por ejemplo, se crea un formulario adaptable con un panel repetible que tiene un cuadro de texto. Al rellenar previamente el formulario con tres cuadros de texto repetibles, necesita el siguiente xml:
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >Para leer datos de AA1, especifique:
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >Para leer datos de AA2, especifique:
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >Para obtener más información, consulte: Clase: Instancias de InstanceManager#en la referencia [de la API de Java de](https://adobe.com/go/learn_aemforms_documentation_63)AEM Forms.

      >[!NOTE]
      >
      >Cuando se eliminan todas las instancias de un panel de un formulario adaptable, para agregar una instancia del panel eliminado, utilice la sintaxis _panelName para capturar el administrador de instancias del panel y utilice la API addInstance de instance manager para agregar la instancia eliminada. Por ejemplo, _panelName.addInstance(). Agrega una instancia del panel quitado.















## Uso del diseño de acordeón para el panel principal {#using-the-accordion-layout-for-the-parent-panel-nbsp}

Un panel tiene varias opciones de diseño. La opción de diseño de acordeón Layout tiene la compatibilidad lista para paneles repetibles. Realice los siguientes pasos en el panel repetible con la opción Diseño para el diseño acorde:

1. En el elemento principal del panel que se va a repetir, toque ![cmppr](assets/cmppr.png). Puede ver las propiedades en la barra lateral. En la lista desplegable **Diseño** , seleccione **Acordeón**.
1. En un panel, que se va a repetir, toque ![cmppr](assets/cmppr.png). Puede ver las propiedades del panel en la barra lateral. Active la ficha **Hacer que el panel sea repetible** y especifique el valor de los campos **Máximo** y **Mínimo** .

   Ahora puede utilizar los botones más (+) y eliminar ( ![eliminar panel](assets/delete-panel.png)) para agregar y quitar los paneles.

## Uso de subformularios de repetición de plantilla de formulario (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

El subformulario repetible es similar al de los paneles repetitivos en los formularios adaptables. En AEM Forms Designer, realice los siguientes pasos para crear un subformulario de repetición:

1. En la paleta Jerarquía, seleccione el subformulario principal del subformulario que desea que se repita.
1. En la paleta Objeto, haga clic en la ficha Subformulario y seleccione De posición variable en la lista Contenido.
1. Seleccione el subformulario que desea que se repita.
1. En la paleta Objeto, haga clic en la ficha Subformulario y seleccione De posición variable o De posición fija en la lista Contenido.
1. Haga clic en la ficha Enlace y seleccione Repetir subformulario para cada elemento de datos.
1. Para especificar el número mínimo de repeticiones, seleccione Mínimo y escriba un número en el cuadro correspondiente. Si la opción se ajusta a 0 y no se suministran datos para los objetos del subformulario en el momento de la combinación de datos, el subformulario no se coloca al procesar el formulario.
1. Para especificar el número máximo de repeticiones de subformulario, seleccione Máx. y escriba un número en el cuadro correspondiente. Si no especifica ningún valor en el cuadro Máx., el número de repeticiones de subformulario es ilimitado.
1. Para especificar un número definido de repeticiones de subformulario, independientemente de la cantidad de datos, seleccione la opción Recuento inicial y escriba un número en el cuadro correspondiente. Si se selecciona esta opción y no hay ningún dato disponible o existen menos entradas de datos que el valor especificado en Recuento inicial, las instancias vacías del subformulario aún se colocan en el formulario.
1. Agregue dos botones en el subformulario principal: uno para agregar instancias y otro para eliminar instancias de subformulario repetibles. Para ver los pasos detallados, consulte [Generar una acción](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Ahora, vincule la plantilla de formulario al formulario adaptable. Para ver los pasos detallados, consulte [Creación de un formulario adaptable basado en una plantilla](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Utilice los botones creados en el paso 9 para agregar y quitar subformularios.

El archivo .zip adjunto contiene un subformulario de ejemplo repetible.

[Obtener archivo](assets/samplerepeatablesubform.zip)

## Uso de la configuración repetida de un esquema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Puede crear paneles repetibles a partir de un esquema XML y de la propiedad minOccours &amp; maxOccurs de cualquier elemento de tipo complejo. Para obtener información detallada sobre el esquema XML, consulte [Creación de formularios adaptables utilizando el esquema XML como modelo](/help/forms/using/adaptive-form-xml-schema-form-model.md)de formulario.

En el código siguiente, el `SampleType`panel utiliza la propiedad minOccours &amp; maxOccurs.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Para una presentación no acordadana, utilice componentes de botón de formulario adaptable para agregar y quitar instancias.
