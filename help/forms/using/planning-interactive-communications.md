---
title: '"Tutorial: Planificar la comunicación interactiva"'
seo-title: Planifique la comunicación interactiva
description: Planifique la anatomía para su comunicación interactiva
seo-description: Planifique la anatomía para su comunicación interactiva
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
translation-type: tm+mt
source-git-commit: 1449ce9aba3014b13421b32db70c15ef09967375

---


# Tutorial: Planificar la comunicación interactiva {#tutorial-plan-the-interactive-communication}

Planifique la anatomía para su comunicación interactiva

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Este tutorial es un paso en la [serie Crear una primera comunicación](/help/forms/using/create-your-first-interactive-communication.md) interactiva. Se recomienda seguir la serie en secuencia cronológica para comprender, realizar y demostrar el caso de uso completo del tutorial.

El primer paso en la planificación de una comunicación interactiva es finalizar el contenido de la comunicación interactiva. Los expertos en la materia de departamentos como legal, financiero, de asistencia o marketing pueden ayudarle a finalizar el contenido. Una vez finalizado el contenido, debe analizarlo para identificar los distintos tipos de recursos necesarios para crear la comunicación interactiva.

## Consideraciones de planificación {#planning-considerations}

Una comunicación interactiva incluye los siguientes elementos:

* **El texto** estático incluye principalmente las partes de la comunicación interactiva que son de naturaleza genérica y están incluidas en la comunicación con todos los clientes. Por ejemplo, encabezado, pie de página, saludo o renuncia de responsabilidad.
* **Los datos procedentes de un sistema back-end (modelo de datos de formulario)** son específicos del cliente y se combinan dinámicamente con la comunicación interactiva. Por ejemplo, el número de directiva o la dirección se pueden originar utilizando el modelo de datos de formulario.
* **Maquetación o plantillas** para la versión impresa y web de la Comunicación interactiva.
* **Orden** en el que aparecen los distintos párrafos de texto en la Comunicación interactiva.
* **Datos introducidos por un empleado de primera línea (IU del agente)** que está personalizando la comunicación antes de enviarla. Por ejemplo, la fecha de vencimiento del pago.

* **Datos** condicionales que se rellenan en función de condiciones predefinidas. Por ejemplo, la fecha en que se genera la comunicación interactiva.
* **Imágenes almacenadas en un repositorio**, como logotipos e imágenes de firma. Imágenes como logotipos corporativos aparecerían en la mayoría o en toda la comunicación interactiva.
* **Tablas** y gráficos necesarios para simplificar la representación de datos complejos en una comunicación interactiva

## Anatomía de la comunicación interactiva {#anatomy-of-the-interactive-communication}

Una vez que haya finalizado el contenido y los elementos utilizados para crear la comunicación interactiva, puede crear una anatomía de la comunicación interactiva. La anatomía debe tener los detalles enumerados en la sección Consideraciones [de](/help/forms/using/planning-interactive-communications.md#planning-considerations) planificación. Según nuestro caso de uso, el siguiente es un ejemplo de anatomía de la factura mensual que un operador de telecomunicaciones envía a sus clientes.

La anatomía incluye datos con los siguientes modos de entrada:

* Texto estático
* Modelo de datos de formulario
* IU del agente
* Datos condicionales
* Imágenes

En cada sección, el texto en negrita representa texto estático. La base de datos incluye tablas de cliente, facturas y llamadas. Un modelo de datos de formulario puede recibir datos de cualquiera de estas tablas. Para obtener más información, consulte [Creación de un modelo](/help/forms/using/create-form-data-model0.md)de datos de formulario.

La siguiente tabla ilustra la fuente de datos de cada campo de la anatomía de la comunicación interactiva:

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
   <td><p>Nº de factura</p> <p>Fecha de facturación</p> <p>Período de facturación</p> <p>Su plan</p> </td>
   <td><p>Valor del <strong>campo </strong>Plan</p> <p>Tabla - cliente</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Nº de factura</li>
     <li>Fecha de facturación</li>
     <li>Período de facturación</li>
    </ul> <p> </p> </td>
   <td>--</td>
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
    </ul> <p>Tabla - cliente</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Lugar de suministro</li>
     <li>Código de estado</li>
     <li>Número de conexiones</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Resumen de facturación</td>
   <td><p>Saldo anterior</p> <p>Pagos</p> <p>Ajustes</p> <p>Cargos en el período de facturación actual</p> <p>Importe pendiente</p> <p>Fecha de vencimiento</p> </td>
   <td><p>Valor del campo <strong>Cargos del período de facturación actual </strong></p> <p>Tabla - facturas</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Saldo anterior</li>
     <li>Pagos</li>
     <li>Ajustes</li>
     <li>Importe pendiente</li>
     <li>Fecha de vencimiento</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Resumen de los cargos</td>
   <td><p>Cargos de llamadas</p> <p>Cargos de llamada de conferencia</p> <p>Gastos por SMS </p> <p>Cargos por Internet móvil</p> <p>Cargos de itinerancia nacionales</p> <p>Cargos de itinerancia internacionales</p> <p>Cargos por servicios de valor agregado</p> <p>Cargos totales</p> <p>TOTAL PAGABLE</p> <p>Condición en el campo Cargos de servicios de valor agregado</p> </td>
   <td><p>Valores de los campos siguientes:</p>
    <ul>
     <li>Cargos de llamadas</li>
     <li>Cargos de llamada de conferencia</li>
     <li>Gastos por SMS </li>
     <li>Cargos por Internet móvil</li>
     <li>Cargos de itinerancia nacionales</li>
     <li>Cargos de itinerancia internacionales</li>
     <li>Cargos por servicios de valor agregado</li>
     <li>Cargos totales (uso recargos calculados, campo)</li>
     <li>TOTAL PAGABLE (uso recargas calculadas, campo)</li>
    </ul> <p>Tabla - facturas</p> </td>
   <td>No hay campos</td>
   <td>--</td>
  </tr>
  <tr>
   <td>Llamadas por elementos: Salientes</td>
   <td><p>Nombres de columna:</p>
    <ul>
     <li>Fecha</li>
     <li>Hora</li>
     <li>Número</li>
     <li>Duración</li>
     <li>Cargos</li>
    </ul> </td>
   <td><p>Todos los valores</p> <p>Tabla: llamadas</p> </td>
   <td>No hay campos</td>
   <td>--</td>
  </tr>
  <tr>
   <td>Pagar ahora</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>Servicios de valor agregado</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>

