---
title: Funciones remotas en el Generador de expresiones
seo-title: Generador de expresiones
description: El Generador de expresiones de la administración de correspondencia permite crear expresiones y funciones remotas.
seo-description: El Generador de expresiones de la administración de correspondencia permite crear expresiones y funciones remotas.
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
translation-type: tm+mt
source-git-commit: 5a586758da84f467e075adcc33cdcede2fbf09c7

---


# Funciones remotas en el Generador de expresiones{#remote-functions-in-expression-builder}

Con el Generador de expresiones, puede crear expresiones o condiciones que realicen cálculos en los valores de datos proporcionados por el diccionario de datos o por los usuarios finales. Correspondence Management utiliza el resultado de la evaluación de expresiones para seleccionar recursos como texto, imágenes, listas y condiciones e insertarlos en la correspondencia según sea necesario.

## Creación de expresiones y funciones remotas con el generador de expresiones {#creating-expressions-and-remote-functions-with-expression-builder}

El Generador de expresiones utiliza de forma interna bibliotecas JSP EL, por lo que la expresión se ajusta a la sintaxis JSPEL. Para obtener más información, consulte Expresiones [de](#exampleexpressions)ejemplo.

![Generador de expresiones](assets/expressionbuilder.png)

### Operadores {#operators}

Los operadores disponibles para su uso en expresiones están disponibles en la barra superior del generador de expresiones.

### Expresiones de ejemplo {#exampleexpressions}

Estos son algunos ejemplos de JSP EL que puede utilizar con frecuencia en su solución de administración de correspondencia:

* Para agregar dos números: ${number1 + number2}
* Para concatenar dos cadenas: ${str1} ${str2}
* Para comparar dos números: ${age &lt; 18}

Puede encontrar más información en la especificación [](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf)JSP EL. El administrador de expresiones del lado del cliente no admite determinadas variables y funciones en la especificación JSP EL, específicamente:

* Los índices de recopilación y las claves de asignación (con la [] notación) no son compatibles con los nombres de variables para las expresiones evaluadas en el lado del cliente.
* A continuación se indican los tipos de parámetro o los tipos de devolución de funciones utilizados en las expresiones:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
   * java.util.list
   * java.lang.Short
   * Corto
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Doble
   * java.lang.Long
   * Largo
   * java.lang.Float
   * Flotante
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### Función remota {#remote-function}

Las funciones remotas proporcionan la capacidad de usar lógica personalizada en expresiones. Puede escribir una lógica personalizada para utilizarla en la expresión como un método en Java y se puede utilizar la misma función dentro de las expresiones. Las funciones remotas disponibles se muestran en la ficha &quot;Funciones remotas&quot;, en la parte izquierda del Editor de expresiones.

![remotefunction](assets/remotefunction.png)

#### Adición de funciones remotas personalizadas {#adding-custom-remote-functions}

Puede crear un paquete personalizado para exportar sus propias funciones remotas y utilizarlas en expresiones internas. Para crear un paquete personalizado y exportar sus propias funciones remotas, realice las siguientes tareas. Muestra cómo escribir una función personalizada que pone en mayúscula su cadena de entrada.

1. Defina una interfaz para el servicio OSGi que contenga métodos que se exportan para su uso por el Administrador de expresiones.
1. Declare los métodos en la interfaz A y anótelos con la anotación @ServiceMethod (com.adobe.exm.expeval.ServiceMethod). El Administrador de expresiones ignora los métodos no anotados. La anotación ServiceMethod tiene los siguientes atributos opcionales que también se pueden especificar:

   1. **Habilitado**: Determina si este método está habilitado. El Administrador de expresiones ignora los métodos deshabilitados.
   1. **familyId**: Especifica la familia (grupo) del método. Si está vacío, el Administrador de expresiones supone que el método pertenece a la familia predeterminada. No hay un registro de familias (excepto el predeterminado) desde donde se eligen las funciones. El Administrador de expresiones crea dinámicamente el registro mediante una unión de todos los ID de familia especificados por todas las funciones exportadas por los distintos paquetes. Asegúrese de que el ID que especifique aquí sea razonablemente legible, ya que también se muestra en la interfaz de usuario de creación de expresiones.
   1. **displayName**: Un nombre legible en lenguaje natural para la función. Este nombre se utiliza con fines de visualización en la interfaz de usuario de creación. Si está vacío, el Administrador de expresiones crea un nombre predeterminado utilizando el prefijo y el nombre local de la función.
   1. **Descripción**: Descripción detallada de la función. Esta descripción se utiliza con fines de visualización en la interfaz de usuario de creación. Si está vacío, el Administrador de expresiones crea una descripción predeterminada utilizando el prefijo y el nombre local de la función.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   Los parámetros de los métodos también se pueden anotar de forma opcional mediante la anotación @ServiceMethodParameter (com.adobe.exm.expeval.ServiceMethodParameter). Esta anotación solo se utiliza para especificar nombres legibles por el usuario y descripciones de parámetros de método para su uso en la interfaz de usuario de creación. Asegúrese de que los parámetros y valores de retorno de los métodos de interfaz pertenecen a uno de los siguientes tipos:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
   * java.lang.Short
   * Corto
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Doble
   * java.lang.Long
   * Largo
   * java.lang.Float
   * Flotante
   * java.util.Calendar
   * java.util.Date
   * java.util.List


1. Defina la implementación de la interfaz, configúrela como un servicio OSGI y defina las siguientes propiedades de servicio:

```
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

La entrada exm.service=true indica al administrador de expresiones que el servicio contiene funciones remotas adecuadas para su uso en expresiones. El valor &lt;service_id> debe ser un identificador Java válido (alfanumérico,$, _ sin ningún otro carácter especial). Este valor, con el prefijo REMOTE_ palabra clave, forma el prefijo que se utiliza dentro de las expresiones. Por ejemplo, se puede hacer referencia a una interfaz con un método anotado bar() y el ID de servicio en las propiedades del servicio dentro de las expresiones mediante REMOTE_foo:bar().

```
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

A continuación se muestran archivos de muestra para utilizar:

* **GoodFunctions.jar.zip** es el archivo jar con paquete que contiene una definición de función remota de muestra. Descargue el archivo GoodFunctions.jar.zip y descomprímalo para obtener el archivo jar.
* **GoodFunctions.zip** es el paquete de código fuente para definir una función remota personalizada y crear un paquete para ella.

GoodFunctions.jar.zip

[Obtener archivo](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[Obtener archivo](assets/goodfunctions.zip)
