---
title: Internacionalización de cadenas de IU
seo-title: Internacionalización de cadenas de IU
description: Las API de Java y Javascript permiten internacionalizar cadenas
seo-description: Las API de Java y Javascript permiten internacionalizar cadenas
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---


# Internacionalización de cadenas de IU {#internationalizing-ui-strings}

Las API de Java y Javascript permiten internacionalizar cadenas en los siguientes tipos de recursos:

* Archivos de origen Java.
* Secuencias de comandos JSP.
* Javascript en bibliotecas del lado del cliente o en el origen de la página.
* Valores de propiedad de nodo JCR utilizados en cuadros de diálogo y propiedades de configuración de componentes.

Para obtener una visión general del proceso de internacionalización y localización, consulte [Internacionalización de componentes](/help/sites-developing/i18n.md).

## Internacionalización de cadenas en código Java y JSP {#internationalizing-strings-in-java-and-jsp-code}

El paquete Java `com.day.cq.i18n` le permite mostrar cadenas localizadas en la interfaz de usuario. La clase `I18n` proporciona el método `get` que recupera las cadenas localizadas del diccionario de AEM. El único parámetro requerido del método `get` es el literal de cadena en inglés. El inglés es el idioma predeterminado para la interfaz de usuario. El ejemplo siguiente localiza la palabra `Search`:

`i18n.get("Search");`

La identificación de la cadena en el idioma inglés difiere de los marcos de internacionalización típicos donde un ID identifica una cadena y se utiliza para hacer referencia a la cadena en tiempo de ejecución. El uso del literal de cadena en inglés ofrece las siguientes ventajas:

* El código es fácil de entender.
* La cadena en el idioma predeterminado siempre está disponible.

### Determinación del idioma del usuario {#determining-the-user-s-language}

Existen dos maneras de determinar el idioma que prefiere el usuario:

* Para los usuarios autenticados, determine el idioma en las preferencias de la cuenta de usuario.
* La configuración regional de la página solicitada.

La propiedad language de la cuenta de usuario es el método preferido porque es más fiable. Sin embargo, el usuario debe iniciar sesión para utilizar este método.

#### Creación del objeto Java I18n {#creating-the-i-n-java-object}

La clase I18n proporciona dos constructores. La forma en que se determina el idioma preferido del usuario determina el constructor que se va a utilizar.

Para presentar la cadena en el idioma especificado en la cuenta de usuario, utilice el constructor siguiente (después de importar `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

El constructor utiliza la `SlingHTTPRequest` para recuperar la configuración de idioma del usuario.

Para utilizar la configuración regional de la página para determinar el idioma, primero debe obtener ResourceBundle para el idioma de la página solicitada:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### Internacionalización de una cadena {#internationalizing-a-string}

Utilice el método `get` del objeto `I18n` para internacionalizar una cadena. El único parámetro requerido del método `get` es la cadena que se va a internacionalizar. La cadena corresponde con una cadena en un diccionario de traductores. El método get busca la cadena en el diccionario y devuelve la traducción del idioma actual.

El primer argumento del método `get` debe cumplir las siguientes reglas:

* El valor debe ser un literal de cadena. No se puede aceptar una variable de tipo `String`.
* El literal de cadena debe expresarse en una sola línea.
* La cadena distingue entre mayúsculas y minúsculas.

```xml
i18n.get("Enter a search keyword");
```

#### Uso de sugerencias de traducción {#using-translation-hints}

Especifique la [sugerencia de traducción](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) de la cadena internacionalizada para distinguir entre cadenas de duplicado en el diccionario. Utilice el segundo parámetro opcional del método `get` para proporcionar la sugerencia de traducción. La sugerencia de traducción debe coincidir exactamente con la propiedad Comment del elemento del diccionario.

Por ejemplo, el diccionario contiene la cadena `Request` dos veces: una vez como verbo y otra como sustantivo. El código siguiente incluye la sugerencia de traducción como un argumento en el método `get`:

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### Inclusión de variables en frases localizadas {#including-variables-in-localized-sentences}

Incluya variables en la cadena localizada para crear un significado contextual en una frase. Por ejemplo, después de iniciar sesión en una aplicación web, la página de inicio muestra el mensaje &quot;Welcome back Administrator&quot; (Bienvenido al administrador). Tienes 2 mensajes en tu bandeja de entrada&quot;. El contexto de página determina el nombre de usuario y el número de mensajes.

[En el diccionario](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings), las variables se representan en cadenas como índices entre corchetes. Especifique los valores de las variables como argumentos del método `get`. Los argumentos se colocan siguiendo la sugerencia de traducción y los índices se corresponden con el orden de los argumentos:

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

La cadena internacionalizada y la sugerencia de traducción deben coincidir exactamente con la cadena y el comentario del diccionario. Puede omitir la sugerencia de localización proporcionando un valor `null` como segundo argumento.

#### Uso del método Get estático {#using-the-static-get-method}

La clase `I18N` define un método estático `get` que resulta útil cuando necesita localizar un pequeño número de cadenas. Además de los parámetros del método `get` de un objeto, el método estático requiere el objeto `SlingHttpRequest` o el `ResourceBundle` que esté utilizando, según cómo esté determinando el idioma preferido del usuario:

* Utilice la preferencia de idioma del usuario: Proporcione SlingHttpRequest como el primer parámetro.

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* Utilice el idioma de la página: Proporcione ResourceBundle como el primer parámetro.

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### Internacionalización de cadenas en código Javascript {#internationalizing-strings-in-javascript-code}

La API de Javascript permite localizar cadenas en el cliente. Al igual que con el código [Java y JSP](#internationalizing-strings-in-java-and-jsp-code), la API de Javascript permite identificar cadenas para localizar, proporcionar sugerencias de localización e incluir variables en las cadenas localizadas.

La `granite.utils` [carpeta de biblioteca de cliente](/help/sites-developing/clientlibs.md) proporciona la API de Javascript. Para utilizar la API, incluya esta carpeta de la biblioteca de cliente en la página. Las funciones de localización utilizan la Área de nombres `Granite.I18n`.

Antes de presentar cadenas localizadas, debe establecer la configuración regional mediante la función `Granite.I18n.setLocale`. La función requiere el código de idioma de la configuración regional como argumento:

```
Granite.I18n.setLocale("fr");
```

Para presentar una cadena localizada, utilice la función `Granite.I18n.get`:

```
Granite.I18n.get("string to localize");
```

El siguiente ejemplo internacionaliza la cadena &quot;Welcome back&quot; (Bienvenido de nuevo):

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

Los parámetros de función son diferentes al método Java I18n.get:

* El primer parámetro es el literal de cadena que se va a localizar.
* El segundo parámetro es una matriz de valores que se inyectarán en el literal de cadena.
* El tercer parámetro es la sugerencia de localización.

En el siguiente ejemplo se utiliza Javascript para localizar el administrador de bienvenida. Tienes 2 mensajes en tu bandeja de entrada&quot;. frase:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### Internacionalización de cadenas de nodos JCR {#internationalizing-strings-from-jcr-nodes}

Las cadenas de interfaz de usuario suelen basarse en propiedades de nodo JCR. Por ejemplo: la propiedad `jcr:title` de una página generalmente se usa como contenido del elemento `h1` en el código de la página. La clase `I18n` proporciona el método `getVar` para localizar estas cadenas.

El siguiente ejemplo de secuencia de comandos JSP recupera la propiedad `jcr:title` del repositorio y muestra la cadena localizada en la página:

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### Especificación de sugerencias de traducción para nodos JCR {#specifying-translation-hints-for-jcr-nodes}

De forma similar a [sugerencias de traducción en la API de Java](#using-translation-hints), puede proporcionar sugerencias de traducción para distinguir las cadenas de duplicado en el diccionario. Proporcione la sugerencia de traducción como una propiedad del nodo que contiene la propiedad internacionalizada. El nombre de la propiedad de sugerencia está compuesto por el nombre de la propiedad internacionalizada con el sufijo `_commentI18n`:

`${prop}_commentI18n`

Por ejemplo, un nodo `cq:page` incluye la propiedad jcr:title que se está localizando. La sugerencia se proporciona como el valor de la propiedad denominada jcr:title_commentI18n.

### Prueba de cobertura de internacionalización {#testing-internationalization-coverage}

Compruebe si ha internacionalizado todas las cadenas de la interfaz de usuario. Para ver qué cadenas están cubiertas, establezca el idioma del usuario en zz_ZZ y abra la interfaz de usuario en el explorador web. Las cadenas internacionalizadas aparecen con una traducción stub en el siguiente formato:

`USR_*Default-String*_尠`

La siguiente imagen muestra la traducción de stub para la página de inicio AEM:

![chlimage_1](assets/chlimage_1a.jpeg)

Para establecer el idioma del usuario, configure la propiedad language del nodo de preferencias para la cuenta de usuario.

El nodo de preferencias de un usuario tiene una ruta de acceso como esta:

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)

