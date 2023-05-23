---
title: Registrar una transacción para implementaciones personalizadas
seo-title: Record a transaction for custom implementations
description: Utilice la API TransactionRecorder para registrar acciones que no se contabilizan como transacciones automáticamente.
seo-description: Use the TransactionRecorder API to record actions which are not accounted as transactions automatically
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
exl-id: a1d97b15-14a6-4c3d-bdd3-6366f7acdfc8
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 56%

---

# Registrar una transacción para implementaciones personalizadas {#record-a-transaction-for-custom-implementations}

Utilice la API TransactionRecorder para registrar acciones que no se contabilizan como transacciones automáticamente.

Puede utilizar el código personalizado para enviar un formulario de PDF o enviar la URL de la vista previa de la interfaz de usuario del agente a los usuarios finales para previsualizar una comunicación interactiva. O bien, envía un formulario mediante métodos personalizados en lugar de utilizar los métodos de envío proporcionados con AEM Forms. Ninguna de las acciones e implementaciones personalizadas de las API de AEM Forms mencionadas anteriormente se contabiliza como una transacción. AEM Forms proporciona una API, [TransactionRecorder](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), para registrar dichas acciones como transacciones.

Para registrar una transacción, escriba el [servlet estándar de sling](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=en) y llame a dicho servlet desde un cliente para registrar una transacción. Puede llamar al servlet mediante AJAX o mediante cualquier otro método estándar.

## Código de ejemplo del lado del servidor {#sample-server-sided-code}

Puede utilizar el siguiente código de ejemplo para ejecutar la API TransactionRecorder desde una clase Java™ mediante un paquete OSGi personalizado.

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

## Ejemplo de código del lado del cliente {#sample-client-side-code}

Puede utilizar el siguiente código de ejemplo para llamar al servlet que tiene la API `TransactionRecorder`.

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
* [Ver y comprender los informes de transacciones](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [API facturables de informes de transacciones](/help/forms/using/transaction-reports-billable-apis.md)
