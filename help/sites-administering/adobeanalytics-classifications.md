---
title: Clasificaciones de Adobe
seo-title: Adobe Classifications
description: Obtenga información sobre las clasificaciones de Adobe.
seo-description: Learn about Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 7%

---

# Clasificaciones de Adobe{#adobe-classifications}

Clasificaciones de Adobe exporta datos de clasificaciones a [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de forma programada. El exportador es una aplicación de un **com.adobe.cq.scheduled.exporter.Exporter**.

Para configurar esto:

1. Uso **Navegación**, seleccione **Herramientas**, **Cloud Services**, luego **Cloud Services heredados**.
1. Desplácese hasta **Adobe Analytics** y seleccione **Mostrar configuraciones**.
1. Haga clic en el **[+]** vínculo junto a la configuración de Adobe Analytics.

1. En el **Crear marco** diálogo:

   * Especifique un **Título**.
   * Si lo desea, puede especificar la variable **Nombre**, para el nodo que almacena los detalles del marco en el repositorio.
   * Select **Clasificaciones de Adobe Analytics**

   Y haga clic en **Crear**.

   ![Cuadro de diálogo Crear marco](assets/aa-25.png)

1. La variable **Configuración de clasificaciones** se abre para editarlo.

   ![Cuadro de diálogo Configuración de clasificaciones](assets/aa-classifications-settings.png)

   Las propiedades incluyen lo siguiente:

   | **Campo** | **Descripción** |
   |---|---|
   | Activado | Select **Sí** para habilitar la configuración de clasificaciones de Adobe. |
   | Sobrescribir en caso de conflicto | Select **Sí** para sobrescribir cualquier conflicto de datos. De forma predeterminada, se establece en **No**. |
   | Eliminar procesados | Si está configurado como **Sí**, elimina los nodos procesados una vez exportados. El valor predeterminado es **False**. |
   | Descripción de la tarea de exportación | Introduzca una descripción para el trabajo Clasificaciones de Adobe. |
   | Correo electrónico de notificación | Introduzca una dirección de correo electrónico para la notificación de clasificaciones de Adobe. |
   | Grupo de informes | Introduzca el grupo de informes para el que ejecutar el trabajo de importación. |
   | Conjunto de datos | Introduzca el ID de relación del conjunto de datos para el que se ejecutará el trabajo de importación. |
   | Transformador | En el menú desplegable, seleccione una implementación de transformador. |
   | Fuente de datos | Vaya a la ruta del contenedor de datos. |
   | Programación de exportación | Seleccione la programación de la exportación. El valor predeterminado es cada 30 minutos. |

1. Haga clic en **OK** para guardar la configuración.

## Modificación del tamaño de la página {#modifying-page-size}

Los registros se procesan en páginas. De forma predeterminada, Clasificaciones de Adobe crea páginas con un tamaño de página de 1000.

Una página puede tener un tamaño máximo de 25000, por definición en las clasificaciones de Adobe y puede modificarse desde la consola Felix. Durante la exportación, las clasificaciones de Adobe bloquean el nodo de origen para evitar modificaciones simultáneas. El nodo se desbloquea tras la exportación, por error o cuando se cierra la sesión.

Para cambiar el tamaño de la página:

1. Vaya a la consola OSGI en **https://&lt;host>:&lt;port>/system/console/configMgr** y seleccione **Adobe AEM Exportador de clasificaciones**.

   ![aa-26](assets/aa-26.png)

1. Actualice el **Exportar tamaño de página** según sea necesario, haga clic en **Guardar**.

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Las clasificaciones de Adobe se conocían anteriormente como SAINT Exporter.

Un exportador puede utilizar un transformador para transformar los datos de exportación a un formato específico. Para las clasificaciones de Adobe, una subinterfaz `SAINTTransformer<String[]>` se ha proporcionado la implementación de la interfaz Transformer . Esta interfaz se utiliza para restringir el tipo de datos a `String[]` que utiliza la API de SAINT y para tener una interfaz de marcador para encontrar dichos servicios para su selección.

En la implementación predeterminada SAINTDefaultTransformer, los recursos secundarios del origen del exportador se tratan como registros con nombres de propiedad como claves y valores de propiedad como valores. La variable **Clave** se añade automáticamente como primera columna: su valor será el nombre del nodo. Propiedades espaciadas con nombres (que contienen `:`) no se tienen en cuenta.

*Estructura del nodo:*

* id-classi `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = My Product Name (String)
      * Precio = 120,90 (cadena)
      * Tamaño = M (cadena)
      * Color = negro (cadena)
      * Color^Code = 101 (cadena)

**Registro y encabezado del SAINT:**

| **Clave** | **Producto** | **Precio** | **Tamaño** | **Color** | **Color^Código** |
|---|---|---|---|---|---|
| 1 | Mi nombre de producto | 120,90 | M | black | 101 |

Las propiedades incluyen lo siguiente:

<table>
 <tbody>
  <tr>
   <td><strong>Ruta de la propiedad</strong></td>
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
   <td>ID de grupos de informes para los que se ejecutará el trabajo de importación. </td>
  </tr>
  <tr>
   <td>conjunto de datos</td>
   <td>ID de relación de conjunto de datos para la que se ejecuta el trabajo de importación. </td>
  </tr>
  <tr>
   <td>Descripción</td>
   <td>Descripción del trabajo. <br /> </td>
  </tr>
  <tr>
   <td>sobrescribir</td>
   <td>Indicador que sobrescribe los conflictos de datos. El valor predeterminado es <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>divisiones de comprobación</td>
   <td>Indicador para comprobar la compatibilidad de los grupos de informes. El valor predeterminado es <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Indicador para eliminar los nodos procesados después de la exportación. El valor predeterminado es <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatización de la exportación de clasificaciones de Adobe {#automating-adobe-classifications-export}

Puede crear su propio flujo de trabajo, de modo que cualquier importación nueva inicie el flujo de trabajo para crear los datos adecuados y correctamente estructurados en **/var/export/** para que se pueda exportar a clasificaciones de Adobe.
