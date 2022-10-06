---
title: Consejos de codificación
seo-title: Coding Tips
description: Sugerencias de codificación para AEM
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: 85ca35e5-6e2b-447a-9711-b12601beacdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Consejos de codificación{#coding-tips}

## Utilice taglibs o HTL tanto como sea posible {#use-taglibs-or-htl-as-much-as-possible}

La inclusión de scripts en JSP dificulta la depuración de problemas en el código. Además, al incluir scripts en JSP, es difícil separar la lógica empresarial de la capa de vista, lo que constituye una violación del principio de responsabilidad única y del patrón de diseño de MVC.

### Escritura de código legible {#write-readable-code}

El código se escribe una vez, pero se lee muchas veces. Pasar algún tiempo por delante para limpiar el código que escribimos dará dividendos en el camino ya que nosotros y otros desarrolladores necesitamos leerlo más tarde.

### Elegir nombres que revelen la intención {#choose-intention-revealing-names}

Idealmente, otro programador no debería tener que abrir un módulo para entender lo que hace. Asimismo, deben poder decir lo que hace un método sin leerlo. Cuanto mejor podamos suscribirnos a estas ideas, más fácil será leer nuestro código y más rápido podremos escribir y cambiar nuestro código.

En la base de código de AEM, se utilizan las siguientes convenciones:


* Se nombra una sola implementación de una interfaz `<Interface>Impl`, es decir, `ReaderImpl`.
* Se nombran varias implementaciones de una interfaz `<Variant><Interface>`, es decir, `JcrReader` y `FileSystemReader`.
* Se asigna un nombre a las clases base abstractas `Abstract<Interface>` o `Abstract<Variant><Interface>`.
* Los paquetes tienen el nombre `com.adobe.product.module`.  Cada artefacto Maven o paquete OSGi debe tener su propio paquete.
* Las implementaciones de Java se colocan en un paquete impl debajo de su API.


Tenga en cuenta que estas convenciones no necesariamente tienen que aplicarse a implementaciones de clientes, pero es importante que las convenciones se definan y se adhieran a ellas para que el código pueda mantenerse.

Idealmente, los nombres deberían revelar su intención. Una prueba de código común para los casos en los que los nombres no están tan claros como deberían ser es la presencia de comentarios que explican para qué sirve la variable o el método:

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
   <td><p>//obtener imágenes etiquetadas<br /> public List getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### No te repitas  {#don-t-repeat-yourself}

DRY indica que el mismo conjunto de código nunca debe duplicarse. Esto también se aplica a cosas como literales de cadena. La duplicación de código abre la puerta a defectos cada vez que algo tiene que cambiar y debe buscarse y eliminarse.

### Evitar reglas CSS sin formato {#avoid-naked-css-rules}

Las reglas CSS deben ser específicas del elemento de destino en el contexto de la aplicación. Por ejemplo, una regla CSS aplicada a *.content.center* sería demasiado amplio y podría terminar impactando en gran cantidad de contenido en su sistema, lo que requeriría que otros anularan este estilo en el futuro. *.myapp-centertext* sería una regla más específica ya que especifica centrado *text* en el contexto de la aplicación.

### Eliminación del uso de API obsoletas {#eliminate-usage-of-deprecated-apis}

Cuando una API está en desuso, siempre es mejor encontrar el nuevo enfoque recomendado en lugar de depender de la API en desuso. Esto garantizará que las actualizaciones sean más fluidas en el futuro.

### Escribir código localizable {#write-localizable-code}

Cualquier cadena que no proporcione un autor debe envolverse en una llamada al diccionario i18n de AEM mediante *I18n.get()* en JSP/Java y *CQ.I18n.get()* en JavaScript. Esta implementación devolverá la cadena que se le pasó si no se encuentra ninguna implementación, por lo que ofrece la flexibilidad de implementar la localización después de implementar las funciones en el idioma principal.

### Escape de rutas de recursos para seguridad {#escape-resource-paths-for-safety}

Aunque las rutas en el JCR no deben contener espacios, su presencia no debe provocar que el código se rompa. Jackrabbit proporciona una clase de utilidad de texto con *escape()* y *escapePath()* métodos. Para JSP, la interfaz de usuario de Granite expone un *granite:encodeURIPath() EL* función.

### Utilice la API XSS o HTL para protegerse contra ataques de scripts entre sitios {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM proporciona una API XSS para limpiar fácilmente los parámetros y garantizar la seguridad frente a ataques de scripts entre sitios. Además, HTL tiene estas protecciones integradas directamente en el idioma de creación de plantillas. Puede descargar una hoja de referencia de API en [Desarrollo: Directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementación del registro adecuado {#implement-appropriate-logging}

Para el código Java, AEM admite slf4j como la API estándar para el registro de mensajes y debe usarse junto con las configuraciones disponibles a través de la consola OSGi para mantener la coherencia en la administración. Slf4j expone cinco niveles de registro diferentes. Se recomienda utilizar las siguientes directrices al elegir el nivel en el que se debe registrar un mensaje:

* ERROR: Cuando algo se ha roto en el código y el procesamiento no puede continuar. Esto suele ocurrir como resultado de una excepción inesperada. Normalmente es útil incluir seguimientos de pila en estos escenarios.
* ADVERTENCIA: Cuando algo no ha funcionado correctamente, pero el procesamiento puede continuar. Esto a menudo será el resultado de una excepción que esperábamos, como un *PathNotFoundException*.
* INFORMACIÓN: Información que sería útil para supervisar un sistema. Tenga en cuenta que este es el valor predeterminado y que la mayoría de los clientes lo dejarán en su lugar en sus entornos. Por lo tanto, no lo utilice excesivamente.
* DEPURACIÓN: Información de nivel inferior sobre el procesamiento. Útil para depurar un problema con compatibilidad.
* TRACE: La información de nivel más bajo, como los métodos de entrada y salida. Normalmente, solo lo utilizan los desarrolladores.

En el caso de JavaScript, *console.log* solo debe utilizarse durante el desarrollo y todas las instrucciones de registro deben eliminarse antes del lanzamiento.

### Evitar la programación del culto de carga {#avoid-cargo-cult-programming}

Evite copiar código sin comprender qué hace. Cuando haya dudas, siempre es mejor preguntar a alguien que tenga más experiencia con el módulo o API en los que no esté claro.
