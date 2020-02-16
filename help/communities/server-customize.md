---
title: Personalización del lado del servidor
seo-title: Personalización del lado del servidor
description: Personalización del lado del servidor en comunidades AEM
seo-description: Personalización del lado del servidor en comunidades AEM
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalización del lado del servidor {#server-side-customization}

| **[Elementos básicos de las funciones de ⇐](essentials.md)** | **[Personalización del cliente](client-customize.md)** |
|---|---|
|  | **[Manillares de SCF Ayudantes](handlebars-helpers.md)** |

## API de Java {#java-apis}

>[!NOTE]
>
>La ubicación del paquete de las API de Communities está sujeta a cambios al actualizar de una versión principal a otra.

### Interfaz de SocialComponent {#socialcomponent-interface}

SocialComponents son POJO que representan un recurso para una función de comunidades AEM. Lo ideal es que cada componente de Social represente un resourceType específico con GETters expuestos que proporcionen datos al cliente para que el recurso se represente con precisión. Toda la lógica empresarial y la lógica de vista se encapsulan en el componente Social, incluida la información de la sesión del visitante del sitio, si es necesario.

La interfaz define un conjunto básico de GETters que son necesarios para representar un recurso. Es importante destacar que la interfaz estipula los métodos Map&lt;String, Object> getAsMap() y String toJSONString() que son necesarios para procesar las plantillas Handlebars y exponer los extremos GET JSON para los recursos.

Todas las clases de SocialComponent deben implementar la interfaz `com.adobe.cq.social.scf.SocialComponent`

### Interfaz de SocialCollectionComponent {#socialcollectioncomponent-interface}

La interfaz SocialCollectionComponent amplía la interfaz de SocialComponent para representar mejor los recursos que son colecciones de otros recursos.

Todas las clases de SocialCollectionComponent deben implementar la interfaz com.adobe.cq.social.scf.SocialCollectionComponent

### Interfaz de SocialComponentFactory {#socialcomponentfactory-interface}

SocialComponentFactory (fábrica) registra un componente de Social con el marco. La fábrica proporciona un medio para permitir que la estructura sepa qué componentes de Social están disponibles para un recursoType determinado y su prioridad de clasificación&amp;ast; cuando se identifican varios componentes de Social.

SocialComponentFactory es responsable de crear una instancia del componente SocialComponent seleccionado, lo que permite inyectar todas las dependencias necesarias para el componente Social desde la fábrica mediante prácticas de ID.

SocialComponentFactory es un servicio OSGi y tiene acceso a otros servicios OSGi que se pueden pasar a SocialComponent a través de un constructor.

Todas las clases de SocialComponentFactory deben implementar la interfaz `com.adobe.cq.social.scf.SocialComponentFactory`

Una implementación del método SocialComponentFactory.getPriority() debe devolver el valor más alto para que la fábrica se utilice para el resourceType dado como lo devuelve getResourceType().

### Interfaz de SocialComponentFactoryManager {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager (administrador) administra todos los componentes de Social registrados en la estructura y es responsable de seleccionar SocialComponentFactory para usar en un recurso determinado (resourceType). Si no hay fábricas registradas para un resourceType específico, el administrador devolverá una fábrica con el supertipo más cercano para el recurso determinado.

SocialComponentFactoryManager es un servicio OSGi y tiene acceso a otros servicios OSGi que se pueden pasar a SocialComponent a través de un constructor.

Se obtiene un identificador del servicio OSGi invocando `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### API HTTP: solicitudes POST {#http-api-post-requests}

#### Clase PostOperation {#postoperation-class}

Los extremos POST de la API HTTP son clases PostOperation definidas mediante la implementación de la `SlingPostOperation`interfaz (paquete `org.apache.sling.servlets.post`).

La implementación de `PostOperation`extremo establece `sling.post.operation`un valor al que responderá la operación. Todas las solicitudes POST con un parámetro:operation establecido en ese valor se delegarán en esta clase de implementación.

El `PostOperation`invoca el `SocialOperation`que realiza las acciones necesarias para la operación.

El `PostOperation`recibe el resultado del `SocialOperation`y devuelve la respuesta adecuada al cliente.

#### Clase SocialOperation {#socialoperation-class}

Cada `SocialOperation`extremo amplía la clase AbstractSocialOperation y anula el método. `performOperation().`Este método realiza todas las acciones necesarias para completar la operación y devolver un error `SocialOperationResult`o, de lo contrario, emitir un `OperationException`, en cuyo caso se devuelve un estado de error HTTP con un mensaje, si está disponible, en lugar de la respuesta JSON normal o el código de estado HTTP de éxito.

La extensión `AbstractSocialOperation`permite reutilizar `SocialComponents`para enviar respuestas JSON.

#### Clase SocialOperationResult {#socialoperationresult-class}

La `SocialOperationResult`clase se devuelve como resultado del `SocialOperation`y se compone de un `SocialComponent`, código de estado HTTP y mensaje de estado HTTP.

El `SocialComponent`representa el recurso afectado por la operación.

Para una operación de creación, el `SocialComponent`incluido en la `SocialOperationResult`representa el recurso que se acaba de crear y, para una operación de actualización, representa el recurso modificado por la operación. No `SocialComponent`se devuelve ningún valor para una operación de eliminación.

Los códigos de estado HTTP de éxito utilizados son

* 201 para operaciones de creación
* 200 para operaciones de actualización
* 204 para operaciones de eliminación

#### Clase OperationException {#operationexception-class}

Se `OperationExcepton`puede generar un error al realizar una operación si la solicitud no es válida o se produce algún otro error, como errores internos, valores de parámetro incorrectos, permisos incorrectos, etc. Un `OperationException`se compone de un código de estado HTTP y un mensaje de error, que se devuelven al cliente como respuesta al `PostOperatoin`.

#### Clase OperationService {#operationservice-class}

El marco de componentes sociales recomienda que la lógica empresarial responsable de realizar la operación no se implemente dentro de la `SocialOperation`clase, sino que se delegue en un servicio OSGi. El uso de un servicio OSGi para la lógica empresarial permite que un `SocialComponent`producto, actuado por un `SocialOperation`punto final, se integre con otro código y se aplique una lógica comercial diferente.

Todas `OperationService`las clases se extienden `AbstractOperationService`, permitiendo extensiones adicionales que pueden engancharse en la operación que se está realizando. Cada operación del servicio está representada por una `SocialOperation`clase. La `OperationExtensions`clase se puede invocar durante la ejecución de la operación llamando a los métodos

* `performBeforeActions()`
Permite realizar comprobaciones previas/preprocesamiento y validaciones
* `performAfterActions()`
Permite una mayor modificación de los recursos o invocar eventos personalizados, flujos de trabajo, etc.

#### Clase OperationExtension {#operationextension-class}

`OperationExtension`son piezas de código personalizadas que se pueden insertar en una operación que permite personalizar las operaciones para satisfacer las necesidades comerciales. Los consumidores del componente pueden añadir funcionalidad de forma dinámica e incremental al componente. El patrón de extensión/gancho permite a los desarrolladores centrarse exclusivamente en las propias extensiones y elimina la necesidad de copiar y anular operaciones y componentes completos.

## Código de muestra {#sample-code}

El código de muestra está disponible en el repositorio de [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) . Busque proyectos con el prefijo `aem-communities` o `aem-scf`.

## Prácticas recomendadas {#best-practices}

Consulte la sección [Directrices](code-guide.md) de codificación para conocer las distintas directrices de codificación y prácticas recomendadas para los desarrolladores de AEM Communities.

Consulte también Proveedor [de recursos de almacenamiento (SRP) para obtener información sobre cómo acceder al contenido generado por el usuario](srp.md) .

| **[Elementos básicos de las funciones de ⇐](essentials.md)** | **[Personalización del cliente](client-customize.md)** |
|---|---|
|  | **[Manillares de SCF Ayudantes](handlebars-helpers.md)** |

