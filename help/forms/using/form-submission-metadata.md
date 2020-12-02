---
title: Añadir información de datos de usuario a metadatos de envío de formulario
seo-title: Añadir información de datos de usuario a metadatos de envío de formulario
description: 'Aprenda a agregar información a los metadatos de un formulario enviado con datos proporcionados por el usuario. '
seo-description: 'Aprenda a agregar información a los metadatos de un formulario enviado con datos proporcionados por el usuario. '
uuid: c3eea3c0-31f8-4bf8-b5cf-34f907bdbdba
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Añadir información de datos de usuario a metadatos de envío de formulario{#adding-information-from-user-data-to-form-submission-metadata}

Puede utilizar valores introducidos en un elemento del formulario para calcular los campos de metadatos de un borrador o un envío de formulario. Los metadatos le permiten filtrar el contenido en función de los datos del usuario. Por ejemplo, un usuario introduce John Doe en el campo de nombre del formulario. Puede utilizar esta información para calcular metadatos que pueden categorizar este envío en el JD de las iniciales.

Para calcular los campos de metadatos con los valores introducidos por el usuario, agregue elementos del formulario en los metadatos. Cuando un usuario introduce un valor en ese elemento, una secuencia de comandos utiliza el valor para calcular la información. Esta información se agrega a los metadatos. Cuando se agrega un elemento como campo de metadatos, se proporciona una clave para él. La clave se agrega como un campo en los metadatos y la información calculada se registra con ella.

Por ejemplo, una empresa de seguros de salud publica un formulario. En este formulario, un campo captura la edad de los usuarios finales. El cliente desea comprobar todos los envíos en un intervalo de edad concreto después de que varios usuarios envíen el formulario. En lugar de pasar por todos los datos que se complican con el aumento del número de formularios, los metadatos adicionales ayudan al cliente. El autor del formulario puede configurar qué propiedades o datos rellenados por el usuario final se almacenan en el nivel superior para que la búsqueda sea más sencilla. Los metadatos adicionales son la información rellenada por el usuario almacenada en el nivel superior del nodo de metadatos, según la configuración del autor.

Considere otro ejemplo de un formulario que captura la identificación de correo electrónico y el número de teléfono. Cuando un usuario visita este formulario de forma anónima y abandona el formulario, el autor puede configurar el formulario para guardar automáticamente la identificación de correo electrónico y el número de teléfono. Este formulario se guarda automáticamente y el número de teléfono y el ID de correo electrónico se almacenan en el nodo de metadatos del borrador. Un caso de uso de esta configuración es el panel de administración de posibles clientes.

## Añadir elementos de formulario en metadatos {#adding-form-elements-to-metadata}

Realice los siguientes pasos para agregar un elemento en los metadatos:

1. Abra el formulario adaptable en modo de edición.\
   Para abrir el formulario en modo de edición, en el administrador de formularios, seleccione el formulario y toque **Abrir**.
1. En el modo de edición, seleccione un componente, toque ![nivel de campo](assets/field-level.png) > **Contenedor de formulario adaptable** y, a continuación, toque ![cmppr](assets/cmppr.png).
1. En la barra lateral, haga clic en **Metadatos**.
1. En la sección Metadatos, haga clic en **Añadir**.
1. Utilice el campo Valor de la ficha Metadatos para agregar secuencias de comandos. Las secuencias de comandos que se agregan recopilan datos de elementos del formulario y calculan los valores que se introducen en los metadatos.

   Por ejemplo, **true** se registra en los metadatos si la edad especificada es buena a 21 y **false** se registra si es menor a 21. La siguiente secuencia de comandos se introduce en la ficha Metadatos:

   `(agebox.value >= 21) ? true : false`

   ![Secuencia de comandos de metadatos](assets/add-element-metadata.png)

   Secuencia de comandos introducida en la ficha Metadatos

1. Haga clic en **Aceptar**.

Una vez que un usuario introduce datos en el elemento seleccionado como campo de metadatos, la información calculada se registra en los metadatos. Puede ver los metadatos en el repositorio configurado para almacenar los metadatos.

## Visualización de metadatos de envío de formulario actualizados: {#seeing-updated-form-nbsp-submission-metadata}

Por ejemplo, los metadatos se almacenan en el repositorio de CRX. El aspecto de los metadatos es el siguiente:

![Metadatos](assets/metadata_entry_new.png)

Si agrega un elemento de casilla de verificación en los metadatos, los valores seleccionados se almacenan como una cadena separada por comas. Por ejemplo, se agrega un componente de casilla de verificación al formulario y se especifica su nombre como `checkbox1`. En las propiedades del componente de casilla de verificación, agregue los elementos Permiso de conducción, Número de seguridad social y Pasaporte para los valores 0, 1 y 2.

![Almacenamiento de varios valores desde una casilla de verificación](assets/checkbox-metadata.png)

Seleccione el contenedor de formulario adaptable y, en las propiedades del formulario, agregue una clave de metadatos `cb1` que almacene `checkbox1.value` y publique el formulario. Cuando un cliente rellena el formulario, selecciona las opciones Pasaporte y Número de seguridad social en el campo de la casilla de verificación. Los valores 1 y 2 se almacenan como 1, 2 en el campo cb1 de los metadatos de envío.

![Entrada de metadatos para varios valores seleccionados en un campo de casilla de verificación](assets/metadata-entry.png)

>[!NOTE]
>
>El ejemplo anterior es solo para fines de aprendizaje. Asegúrese de buscar metadatos en la ubicación correcta, según la configuración de la implementación de AEM Forms.

