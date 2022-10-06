---
title: Creación de una nueva pantalla de inicio de sesión
seo-title: Creating a new login screen
description: Modificación de la página de inicio de sesión de los módulos de LiveCycle, por ejemplo, del espacio de trabajo de AEM Forms o de Forms Manager.
seo-description: How-to modify the login page of LiveCycle modules, for example of AEM Forms workspace or Forms Manager.
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 5%

---

# Creación de una nueva pantalla de inicio de sesión{#creating-a-new-login-screen}

Puede modificar la pantalla de inicio de sesión de todos los módulos de AEM Forms que utilizan la pantalla de inicio de sesión de AEM Forms. Por ejemplo, las modificaciones afectan a la pantalla de inicio de sesión de Forms Manager y del espacio de trabajo de AEM Forms.

## Requisitos previos {#prerequisite}

1. Iniciar sesión en `/lc/crx/de` con permisos de administrador.
1. Realice las siguientes acciones:

   1. Duplique la estructura jerárquica: de `/libs/livecycle/core/content` at `/apps/livecycle/core/content`.

      Mantener las mismas propiedades (nodo/carpeta) y control de acceso.

   1. Copie la carpeta de contenido:

      de: `/libs/livecycle/core`

      hasta: `/apps/livecycle/core`.

   1. Eliminar el contenido de `/apps/livecycle/core` carpeta.

1. Realice estas acciones:

   1. Duplique la estructura jerárquica: de `/libs/livecycle/core/components/login` at `/apps/livecycle/core/components/login`. Mantener las mismas propiedades (nodo/carpeta) y control de acceso.

   1. Copie la carpeta de componentes: from `/libs/livecycle/core` a `/apps/livecycle/core`.

   1. Elimine el contenido de la carpeta: `/apps/livecycle/core/components/login`.

### Adición de una nueva configuración regional {#adding-a-new-locale}

1. Copie el `i18n` carpeta:

   * de `/libs/livecycle/core/components/login`
   * hasta `/apps/livecycle/core/components/login`

1. Eliminar todas las carpetas dentro de `i18n` excepto uno, digamos `en`.

1. En la carpeta `en`, realice estas acciones:

   1. Cambie el nombre de la carpeta por el nombre de la configuración regional que desee admitir. Por ejemplo, `ar`.

   1. Cambiar la propiedad `jcr:language` valor `ar`(para `ar` carpeta).
   >[!NOTE]
   >
   >Si la configuración regional es una combinación de código de país de idioma, por ejemplo, `ar-DZ`y, a continuación, cambie el nombre de la carpeta y el valor de la propiedad a `ar-DZ`.

1. Copiar `login.jsp`:

   * de `/libs/livecycle/core/components/login`
   * hasta `/apps/livecycle/core/components/login`

1. Modifique el siguiente fragmento de código para `/apps/livecycle/core/components/login/login.jsp`:

***La configuración regional es código de idioma***

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

A

```jsp
String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("ar")) {
            browserLocale = "ar";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

A

```jsp
String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
            browserLocale = "ar-DZ";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

***Para cambiar la configuración regional predeterminada***

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### Adición de texto nuevo o modificación de texto existente {#adding-new-text-or-modifying-existing-text}

1. Copiar `i18n` carpeta:

   * de `/libs/livecycle/core/components/login`
   * hasta `/apps/livecycle/core/components/login`

1. Ahora modifique el valor de la propiedad `sling:message` del nodo (en la carpeta de código de configuración regional deseada) para el que desea cambiar el texto. La traducción se realiza mediante la clave mencionada en el valor de `sling:key` propiedad del nodo .

1. Para agregar un nuevo par clave-valor, realice las siguientes acciones. Compruebe un ejemplo en la captura de pantalla siguiente.

   1. Crear un nodo de tipo `sling:MessageEntry`o copie un nodo existente y renómbrelo, en todas las carpetas de configuración regional.
   1. Copiar `login.jsp` :

      * de `/libs/livecycle/core/components/login`

      * hasta `/apps/livecycle/core/components/login`
   1. Modificar `/apps/livecycle/core/components/login/login.jsp` para incorporar el texto recientemente añadido.

   ![Añadir nuevo par clave-valor](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   A

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### Adición de un nuevo estilo o modificación de un estilo existente {#adding-new-style-or-modifying-existing-style}

1. Copiar `login` nodo:

   * de `/libs/livecycle/core/content`
   * hasta `/apps/livecycle/core/content`

1. Eliminar archivos `login.js` y `jquery-1.8.0.min.js`, desde el nodo `/apps/livecycle/core/content/login.`
1. Modifique los estilos del archivo CSS.
1. Para agregar nuevos estilos:

   1. Añadir nuevos estilos a `/apps/livecycle/core/content/login/login.css`
   1. Copiar `login.jsp`

      * de `/libs/livecycle/core/components/login`

      * hasta `/apps/livecycle/core/components/login`
   1. Modificar `/apps/livecycle/core/components/login/login.jsp` para incorporar los estilos recién añadidos.



Por ejemplo:

* Agregue lo siguiente a `/apps/livecycle/core/content/login/login.css`.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* Modifique lo siguiente en `/apps/livecycle/core/components/login.jsp`.


   ```jsp
   <div class="loginContentArea">
   ```

   A

   ```jsp
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>Si las imágenes existentes en `/apps/livecycle/core/content/login` (copiado de `/libs/livecycle/core/content/login`) y, a continuación, elimine las referencias correspondientes en CSS.

### Añadir nuevas imágenes {#add-new-images}

1. Siga los pasos para Añadir un nuevo estilo o modificar un estilo existente (documentados anteriormente).
1. Añadir nuevas imágenes en `/apps/livecycle/core/content/login`. Para agregar una imagen:

   1. Instale el cliente WebDAV.
   1. Vaya a `/apps/livecycle/core/content/login` carpeta, utilizando el cliente webDAV. Para obtener más información, consulte: [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   1. Añada nuevas imágenes.

1. Añadir nuevos estilos en `/apps/livecycle/core/content/login/login.css,` correspondiente a las nuevas imágenes agregadas en `/apps/livecycle/core/content/login`.
1. Utilice los nuevos estilos en `login.jsp` at `/apps/livecycle/core/components`.

Por Ejemplo:


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    * Modifique lo siguiente en /apps/livecycle/core/components/login.jsp.

```jsp
<div class="loginContainerBkg">
```

A

```jsp
<div class="newLginContainerBkg">
```
