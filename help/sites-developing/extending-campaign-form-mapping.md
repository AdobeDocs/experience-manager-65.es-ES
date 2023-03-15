---
title: Creación de asignaciones de formularios personalizados
seo-title: Creating Custom Form Mappings
description: Al crear una tabla personalizada en Adobe Campaign AEM, es posible que desee crear un formulario en que se asigne a esa tabla personalizada en la que se cree una tabla personalizada.
seo-description: When you create a custom table in Adobe Campaign, you may want to build a form in AEM that maps to that custom table
uuid: f3bde513-6edb-4eb6-9048-40045ee08c4a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d5dac1db-2dde-4b75-a31b-e057b447f6e2
exl-id: bce6c586-9962-4217-82cb-c837e479abc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 3%

---

# Creación de asignaciones de formularios personalizados{#creating-custom-form-mappings}

Al crear una tabla personalizada en Adobe Campaign AEM, es posible que desee crear un formulario en que se asigne a esa tabla personalizada.

Este documento describe cómo crear asignaciones de formularios personalizadas. Cuando complete los pasos de este documento, proporcionará a los usuarios una página de evento en la que podrán registrarse en un evento próximo. A continuación, puede realizar un seguimiento con estos usuarios a través de Adobe Campaign.

## Requisitos previos {#prerequisites}

Debe tener instalado lo siguiente:

* Adobe Experience Manager
* Adobe Campaign Classic

Consulte [AEM Integración de los usuarios de con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) para obtener más información.

## Creación de asignaciones de formularios personalizados {#creating-custom-form-mappings-2}

Para crear asignaciones de formularios personalizadas, debe seguir estos pasos de alto nivel, que se describen en detalle en las secciones siguientes:

1. Cree una tabla personalizada.
1. Ampliación de la **semilla** tabla.
1. Cree una asignación personalizada.
1. Cree una entrega basado en la asignación personalizada.
1. AEM Genere el formulario en, que utilizará la entrega creada en el momento de la entrega.
1. Envíe el formulario para probarlo.

### Creación de la tabla personalizada en Adobe Campaign {#creating-the-custom-table-in-adobe-campaign}

Comience creando una tabla personalizada en Adobe Campaign. En este ejemplo, se utiliza la siguiente definición para crear una tabla de eventos:

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

Después de crear la tabla de eventos, ejecute el **Actualizar asistente de estructura de base de datos** para crear la tabla.

### Ampliación de la tabla semilla {#extending-the-seed-table}

En Adobe Campaign, pulse o haga clic en **Añadir** para crear una nueva extensión de **Direcciones semilla (nms)** tabla.

![chlimage_1-194](assets/chlimage_1-194.png)

Ahora, utilice los campos del **evento** tabla para ampliar el **semilla** tabla:

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

Después de esto, ejecute **Actualizar asistente de base de datos** para aplicar los cambios.

### Creación de asignaciones de destino personalizadas {#creating-custom-target-mapping}

Entrada **Administración/Administración de campañas** t, vaya a **Asignaciones de destino** y agregue una nueva **Asignación de destino.**

>[!NOTE]
>
>Asegúrese de utilizar un nombre significativo para **Nombre interno**.

![chlimage_1-195](assets/chlimage_1-195.png)

### Creación de una plantilla de envíos personalizada {#creating-a-custom-delivery-template}

En este paso, se añade una plantilla de envío que utiliza el **Asignación de destino**.

Entrada **Recursos/Plantillas** AEM , vaya a la plantilla de envío y duplique la entrega de la aplicación existente en el mercado de trabajo Al hacer clic en **Hasta**, seleccione el evento create **Asignación de destino**.

![chlimage_1-196](assets/chlimage_1-196.png)

### AEM Creación del formulario en la {#building-the-form-in-aem}

AEM En, asegúrese de que ha configurado un Cloud Service en **Propiedades de página**.

A continuación, en la **Adobe Campaign** pestaña, seleccione la entrega que se creó en [Creación de una plantilla de envíos personalizada](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

Al configurar los campos, asegúrese de especificar nombres de elemento únicos para los campos de formulario.

Una vez configurados los campos, debe cambiar manualmente la asignación.

En CRXDE-lite, vaya a **jcr:contenido** (de la página) y cambie el **acMapping** al nombre interno de la variable **Asignación de destino**.

![chlimage_1-198](assets/chlimage_1-198.png)

En la configuración del formulario, asegúrese de marcar la casilla para crear si no existe

![chlimage_1-199](assets/chlimage_1-199.png)

### Enviar el formulario {#submitting-the-form}

Ahora puede enviar el formulario y validar en Adobe Campaign si los valores se han guardado.

![chlimage_1-200](assets/chlimage_1-200.png)

## Solución de problemas {#troubleshooting}

**&quot;Tipo no válido para el valor &#39;02/02/2015&#39; del elemento &#39;@eventdate&#39; (documento de tipo &#39;Event ([adb:evento])&#39;)&quot;**

Al enviar el formulario, este error se registra en **error.log** AEM en la.

Esto se debe a un formato no válido para el campo de fecha. La solución es proporcionar **aaaa-mm-dd** como el valor.
