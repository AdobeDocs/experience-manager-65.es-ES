---
title: Consejos de codificación
seo-title: Consejos de codificación
description: Sugerencias para la codificación de AEM
seo-description: Sugerencias para la codificación de AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---


# Sugerencias de codificación{#coding-tips}

## Utilice taglibs o HTL tanto como sea posible {#use-taglibs-or-htl-as-much-as-possible}

La inclusión de scripts en JSP dificulta la depuración de problemas en el código. Además, al incluir scripts en JSP, es difícil separar la lógica empresarial de la capa de vista, lo que infringe el principio de responsabilidad única y el patrón de diseño de MVC.

### Escribir código legible {#write-readable-code}

El código se escribe una vez, pero se lee muchas veces. Pasar algún tiempo por adelantado para limpiar el código que escribimos generará dividendos en el camino mientras nosotros y otros desarrolladores necesitemos leerlo más tarde.

### Elija nombres que revelen intenciones {#choose-intention-revealing-names}

Idealmente, otro programador no debería tener que abrir un módulo para entender lo que hace. Del mismo modo, deberían poder decir lo que hace un método sin leerlo. Cuanto mejor podamos suscribirnos a estas ideas, más fácil será leer nuestro código y más rápido podremos escribir y cambiar nuestro código.

En la base de código de AEM se utilizan las siguientes convenciones:


* Una sola implementación de una interfaz se denomina `<Interface>Impl`, por ejemplo: `ReaderImpl`.
* Varias implementaciones de una interfaz se denominan `<Variant><Interface>`, es decir: `JcrReader` y `FileSystemReader`.
* Las clases base abstractas se denominan `Abstract<Interface>` o `Abstract<Variant><Interface>`.
* Los paquetes se denominan `com.adobe.product.module`.  Cada artefacto Maven o paquete OSGi debe tener su propio paquete.
* Las implementaciones de Java se colocan en un paquete impl debajo de su API.


Tenga en cuenta que estas convenciones no necesariamente tienen que aplicarse a las implementaciones de los clientes, pero es importante que las convenciones se definan y se respeten para que el código pueda mantenerse.

Idealmente, los nombres deberían revelar su intención. Una prueba de código común para los casos en los que los nombres no son tan claros como deberían ser es la presencia de comentarios que explican para qué sirve la variable o el método:

<table>
 <tbody>
  <tr>
   <td><p><strong>Unclear</strong></p> </td>
   <td><p><strong>Borrar</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //tiempo transcurrido en días</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//obtener imágenes etiquetadas<br /> Lista pública getItems() {}</p> </td>
   <td><p>public Lista getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### No se repita {#don-t-repeat-yourself}

DRY establece que el mismo conjunto de códigos nunca debe duplicarse. Esto también se aplica a cosas como literales de cadena. La duplicación de códigos abre la puerta a defectos cada vez que algo tiene que cambiar y debe buscarse y eliminarse.

### Evite las reglas CSS desnudas {#avoid-naked-css-rules}

Las reglas CSS deben ser específicas del elemento de destinatario en el contexto de la aplicación. Por ejemplo, una regla CSS aplicada a *.content.center* sería excesivamente amplia y podría afectar a muchos contenidos en todo el sistema, lo que requeriría que otros usuarios anularan este estilo en el futuro. *.myapp-* centertext sería una regla más específica ya que especifica  ** texto centrado en el contexto de la aplicación.

### Elimine el uso de API obsoletas {#eliminate-usage-of-deprecated-apis}

Cuando una API está en desuso, siempre es mejor encontrar el nuevo método recomendado en lugar de depender de la API en desuso. Esto garantizará que las actualizaciones sean más fluidas en el futuro.

### Escribir código localizable {#write-localizable-code}

Cualquier cadena que no proporcione un autor debe envolverse en una llamada al diccionario i18n de AEM mediante *I18n.get()* en JSP/Java y *CQ.I18n.get()* en JavaScript. Esta implementación devolverá la cadena que se le pasó si no se encuentra ninguna implementación, de modo que esto oferta la flexibilidad de implementar la localización después de implementar las características en el idioma principal.

### Escape de rutas de recursos para seguridad {#escape-resource-paths-for-safety}

Mientras que las rutas en el JCR no deben contener espacios, su presencia no debe provocar que el código se rompa. Jackrabbit proporciona una clase de utilidad Text con métodos *escape()* y *escapePath()*. Para JSP, la interfaz de usuario de Granite expone una función *granite:encodeURIPath() EL*.

### Utilice la API XSS y/o HTL para protegerse contra ataques de scripts entre sitios {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM proporciona una API XSS para limpiar fácilmente los parámetros y garantizar la seguridad de los ataques de secuencias de comandos entre sitios. Además, HTL tiene estas protecciones integradas directamente en el lenguaje de plantilla. Se puede descargar una hoja de trucos de API en [Desarrollo: directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementar el registro apropiado {#implement-appropriate-logging}

Para el código Java, AEM admite slf4j como la API estándar para el registro de mensajes y debe usarse junto con las configuraciones disponibles a través de la consola OSGi para lograr coherencia en la administración. Slf4j expone cinco niveles de registro diferentes. Se recomienda utilizar las siguientes directrices al elegir el nivel en el que se registra un mensaje:

* ERROR: Cuando algo se ha roto en el código y el procesamiento no puede continuar. Esto suele ocurrir como resultado de una excepción inesperada. Normalmente resulta útil incluir rastros de pila en estos escenarios.
* ADVERTENCIA: Cuando algo no ha funcionado correctamente, pero el procesamiento puede continuar. Esto suele ser el resultado de una excepción que esperábamos, como una *PathNotFoundException*.
* INFORMACIÓN: Información que sería útil para supervisar un sistema. Tenga en cuenta que este es el valor predeterminado y que la mayoría de los clientes lo dejarán en sus entornos. Por lo tanto, no la use excesivamente.
* DEPURAR: Información de nivel inferior sobre el procesamiento. Resulta útil cuando se depura un problema con compatibilidad.
* TRACE: La información de nivel más bajo, como los métodos de entrada y salida. Normalmente, esto solo lo utilizarán los desarrolladores.

En el caso de JavaScript, *console.log* sólo debe usarse durante el desarrollo y todas las sentencias de registro deben eliminarse antes de la versión.

### Evitar la programación del culto de carga {#avoid-cargo-cult-programming}

Evite copiar código sin comprender qué hace. En caso de duda, siempre es mejor preguntar a alguien que tenga más experiencia con el módulo o la API sobre la que no esté seguro.
