---
title: Personalización del seguimiento de sucesos de formulario
seo-title: Personalización del seguimiento de sucesos de formulario
description: Si un usuario emplea más de 60 segundos en un campo, se activa un evento de visita de campo y los detalles del campo se envían a Adobe SiteCatalyst.
seo-description: Si un usuario emplea más de 60 segundos en un campo, se activa un evento de visita de campo y los detalles del campo se envían a Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
translation-type: tm+mt
source-git-commit: dfa983db4446cbb0cbdeb42297248aba55b3dffd

---


# Personalización del seguimiento de sucesos de formulario {#customizing-form-event-tracking}

De forma predeterminada, los siguientes eventos se rastrean en un formulario adaptable habilitado para análisis:

<table>
 <tbody>
  <tr>
   <th>Evento</th>
   <th>Variables disponibles</th>
  </tr>
  <tr>
   <td>procesar</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>abandono</td>
   <td>formName, formTitle, formInstance, panelName, panelTitle</td>
  </tr>
  <tr>
   <td>save</td>
   <td>formName, formTitle, formInstance, panelName, source</td>
  </tr>
  <tr>
   <td>submit</td>
   <td>formName, formTitle, formInstance, source</td>
  </tr>
  <tr>
   <td>error</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>ayuda</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName, formTitle, fieldName, fieldTitle, panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName, formTitle, panelName, panelTitle</td>
  </tr>
 </tbody>
</table>

## Personalización del tiempo de espera del evento de visita de campo {#customizing-the-field-visit-event-timeout}

En la configuración de formulario predeterminada de AEM, si un usuario emplea más de 60 segundos en un campo, se activa un `fieldvisit` evento y los detalles del campo se envían a Adobe Analytics. Puede personalizar la línea de base del seguimiento de tiempo de campo en Configuración de AEM Forms Analytics en la consola de configuración de AEM (/system/console/configMgr) para aumentar o reducir el límite de tiempo de espera.

## Personalización de los eventos de seguimiento {#customizing-the-tracking-events}

Puede modificar la `trackEvent`función disponible en el `/libs/afanalytics/js/custom.js` archivo para personalizar el seguimiento de eventos. Siempre que un suceso que se esté rastreando se produzca en un formulario adaptable, se llamará a la `trackEvent`función. La `trackEvent` función acepta dos parámetros: `eventName`y `variableValueMap`.

Puede evaluar el valor de los argumentos *eventName* y *variableValueMap* para cambiar el comportamiento de seguimiento de los eventos. Por ejemplo, puede elegir enviar la información al servidor de Analytics después de que se produzca un determinado número de eventos de error. También puede elegir realizar cualquiera de las siguientes personalizaciones:

* Puede establecer una hora de umbral antes de enviar el evento.
* Puede mantener un estado para decidir la acción; por ejemplo, *fieldVisit* genera un evento ficticio basado en la marca de tiempo del último evento.
* Puede utilizar la `pushEvent` función para enviar el evento al servidor de Analytics *.*

* Puede optar por no insertar el evento en el servidor de Analytics.

### Ejemplo {#sample}

En el siguiente ejemplo, se mantiene el estado del evento de *error* de cada atributo *fieldName* . El evento se envía al servidor de Analytics solo si se vuelve a producir un error.

```
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalización del evento panelvisit {#customizing-the-panelvisit-event}

En la configuración predeterminada de AEM Forms, cada 60 segundos se comprueba si la ventana que contiene el formulario adaptable está activa. Si la ventana está activa, se activa un `panelVisit`evento en Adobe Analytics. Ayuda a comprobar que el documento o el formulario están activos y a calcular el tiempo empleado en el formulario o documento correspondiente.

>[!NOTE]
>
>El nombre del evento que se utiliza para determinar la actividad y calcular el tiempo empleado es &quot;panelVisit&quot;. Este evento es diferente del evento de visita del panel que se enumera en la tabla anterior.

Puede modificar la función scheduleHeartBeatCheck disponible en el `/libs/afanalytics/js/custom.js` archivo para cambiar o detener este evento enviado a Adobe Analytics a intervalos regulares.
