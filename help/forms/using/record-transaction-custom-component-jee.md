---
title: Registre una transacción para la API de componente personalizada para AEM Forms en JEE.
description: Obtenga información acerca del uso de la API TransactionRecorder para registrar transacciones de componentes personalizados.
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Registre una transacción para las API de componentes personalizadas para AEM Forms en JEE {#record-a-transaction-for-custom-components}

Al utilizar API facturables en el componente personalizado, puede habilitar la creación de informes de transacciones para el componente. Para habilitar los informes de transacciones, modifique la `component.xml` del componente y añada la etiqueta que se indica a continuación en la operación para la que se deben habilitar los informes de transacciones.

**Etiqueta**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Etiqueta de operación antigua | Nueva etiqueta de operación |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Si debe capturar más de una transacción para una API, como una API por lotes en la que el recuento de transacciones varía según el número de recuentos de entrada, administre el recuento de transacciones en el nivel de API.

**Para registrar el recuento de transacciones variadas:**

1. Importar clase `"com.adobe.idp.dsc.InvocationContextStack"` en el código. La clase forma parte del `adobe-livecycle-client.jar` archivo sdk. El archivo sdk está disponible en `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Actualice el archivo de cliente compartido anteriormente en el proyecto de cliente con el nuevo archivo en caso de que ya esté empaquetado.

1. En la API para la cual se deben registrar varias transacciones:
   1. Agregue lógica para poder almacenar el recuento de transacciones en alguna variable entera, como, `transaction_count`.
   1. Cuando la operación se realice correctamente, agregue. `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Artículos relacionados

* [Activación y visualización de informes de transacciones para AEM Forms en JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Lista de API facturables para AEM Forms en JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)
