---
title: Internacionalización de cadenas de IU
seo-title: Internationalizing UI Strings
description: Las API de Java y Javascript permiten internacionalizar cadenas
seo-description: Java and Javascript APIs enable you to internationalize strings
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# Internacionalización de cadenas de IU {#internationalizing-ui-strings}

Las API de Java y Javascript permiten internacionalizar cadenas en los siguientes tipos de recursos:

* Archivos de origen Java.
* Secuencias de comandos JSP.
* Javascript en bibliotecas del lado del cliente o en el origen de página.
* Valores de propiedad del nodo JCR utilizados en cuadros de diálogo y propiedades de configuración de componentes.

Para obtener una descripción general del proceso de internacionalización y localización, consulte [Internacionalización de componentes](/help/sites-developing/i18n.md).

## Internacionalización de cadenas en Java y código JSP {#internationalizing-strings-in-java-and-jsp-code}

La variable `com.day.cq.i18n` El paquete Java le permite mostrar cadenas localizadas en la interfaz de usuario. La variable `I18n` proporciona la variable `get` método que recupera cadenas localizadas del diccionario de AEM. El único parámetro requerido de la variable `get` es el literal de cadena en inglés. El inglés es el idioma predeterminado para la interfaz de usuario. El ejemplo siguiente localiza la palabra `Search`:

`i18n.get("Search");`

La identificación de la cadena en inglés difiere de los marcos de internacionalización típicos en los que un ID identifica una cadena y se utiliza para hacer referencia a la cadena durante la ejecución. El uso del literal de cadena en inglés ofrece las siguientes ventajas:

* El código es fácil de entender.
* La cadena en el idioma predeterminado siempre está disponible.

### Determinación del idioma del usuario {#determining-the-user-s-language}

Existen dos formas de determinar el idioma que prefiere el usuario:

* Para los usuarios autenticados, determine el idioma a partir de las preferencias en la cuenta de usuario.
* La configuración regional de la página solicitada.

La propiedad language de la cuenta de usuario es el método preferido porque es más fiable. Sin embargo, el usuario debe iniciar sesión para utilizar este método.

#### Creación del objeto Java I18n {#creating-the-i-n-java-object}

La clase I18n proporciona dos constructores. La forma en que determina el idioma preferido del usuario determina el constructor que debe utilizar.

Para presentar la cadena en el idioma especificado en la cuenta de usuario, utilice el constructor siguiente (después de importar `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

El constructor utiliza la variable `SlingHTTPRequest` para recuperar la configuración de idioma del usuario.

Para utilizar la configuración regional de la página para determinar el idioma, primero debe obtener el ResourceBundle para el idioma de la página solicitada:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### Internacionalización de una cadena {#internationalizing-a-string}

Utilice la variable `get` método de la variable `I18n` para internacionalizar una cadena. El único parámetro requerido de la variable `get` es la cadena que se va a internacionalizar. La cadena corresponde a una cadena de un diccionario de traductores. El método get busca la cadena en el diccionario y devuelve la traducción para el idioma actual.

El primer argumento de la variable `get` debe cumplir las siguientes reglas:

* El valor debe ser un literal de cadena. Una variable de tipo `String` no es aceptable.
* El literal de cadena debe expresarse en una sola línea.
* La cadena distingue entre mayúsculas y minúsculas.

```xml
i18n.get("Enter a search keyword");
```

#### Uso de sugerencias de traducción {#using-translation-hints}

Especifique la variable [sugerencia de traducción](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) de la cadena internacionalizada para distinguir entre cadenas duplicadas en el diccionario. Utilice el segundo parámetro opcional de la variable `get` para proporcionar la sugerencia de traducción. La sugerencia de traducción debe coincidir exactamente con la propiedad Comment del elemento del diccionario.

Por ejemplo, el diccionario contiene la cadena `Request` dos veces: una vez como verbo y otra como sustantivo. El siguiente código incluye la sugerencia de traducción como un argumento en la variable `get` método:

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### Inclusión de variables en frases localizadas {#including-variables-in-localized-sentences}

Incluya variables en la cadena localizada para crear un significado contextual en una oración. Por ejemplo, después de iniciar sesión en una aplicación web, la página principal muestra el mensaje &quot;Bienvenido de nuevo administrador&quot;. Tienes 2 mensajes en la bandeja de entrada&quot;. El contexto de página determina el nombre de usuario y el número de mensajes.

[En el diccionario](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings), las variables se representan en cadenas como índices entre corchetes. Especifique los valores de las variables como argumentos de la variable `get` método. Los argumentos se colocan siguiendo la sugerencia de traducción y los índices se corresponden con el orden de los argumentos:

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

La cadena internacionalizada y la sugerencia de traducción deben coincidir exactamente con la cadena y el comentario del diccionario. Puede omitir la sugerencia de localización proporcionando un `null` como segundo argumento.

#### Uso del método Get estático {#using-the-static-get-method}

La variable `I18N` define una clase estática `get` que resulta útil cuando necesita localizar un pequeño número de cadenas. Además de los parámetros de la variable `get` , el método estático requiere la variable `SlingHttpRequest` o `ResourceBundle` que está utilizando, según cómo esté determinando el idioma preferido del usuario:

* Utilice la preferencia de idioma del usuario: Proporcione SlingHttpRequest como el primer parámetro.

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* Utilice el idioma de la página: Proporcione ResourceBundle como el primer parámetro.

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### Internacionalización de cadenas en código Javascript {#internationalizing-strings-in-javascript-code}

La API de Javascript permite localizar cadenas en el cliente. Como con [Java y JSP](#internationalizing-strings-in-java-and-jsp-code) , la API de JavaScript permite identificar cadenas para localizar, proporcionar sugerencias de localización e incluir variables en las cadenas localizadas.

La variable `granite.utils` [carpeta de biblioteca cliente](/help/sites-developing/clientlibs.md) proporciona la API de JavaScript. Para utilizar la API, incluya esta carpeta de la biblioteca del cliente en la página. Las funciones de localización utilizan la variable `Granite.I18n` espacio de nombres.

Antes de presentar cadenas localizadas, debe establecer la configuración regional mediante la variable `Granite.I18n.setLocale` función. La función requiere el código de idioma de la configuración regional como argumento:

```
Granite.I18n.setLocale("fr");
```

Para presentar una cadena localizada, utilice la variable `Granite.I18n.get` función:

```
Granite.I18n.get("string to localize");
```

El siguiente ejemplo internacionaliza la cadena &quot;Bienvenido de nuevo&quot;:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

Los parámetros de función son diferentes al método Java I18n.get :

* El primer parámetro es el literal de cadena que se va a localizar.
* El segundo parámetro es una matriz de valores que se van a insertar en el literal de cadena.
* El tercer parámetro es la sugerencia de localización.

El siguiente ejemplo utiliza Javascript para localizar el &quot;Bienvenido de nuevo administrador&quot;. Tienes 2 mensajes en la bandeja de entrada&quot;. frase:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### Internacionalización de cadenas de nodos JCR {#internationalizing-strings-from-jcr-nodes}

Las cadenas de interfaz de usuario se basan a menudo en las propiedades del nodo JCR. Por ejemplo, la variable `jcr:title` La propiedad de una página se utiliza generalmente como el contenido de la variable `h1` en el código de página. La variable `I18n` proporciona la variable `getVar` para localizar estas cadenas.

El siguiente ejemplo de script JSP recupera el `jcr:title` del repositorio y muestra la cadena localizada en la página:

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### Especificación de sugerencias de traducción para nodos JCR {#specifying-translation-hints-for-jcr-nodes}

Similar a [sugerencias de traducción en la API de Java](#using-translation-hints), puede proporcionar sugerencias de traducción para distinguir cadenas duplicadas en el diccionario. Proporcione la sugerencia de traducción como una propiedad del nodo que contiene la propiedad internacionalizada. El nombre de la propiedad hint consta del nombre de la propiedad internacionalizada con la variable `_commentI18n` sufijo:

`${prop}_commentI18n`

Por ejemplo, una `cq:page` incluye la propiedad jcr:title que se está localizando. La sugerencia se proporciona como el valor de la propiedad llamada jcr:title_commentI18n.

### Prueba de cobertura de internacionalización {#testing-internationalization-coverage}

Compruebe si ha internacionalizado todas las cadenas de la interfaz de usuario. Para ver qué cadenas están cubiertas, establezca el idioma del usuario en zz_ZZ y abra la IU en el explorador web. Las cadenas internacionalizadas aparecen con una traducción stub en el siguiente formato:

`USR_*Default-String*_尠`

La siguiente imagen muestra la traducción de stub para la página principal de AEM:

![imagen_1](assets/chlimage_1a.jpeg)

Para establecer el idioma del usuario, configure la propiedad language del nodo preferencias de la cuenta de usuario.

El nodo de preferencias de un usuario tiene una ruta como esta:

`/home/users/<letter>/<hash>/preferences`

![Chlimage_1-1](assets/chlimage_1-1a.jpeg)
