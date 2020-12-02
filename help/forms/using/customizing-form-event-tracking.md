---
title: Personalización del seguimiento del evento de formularios
seo-title: Personalización del seguimiento del evento de formularios
description: Si un usuario invierte más de 60 segundos en un campo, se activa un evento de visita de campo y los detalles del campo se envían a Adobe SiteCatalyst.
seo-description: Si un usuario invierte más de 60 segundos en un campo, se activa un evento de visita de campo y los detalles del campo se envían a Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Personalización del seguimiento del evento de formularios {#customizing-form-event-tracking}

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

## Personalización del tiempo de espera de evento de visita de campo {#customizing-the-field-visit-event-timeout}

En la configuración de formulario AEM predeterminada, si un usuario emplea más de 60 segundos en un campo, se activa un evento `fieldvisit` y se envían los detalles del campo a Adobe Analytics. Puede personalizar la línea base de seguimiento de tiempo de campo en Configuración de AEM Forms Analytics en AEM consola de configuración (/system/console/configMgr) para aumentar o reducir el límite de tiempo de espera.

## Personalización de los eventos de seguimiento {#customizing-the-tracking-events}

Puede modificar la función `trackEvent`disponible en el archivo `/libs/afanalytics/js/custom.js` para personalizar el seguimiento de evento. Siempre que un evento que se rastrea se produce en un formulario adaptable, se llama a la función `trackEvent`. La función `trackEvent` acepta dos parámetros: `eventName`y `variableValueMap`.

Puede evaluar el valor de los argumentos *eventName* y *variableValueMap* para cambiar el comportamiento de seguimiento de los eventos. Por ejemplo, puede elegir enviar la información al servidor de Analytics después de que se produzca un determinado número de eventos de error. También puede elegir realizar cualquiera de las siguientes personalizaciones:

* Puede establecer un tiempo de umbral antes de enviar el evento.
* Puede mantener un estado para decidir la acción; por ejemplo, *fieldVisit* inserta un evento ficticio basado en la marca de tiempo del último evento.
* Puede utilizar la función `pushEvent` para enviar el evento al servidor de análisis *.*

* Puede optar por no insertar el evento en el servidor de Analytics.

### Muestra {#sample}

En el siguiente ejemplo, se mantiene el estado del evento *error* de cada atributo *fieldName*. El evento se envía al servidor de Analytics solo si se vuelve a producir un error.

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## Personalización del evento panelvisit {#customizing-the-panelvisit-event}

En la configuración predeterminada de AEM Forms, cada 60 segundos se comprueba si la ventana que contiene el formulario adaptable está activa. Si la ventana está activa, se activa un evento `panelVisit`en Adobe Analytics. Ayuda a comprobar que el documento o el formulario están activos y a calcular el tiempo empleado en el formulario o documento correspondiente.

>[!NOTE]
>
>El nombre del evento utilizado para obtener actividad y calcular el tiempo empleado es &quot;panelVisit&quot;. Este evento es diferente del evento de visitas del panel que se muestra en la tabla que se muestra arriba.

Puede modificar la función scheduleHeartBeatCheck disponible en el archivo `/libs/afanalytics/js/custom.js` para cambiar o detener este evento enviado a Adobe Analytics a intervalos regulares.
