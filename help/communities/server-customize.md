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

| **[⇐ aspectos básicos de funciones](essentials.md)** | **[⇒ de personalización de cliente](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

## API de Java {#java-apis}

>[!NOTE]
>
>La ubicación del paquete de las API de Communities está sujeta a cambios al actualizar de una versión principal a la siguiente.

### Interfaz de SocialComponent {#socialcomponent-interface}

Los componentes sociales son POJO que representan un recurso para una función de AEM Communities. Lo ideal es que cada SocialComponent represente un resourceType específico con GETters expuestos que proporcionen datos al cliente para que el recurso se represente con precisión. Toda la lógica empresarial y la lógica de vista se encapsulan en el componente social, incluida la información de sesión del visitante del sitio, si es necesario.

La interfaz define un conjunto básico de GETters necesarios para representar un recurso. Es importante destacar que la interfaz estipula Mapa&lt;string object=&quot;&quot;> Los métodos getAsMap() y String toJSONString() son necesarios para procesar plantillas Handlebars y exponer extremos JSON de GET para los recursos.

Todas las clases de SocialComponent deben implementar la interfaz `com.adobe.cq.social.scf.SocialComponent`

### Interfaz de SocialCollectionComponent {#socialcollectioncomponent-interface}

La interfaz SocialCollectionComponent amplía la interfaz SocialComponent para representar mejor los recursos que son colecciones de otros recursos.

Todas las clases SocialCollectionComponent deben implementar la interfaz com.adobe.cq.social.scf.SocialCollectionComponent

### Interfaz de SocialComponentFactory {#socialcomponentfactory-interface}

Un SocialComponentFactory (generador) registra un SocialComponent con el marco de trabajo. La fábrica proporciona un medio para hacer saber al marco qué componentes sociales están disponibles para un resourceType determinado y su clasificación de prioridad cuando se identifican varios componentes sociales.

Un SocialComponentFactory es responsable de crear una instancia del SocialComponent seleccionado, lo que permite inyectar todas las dependencias que necesita el SocialComponent desde la fábrica mediante prácticas de ID.

Un SocialComponentFactory es un servicio OSGi y tiene acceso a otros servicios OSGi que se pueden pasar al SocialComponent a través de un constructor.

Todas las clases SocialComponentFactory deben implementar la interfaz `com.adobe.cq.social.scf.SocialComponentFactory`

Una implementación del método SocialComponentFactory.getPriority() debe devolver el valor más alto para que el generador se utilice para el resourceType dado tal como lo devuelve getResourceType().

### Interfaz de SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (administrador) administra todos los SocialComponents registrados con el marco de trabajo y es responsable de seleccionar SocialComponentFactory para utilizar en un recurso determinado (resourceType). Si no hay fábricas registradas para un resourceType específico, el administrador devolverá una fábrica con el supertipo más cercano para el recurso determinado.

Un SocialComponentFactoryManager es un servicio OSGi y tiene acceso a otros servicios OSGi que se pueden pasar al SocialComponent a través de un constructor.

Se obtiene un identificador para el servicio OSGi invocando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP: solicitudes del POST {#http-api-post-requests}

#### Clase PostOperation {#postoperation-class}

Los extremos del POST de la API HTTP son clases PostOperation definidas mediante la implementación de `SlingPostOperation` interfaz (paquete) `org.apache.sling.servlets.post`).

El `PostOperation` conjuntos de implementación de extremos `sling.post.operation` a un valor al que responderá la operación. Todas las solicitudes de POST con un parámetro:operation establecido en ese valor se delegarán a esta clase de implementación.

El `PostOperation` invoca el `SocialOperation` que realiza las acciones necesarias para la operación.

El `PostOperation` recibe el resultado de la `SocialOperation` y devuelve la respuesta adecuada al cliente.

#### Clase SocialOperation {#socialoperation-class}

Cada `SocialOperation` El extremo extiende la clase AbstractSocialOperation y reemplaza el método `performOperation()`. Este método realiza todas las acciones necesarias para completar la operación y devolver un `SocialOperationResult` o si no, arrojar un `OperationException`, en cuyo caso se devuelve un estado de error HTTP con un mensaje, si está disponible, en lugar del código de estado HTTP de éxito o de respuesta JSON normal.

Ampliación `AbstractSocialOperation` hace posible la reutilización de `SocialComponents` para enviar respuestas JSON.

#### Clase SocialOperationResult {#socialoperationresult-class}

El `SocialOperationResult` se devuelve como resultado de la variable `SocialOperation` y se compone de un `SocialComponent`, código de estado HTTP y mensaje de estado HTTP.

El `SocialComponent` representa el recurso afectado por la operación.

Para una operación Create, la variable `SocialComponent` incluido en el `SocialOperationResult` representa el recurso que acaba de crear y, para una operación Update, representa el recurso que la operación modificó. No `SocialComponent` se devuelve para una operación Delete.

Los códigos de estado HTTP de éxito utilizados son:

* 201 para Crear operaciones
* 200 para operaciones de actualización
* 204 para operaciones de eliminación

#### Clase OperationException {#operationexception-class}

Un `OperationExcepton` se puede generar al realizar una operación si la solicitud no es válida o si se produce algún otro error, como errores internos, valores de parámetros incorrectos, permisos incorrectos, etc. Un `OperationException` se compone de un código de estado HTTP y un mensaje de error, que se devuelven al cliente como respuesta al `PostOperatoin`.

#### Clase OperationService {#operationservice-class}

El marco del componente social recomienda que la lógica empresarial responsable de realizar la operación no se implemente dentro de la `SocialOperation` , sino que se delega a un servicio OSGi. El uso de un servicio OSGi para la lógica empresarial permite un `SocialComponent`, actuado por un `SocialOperation` punto final, que se integrará con otro código y se aplicará una lógica empresarial diferente.

Todo `OperationService` Las clases amplían `AbstractOperationService`, lo que permite extensiones adicionales que se pueden conectar a la operación que se está realizando. Cada operación del servicio está representada por un `SocialOperation` clase. El `OperationExtensions` La clase se puede invocar durante la ejecución de la operación llamando a los métodos

* `performBeforeActions()`

   Permite comprobaciones, preprocesamiento y validaciones.
* `performAfterActions()`

   Permite realizar más modificaciones en los recursos o invocar eventos, flujos de trabajo, etc. personalizados

#### Clase OperationExtension {#operationextension-class}

`OperationExtension` Las clases son fragmentos de código personalizados que se pueden insertar en una operación que permite personalizar las operaciones para satisfacer las necesidades comerciales. Los consumidores del componente pueden agregar funcionalidad de forma dinámica e incremental al componente. El patrón de extensión/vínculo permite a los desarrolladores centrarse exclusivamente en las propias extensiones y elimina la necesidad de copiar y anular operaciones y componentes completos.

## Código de ejemplo {#sample-code}

El código de muestra está disponible en la variable [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) repositorio. Busque proyectos con el prefijo `aem-communities` o `aem-scf`.

## Prácticas recomendadas {#best-practices}

Ver el [Directrices de codificación](code-guide.md) para obtener varias directrices de codificación y prácticas recomendadas para desarrolladores de AEM Communities.

Consulte también [Proveedor de recursos de almacenamiento (SRP) para UGC](srp.md) para obtener más información sobre el acceso al contenido generado por el usuario.

| **[⇐ aspectos básicos de funciones](essentials.md)** | **[⇒ de personalización de cliente](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
