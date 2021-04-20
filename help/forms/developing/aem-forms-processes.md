---
title: Explicación de los procesos de AEM Forms
seo-title: Explicación de los procesos de AEM Forms
description: Explicación de los procesos de AEM Forms
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---


# Explicación de los procesos de AEM Forms {#understanding-aem-forms-processes}

**Los ejemplos y ejemplos de este documento son solo para AEM Forms en un entorno JEE.**

Un caso de uso común es el de un conjunto de servicios de AEM Forms que funcionan en un solo documento. Puede enviar una solicitud al contenedor de servicios creando un proceso mediante Workbench. Un proceso representa un proceso empresarial que está automatizando. Para obtener información sobre la creación de procesos, consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Una vez activado un proceso, se convierte en un servicio y se puede invocar como otros servicios. Una diferencia entre un servicio estándar, como el servicio de cifrado y un servicio originado en un proceso, es que este último tiene una operación que realiza muchas acciones. Por el contrario, un servicio estándar tiene muchas operaciones. Cada operación suele realizar una acción, como aplicar una política a un documento o codificar un documento.

Los procesos pueden durar poco o durar mucho tiempo. Un proceso de corta duración es una operación que se realiza sincrónicamente y en el mismo subproceso de ejecución desde el que se invoca. Las operaciones de corta duración son comparables al comportamiento estándar que se encuentra en la mayoría de los lenguajes de programación, donde una aplicación cliente llama a un método y espera un valor devuelto.

Sin embargo, hay situaciones en las que un proceso no se puede completar sincrónicamente debido a factores como estos:

* Un proceso puede abarcar una cantidad de tiempo considerable.
* Un proceso puede abarcar límites organizativos.
* Un proceso necesita una entrada externa para que finalice. Por ejemplo, considere una situación en la que se envía un formulario a un administrador que está fuera de la oficina. En este caso, el proceso no se completa hasta que el administrador vuelva y rellene el formulario.

   Estos tipos de procesos se conocen como procesos de larga duración. Un proceso de larga duración se realiza asincrónicamente, lo que permite que los sistemas interactúen mientras los recursos lo permiten y permite el seguimiento y la supervisión de la operación. Cuando se invoca un proceso de larga duración, AEM Forms crea un valor de identificador de invocación como parte de un registro que rastrea el estado del proceso de larga duración. El registro se almacena en la base de datos de AEM Forms. Puede purgar los registros de procesos de larga duración cuando ya no se necesitan.

>[!NOTE]
>
>AEM Forms no crea ningún registro cuando se invoca un proceso de corta duración.

Con el valor del identificador de invocación, se puede realizar un seguimiento del estado del proceso de larga duración. Por ejemplo, puede utilizar el valor del identificador de invocación del proceso para realizar operaciones del Administrador de procesos, como terminar una instancia de proceso en ejecución.

**Ejemplo de proceso de corta duración**

La siguiente ilustración es un ejemplo de un proceso de corta duración llamado *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Este proceso no se basa en un proceso de AEM Forms existente. Para seguir los ejemplos de código que tratan sobre cómo invocar este proceso, cree un proceso denominado `MyApplication/EncryptDocument` con Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

Cuando se invoca este proceso de corta duración, realiza las siguientes acciones:

1. Obtiene el documento PDF no protegido que se pasa al proceso como valor de entrada.
1. Codifica el documento PDF con una contraseña. El nombre del parámetro de entrada para este proceso es `inDoc` y el tipo de datos es document.
1. Guarda el documento PDF con contraseña cifrada como archivo PDF en el sistema de archivos local. Este proceso devuelve el documento PDF cifrado como un valor de salida. El nombre del parámetro de salida para este proceso es `outDoc` y el tipo de datos es document.

   Este proceso se completa sincrónicamente en el mismo subproceso de ejecución desde el que se invocó. El nombre de este proceso de corta duración es `MyApplication/EncryptDocument`y su operación es `invoke`.

   >[!NOTE]
   >
   >Normalmente, un proceso de corta duración consta de más de tres acciones. Puede crear un proceso mediante Workbench. (Consulte [Uso de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)).

   *La programación con* formularios de AEM describe las siguientes formas en las que puede invocar mediante programación este proceso de corta duración:

   * [Invocación de un proceso de corta duración al pasar un documento no seguro mediante AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)  (con una aplicación de Flex)
   * [Invocación de un proceso de corta duración mediante la API de invocación](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api)  (API de invocación de Java)
   * [Invocación de AEM Forms mediante la codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)  (ejemplo de servicio web)
   * [Invocación de AEM Forms mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)  (ejemplo de servicio web)
   * [Invocación de AEM Forms mediante SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)  (ejemplo de servicio web)
   * [Invocación de AEM Forms mediante datos BLOB a través de HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http)  (ejemplo de servicio web)
   * [Invocación de AEM Forms mediante DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime)  (ejemplo de servicio web)
   * [Invocación del proceso MyApplication/EncryptDocument mediante REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Ejemplo de proceso de larga duración**

La siguiente ilustración es un ejemplo de un proceso de larga duración.

Este proceso se invoca cuando un solicitante presenta un formulario de préstamo. El proceso no está completo hasta que un funcionario de préstamos apruebe o rechace la solicitud de préstamo. El nombre de este proceso de larga duración es *FirstAppSolution/PreLoanProcess* y su operación es `invoke_Async`. Este proceso debe invocarse asincrónicamente. Para obtener información sobre cómo invocar mediante programación este proceso de larga duración, consulte [Invocación de procesos de larga duración centrados en los humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>Este proceso se puede crear siguiendo el tutorial especificado en [Creación de la primera aplicación de AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).