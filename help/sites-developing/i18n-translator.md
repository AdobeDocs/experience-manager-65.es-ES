---
title: Uso del traductor para administrar diccionarios
seo-title: Uso del traductor para administrar diccionarios
description: AEM proporciona una consola para administrar las distintas traducciones de textos que se utilizan en la interfaz de usuario de los componentes
seo-description: AEM proporciona una consola para administrar las distintas traducciones de textos que se utilizan en la interfaz de usuario de los componentes
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---


# Uso del traductor para administrar diccionarios{#using-translator-to-manage-dictionaries}

AEM proporciona una consola para administrar las distintas traducciones de textos que se utilizan en la interfaz de usuario de los componentes. Esta consola está disponible en

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

Utilice la herramienta de traducción para administrar las cadenas en inglés y sus traducciones. Los diccionarios se crean en el repositorio, por ejemplo /apps/myproject/i18n.

Tenga en cuenta que la herramienta Traductor y los diccionarios que administra sirven para presentar la interfaz de usuario de los componentes en distintos idiomas. Si desea traducir contenido generado por usuarios o páginas, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) y [Traducción de contenido generado por el usuario](/help/communities/translate-ugc.md).

>[!CAUTION]
>
>Solo edite los diccionarios que se han creado para el proyecto y residen en `/apps`.
>
>AEM diccionarios del sistema también están disponibles en esta herramienta. No cambie los diccionarios del sistema de AEM, ya que esto puede causar problemas con la IU AEM. Además, los cambios se pueden perder al actualizar. AEM diccionarios del sistema se encuentran en `/libs`.

>[!NOTE]
>
>Aunque la herramienta Traductor tiene una interfaz de usuario clásica, se utiliza para traducir frases independientemente de la interfaz en la que se encuentren.

El traductor lista los textos utilizados en AEM con las diferentes traducciones de idiomas entre sí:

![chlimage_1-205](assets/chlimage_1-205.png)

Puede buscar, filtrar y editar el texto en inglés y los textos traducidos. También puede exportar diccionarios al formato XLIFF para su traducción y, a continuación, volver a importar las traducciones a los diccionarios.

También es posible añadir los diccionarios i18n a un proyecto de traducción desde esta consola. Puede crear uno nuevo o agregarlo a un proyecto existente.

1. Haga clic en **Traducir diccionario**.

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. Seleccione la opción Crear o Añadir según sus necesidades. Se abre un cuadro de diálogo.

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. Rellene los campos según sea necesario y haga clic en Aceptar. ![chlimage_1-208](assets/chlimage_1-208.png)

1. Ahora puede hacer clic en **Aceptar** o ver el diccionario de Destinatario.

   >[!NOTE]
   >
   >Para obtener más información acerca de los proyectos de traducción, lea [Administración de proyectos de traducción](/help/sites-administering/tc-manage.md).

## Creación de un diccionario {#creating-a-dictionary}

Cree un diccionario para administrar las cadenas de IU localizadas. Después de crear un diccionario, puede utilizar la herramienta Traducción para administrarlo.

1. Con CRXDE Lite, agregue el nodo raíz ( `sling:Folder`) para el nuevo diccionario como estructura para contener las definiciones de idioma:

   ` /apps/<projectName>/i18n`

   Por ejemplo, `/apps/myProject/i18n`

1. Añada la estructura de idioma requerida en esta raíz. Por ejemplo:

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >Esta es la estructura del módulo [Sling i18n](https://sling.apache.org/site/internationalization-support.html).

1. Vuelva a cargar el traductor y la ruta del diccionario (p. ej. `/apps/myProject/i18n`) estará disponible en el selector desplegable de la barra de herramientas. Seleccione esta opción para añadir cadenas y sus traducciones en inicio.

   >[!NOTE]
   >
   >El traductor sólo guardará las traducciones para los idiomas que realmente están presentes debajo de la ruta (p. ej. `/apps/myProject/i18n`).
   >
   >Asegúrese de que se corresponden con los idiomas mostrados en la cuadrícula.

## Administración de cadenas de diccionario {#managing-dictionary-strings}

Utilice la herramienta Traducción para administrar las cadenas de los diccionarios. Puede agregar, modificar y eliminar cadenas en inglés, así como proporcionar cadenas traducidas.

>[!CAUTION]
>
>Solo edite los diccionarios que se han creado para el proyecto y residen en `/apps`.
>
>No cambie los diccionarios del sistema de AEM, ya que esto puede causar problemas con la IU AEM. Además, los cambios se pueden perder al actualizar. AEM diccionarios del sistema se encuentran en `/libs`.

### Añadir, cambiar y eliminar cadenas {#adding-changing-and-removing-strings}

Añada cadenas en inglés a un diccionario que su componente haya internacionalizado. Solo agregue cadenas internacionalizadas para no desperdiciar recursos traduciendo cadenas que no se utilizan.

Las cadenas que agregue a un diccionario deben coincidir exactamente con la cadena especificada en el código. Si la cadena inglesa predeterminada que se utiliza en el código no coincide con la cadena inglesa de un diccionario, la cadena traducida no aparece en la interfaz de usuario cuando es necesario. Las cadenas distinguen entre mayúsculas y minúsculas.

**Proporcionar sugerencias de traducción**

Utilice la propiedad Commenet de la cadena de diccionario para proporcionar información al traductor para aclarar el significado de la cadena. Normalmente, la interfaz de usuario ayuda a los usuarios a determinar el significado de palabras ambiguas. Sin embargo, el traductor no ve la cadena en el contexto de la interfaz de usuario. La sugerencia de traducción elimina la ambigüedad. Por ejemplo, un comentario ayuda al traductor a comprender que la palabra Solicitud en inglés se utiliza como un sustantivo en lugar de como un verbo.

Las sugerencias de traducción también distinguen cadenas que son idénticas y tienen distintos significados. Por ejemplo, la palabra Buscar puede ser un sustantivo o un verbo, lo que requiere dos entradas &quot;Buscar&quot; en el diccionario con dos sugerencias de traducción diferentes. El código que solicita la cadena también incluye la sugerencia de traducción para que se utilice la cadena correcta en la interfaz de usuario.

**Inclusión de variables indizadas**

Incluya variables en la cadena localizada para crear un significado contextual en una frase. Por ejemplo, después de iniciar sesión en una aplicación web, la página de inicio muestra el mensaje &quot;Welcome back Administrator&quot; (Bienvenido al administrador). Tienes 2 mensajes en tu bandeja de entrada&quot;. El contexto de página determina el nombre de usuario y el número de mensajes.

Para incluir variables en la cadena localizada, coloque índices entre corchetes en la ubicación de las variables en el primer argumento del método get. Utilice la sugerencia de localización para describir los valores. El traductor debe comprender el significado de las variables porque los distintos idiomas utilizan diferentes estructuras de frase.

Tenga en cuenta que [el código que solicita la cadena traducida](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) proporciona valores para las variables indizadas según el contexto.

Por ejemplo, la siguiente cadena aparece cuando un usuario inicia sesión en un sitio web y se incluye en el diccionario:

`Welcome back {0}. You have {1} messages.`

El siguiente comentario describe las variables:

`{0} = the user name, {1} = the number of items in the user's inbox`

**Modificación de cadenas**

Cambie o elimine las cadenas en inglés a medida que se cambien o eliminen en el código. Cuando se cambia una cadena, la cadena original permanece y se crea una nueva cadena que refleja el cambio. Antes de eliminar una cadena, asegúrese de que ningún código la utiliza.

Utilice el procedimiento siguiente para agregar una cadena.

1. En el menú desplegable Diccionarios, seleccione el diccionario al que va a agregar una cadena. En el menú desplegable, los diccionarios se representan por su ruta en el repositorio.
1. Arriba de la tabla Cadenas y traducciones, haga clic en Añadir.

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. En el cuadro Cadena del cuadro de diálogo Añadir cadena, escriba la cadena en inglés. En el cuadro Comentario, escriba una sugerencia de traducción para el traductor si es necesario.
1. Haga clic en Aceptar.
1. Haga clic en Guardar.

   ![chlimage_1-210](assets/chlimage_1-210.png)

Utilice el siguiente procedimiento para cambiar una cadena en un diccionario.

1. En el menú desplegable Diccionarios, seleccione el diccionario que contiene la cadena que desea cambiar.
1. Haga clic con el doble en la cadena que desea cambiar.
1. En el cuadro de diálogo Editar cadena, seleccione Modificar cadena o Comentario (Crea una copia).

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. Modifique la cadena o el comentario y haga clic en Aceptar.
1. Haga clic en Guardar.

   ![chlimage_1-212](assets/chlimage_1-212.png)

Utilice el procedimiento siguiente para quitar una cadena de un diccionario.

1. En el menú desplegable Diccionarios, seleccione el diccionario del que está quitando una cadena.
1. Haga clic en Quitar.

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. Haga clic en Guardar.

   ![chlimage_1-214](assets/chlimage_1-214.png)

### Buscando cadenas {#searching-for-strings}

La barra de búsqueda situada en la parte inferior de la herramienta Traductor proporciona opciones de selección de cadenas:

* **Filtrar por texto:** Un patrón que coincide con la cadena, el comentario o las traducciones en inglés. En la tabla solo aparecen los elementos que coinciden con todo o parte del patrón.
* **Cambios: Cualquiera, Modificado, Nuevo, Eliminado:** muestra los elementos que se han cambiado y no guardado.

   * Cualquiera: Mostrar los elementos que se han modificado, agregado o eliminado.
   * Modificado: Mostrar los elementos que se han cambiado.
   * Nuevo: Mostrar los elementos que se han agregado.
   * Eliminado: Mostrar los elementos que se van a eliminar.
   * Varias selecciones: Muestra los elementos que tienen todas las propiedades seleccionadas.

* **Tiene un comentario**: Mostrar los elementos que tienen comentarios para los traductores.
* **Traducciones que faltan:** mostrar elementos en los que al menos un idioma no tiene traducción.

![chlimage_1-215](assets/chlimage_1-215.png)

1. En la barra de búsqueda, seleccione las opciones de filtrado.
1. Para filtrar con las opciones, haga clic en Filtro.
1. Para eliminar los filtros y ver todos los elementos del diccionario, haga clic en Borrar.

### Edición de cadenas traducidas {#editing-translated-strings}

Después de agregar la cadena en inglés a un diccionario, puede agregar traducciones de la cadena. También puede [exportar el diccionario](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) para que lo traduzca un tercero.

1. Seleccione [el diccionario específico del proyecto](#creating-a-dictionary) ya que especifica la ruta en el repositorio que contiene las traducciones. Por ejemplo, seleccione **Diccionarios** como:

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >Solo edite los diccionarios que se han creado para el proyecto y residen en `/apps`.
   >
   >AEM diccionarios del sistema también están disponibles en esta herramienta. No cambie los diccionarios del sistema de AEM, ya que esto puede causar problemas con la IU AEM. Además, los cambios se pueden perder al actualizar. AEM diccionarios del sistema se encuentran en `/libs`.

1. Para editar los textos traducidos de una de las cadenas, puede:

   * Haga clic en el idioma correspondiente de la cadena requerida para editar ese texto único:

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * Haga clic en el doble en los campos **String** o **Comment** de la cadena requerida para abrir el cuadro de diálogo **Editar cadena**, edite las traducciones según sea necesario y haga clic en **Aceptar** para cerrar el cuadro de diálogo:

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Haga clic en **Guardar** en la barra de herramientas para confirmar los cambios.

   >[!NOTE]
   >
   >Al hacer clic en **Restablecer y actualizar** (en lugar de **Guardar**) se revierten los cambios realizados en los textos anteriores.

## Uso de traductores de terceros {#using-third-party-translators}

Para apoyar el uso de servicios de traducción de terceros, la herramienta Traducción le permite exportar e importar diccionarios.

### Exportación de un diccionario {#exporting-a-dictionary}

Exporte un diccionario a un archivo XLIFF para que un servicio de terceros pueda traducir las cadenas del diccionario.

* Exporte un diccionario e incluya el inglés y los términos traducidos para un idioma.
* Exporte algunas o todas las cadenas en inglés.

Al exportar un archivo XLIFF e incluir un idioma, la estructura de nodos del diccionario en el repositorio debe incluir ese idioma. Si no se incluye el idioma, se producen errores. Por ejemplo, para exportar el archivo XLIFF en francés, la carpeta de diccionario debe incluir el nodo secundario `mix:language` denominado `fr`. (Consulte [Creación de un diccionario](/help/sites-developing/i18n-translator.md#creating-a-dictionary)).

Utilice el siguiente procedimiento para exportar un archivo XLIFF para un idioma específico.

1. Abra la herramienta Traducción `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Utilice el menú desplegable Diccionarios para seleccionar el diccionario que desea exportar.
1. Haga clic en Exportar > Exportar opciones de Xliff completas *XX*, donde *XX* es el código de idioma de dos letras como DE o FR.

   El archivo XLIFF se abre en una nueva ficha o ventana.

1. Utilice los comandos del explorador Web para guardar la página como un archivo en el sistema de archivos, como Archivo > Guardar página como.

Utilice el siguiente procedimiento para exportar todas o algunas de las cadenas inglesas únicamente.

1. Abra la herramienta Traducción. `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Utilice el menú desplegable Diccionarios para seleccionar el diccionario que desea exportar.
1. Si va a exportar un subconjunto de las cadenas, seleccione los elementos del diccionario que desea exportar. Al seleccionar ningún elemento se exportan todos los elementos.
1. Haga clic en Exportar > Exportar selección como Xliff (solo cadenas).
1. En el cuadro de diálogo que aparece, copie el texto y péguelo en un archivo de texto.

### Importación de un diccionario {#importing-a-dictionary}

Importe un archivo XLIFF en un diccionario para rellenar el diccionario. Cuando el diccionario incluye una traducción para una cadena en inglés y el archivo XLIFF contiene una traducción diferente para la misma cadena, se reemplaza la traducción del diccionario.

1. Abra la herramienta Traducción `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Haga clic en Importar > Traducciones XLIFF.
1. Seleccione el archivo que desea importar y haga clic en Aceptar.

## Administración de idiomas admitidos {#managing-supported-lanuages}

Añada o elimine los idiomas compatibles con la herramienta Traducción y que se proporcionan a los usuarios de las páginas web.

### Cambio de los idiomas enumerados en la tabla de diccionario {#changing-languages-listed-in-the-dictionary-table}

La herramienta Traductor incluye los siguientes idiomas en la tabla de diccionario:

* de - Alemán
* fr - Francés
* it - Italiano
* es - Español
* ja - Japonés
* pt-br - Portugués brasileño
* zh-cn - Chino simplificado
* zh-tw - Chino tradicional (soporte limitado)
* ko-kr - Coreano

Utilice el siguiente procedimiento para agregar o quitar idiomas.

1. Con CRXDE Lite, cree un nuevo nodo:

   `/etc/languages`

1. En este nodo, cree una propiedad:

   * **Nombre**: `languages`
   * **Tipo**: `Multi-String`
   * **Valor**: la lista de idiomas que desea mostrar. Por ejemplo:

      * fr
      * es

   >[!NOTE]
   >
   >Los códigos de idioma deben escribirse en minúsculas.

1. Haga clic en **Guardar todo** en el CRXDE Lite y vuelva a cargar el traductor. La cuadrícula se actualizará para mostrar los idiomas definidos.

   >[!NOTE]
   >
   >El traductor sólo guardará traducciones para idiomas que estén [presentes en el diccionario](#creating-a-dictionary) (es decir, debajo de la ruta del diccionario como `/apps/myProject/i18n`).
   >
   >Asegúrese de que se corresponden con los idiomas mostrados en la cuadrícula.

### Poner los idiomas a disposición de los autores {#making-languages-available-to-authors}

Después de definir un diccionario para un idioma nuevo de la instancia de AEM, debe hacer que esté disponible para que lo seleccionen los autores (por ejemplo, para utilizarlo en **Preferencias**):

1. Para cambiar la lista de idiomas disponibles en **Preferencias** de la consola **Seguridad**:

   1. Cree una superposición en el código de la aplicación para:

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. Para que el idioma esté disponible en **Preferencias** desde la consola **Sitios web**, debe realizar los siguientes cambios en la aplicación:

   1. Cree una superposición para la estructura en:

      `/libs/cq/security/content/tools/userProperties`

   1. Dentro de la superposición, actualice la lista de idioma en:

      `items/common/items /lang/options`

1. Guarde todo y vuelva a cargar la consola adecuada.

### Cambio de los nombres de idioma y los países predeterminados {#changing-language-names-and-default-countries}

Varios países usan el mismo idioma, por ejemplo, Estados Unidos, Reino Unido y Australia, todos usan inglés. Esto se indica con un código que indica idioma y país como `en_US`, `en_GB` y `en_AU`.

Los países predeterminados se utilizan al mostrar los indicadores (por ejemplo, en el cuadro de diálogo de copia de idioma), para resolver el país de un código de idioma.

>[!NOTE]
>
>Para localizaciones administradas por el traductor de arriba, sólo funciona el idioma exacto. Si la lista desplegable de preferencias de idioma utiliza `en_uk`, debe haber un diccionario `en_uk` en el repositorio.

Para cambiar las definiciones predeterminadas:

1. Una lista de idioma se almacena en:

   `/libs/wcm/core/resources/languages`

   Superponga esto copiándolo en:

   `/apps/wcm/core/resources/languages`

   Luego cambiar o extender la lista allí. La propiedad `defaultCountry` en un nodo de idioma (p. ej. `ja`) debe contener el código completo, como `ja_jp`, que definiría `jp` como el país predeterminado para el idioma `ja`.

1. Actualice el **Administrador de idioma de CQ WCM**.

   * **Lista** de idioma:

      Ruta de acceso a la lista de idioma en el repositorio. Establezca esta opción en la ubicación utilizada para la superposición:

      ```
             /apps/wcm/core/resources/languages
      ```
   Puede hacerlo mediante la Consola Web OSGi:

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## Publicación de diccionarios {#publishing-dictionaries}

Incorpore los diccionarios en el proceso de administración de versiones de sus aplicaciones AEM. Por ejemplo, incluya el diccionario en el paquete de contenido de la aplicación para su implementación en la instancia de publicación. Esta estrategia ofrece los siguientes beneficios:

* Los diccionarios están disponibles para los componentes en su entorno de publicación.
* Los cambios en las cadenas de la interfaz de usuario de los componentes se implementan junto con las traducciones actualizadas.

Del mismo modo, las pruebas de cadenas de diccionario deben realizarse como parte de su ciclo de vida normal de desarrollo de software.

>[!NOTE]
>
>La funcionalidad de publicación regular, o replicación, no debe usarse para diccionarios. En su lugar, los diccionarios deben tratarse del mismo modo que el código y la configuración. Esto incluye el uso del control de código fuente para realizar un seguimiento de los cambios y el uso de paquetes de contenido para aplicar cambios al autor y la publicación.

>[!NOTE]
>
>Al utilizar Dispatcher, debe [invalidar las páginas en caché](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) para incluir nuevas cadenas dicacionarias en las cadenas de componentes procesadas.

