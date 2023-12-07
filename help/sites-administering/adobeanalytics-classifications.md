---
title: Clasificaciones de Adobe
description: Aprenda a utilizar las clasificaciones de Adobes para exportar datos de clasificaciones a Adobe Analytics.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 5%

---

# Clasificaciones de Adobe{#adobe-classifications}

Clasificaciones de Adobes exporta datos de clasificaciones a [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de forma programada. El exportador es una implementación de un **com.adobe.cq.scheduled.exporter.Exporter**.

Para configurar esto:

1. Uso de **Navegación**, seleccione **Herramientas**, **Cloud Service**, entonces **Cloud Service heredados**.
1. Desplazarse a **Adobe Analytics** y seleccione **Mostrar configuraciones**.
1. Haga clic en **[+]** junto a la configuración de Adobe Analytics.

1. En el **Crear marco** diálogo:

   * Especifique un **Título**.
   * Si lo desea, puede especificar **Nombre**, para el nodo que almacena los detalles del marco de trabajo en el repositorio.
   * Seleccionar **Clasificaciones de Adobe Analytics**

   Y haga clic en **Crear**.

   ![Cuadro de diálogo Crear marco](assets/aa-25.png)

1. El **Configuración de clasificaciones** se abre para editarlo.

   ![Diálogo Configuración de clasificaciones](assets/aa-classifications-settings.png)

   Las propiedades incluyen lo siguiente:

   | **Campo** | **Descripción** |
   |---|---|
   | Habilitado | Seleccionar **Sí** para habilitar la configuración de Clasificaciones de Adobe. |
   | Sobrescribir en caso de conflicto | Seleccionar **Sí** para sobrescribir cualquier conflicto de datos. De forma predeterminada, se establece en **No**. |
   | Eliminar procesados | Si se establece en **Sí**, elimina los nodos procesados una vez exportados. El valor predeterminado es **Falso**. |
   | Descripción de la tarea de exportación | Introduzca una descripción para el trabajo de clasificación de Adobes. |
   | Correo electrónico de notificación | Introduzca una dirección de correo electrónico para la notificación de clasificaciones de Adobes. |
   | Grupo de informes | Introduzca el grupo de informes para el que se ejecutará el trabajo de importación. |
   | Conjunto de datos | Introduzca el ID de relación del conjunto de datos para el que se ejecutará el trabajo de importación. |
   | Transformador | En el menú desplegable, seleccione una implementación de transformador. |
   | Fuente de datos | Vaya a la ruta del contenedor de datos. |
   | Programación de exportación | Seleccione la programación de la exportación. El valor predeterminado es cada 30 minutos. |

1. Clic **OK** para guardar la configuración.

## Modificación del tamaño de página {#modifying-page-size}

Los registros se procesan en páginas. De forma predeterminada, Clasificaciones de Adobe crea páginas con un tamaño de página de 1000.

Una página puede tener un tamaño 25000 máximo, por definición en Clasificaciones de Adobe, y puede modificarse desde la consola Felix. Durante la exportación, Clasificaciones de Adobe bloquea el nodo de origen para evitar modificaciones simultáneas. El nodo se desbloquea después de la exportación, por error o cuando se cierra la sesión.

Para cambiar el tamaño de la página:

1. Vaya a la consola OSGI en **https://&lt;host>:&lt;port>/system/console/configMgr** y seleccione **Adobe AEM Exportador de clasificaciones**.

   ![aa-26](assets/aa-26.png)

1. Actualice el **Exportar tamaño de página** según sea necesario, haga clic en **Guardar**.

## SAINTefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Las clasificaciones de Adobe se conocían anteriormente como el exportador SAINT.

Un exportador puede utilizar un transformador para transformar los datos de exportación a un formato específico. Para las clasificaciones de Adobe, una subinterfaz `SAINTTransformer<String[]>` se ha proporcionado la implementación de la interfaz del transformador. Esta interfaz se utiliza para restringir el tipo de datos a `String[]` que utiliza la API de SAINT y para tener una interfaz de marcador que busque estos servicios para seleccionarlos.

En la implementación predeterminada SAINTDefaultTransformer, los recursos secundarios del origen del exportador se tratan como registros con nombres de propiedad como claves y valores de propiedad como valores. El **Clave** La columna se añade automáticamente como primera columna: su valor será el nombre del nodo. Propiedades de espacio de nombres (que contienen `:`) no se tienen en cuenta.

*Estructura del nodo:*

* id-clasificación `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = Mi nombre de producto (String)
      * Price = 120.90 (String)
      * Tamaño = M (Cadena)
      * Color = negro (String)
      * Color^Código = 101 (Cadena)

**Encabezado y registro de SAINT:**

| **Clave** | **Producto** | **Precio** | **Tamaño** | **Color** | **Color^Código** |
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
   <td>Un nombre de clase de una implementación de SAINTransformer</td>
  </tr>
  <tr>
   <td>correo electrónico</td>
   <td>Dirección de correo electrónico de notificación.</td>
  </tr>
  <tr>
   <td>grupos de informes</td>
   <td>ID del grupo de informes para los que se ejecutará el trabajo de importación. </td>
  </tr>
  <tr>
   <td>conjunto de datos</td>
   <td>ID de relación del conjunto de datos para el que se ejecutará el trabajo de importación. </td>
  </tr>
  <tr>
   <td>descripción</td>
   <td>Descripción del trabajo. <br /> </td>
  </tr>
  <tr>
   <td>sobrescribir</td>
   <td>Indicador para sobrescribir los conflictos de datos. El valor predeterminado es <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>divisiones de comprobación</td>
   <td>Marcar para comprobar la compatibilidad de los grupos de informes. El valor predeterminado es <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Indicador para eliminar los nodos procesados después de la exportación. El valor predeterminado es <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatización de la exportación de clasificaciones de Adobe {#automating-adobe-classifications-export}

Puede crear su propio flujo de trabajo, de modo que las nuevas importaciones inicien el flujo de trabajo para crear los datos adecuados y correctamente estructurados en **/var/export/** para que se pueda exportar a Clasificaciones de Adobes.
