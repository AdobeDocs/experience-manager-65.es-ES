---
title: Personalización del lado del servidor
seo-title: Server-side Customization
description: Personalización del lado del servidor en AEM Communities
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# Personalización del lado del servidor {#server-side-customization}

| **[⇐ de características esenciales](essentials.md)** | **[Criterios de personalización del lado del cliente](client-customize.md)** |
|---|---|
|  | **[Manillares SCF Helpers](handlebars-helpers.md)** |

## API de Java {#java-apis}

>[!NOTE]
>
>La ubicación del paquete de las API de Communities está sujeta a cambios al actualizar de una versión principal a otra.

### Interfaz de SocialComponent {#socialcomponent-interface}

Los componentes sociales son POJO que representan un recurso para una función de AEM Communities. Lo ideal es que cada SocialComponent represente un resourceType específico con GETters expuestos que proporcionen datos al cliente para que el recurso se represente con precisión. Toda la lógica empresarial y la lógica de vista se encapsulan en el componente Social, incluida la información de sesión del visitante del sitio, si es necesario.

La interfaz define un conjunto básico de GETters que son necesarios para representar un recurso. Es importante destacar que la interfaz estipula Mapa&lt;string object=&quot;&quot;> métodos getAsMap() y String toJSONString() que son necesarios para procesar plantillas Handlebars y exponer puntos finales JSON de GET para recursos.

Todas las clases SocialComponent deben implementar la interfaz `com.adobe.cq.social.scf.SocialComponent`

### Interfaz de SocialCollectionComponent {#socialcollectioncomponent-interface}

La interfaz SocialCollectionComponent amplía la interfaz SocialComponent para representar mejor los recursos que son colecciones de otros recursos.

Todas las clases SocialCollectionComponent deben implementar la interfaz com.adobe.cq.social.scf.SocialCollectionComponent

### Interfaz de SocialComponentFactory {#socialcomponentfactory-interface}

SocialComponentFactory (fábrica) registra un SocialComponent con el marco. La fábrica proporciona una forma de informar a la estructura de qué componentes sociales están disponibles para un resourceType determinado y de su clasificación de prioridad cuando se identifican varios componentes sociales.

SocialComponentFactory es responsable de crear una instancia del SocialComponent seleccionado, lo que permite insertar todas las dependencias necesarias para el SocialComponent desde la fábrica mediante las prácticas de ID.

SocialComponentFactory es un servicio OSGi y tiene acceso a otros servicios OSGi que se pueden pasar al componente SocialComponent a través de un constructor.

Todas las clases SocialComponentFactory deben implementar la interfaz `com.adobe.cq.social.scf.SocialComponentFactory`

Una implementación del método SocialComponentFactory.getPriority() debería devolver el valor más alto para que la fábrica se use para el resourceType dado como lo devuelve getResourceType().

### Interfaz de SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (administrador) administra todos los SocialComponents registrados con la estructura y es responsable de seleccionar SocialComponentFactory para usar con un recurso determinado (resourceType). Si no hay fábricas registradas para un resourceType específico, el administrador devolverá una fábrica con el supertipo más cercano para el recurso dado.

SocialComponentFactoryManager es un servicio OSGi y tiene acceso a otros servicios OSGi que se pueden pasar al componente SocialComponent a través de un constructor.

Se obtiene un identificador del servicio OSGi invocando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP: solicitudes de POST {#http-api-post-requests}

#### Clase PostOperation {#postoperation-class}

Los extremos del POST de la API HTTP son clases de PostOperation definidas mediante la implementación de la variable `SlingPostOperation` interfaz (paquete `org.apache.sling.servlets.post`).

La variable `PostOperation` conjuntos de implementación de endpont `sling.post.operation` a un valor al que responda la operación. Todas las solicitudes de POST con un parámetro:operation establecido en ese valor se delegarán a esta clase de implementación.

La variable `PostOperation` invoca la variable `SocialOperation` que realiza las acciones necesarias para la operación.

La variable `PostOperation` recibe el resultado de la variable `SocialOperation` y devuelve la respuesta adecuada al cliente.

#### Clase SocialOperation {#socialoperation-class}

Cada `SocialOperation` el extremo extiende la clase AbstractSocialOperation y anula el método `performOperation()`. Este método realiza todas las acciones necesarias para completar la operación y devolver un `SocialOperationResult` o arrojar un `OperationException`, en cuyo caso se devuelve un estado de error HTTP con un mensaje, si está disponible, en lugar de la respuesta JSON normal o el código de estado HTTP de éxito.

Ampliación `AbstractSocialOperation` permite la reutilización de `SocialComponents` para enviar respuestas JSON.

#### Clase SocialOperationResult {#socialoperationresult-class}

La variable `SocialOperationResult` se devuelve como resultado del `SocialOperation` y está compuesto por un `SocialComponent`, código de estado HTTP y mensaje de estado HTTP.

La variable `SocialComponent` representa el recurso afectado por la operación.

Para una operación de creación, la variable `SocialComponent` incluido en la variable `SocialOperationResult` representa el recurso que se acaba de crear y, para una operación Update, representa el recurso que modificó la operación. No `SocialComponent` para una operación de eliminación.

Los códigos de estado HTTP de éxito utilizados son:

* 201 para operaciones de creación
* 200 para operaciones de actualización
* 204 para operaciones de eliminación

#### Clase OperationException {#operationexception-class}

Un `OperationExcepton` se puede iniciar al realizar una operación si la solicitud no es válida o si se produce algún otro error, como errores internos, valores de parámetros incorrectos, permisos incorrectos, etc. Un `OperationException` se compone de un código de estado HTTP y un mensaje de error, que se devuelven al cliente como respuesta a la variable `PostOperatoin`.

#### Clase OperationService {#operationservice-class}

El marco de componentes sociales recomienda que la lógica empresarial responsable de realizar la operación no se implemente dentro del `SocialOperation` , pero delegada a un servicio OSGi. El uso de un servicio OSGi para la lógica empresarial permite `SocialComponent`, actuado por un `SocialOperation` , para integrarse con otro código y que tenga una lógica empresarial diferente aplicada.

Todo `OperationService` clases extendidas `AbstractOperationService`, lo que permite extensiones adicionales que pueden conectarse a la operación que se está realizando. Cada operación del servicio se representa mediante un `SocialOperation` Clase . La variable `OperationExtensions` se puede invocar durante la ejecución de la operación llamando a los métodos

* `performBeforeActions()`

   Permite comprobaciones previas/preprocesamiento y validaciones
* `performAfterActions()`

   Permite realizar más modificaciones en los recursos o invocar eventos, flujos de trabajo personalizados, etc.

#### Clase OperationExtension {#operationextension-class}

`OperationExtension` son fragmentos de código personalizados que se pueden insertar en una operación que permite personalizar operaciones para satisfacer las necesidades comerciales. Los consumidores del componente pueden añadir funcionalidad de forma dinámica e incremental al componente. El patrón de extensión/enlace permite a los desarrolladores centrarse exclusivamente en las propias extensiones y elimina la necesidad de copiar y anular operaciones y componentes completos.

## Código de muestra {#sample-code}

El código de muestra está disponible en la [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) repositorio. Busque proyectos con el prefijo `aem-communities` o `aem-scf`.

## Prácticas recomendadas {#best-practices}

Consulte la [Directrices de codificación](code-guide.md) para obtener más información sobre las directrices de codificación y las prácticas recomendadas para los desarrolladores de AEM Communities.

Consulte también [Proveedor de recursos de almacenamiento (SRP) para UGC](srp.md) para obtener información sobre el acceso al contenido generado por el usuario.

| **[⇐ de características esenciales](essentials.md)** | **[Criterios de personalización del lado del cliente](client-customize.md)** |
|---|---|
|  | **[Manillares SCF Helpers](handlebars-helpers.md)** |
