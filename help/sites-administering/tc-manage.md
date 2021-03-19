---
title: Administración de proyectos de traducción
seo-title: Administración de proyectos de traducción
description: Aprenda a administrar proyectos de traducción en AEM.
seo-description: Aprenda a administrar proyectos de traducción en AEM.
uuid: f6f79b5b-dc08-4dde-b464-719345d233a6
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c8672774-6911-497d-837b-1e5953c4226a
feature: Copiar idioma
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '3455'
ht-degree: 1%

---


# Administración de proyectos de traducción{#managing-translation-projects}

Después de preparar el contenido para la traducción, debe completar la estructura del idioma creando las copias de idioma que faltan y crear proyectos de traducción.

Los proyectos de traducción permiten administrar la traducción de AEM contenido. Un proyecto de traducción es un tipo de AEM [proyecto](/help/sites-authoring/projects.md) que contiene recursos que se deben traducir a otros idiomas. Estos recursos son las páginas y los recursos de las [copias de idioma](/help/sites-administering/tc-prep.md) que se crean a partir del maestro de idioma.

Cuando se añaden recursos a un proyecto de traducción, se crea un trabajo de traducción para ellos. Los trabajos proporcionan comandos e información de estado que se utilizan para administrar los flujos de trabajo de traducción humana y traducción automática que se ejecutan en los recursos.

>[!NOTE]
>
>Un proyecto de traducción puede contener varios trabajos de traducción.

Los proyectos de traducción son temas de larga duración, definidos por el idioma y el método/proveedor de traducción para alinearse con la gobernanza organizativa para la globalización. Deben iniciarse una vez, ya sea durante la traducción inicial o manualmente, y permanecer en vigor durante todas las actividades de actualización de contenido y traducción.

Los proyectos y trabajos de traducción se crean con los flujos de trabajo de preparación de la traducción. Estos flujos de trabajo tienen tres opciones, tanto para la traducción inicial (Create&amp;Translate) como para las actualizaciones (Update Translation):

1. [Crear nuevo proyecto](#creating-translation-projects-using-the-references-panel)
1. [Agregar a un proyecto existente](#adding-pages-to-a-translation-project)
1. [Solo estructura de contenido](#creating-the-structure-of-a-language-copy)

>[!NOTE]
>
>La opción 3 no está relacionada con el trabajo o proyecto de traducción. Le permite copiar el contenido y los cambios estructurales en el idioma maestro a (sin traducir) copias de idioma. Puede usar esto para mantener a los maestros de idiomas sincronizados, incluso sin traducción.

## Realización de traducciones iniciales y actualización de traducciones existentes {#performing-initial-translations-and-updating-existing-translations}

AEM detecta si se está creando un proyecto de traducción para la traducción inicial del contenido o para actualizar las copias de idioma ya traducidas. Cuando crea un proyecto de traducción para una página e indica los textos de idiomas para los que está traduciendo, AEM detecta si la página de origen ya existe en los textos de idiomas de destino:

* **La copia de idioma no incluye la página:** AEM trata esta situación como la traducción inicial. La página se copia inmediatamente en la copia de idioma y se incluye en el proyecto. Cuando la página traducida se importa a AEM, AEM la copia directamente en el idioma.
* **La copia de idioma ya incluye la página:** AEM trata esta situación como una traducción actualizada. Se crea un lanzamiento, se agrega una copia de la página al lanzamiento y se incluye en el proyecto. Los lanzamientos permiten revisar las traducciones actualizadas antes de enviarlas a la copia de idioma:

   * Cuando la página traducida se importa a AEM, sobrescribe la página en el lanzamiento.
   * La página traducida sobrescribe la copia de idioma solo cuando se promociona el lanzamiento.

Por ejemplo, la raíz de idioma /content/geometrixx/fr se crea para la traducción al francés del idioma maestro /content/geometrixx/en. No hay otras páginas en francés.

* Se crea un proyecto de traducción para la página /content/geometrixx/en/products y todas las páginas secundarias, dirigiéndose a la copia en francés. Como la copia de idioma no incluye la página /content/geometrixx/fr/products , AEM copia inmediatamente la página /content/geometrixx/en/products y todas las páginas secundarias a la copia en francés. Las copias también se incluyen en el proyecto de traducción.
* Se crea un proyecto de traducción para la página /content/geometrixx/en y todas las páginas secundarias, con el objetivo de la copia en francés. Como la copia de idioma incluye la página que corresponde a la página /content/geometrixx/en (la raíz del idioma), AEM copia la página /content/geometrixx/en y todas las páginas secundarias y las añade a un lanzamiento. Las copias también se incluyen en el proyecto de traducción.

## Creación de proyectos de traducción mediante el panel Referencias {#creating-translation-projects-using-the-references-panel}

Cree proyectos de traducción para poder ejecutar y administrar el flujo de trabajo de traducción de los recursos del maestro de idioma. Cuando cree proyectos, especifique la página en el idioma maestro que está traduciendo y las copias de idioma para las que está realizando la traducción:

* La configuración de nube del marco de integración de traducción asociado a la página seleccionada determina muchas propiedades de los proyectos de traducción, como el flujo de trabajo de traducción que se va a utilizar.
* Se crea un proyecto para cada copia de idioma seleccionada.
* Se crea una copia de la página seleccionada y los recursos asociados, que se añaden a cada proyecto. Estas copias se envían posteriormente al proveedor de traducción para su traducción.

Puede especificar que las páginas secundarias de la página seleccionada también estén seleccionadas. En este caso, también se agregan copias de las páginas secundarias a cada proyecto para que se traduzcan. Cuando alguna página secundaria está asociada con diferentes configuraciones del marco de integración de traducción, AEM crea proyectos adicionales.

También puede [crear manualmente proyectos de traducción](#creating-a-translation-project-using-the-projects-console).

>[!NOTE]
>
>Para crear un proyecto, la cuenta debe ser miembro del grupo `project-administrators` .

**Traducciones iniciales y actualización de traducciones**

El panel Referencias indica si está actualizando las copias de idioma existentes o creando la primera versión de las copias de idioma. Cuando existe una copia de idioma para la página seleccionada, aparece la ficha Actualizar copias de idioma para proporcionar acceso a los comandos relacionados con el proyecto.

![chlimage_1-239](assets/chlimage_1-239.png)

Después de traducir, puede [revisar la traducción](#reviewing-and-promoting-updated-content) antes de sobrescribir la copia de idioma con ella. Cuando no existe ninguna copia de idioma para la página seleccionada, aparece la pestaña Crear y traducir para proporcionar acceso a los comandos relacionados con el proyecto.

![chlimage_1-240](assets/chlimage_1-240.png)

### Creación de proyectos de traducción para una copia de idioma nueva {#create-translation-projects-for-a-new-language-copy}

1. Utilice la consola Sitios para seleccionar la página que está agregando a los proyectos de traducción.

   Por ejemplo, para traducir las páginas en inglés de Sitio de demostración de Geometrixx, seleccione Sitio de demostración de Geometrixx > Inglés.

1. En la barra de herramientas, pulse o haga clic en Referencias.

   ![chlimage_1-241](assets/chlimage_1-241.png)

1. Seleccione Textos en idiomas y, a continuación, seleccione los textos en idiomas para los que traduce las páginas de origen.
1. Pulse o haga clic en Crear y traducir y, a continuación, configure el trabajo de traducción:

   * Utilice la lista desplegable Idiomas para seleccionar una copia de idioma para la que desee traducir. Seleccione otros idiomas según sea necesario. Los idiomas que aparecen en la lista corresponden a las [raíces de idioma que ha creado](/help/sites-administering/tc-prep.md#creating-a-language-root).
   * Para traducir la página seleccionada y todas las páginas secundarias, seleccione Seleccionar todas las subpáginas. Para traducir solo la página seleccionada que ha seleccionado, desactive la opción .
   * En Proyecto, seleccione Crear nuevo proyecto de traducción.
   * Escriba un nombre para el proyecto.

   ![chlimage_1-242](assets/chlimage_1-242.png)

1. Haga clic o pulse Crear.

### Crear proyectos de traducción para una copia de idioma existente {#create-translation-projects-for-an-existing-language-copy}

1. Utilice la consola Sitios para seleccionar la página que está agregando a los proyectos de traducción.

   Por ejemplo, para traducir las páginas en inglés de Sitio de demostración de Geometrixx, seleccione Sitio de demostración de Geometrixx > Inglés.

1. En la barra de herramientas, pulse o haga clic en Referencias.

   ![imagen_1-243](assets/chlimage_1-243.png)

1. Seleccione Textos en idiomas y, a continuación, seleccione los textos en idiomas para los que traduce las páginas de origen.
1. Pulse o haga clic en Actualizar copias de idioma y, a continuación, configure el trabajo de traducción:

   * Para traducir la página seleccionada y todas las páginas secundarias, seleccione Seleccionar todas las subpáginas. Para traducir solo la página seleccionada que ha seleccionado, desactive la opción .
   * En Proyecto, seleccione Crear nuevo proyecto de traducción.
   * Escriba un nombre para el proyecto.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. Toque o haga clic en Iniciar.

## Adición de páginas a un proyecto de traducción {#adding-pages-to-a-translation-project}

Después de crear un proyecto de traducción, puede usar el panel Recursos para agregar páginas al proyecto. Agregar páginas resulta útil cuando se incluyen páginas de distintas ramas en el mismo proyecto.

Al agregar páginas a un proyecto de traducción, estas se incluyen en un nuevo trabajo de traducción. También puede [agregar páginas a un trabajo existente](#adding-pages-assets-to-a-translation-job).

Al igual que al crear un nuevo proyecto, al agregar páginas, se añaden copias de las páginas a un lanzamiento cuando es necesario para evitar sobrescribir las copias de idioma existentes. (Consulte [Creación de proyectos de traducción para copias de idioma existentes](#performing-initial-translations-and-updating-existing-translations)).

1. Utilice la consola Sitios para seleccionar la página que está agregando al proyecto de traducción.

   Por ejemplo, para traducir las páginas en inglés de Sitio de demostración de Geometrixx, seleccione Sitio de demostración de Geometrixx > Inglés.

1. En la barra de herramientas, pulse o haga clic en Referencias.

   ![chlimage_1-245](assets/chlimage_1-245.png)

1. Seleccione Textos en idiomas y, a continuación, seleccione los textos en idiomas para los que traduce las páginas de origen.

   ![chlimage_1-35](assets/chlimage_1-35.jpeg)

1. Pulse o haga clic en Actualizar copias de idioma y, a continuación, configure las propiedades:

   * Para traducir la página seleccionada y todas las páginas secundarias, seleccione Seleccionar todas las subpáginas. Para traducir solo la página seleccionada que ha seleccionado, desactive la opción .
   * En Proyecto, seleccione Agregar a proyecto de traducción existente.
   * Seleccione el proyecto.

   >[!NOTE]
   >
   >El idioma de destino definido en el proyecto de traducción debe coincidir con la ruta de la copia de idioma, como se muestra en el panel Referencias.

   ![chlimage_1-36](assets/chlimage_1-36.jpeg)

1. Toque o haga clic en Iniciar.

## Adición de páginas/recursos a un trabajo de traducción {#adding-pages-assets-to-a-translation-job}

Puede agregar páginas, recursos, etiquetas o diccionarios i18n al trabajo de traducción de su proyecto de traducción. Para agregar páginas o recursos:

1. En la parte inferior del mosaico Trabajo de traducción del proyecto de traducción, toque o haga clic en los puntos suspensivos.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Toque o haga clic en Agregar y en Páginas/Recursos.

   ![chlimage_1-247](assets/chlimage_1-247.png)

1. Seleccione el elemento superior de la rama que desea agregar y, a continuación, toque o haga clic en el icono de marca de verificación. Puede realizar varias selecciones.

   ![chlimage_1-247](assets/chlimage_1-248.png)

1. También puede seleccionar el icono de búsqueda para buscar fácilmente páginas o recursos que desee agregar a su trabajo de traducción.

   ![chlimage_1-249](assets/chlimage_1-249.png)

Sus páginas o recursos se añaden a su trabajo de traducción.

## Agregar diccionarios i18n a un trabajo de traducción {#adding-i-n-dictionaries-to-a-translation-job}

Puede agregar páginas, recursos, etiquetas o diccionarios i18n al trabajo de traducción de su proyecto de traducción. Para añadir un diccionario i18n:

1. En la parte inferior del mosaico Trabajo de traducción del proyecto de traducción, toque o haga clic en los puntos suspensivos.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Toque o haga clic en Agregar y en el diccionario I18N.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Seleccione el diccionario que desea agregar y, a continuación, toque o haga clic en el botón Agregar .

   ![chlimage_1-252](assets/chlimage_1-252.png)

El diccionario está ahora en su trabajo de traducción.

![chlimage_1-253](assets/chlimage_1-253.png)

>[!NOTE]
>
>Para obtener más información sobre los diccionarios de i18n, lea [Uso del traductor para administrar diccionarios](/help/sites-developing/i18n-translator.md).

## Adición de etiquetas a un trabajo de traducción {#adding-tags-to-a-translation-job}

Puede agregar páginas, recursos, etiquetas o diccionarios i18n al trabajo de traducción de su proyecto de traducción. Para agregar etiquetas:

1. En la parte inferior del mosaico Trabajo de traducción del proyecto de traducción, toque o haga clic en los puntos suspensivos.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Toque o haga clic en Agregar y, a continuación, en Etiquetas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Seleccione las etiquetas que desee agregar y, a continuación, toque o haga clic en el icono de marca de verificación. Puede realizar varias selecciones.

   ![chlimage_1-256](assets/chlimage_1-256.png)

Las etiquetas ahora se añaden en el trabajo de traducción.

![chlimage_1-257](assets/chlimage_1-257.png)

## Ver detalles del proyecto de traducción {#seeing-translation-project-details}

El mosaico Resumen de traducción contiene las propiedades configuradas para un proyecto de traducción. Además de la [información genérica del proyecto](/help/sites-authoring/projects.md#project-info), la pestaña Translation contiene propiedades específicas de la traducción:

* Idioma de origen: El idioma de las páginas que se están traduciendo.
* Idioma de destino: El idioma en que se traducen las páginas.
* Método de traducción: Flujo de trabajo de traducción. Se admite la traducción humana o la traducción automática.
* Proveedor de traducción: El proveedor de servicios de traducción que está realizando la traducción.
* Categoría de contenido: (Traducción automática) La categoría de contenido que se utiliza para la traducción.
* Configuración de nube: La configuración de nube para el conector del servicio de traducción que se utiliza para el proyecto.

Cuando se crea un proyecto con el panel Recursos de una página, estas propiedades se configuran automáticamente según las propiedades de la página de origen.

![chlimage_1-258](assets/chlimage_1-258.png)

## Monitorización del estado de un trabajo de traducción {#monitoring-the-status-of-a-translation-job}

El mosaico Trabajo de traducción de un proyecto de traducción proporciona el estado de un trabajo de traducción, así como el número de páginas y recursos del trabajo.

![chlimage_1-259](assets/chlimage_1-259.png)

En la tabla siguiente se describe cada estado que puede tener un trabajo o un elemento del trabajo:

| Estado | Descripción |
|---|---|
| Borrador | El trabajo de traducción no se ha iniciado. Los trabajos de traducción están en estado BORRADOR cuando se crean. |
| Enviado | Los archivos del trabajo de traducción tienen este estado cuando se han enviado correctamente al servicio de traducción. Este estado puede ocurrir después de que se emita el comando Solicitar ámbito o el comando Inicio. |
| Previsión solicitada | Para el flujo de trabajo Traducción humana, los archivos del trabajo se han enviado al proveedor de traducción para que los examine. Este estado aparece después de emitir el comando Solicitar ámbito. |
| Previsión finalizada | El proveedor ha creado un ámbito para el trabajo de traducción. |
| Comprometido para traducción | El propietario del proyecto ha aceptado el alcance. Este estado indica que el proveedor de traducción debe empezar a traducir los archivos del trabajo. |
| Traducción En Curso | Para un trabajo, la traducción de uno o más archivos del trabajo aún no está completa. Para un elemento del trabajo, el artículo se está traduciendo. |
| Traducido | Para un trabajo, se ha completado la traducción de todos los archivos del trabajo. Para un artículo del trabajo, el artículo se traduce. |
| Listo para revisión | El elemento del trabajo se traduce y el archivo se ha importado a AEM. |
| Completar | El propietario del proyecto ha indicado que el contrato de traducción ha concluido. |
| Cancelar | Indica que el proveedor de traducción debe dejar de trabajar en un trabajo de traducción. |
| Actualización de error | Se ha producido un error al transferir archivos entre AEM y el servicio de traducción. |
| Estado desconocido | Se ha producido un error desconocido. |

Para ver el estado de cada archivo en el trabajo, toque o haga clic en los puntos suspensivos en la parte inferior del mosaico.

## Configuración de la fecha de vencimiento de los trabajos de traducción {#setting-the-due-date-of-translation-jobs}

Especifique la fecha antes de la cual el proveedor de traducción debe devolver los archivos traducidos. Puede establecer la fecha de vencimiento del proyecto o de un trabajo específico:

* **Proyecto:** los trabajos de traducción del proyecto heredan la fecha de vencimiento.
* **Trabajo:** la fecha de vencimiento establecida para el trabajo anula la fecha de vencimiento establecida para el proyecto.

La configuración de la fecha de vencimiento funciona correctamente solo cuando el proveedor de traducción que está utilizando admite esta función.

El siguiente procedimiento establece la fecha de vencimiento de un proyecto.

1. Toque o haga clic en los puntos suspensivos en la parte inferior del mosaico Resumen de traducción.

   ![chlimage_1-260](assets/chlimage_1-260.png)

1. En la ficha Básico , utilice el selector de fechas de la propiedad Fecha de vencimiento para seleccionar la fecha de vencimiento.

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. Toque o haga clic en Finalizado.

El siguiente procedimiento establece la fecha de vencimiento de un trabajo de traducción.

1. En el mosaico Trabajo de traducción, toque o haga clic en el menú de comandos y, a continuación, toque o haga clic en Fecha de vencimiento.

   ![chlimage_1-262](assets/chlimage_1-262.png)

1. En el cuadro de diálogo, toque o haga clic en el icono de calendario y, a continuación, seleccione la fecha y la hora de uso como fecha de vencimiento y, a continuación, haga clic en Guardar.

   ![chlimage_1-263](assets/chlimage_1-263.png)

## Creación de ámbitos para un trabajo de traducción {#scoping-a-translation-job}

Alcance un trabajo de traducción para obtener una estimación del coste de traducción de su proveedor de servicios de traducción. Cuando se define un trabajo, los archivos de origen se envían al proveedor de traducción que compara el texto con su grupo de traducciones almacenadas (memoria de traducción). Normalmente, el ámbito es el número de palabras que se deben traducir.

Para obtener más información sobre los resultados de alcance, póngase en contacto con el proveedor de traducción.

>[!NOTE]
>
>El ámbito es opcional. Puede iniciar un trabajo de traducción sin ámbitos.

Cuando se define un trabajo de traducción, el estado del trabajo es `Scope Requested`. Cuando el proveedor de traducción devuelve el ámbito, el estado cambia a `Scope Completed`. Cuando finalice el alcance, puede utilizar el comando Mostrar ámbito para revisar los resultados del alcance.

El ámbito funciona correctamente solo cuando el proveedor de traducción que está utilizando admite esta función.

1. En la consola Proyectos , abra el proyecto de traducción.
1. En el mosaico Trabajo de traducción, pulse o haga clic en el menú de comandos y, a continuación, pulse o haga clic en Solicitar ámbito.

   ![chlimage_1-264](assets/chlimage_1-264.png)

1. Cuando el estado del trabajo cambie a SCOPE_COMPLETED, en el mosaico Trabajo de traducción pulse o haga clic en el menú de comandos y, a continuación, pulse o haga clic en Mostrar ámbito.

## Inicio de un trabajo de traducción {#starting-a-translation-job}

Inicie un trabajo de traducción para traducir las páginas de origen al idioma de destino. La traducción se realiza según los valores de propiedad del mosaico Resumen de traducción.

Después de iniciar el trabajo de traducción, el mosaico Trabajo de traducción muestra el estado Traducción en curso.

![chlimage_1-265](assets/chlimage_1-265.png)

1. En la consola Proyectos , abra el proyecto de traducción.
1. En el mosaico Trabajo de traducción, toque o haga clic en el menú de comandos y, a continuación, toque o haga clic en Inicio.

   ![chlimage_1-266](assets/chlimage_1-266.png)

1. En el cuadro de diálogo Acción que confirma el inicio de la traducción, toque o haga clic en Cerrar.

## Cancelación de un trabajo de traducción {#canceling-a-translation-job}

Cancelar un trabajo de traducción para detener el proceso de traducción e impedir que el proveedor de traducción realice más traducciones. Puede cancelar un trabajo cuando el trabajo tenga el estado `Committed For Translation` o `Translation In Progress`.

1. En la consola Proyectos , abra el proyecto de traducción.
1. En el mosaico Trabajo de traducción, toque o haga clic en el menú de comandos y, a continuación, toque o haga clic en Cancelar.
1. En el cuadro de diálogo Acción que confirma la cancelación de la traducción, pulse o haga clic en Aceptar.

## Aceptar/Rechazar flujo de trabajo {#accept-reject-workflow}

Cuando el contenido vuelve después de la traducción y está en estado Listo para revisión, puede ir al trabajo de traducción y aceptar/rechazar el contenido.

![chlimage_1-267](assets/chlimage_1-267.png)

Si selecciona Rechazar traducción, tiene la opción de agregar un comentario.

![chlimage_1-268](assets/chlimage_1-268.png)

El rechazo de contenido lo devuelve al proveedor de traducción donde podrá ver el comentario.

## Revisión y promoción del contenido actualizado {#reviewing-and-promoting-updated-content}

Cuando el contenido se traduce para una copia de idioma existente, revise las traducciones, realice cambios si es necesario y, a continuación, promueva las traducciones para moverlo a la copia de idioma. Puede revisar los archivos traducidos cuando el trabajo de traducción muestre el estado Listo para revisión .

![chlimage_1-269](assets/chlimage_1-269.png)

1. Seleccione la página en el patrón de idioma, pulse o haga clic en Referencias y, a continuación, pulse o haga clic en Textos en idiomas.
1. Toque o haga clic en la copia de idioma para revisarla.

   ![chlimage_1-270](assets/chlimage_1-270.png)

1. Toque o haga clic en Launch para mostrar los comandos relacionados con el lanzamiento.

   ![chlimage_1-271](assets/chlimage_1-271.png)

1. Para abrir la copia de lanzamiento de la página para revisar y editar el contenido, haga clic en Abrir página.
1. Después de revisar el contenido y realizar los cambios necesarios, para promocionar la copia de lanzamiento, haga clic en Promocionar.
1. En la página Promocionar lanzamiento , especifique las páginas que desea promocionar y, a continuación, toque o haga clic en Promocionar .

## Comparación de copias de idioma {#comparing-language-copies}

Para comparar copias de idioma con el idioma maestro:

1. En la consola **Sitios**, vaya a la copia de idioma que desee comparar.
1. Abra el panel **[Referencias](/help/sites-authoring/basic-handling.md#references)**.
1. En el encabezado **Copies** seleccione **Textos en idiomas.**
1. Seleccione la copia de idioma específica y, a continuación, puede hacer clic en **Comparar con maestro **o **Comparar con anterior **si corresponde.

   ![chlimage_1-37](assets/chlimage_1-37.jpeg)

1. Las dos páginas (lanzamiento y origen) se abrirán en paralelo.

   Para obtener información completa sobre el uso de esta característica, consulte la [diferencia de la página](/help/sites-authoring/page-diff.md).

## Finalización y archivado de trabajos de traducción {#completing-and-archiving-translation-jobs}

Complete un trabajo de traducción después de haber revisado los archivos traducidos del proveedor. Para los flujos de trabajo de traducción humana, completar una traducción indica al proveedor que el contrato de traducción se ha cumplido y que debe guardar la traducción en su memoria de traducción.

Una vez completado el trabajo, el trabajo tiene el estado Complete .

![chlimage_1-272](assets/chlimage_1-272.png)

Archive un trabajo de traducción una vez completado y ya no necesita ver los detalles del estado del trabajo. Al archivar el trabajo, el mosaico Trabajo de traducción se elimina del proyecto.

## Creación de la estructura de una copia de idioma {#creating-the-structure-of-a-language-copy}

Rellene la copia de idioma para que contenga contenido del idioma maestro que está traduciendo. Antes de rellenar la copia de idioma, debe haber [creado la raíz del idioma](/help/sites-administering/tc-prep.md#creating-a-language-root) de la copia de idioma.

1. Utilice la consola Sitios para seleccionar la raíz de idioma del idioma maestro que está utilizando como origen. Por ejemplo, para traducir las páginas en inglés del sitio de demostración de Geometrixx, seleccione Contenido > Sitio de demostración de Geometrixx > Inglés.
1. En la barra de herramientas, pulse o haga clic en Referencias.

   ![chlimage_1-273](assets/chlimage_1-273.png)

1. Seleccione Textos en idiomas y, a continuación, seleccione los textos en idiomas que desea rellenar.

   ![chlimage_1-38](assets/chlimage_1-38.jpeg)

1. Toque o haga clic en Actualizar copias de idioma para mostrar las herramientas de traducción y configure las propiedades:

   * Seleccione la opción Select All Sub-pages .
   * Para Project, seleccione Crear estructura solamente.

   ![chlimage_1-39](assets/chlimage_1-39.jpeg)

1. Toque o haga clic en Iniciar.

## Creación de un proyecto de traducción mediante la consola Proyectos {#creating-a-translation-project-using-the-projects-console}

Puede crear manualmente un proyecto de traducción si prefiere usar la consola Proyectos .

>[!NOTE]
>
>Para crear un proyecto, la cuenta debe ser miembro del grupo `project-administrators` .

Cuando cree manualmente un proyecto de traducción, debe proporcionar valores para las siguientes propiedades relacionadas con la traducción, además de las [propiedades básicas](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project):

* **Nombre:** Nombre del proyecto.
* **Idioma de origen:** el idioma del contenido de origen.
* **Idioma de destino:** el idioma en el que se traduce el contenido.
* **Método de traducción:** seleccione Traducción humana para indicar que la traducción se debe realizar manualmente.

1. En la barra de herramientas de la consola Proyectos , toque o haga clic en Crear .
1. Seleccione la plantilla Proyecto de traducción y, a continuación, toque o haga clic en Siguiente.
1. Introduzca valores para las propiedades básicas.
1. Toque o haga clic en Avanzadas y proporcione valores para las propiedades relacionadas con la traducción.
1. Haga clic o pulse Crear. En el cuadro de confirmación, toque o haga clic en Listo para volver a la consola Proyectos o haga clic o pulse Abrir proyecto para abrir y comenzar a administrar el proyecto.

## Exportación de un trabajo de traducción {#exporting-a-translation-job}

Puede descargar el contenido de un trabajo de traducción, por ejemplo, para enviarlo a un proveedor de traducción que no esté integrado con AEM a través de un conector o para revisar el contenido.

1. En el menú desplegable del mosaico Trabajo de traducción , pulse o haga clic en Exportar.
1. En el cuadro de diálogo Exportar, pulse o haga clic en Descargar archivo exportado y, si es necesario, utilice el cuadro de diálogo del explorador web para guardar el archivo.
1. En el cuadro de diálogo Exportar, pulse o haga clic en Cerrar.

## Importación de un trabajo de traducción {#importing-a-translation-job}

Puede importar contenido traducido a AEM, por ejemplo, cuando el proveedor de traducción se lo envía porque no están integrados con AEM a través de un conector.

1. En el menú desplegable del mosaico Trabajo de traducción , pulse o haga clic en Importar.
1. Utilice el cuadro de diálogo del explorador web para seleccionar el archivo que desea importar.
1. En el cuadro de diálogo Importar, pulse o haga clic en Cerrar.

