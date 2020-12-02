---
title: Registrar una transacción para implementaciones personalizadas
seo-title: Registrar una transacción para implementaciones personalizadas
description: Utilice la API TransactionRecorder para registrar automáticamente las acciones que no se contabilizan como transacciones
seo-description: Utilice la API TransactionRecorder para registrar automáticamente las acciones que no se contabilizan como transacciones
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Registrar una transacción para implementaciones personalizadas {#record-a-transaction-for-custom-implementations}

Utilice la API TransactionRecorder para registrar automáticamente las acciones que no se contabilizan como transacciones

Puede utilizar un código personalizado para enviar un formulario PDF, enviar la URL de previsualización de la interfaz de usuario del agente a los usuarios finales para realizar la previsualización de una comunicación interactiva o enviar un formulario mediante métodos personalizados en lugar de utilizar métodos de envío proporcionados con AEM Forms. Todas las acciones y las implementaciones personalizadas de las API de AEM Forms mencionadas anteriormente no se contabilizan como transacciones. AEM Forms proporciona una API, [TransactionRecorder](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), para registrar acciones como transacciones.

Para registrar una transacción, escriba el [servlet sling estándar](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html) y llame al servlet desde un cliente para registrar una transacción. Puede llamar al servlet mediante AJAX o cualquier otro método estándar.

## Ejemplo de código de servidor {#sample-server-sided-code}

Puede utilizar el código de muestra siguiente para ejecutar la API TransactionRecorder desde una clase JAVA mediante un paquete OSGi personalizado.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Ejemplo de código de cliente {#sample-client-side-code}

Puede utilizar el código de muestra siguiente para llamar al servlet que tiene la API `TransactionRecorder`.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Artículos relacionados {#related-articles}

* [Información general sobre los informes de transacciones](/help/forms/using/transaction-reports-overview.md)
* [Visualización y comprensión de los informes de transacciones](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [Informes de transacciones API facturables](/help/forms/using/transaction-reports-billable-apis.md)

