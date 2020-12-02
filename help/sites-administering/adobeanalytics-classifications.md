---
title: Clasificaciones de Adobes
seo-title: Clasificaciones de Adobes
description: Obtenga información sobre las clasificaciones de Adobe.
seo-description: Obtenga información sobre las clasificaciones de Adobe.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
translation-type: tm+mt
source-git-commit: 4456b5366387c27810c407d6ac9e6c17fc290269
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 5%

---


# Clasificaciones de Adobes{#adobe-classifications}

Las clasificaciones de Adobe exportan datos de clasificaciones a [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de manera programada. El exportador es una implementación de **com.adobe.cq.scheduled.exporter.Exporter**.

Para configurar esto:

1. Utilizando **Navegación**, seleccione **Herramientas**, **Cloud Services** y luego **Cloud Services heredados**.
1. Desplácese hasta **Adobe Analytics** y seleccione **Mostrar configuraciones**.
1. Haga clic en el vínculo **[+]** al lado de la configuración de Adobe Analytics.

1. En el cuadro de diálogo **Crear marco**:

   * Especifique un **Título**.
   * Opcionalmente, puede especificar el **Nombre** para el nodo que almacena los detalles del marco en el repositorio.
   * Seleccionar **Clasificaciones de Adobe Analytics**

   Y haga clic en **Crear**.

   ![Cuadro de diálogo Crear marco](assets/aa-25.png)

1. Se abre el cuadro de diálogo **Configuración de clasificaciones** para su edición.

   ![Cuadro de diálogo Configuración de clasificaciones](assets/aa-classifications-settings.png)

   Las propiedades incluyen lo siguiente:

   | **Campo** | **Descripción** |
   |---|---|
   | Activado | Seleccione **Sí** para habilitar la configuración de Clasificaciones de Adobe. |
   | Sobrescribir en caso de conflicto | Seleccione **Sí** para sobrescribir cualquier conflicto de datos. De forma predeterminada, se establece en **No**. |
   | Eliminar procesados | Si se establece en **Sí**, elimina los nodos procesados después de exportarlos. El valor predeterminado es **False**. |
   | Descripción de la tarea de exportación | Escriba una descripción para el trabajo de Clasificaciones de Adobe. |
   | Correo electrónico de notificación | Introduzca una dirección de correo electrónico para la notificación de clasificaciones de Adobe. |
   | Grupo de informes | Introduzca el grupo de informes para el cual ejecutar el trabajo de importación. |
   | Conjunto de datos | Introduzca el ID de relación de conjunto de datos para el que se ejecutará el trabajo de importación. |
   | Transformador | En el menú desplegable, seleccione una implementación de transformador. |
   | Fuente de datos | Vaya a la ruta del contenedor de datos. |
   | Programación de exportación | Seleccione la programación para la exportación. El valor predeterminado es cada 30 minutos. |

1. Haga clic en **Aceptar** para guardar la configuración.

## Modificación del tamaño de página {#modifying-page-size}

Los registros se procesan en páginas. De forma predeterminada, las clasificaciones de Adobe crean páginas con un tamaño de página de 1000.

Una página puede tener un tamaño máximo de 25000 páginas por definición en las clasificaciones de Adobe y puede modificarse desde la consola Félix. Durante la exportación, las clasificaciones de Adobe bloquean el nodo de origen para evitar modificaciones simultáneas. El nodo se desbloquea tras la exportación, por error o cuando se cierra la sesión.

Para cambiar el tamaño de la página:

1. Vaya a la consola OSGI en **https://&lt;host>:&lt;puerto>/system/console/configMgr** y seleccione **Adobe AEM Classifications Exporter**.

   ![aa-26](assets/aa-26.png)

1. Actualice **Exportar tamaño de página** según sea necesario y haga clic en **Guardar**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Las clasificaciones de Adobe se conocían anteriormente como SAINT Exporter.

Un exportador puede utilizar un transformador para transformar los datos de exportación a un formato específico. Para las clasificaciones de Adobe, se ha proporcionado una subinterfaz `SAINTTransformer<String[]>` que implementa la interfaz Transformador. Esta interfaz se utiliza para restringir el tipo de datos a `String[]`, que utiliza la API de SAINT, y para tener una interfaz de marcador para encontrar dichos servicios para la selección.

En la implementación predeterminada SAINTDefaultTransformer, los recursos secundarios del origen del exportador se tratan como registros con nombres de propiedad como claves y valores de propiedad como valores. La columna **Key** se agrega automáticamente como primera columna; su valor será el nombre del nodo. No se tienen en cuenta las propiedades con espacio de nombres (que contienen `:`).

*Estructura de nodos:*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = My Product Name (String)
      * Precio = 120,90 (Cadena)
      * Tamaño = M (Cadena)
      * Color = negro (cadena)
      * Color^Code = 101 (Cadena)

**Registro y encabezado del SAINT:**

| **Clave** | **Producto** | **Precio** | **Tamaño** | **Color** | **Color^Code** |
|---|---|---|---|---|---|
| 1 | Mi nombre de producto | 120,90 | M | black | 101 |

Las propiedades incluyen lo siguiente:

<table>
 <tbody>
  <tr>
   <td><strong>Ruta de propiedad</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>transformador</td>
   <td>Nombre de clase de una implementación de SAINTTransformer</td>
  </tr>
  <tr>
   <td>correo electrónico</td>
   <td>Dirección de correo electrónico de notificación.</td>
  </tr>
  <tr>
   <td>grupos de informes</td>
   <td>ID de grupos de informes para los que ejecutar el trabajo de importación. </td>
  </tr>
  <tr>
   <td>conjunto de datos</td>
   <td>Id. de relación de conjunto de datos para ejecutar el trabajo de importación. </td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Descripción del trabajo. <br /> </td>
  </tr>
  <tr>
   <td>sobrescribir</td>
   <td>Indicador para sobrescribir los conflictos de datos. El valor predeterminado es <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>divisiones de comprobación</td>
   <td>Marca para comprobar la compatibilidad de los grupos de informes. El valor predeterminado es <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>elimineprocesado</td>
   <td>Indicador para eliminar los nodos procesados después de la exportación. El valor predeterminado es <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatización de la exportación de clasificaciones de Adobe {#automating-adobe-classifications-export}

Puede crear su propio flujo de trabajo para que cualquier importación nueva inicie el flujo de trabajo a fin de crear los datos adecuados y correctamente estructurados en **/var/export/** para que se puedan exportar a las clasificaciones de Adobe.
