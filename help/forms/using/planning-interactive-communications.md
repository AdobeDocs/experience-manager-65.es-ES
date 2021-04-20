---
title: '"Tutorial: Planificar la comunicación interactiva"'
seo-title: Planificar la comunicación interactiva
description: Planifique la anatomía para su comunicación interactiva
seo-description: Planifique la anatomía para su comunicación interactiva
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 3%

---


# Tutorial: Planifique la comunicación interactiva {#tutorial-plan-the-interactive-communication}

Planifique la anatomía para su comunicación interactiva

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Este tutorial es un paso de la serie [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) . Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

El primer paso en la planificación de una comunicación interactiva es finalizar el contenido de la comunicación interactiva. Expertos en temas de departamentos como legal, financiero, de asistencia o marketing pueden ayudarle a finalizar el contenido. Una vez finalizado el contenido, debe analizarlo para identificar los distintos tipos de recursos necesarios para crear la comunicación interactiva.

## Consideraciones de planificación {#planning-considerations}

Una comunicación interactiva incluye los siguientes elementos:

* **El** texto estático incluye principalmente las partes de la comunicación interactiva que son de naturaleza genérica y están incluidas en la comunicación con todos los clientes. Por ejemplo, encabezado, pie de página, saludo o renuncia de responsabilidad.
* **Los datos procedentes de un sistema back-end (modelo de datos de formulario)**  son específicos del cliente y se combinan dinámicamente con la comunicación interactiva. Por ejemplo, el número de directiva o la dirección pueden obtenerse utilizando el modelo de datos de formulario.
* **Diseño o** plantillas para la versión impresa y web de la comunicación interactiva.
* **** Orden en que aparecen los distintos párrafos de texto en la comunicación interactiva.
* **Datos introducidos por un empleado de primera línea (interfaz de usuario del agente)**  que está personalizando la comunicación antes de enviarla. Por ejemplo, la fecha de vencimiento del pago.

* **Los** datos condicionales que se rellenan en función de condiciones predefinidas. Por ejemplo, la fecha en la que se genera la comunicación interactiva.
* **Imágenes almacenadas en un repositorio**, como logotipos e imágenes de firma. Imágenes como logotipos corporativos aparecerían en la mayoría o en toda la comunicación interactiva.
* **Gráficos y** tablas necesarios para simplificar la representación de datos complejos en una comunicación interactiva

## Anatomía de la comunicación interactiva {#anatomy-of-the-interactive-communication}

Una vez finalizado el contenido y los elementos utilizados para crear la comunicación interactiva, puede crear una anatomía de la comunicación interactiva. La anatomía debe tener los detalles enumerados en la sección [Consideraciones de planificación](/help/forms/using/planning-interactive-communications.md#planning-considerations). En función de nuestro caso de uso, el siguiente es un ejemplo de una anatomía de la factura mensual que un operador de telecomunicaciones envía a sus clientes.

La anatomía incluye datos con los siguientes modos de entrada:

* Texto estático
* Modelo de datos de formulario
* IU del agente
* Datos condicionales
* Imágenes

En cada sección, el texto en negrita representa texto estático. La base de datos incluye tablas cliente, facturas y llamadas. Un modelo de datos de formulario puede recibir datos de cualquiera de estas tablas. Para obtener más información, consulte [Crear modelo de datos de formulario](/help/forms/using/create-form-data-model0.md).

La siguiente tabla ilustra la fuente de datos de cada campo en la anatomía de la comunicación interactiva:

<table>
 <tbody>
  <tr>
   <td>Sección</td>
   <td>Texto estático</td>
   <td>FDM </td>
   <td>IU del agente</td>
   <td>Imágenes</td>
  </tr>
  <tr>
   <td>Detalles de la factura</td>
   <td><p>Nº de factura</p> <p>Fecha de factura</p> <p>Período de facturación</p> <p>Su plan</p> </td>
   <td><p>Valor del campo <strong>Your Plan </strong>1</p> <p>Tabla: cliente</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Nº de factura</li>
     <li>Fecha de factura</li>
     <li>Período de facturación</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Detalles del cliente</td>
   <td><p>Lugar de suministro</p> <p>Código de estado</p> <p>Número de móvil</p> <p>Número de contacto alternativo</p> <p>Número de relación</p> <p>Número de conexiones</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Nombre</li>
     <li>Dirección</li>
     <li>Número de móvil</li>
     <li>Número de contacto alternativo</li>
     <li>Número de relación</li>
    </ul> <p>Tabla: cliente</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Lugar de suministro</li>
     <li>Código de estado</li>
     <li>Número de conexiones</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Resumen de facturación</td>
   <td><p>Saldo anterior</p> <p>Pagos</p> <p>Ajustes</p> <p>Cargos período de factura actual</p> <p>Importe vencido</p> <p>Fecha de vencimiento</p> </td>
   <td><p>Valor para el campo <strong>Cargos período de factura actual </strong></p> <p>Tabla - Letras</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Saldo anterior</li>
     <li>Pagos</li>
     <li>Ajustes</li>
     <li>Importe vencido</li>
     <li>Fecha de vencimiento</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Resumen de gastos</td>
   <td><p>Cargos de llamada</p> <p>Cargos por llamada de conferencia</p> <p>Cargos por SMS </p> <p>Cargos por Internet móvil</p> <p>Cargos de itinerancia nacionales</p> <p>Cargos de itinerancia internacionales</p> <p>Cargos por servicios de valor agregado</p> <p>Cargos totales</p> <p>TOTAL PAGADO</p> <p>Condición en el campo Cargos de servicios de valor añadido</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Cargos de llamada</li>
     <li>Cargos por llamada de conferencia</li>
     <li>Cargos por SMS </li>
     <li>Cargos por Internet móvil</li>
     <li>Cargos de itinerancia nacionales</li>
     <li>Cargos de itinerancia internacionales</li>
     <li>Cargos por servicios de valor agregado</li>
     <li>Cargos totales (campo calculado de recargos)</li>
     <li>TOTAL PAGO (campo calculado de recargos)</li>
    </ul> <p>Tabla - Letras</p> </td>
   <td>Sin campos</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Llamadas desglosadas: salientes</td>
   <td><p>Nombres de columna:</p>
    <ul>
     <li>Fecha</li>
     <li>Hora</li>
     <li>Número</li>
     <li>Duración</li>
     <li>Cargos</li>
    </ul> </td>
   <td><p>Todos los valores</p> <p>Tabla: llamadas</p> </td>
   <td>Sin campos</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Pagar ahora</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>Servicios de valor agregado</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>

