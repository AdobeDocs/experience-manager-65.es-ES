---
title: Informes
seo-title: Reporting
description: Aprenda a trabajar con Informes en AEM.
seo-description: Learn how to work with Reporting in AEM.
uuid: eee4befd-5fa9-4ebc-8eea-56e1534a6b9b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 7e2b30a3-75ff-4735-8038-5c5391ac36f3
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
source-git-commit: 429f3ee859477fb38938fd6b9706c8006623eb03
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 5%

---

# Informes {#reporting}

Para ayudarle a supervisar y analizar el estado de su instancia, AEM proporciona una selección de informes predeterminados que pueden configurarse para sus necesidades individuales:

* [Informe de componentes](#component-report)
* [Uso del disco](#disk-usage)
* [Comprobación de estado](#health-check)
* [Informe de actividad de la página](#page-activity-report)
* [Informe de contenido generado por el usuario](#user-generated-content-report)
* [Informe del usuario](#user-report)
* [Informe de instancia de flujo de trabajo](#workflow-instance-report)
* [Informe de flujo de trabajo](#workflow-report)

>[!NOTE]
>
>Estos informes solo están disponibles en la IU clásica. Para ver la supervisión y los informes del sistema en la IU moderna, consulte la [Tablero de operaciones.](/help/sites-administering/operations-dashboard.md)

Se puede acceder a todos los informes desde la **Herramientas** consola. Select **Informes** en el panel izquierdo, haga doble clic en el informe requerido en el panel derecho para abrirlo para verlo o configurarlo.

También se pueden crear nuevas instancias de un informe desde la variable **Herramientas** consola. Select **Informes** en el panel izquierdo y, a continuación, **Nuevo...** en la barra de herramientas. Defina un **Título** y **Nombre**, seleccione el tipo de informe que desee y haga clic en **Crear**. La nueva instancia del informe aparecerá en la lista. Haga doble clic en esto para abrirlo y, a continuación, arrastre un componente desde la barra de tareas para crear la primera columna e iniciar la definición del informe.

>[!NOTE]
>
>Además de los informes de AEM estándar disponibles de forma predeterminada, puede [desarrollar sus propios informes (completamente nuevos)](/help/sites-developing/dev-reports.md).

## Aspectos básicos de la personalización de informes {#the-basics-of-report-customization}

Hay varios formatos de informes disponibles. Los siguientes informes utilizan columnas que se pueden personalizar como se detalla en las secciones siguientes:

* [Informe de componentes](#component-report)
* [Informe de actividad de la página](#page-activity-report)
* [Informe de contenido generado por el usuario](#user-generated-content-report)
* [Informe del usuario](#user-report)
* [Informe de instancia de flujo de trabajo](#workflow-instance-report)

>[!NOTE]
>
>Los siguientes informes tienen su propio formato y personalización:
>
>
>* [Comprobación de estado](#health-check) utiliza los campos de selección para especificar los datos sobre los que desea crear el informe.
>* [Uso del disco](#disk-usage) utiliza vínculos para explorar en profundidad la estructura del repositorio.
>* [Informe de flujo de trabajo](/help/sites-administering/reporting.md#workflow-report) proporciona una descripción general de los flujos de trabajo que se ejecutan en la instancia.
>
>Por lo tanto, los siguientes procedimientos para la configuración de columnas no son apropiados. Consulte las descripciones de los informes individuales para ver sus detalles.

### Selección y colocación de las columnas de datos {#selecting-and-positioning-the-data-columns}

Las columnas se pueden agregar, cambiar de posición o eliminar de cualquiera de los informes, ya sea estándar o personalizado.

La variable **Componentes** en la barra de tareas (disponible en la página del informe) se enumeran todas las categorías de datos que se pueden seleccionar como columnas.

Para cambiar la selección de datos:

* para agregar una columna nueva, arrastre el componente requerido desde la barra de tareas y suéltelo en la posición que desee

   * un visto verde indicará cuándo es válida la posición y un par de flechas indicará exactamente dónde se colocará
   * un símbolo rojo sin signo indica si la posición no es válida

* para mover una columna, haga clic en el encabezado, mantenga presionada la tecla y arrástrela a la nueva posición
* para quitar una columna, haga clic en el título de la columna, mantenga presionada la columna y arrástrela hasta el área del encabezado del informe (un símbolo rojo menos indicará que la posición no es válida); suelte el botón del ratón y el cuadro de diálogo Eliminar componentes solicitará confirmación de que realmente desea eliminar la columna.

### Menú desplegable Columna {#column-drop-down-menu}

Cada columna del informe tiene un menú desplegable. Esto se vuelve visible cuando el cursor del ratón se mueve sobre la celda del título de la columna.

En el extremo derecho de la celda del título, aparecerá una cabeza de flecha (no debe confundirse con la cabeza de flecha que aparece inmediatamente a la derecha del texto del título que indica la variable [mecanismo de ordenación actual](#sorting-the-data)).

![reportcolumnsort](assets/reportcolumnsort.png)

Las opciones disponibles en el menú dependerán de la configuración de la columna (tal y como se hace durante el desarrollo del proyecto), las opciones no válidas se atenuarán.

### Clasificación de los datos {#sorting-the-data}

Los datos se pueden ordenar según una columna específica:

* hacer clic en el encabezado de columna correspondiente; la ordenación cambiará entre ascendente y descendente, indicada por una flecha situada justo al lado del texto del título
* use el [menú desplegable de la columna](#column-drop-down-menu) para seleccionar **Orden ascendente** o **Orden descendente**; de nuevo, esto se indicará con una cabeza de flecha justo al lado del texto del título

### Grupos y el gráfico de datos actuales {#groups-and-the-current-data-chart}

En las columnas apropiadas, puede seleccionar **Agrupar por esta columna** de la variable [menú desplegable de la columna](#column-drop-down-menu). De este modo, los datos se agrupan según cada valor distinto dentro de esa columna. Puede seleccionar más de una columna para agruparla. La opción se verá atenuada cuando los datos de la columna no sean adecuados; es decir, cada entrada es distinta y única, por lo que no se pueden formar grupos, por ejemplo la columna ID de usuario del informe de usuario.

Después de agrupar al menos una columna, un gráfico circular de **Datos actuales** se generarán en función de esta agrupación. Si se agrupan varias columnas, también se indicará en el gráfico.

![reportuser](assets/reportuser.png)

Si se mueve el cursor sobre el gráfico circular, se mostrará el valor agregado para el segmento correspondiente. Utiliza el agregado definido actualmente para la columna; por ejemplo, count, Minimum, average, entre otros.

### Filtros y agregados {#filters-and-aggregates}

En las columnas apropiadas también puede configurar **Configuración de filtro** y/o **Agregados** de la variable [menú desplegable de la columna](#column-drop-down-menu).

#### Filtros {#filters}

La configuración de filtro le permite especificar los criterios para que se muestren las entradas. Los operadores disponibles son:

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

Para definir un filtro:

1. Seleccione el operador que desee en la lista desplegable.
1. Introduzca el texto en el que desea filtrar.
1. Haga clic en **Aplicar**.

Para desactivar el filtro:

1. Elimine el texto del filtro.
1. Haga clic en **Aplicar**.

#### Agregados {#aggregates}

También puede seleccionar un método de agregación (estos pueden variar según la columna seleccionada):

![reportaggregate](assets/reportaggregate.png)

### Propiedades de columna {#column-properties}

Esta opción solo está disponible cuando la variable [Columna genérica](#generic-column) se ha utilizado en la variable [Informe de usuario](#user-report).

### Datos históricos {#historic-data}

Puede ver un gráfico del cambio en los datos a lo largo del tiempo en **Datos históricos**. Esto se deriva de las instantáneas tomadas a intervalos regulares.

Los datos son:

* Recopilado por, si está disponible, la primera columna ordenada; en caso contrario, la primera columna (no agrupada)
* Agrupado por la columna adecuada

El informe se puede generar:

1. Establezca **Agrupación** en la columna requerida.
1. **Editar** la configuración para definir la frecuencia con la que se deben realizar las instantáneas; por hora o por día.
1. **Finalizar...** la definición para iniciar la colección de instantáneas.

   El botón deslizante rojo/verde en la parte superior izquierda indica cuándo se recopilan las instantáneas.

El gráfico resultante se muestra en la parte inferior derecha:

![tendencias de informes](assets/reporttrends.png)

Una vez iniciada la recopilación de datos, puede seleccionar:

* **Período**

   Puede seleccionar entre y hasta las fechas para que se muestren los datos del informe.

* **Intervalo**

   Se puede seleccionar Mes, Semana, Día, Hora para la escala y la agregación del informe.

   Por ejemplo, si hay instantáneas diarias disponibles para febrero de 2011:

   * Si el intervalo está establecido en `Day`, cada instantánea se muestra como un solo valor en el gráfico.
   * Si el intervalo está establecido en `Month`, todas las instantáneas de febrero se acumulan en un solo valor (mostrado como un solo &quot;punto&quot; en el gráfico).

Seleccione los requisitos y haga clic en **Ir** para aplicarlos al informe. Para actualizar la visualización después de realizar más instantáneas, haga clic en **Ir** de nuevo.

![imagen_1-43](assets/chlimage_1-43.png)

Cuando se recopilan instantáneas, puede:

* Uso **Finalizar...** para reiniciar la colección.

   **Finalizar** &quot;bloquea&quot; la estructura del informe (es decir, las columnas asignadas al informe y que se agrupan, ordenan, filtran, etc.) y comienza a tomar instantáneas.

* Abra el **Editar** cuadro de diálogo que desea seleccionar **Sin instantáneas de datos** para finalizar la recopilación hasta que sea necesario.

   **Editar** solo activa o desactiva la toma de instantáneas. Si se vuelve a activar la toma de instantáneas, se utiliza el estado del informe cuando finalizó por última vez para tomar más instantáneas.

>[!NOTE]
>
>Las instantáneas se almacenan en `/var/reports/...` donde el resto de la ruta refleja la ruta del informe y el ID respectivos creados cuando el informe finalizó.
>
>
>Las instantáneas antiguas se pueden eliminar manualmente si está completamente seguro de que ya no necesita esas instancias.

>[!NOTE]
>
>Los informes preconfigurados no requieren un alto rendimiento, pero se recomienda utilizar instantáneas diarias en un entorno de producción. Si es posible, ejecute estas instantáneas diarias en un momento del día en el que no haya mucha actividad en su sitio web; esto se puede definir con la variable `Daily snapshots (repconf.hourofday)` para **Configuración de informes CQ de día**; see [Configuración OSGI](/help/sites-deploying/configuring-osgi.md) para obtener más información sobre cómo configurarlo.

#### Límites de visualización {#display-limits}

El informe de datos históricos también puede cambiar ligeramente de aspecto debido a los límites que se pueden configurar, según el número de resultados para el periodo seleccionado.

Cada línea horizontal se conoce como serie (y corresponde a una entrada en la leyenda del gráfico), cada columna vertical de puntos representa las instantáneas agregadas.

![imagen_1-44](assets/chlimage_1-44.png)

Para mantener el gráfico limpio durante períodos de tiempo más largos, hay límites que se pueden configurar. Para los informes estándar, estos son:

* serie horizontal: tanto el valor predeterminado como el máximo del sistema son `9`

* instantáneas agregadas verticales: el valor predeterminado es `35` (por serie horizontal)

Por lo tanto, cuando se exceden los límites (adecuados), se recomienda:

* los puntos no se muestran
* es posible que el pie de ilustración del gráfico de datos histórico muestre un número diferente de entradas al del gráfico de datos actual

![chlimage_1-45](assets/chlimage_1-45.png)

Los informes personalizados también pueden mostrar la variable **Total** para todas las series. Se muestra como una serie (línea horizontal y entrada en la leyenda).

>[!NOTE]
>
>Para los informes personalizados, los límites se pueden configurar de forma diferente.

### Editar (informe) {#edit-report}

La variable **Editar** abre **Editar informe** Cuadro de diálogo.

Esta es una ubicación en la que el periodo para recopilar instantáneas para [Datos históricos](#historic-data) está definida, pero también se pueden definir varias otras configuraciones:

![reportedit](assets/reportedit.png)

* **Título**

   Puede definir su propio título.

* **Descripción**

   Puede definir su propia descripción.

* **Ruta raíz** (*solo activa para determinados informes*)

   Utilícelo para limitar el informe a una sección (subsección) del repositorio.

* **Procesamiento de informes**

   * **datos actualizados automáticamente**

      Los datos del informe se actualizarán cada vez que actualice la definición del informe.

   * **datos actualizados manualmente**

      Esta opción se puede utilizar para evitar demoras causadas por las operaciones de actualización automática cuando hay un gran volumen de datos.

      Si selecciona esta opción, los datos del informe deben actualizarse manualmente cuando haya cambiado cualquier aspecto de la configuración del informe. También significa que tan pronto como cambie cualquier aspecto de la configuración, la tabla del informe quedará en blanco.

      Cuando se selecciona esta opción, la variable **[Carga de datos](#load-data)** se muestra (junto a **Editar** en el informe). **Carga de datos** cargará los datos y actualizará los datos del informe mostrados.

* **Instantáneas**
Puede definir la frecuencia con la que se realizan las instantáneas; diariamente, por hora o no.

### Cargar datos {#load-data}

La variable **Carga de datos** solo está visible cuando **actualizar manualmente los datos** se ha seleccionado de **[Editar](#edit-report)**.

![imagen_1-46](assets/chlimage_1-46.png)

Haga clic en **Carga de datos** volverá a cargar los datos y actualizará el informe que se muestra.

Si selecciona esta opción para actualizar manualmente los datos:

1. Tan pronto como cambie la configuración del informe, la tabla de datos del informe quedará en blanco.

   Por ejemplo, si cambia el mecanismo de ordenación de una columna, no se mostrarán los datos.

1. Si desea que los datos del informe se muestren de nuevo, deberá hacer clic en **Carga de datos** para volver a cargar los datos.

### Finalizar (informe) {#finish-report}

Cuando **Finalizar** el informe:

* La definición del informe *a partir de ese momento* se utilizará para tomar las instantáneas (después puede seguir trabajando en una definición de informe ya que luego es independiente de las instantáneas).
* Se eliminarán todas las instantáneas existentes.
* Las nuevas instantáneas se recopilan para el [Datos históricos](#historic-data).

Con este cuadro de diálogo puede definir o actualizar su propio título y descripción para el informe resultante.

![reportend](assets/reportfinish.png)

## Tipos de informes {#report-types}

### Informe de componentes {#component-report}

El informe de componentes proporciona información sobre cómo el sitio web utiliza los componentes.

[Columnas de información](#selecting-and-positioning-the-data-columns) acerca de:

* Autor
* Ruta del componente
* Tipo de componente
* Última modificación
* Página

Significa que puede ver, por ejemplo:

* Qué componentes se utilizan donde.

   Útil, por ejemplo, al realizar pruebas.

* Cómo se distribuyen las instancias de un componente específico.

   Esto puede resultar interesante si se usan páginas específicas (p. ej. &quot;páginas pesadas&quot;) están experimentando problemas de rendimiento.

* Identificar partes del sitio con cambios frecuentes/menos frecuentes.
* Consulte cómo se desarrolla el contenido de la página a lo largo del tiempo.

Se incluyen todos los componentes, estándar de producto y específicos de proyecto. Al usar la variable **Editar** diálogo el usuario también puede establecer un **Ruta raíz** que define el punto de partida del informe: todos los componentes de esa raíz se consideran para el informe.

![componente de informe](assets/reportcomponent.png) ![reportcompentall](assets/reportcompentall.png)

### Uso del disco {#disk-usage}

El informe de uso del disco muestra información sobre los datos almacenados en el repositorio.

El informe se inicia en la raíz ( / ) del repositorio; al hacer clic en una rama en particular, puede explorar en profundidad dentro del repositorio (la ruta actual se reflejará en el título del informe).

![reportdiskusage](assets/reportdiskusage.png)

### Comprobación de estado {#health-check}

Este informe analiza el registro de solicitudes actual:

`<cq-installation-dir>/crx-quickstart/logs/request.log`
para ayudarle a identificar las solicitudes más costosas dentro de un periodo determinado.

Para generar el informe, puede especificar:

* **Periodo (horas)**

   Número de horas (pasadas) que se van a analizar.

   Predeterminado: `24`

* **max. Resultados**

   Número máximo de líneas de salida.

   Predeterminado: `50`

* **max. Solicitudes**

   Número máximo de solicitudes que se van a analizar.

   Predeterminado: `-1` (todos)

* **Dirección de correo electrónico**

   Envíe los resultados a una dirección de correo electrónico.

   Opcional; Predeterminado: blank

* **Ejecutar cada día a las (hh:mm)**

   Especifique una hora para que el informe se ejecute automáticamente a diario.

   Opcional; Predeterminado: blank

![reportthe](assets/reporthealth.png)

### Informe de actividad de la página {#page-activity-report}

El informe de actividad de página enumera las páginas y las acciones realizadas en ellas.

[Columnas de información](#selecting-and-positioning-the-data-columns) acerca de:

* Página
* Hora
* Tipo
* Usuario

Significa que puede monitorizar:

* Últimas modificaciones.
* Autores que trabajan en páginas específicas.
* Páginas que no se han modificado recientemente, por lo que puede que necesiten alguna acción.
* Páginas que se cambian con mayor o menor frecuencia.
* Usuarios más/menos activos.

El informe de actividad de página toma toda la información del registro de auditoría. De forma predeterminada, la ruta raíz está configurada en el registro de auditoría en `/var/audit/com.day.cq.wcm.core.page`.

![reportpageactivity](assets/reportpageactivity.png)

### Informe de contenido generado por el usuario {#user-generated-content-report}

Este informe proporciona información sobre el contenido generado por el usuario; sean comentarios, clasificaciones o foros.

[Columnas de información](#selecting-and-positioning-the-data-columns) en:

* Fecha
* Dirección IP
* Página
* Referencia
* Tipo
* Identificador de usuario

Permita:

* Ver las páginas que reciben más comentarios.
* Obtenga una descripción general de todos los comentarios que abandonan los visitantes específicos del sitio, tal vez los problemas estén relacionados.
* Juzgue si el nuevo contenido está provocando comentarios mediante la supervisión cuando los comentarios se hacen en una página.

![reportusercontent](assets/reportusercontent.png)

### Informe del usuario {#user-report}

Este informe proporciona información sobre todos los usuarios que han registrado una cuenta o perfil; esto puede incluir tanto a autores dentro de su organización como a visitantes externos.

[Columnas de información](#selecting-and-positioning-the-data-columns) (si está disponible) acerca de:

* Edad
* País
* Dominio
* Correo electrónico
* Apellido
* Sexo
* [Genérico](#generic-column)
* Nombre de pila
* Información
* Interés
* Idioma
* Código Hash NTLM
* ID de usuario

Permita:

* Consulte la expansión demográfica de los usuarios.
* Informe de los campos personalizados que ha agregado a los perfiles.

![reportusercanned](assets/reportusercanned.png)

#### Columna genérica {#generic-column}

La variable **Genéricas** está disponible en el Informe de usuarios para que pueda acceder a la información personalizada, normalmente desde la [perfiles de usuario](/help/sites-administering/identity-management.md#profiles-and-user-accounts); por ejemplo, [Color favorito tal como se detalla en Añadir campos a la definición del perfil](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

El cuadro de diálogo Columna genérica se abrirá cuando:

* Arrastre el componente Genérico de la barra de tareas al informe.
* Seleccione Propiedades de columna para una columna genérica existente.

![reportusrgenericcolm](assets/reportusrgenericcolm.png)

En el **Definiciones** puede definir:

* **Título**

   Su propio título para la columna genérica.

* **Propiedad**

   El nombre de propiedad tal como se almacena en el repositorio, generalmente dentro del perfil del usuario.

* **Ruta**

   Normalmente, la propiedad se toma del `profile`.

* **Tipo**

   Seleccione el tipo de campo de `String`, `Number`, `Integer`, `Date`.

* **Agregado predeterminado**

   Esto define el agregado utilizado de forma predeterminada si la columna se desagrupa en un informe con al menos una columna agrupada. Seleccione el agregado requerido de `Count`, `Minimum`, `Average`, `Maximum`, `Sum`.

   Por ejemplo, *Recuento* para un `String` campo significa que el número de `String` para la columna en el estado agregado.

En el **Extendido** también puede definir los agregados y filtros disponibles:

![reportusrgenericcolmextented](assets/reportusrgenericcolmextented.png)

### Informe de instancia de flujo de trabajo {#workflow-instance-report}

Esto le ofrece una descripción general concisa, que proporciona información sobre las instancias individuales de los flujos de trabajo, tanto en ejecución como completadas.

[Columnas de información](#selecting-and-positioning-the-data-columns) acerca de:

* Completado
* Duración
* Iniciador
* Modelo
* Carga útil
* Iniciado
* Estado

Significa que puede:

* Monitorizar la duración media de los flujos de trabajo; si esto sucede con regularidad, puede resaltar problemas con el flujo de trabajo.

![reportworkflowintance](assets/reportworkflowintance.png)

### Informe de flujo de trabajo {#workflow-report}

Esto proporciona estadísticas clave sobre los flujos de trabajo que se ejecutan en la instancia.

![flujo de trabajo de informes](assets/reportworkflow.png)

## Uso de informes en un entorno de publicación {#using-reports-in-a-publish-environment}

Una vez configurados los informes según sus requisitos específicos, puede activarlos para transferir la configuración al entorno de publicación.

>[!CAUTION]
>
>Si desea **Datos históricos** para el entorno de publicación, **Finalizar** informe sobre el entorno de creación antes de activar la página.

A continuación, se puede acceder al informe correspondiente en

`/etc/reports`

Por ejemplo, el informe Contenido generado por el usuario se encuentra en:

`http://localhost:4503/etc/reports/ugcreport.html`

Esto ahora informará sobre los datos recopilados del entorno de publicación.

Como no se permite ninguna configuración de informe en el entorno de publicación, la variable **Editar** y **Finalizar** no están disponibles. Sin embargo, puede seleccionar el **Periodo** y **Intervalo** para el **Datos históricos** informe si se están recopilando instantáneas.

![reportsucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>El acceso a estos informes puede ser un problema de seguridad; por lo tanto, le recomendamos que configure Dispatcher para que `/etc/reports` no está disponible para visitantes externos. Consulte la [Lista de comprobación de seguridad](security-checklist.md) para obtener más información.

## Permisos necesarios para ejecutar informes {#permissions-needed-for-running-reports}

Los permisos necesarios dependen de la acción :

* Los datos del informe se recopilan básicamente con los privilegios del usuario actual.
* Los datos históricos se recopilan con los privilegios del usuario que ha finalizado el informe.

En una instalación de AEM estándar, los siguientes permisos están preestablecidos para los informes:

* **Informe del usuario**

   `user administrators` - leer y escribir

* **Informe de actividad de la página**

   `contributors` - leer y escribir

* **Informe de componentes**

   `contributors` - leer y escribir

* **Informe de contenido generado por el usuario**

   `contributors` - leer y escribir

* **Informe de instancia de flujo de trabajo**

   `workflow-users` - leer y escribir

Todos los miembros del `administrators` tienen los derechos necesarios para crear nuevos informes.
