---
title: Exportación de fragmentos de experiencia a Adobe Target
seo-title: Exportación de fragmentos de experiencia a Adobe Target
description: Exportación de fragmentos de experiencia a Adobe Target
seo-description: Exportación de fragmentos de experiencia a Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
translation-type: tm+mt
source-git-commit: 6723b12bebba2f239c0886e5f378f1dc70e5e247

---


# Exportación de fragmentos de experiencia a Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Algunas funciones de esta página requieren la aplicación de AEM 6.5.3.0.
>
>6.5.3.0
>
>* **Ahora se pueden seleccionar dominios** de externalizador.
>
>
6.5.2.0:
>
>* Los fragmentos de experiencia se pueden exportar a:
   >   * espacio de trabajo predeterminado.
   >   * espacio de trabajo con nombre, especificado en Configuración de nube.
>* AEM debe estar [integrado con Adobe Target mediante Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).
>
>
AEM 6.5.0.0 y 6.5.1.0:
>
>* Los fragmentos de experiencia de AEM se exportan al espacio de trabajo predeterminado de Adobe Target.
>* AEM debe integrarse con Adobe Target según las instrucciones de la sección [Integración con Adobe Target](/help/sites-administering/target.md).


Puede exportar fragmentos [de experiencias](/help/sites-authoring/experience-fragments.md), creados en Adobe Experience Manager (AEM), a Adobe Target (Target). A continuación, se pueden usar como ofertas en actividades de Target para probar y personalizar experiencias a escala.

Existen tres opciones de formato disponibles para exportar un fragmento de experiencia a Adobe Target:

* HTML (predeterminado): Compatibilidad con la entrega de contenido web e híbrido
* JSON: Compatibilidad con la entrega de contenido sin encabezado
* HTML y JSON

Los fragmentos de experiencia de AEM se pueden exportar al espacio de trabajo predeterminado en Adobe Target o a espacios de trabajo definidos por el usuario para Adobe Target. Esto se realiza mediante Adobe I/O, para lo cual AEM debe [integrarse con Adobe Target mediante Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).

>[!NOTE]
>
>Los espacios de trabajo de Adobe Target no existen en el propio Adobe Target. Se definen y administran en Adobe IMS (Identity Management System) y, a continuación, se seleccionan para su uso en distintas soluciones mediante integraciones de Adobe I/O.

>[!NOTE]
>
>Los espacios de trabajo de Adobe Target se pueden usar para permitir que los miembros de una organización (grupo) creen y gestionen ofertas y actividades solo para esta organización; sin dar acceso a otros usuarios. Por ejemplo, las organizaciones dedicadas a países concretos dentro de una preocupación mundial.

>[!NOTE]
>
>Para obtener más información, consulte también:
>
>* [Desarrollo de Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Componentes principales: fragmentos de experiencias](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>



## Requisitos previos {#prerequisites}

>[!CAUTION]
>
>Algunas funciones de esta página requieren la aplicación de AEM 6.5.3.0.

Se requieren varias acciones:

1. Debe [integrar AEM con Adobe Target mediante Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).
2. Los fragmentos de experiencia se exportan desde la instancia de creación de AEM, por lo que debe [configurar el Externalizador](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) de vínculos de AEM en la instancia de creación para garantizar que todas las referencias dentro del fragmento de experiencia se externalicen para la publicación en la Web.

   >[!NOTE]
   >
   >Para la reescritura de vínculos no cubierta de forma predeterminada, está disponible el proveedor [de reescritura de vínculos de fragmentos de](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) experiencia. Con esto, se pueden desarrollar reglas personalizadas para su caso.

## Agregar la configuración de nube {#add-the-cloud-configuration}

Antes de exportar un fragmento, debe agregar la Configuración **de** nube para **Adobe Target** al fragmento o la carpeta. Esto también le permite:

* especifique las opciones de formato que se utilizarán para la exportación
* seleccionar un espacio de trabajo de Target como destino
* seleccione un dominio externalizador para reescribir referencias en el fragmento de experiencias (opcional)

Las opciones requeridas se pueden seleccionar en Propiedades **de** página de la carpeta o fragmento requerido; la especificación se heredará según sea necesario.

1. Vaya a la consola Fragmentos **de** experiencia.

1. Abra Propiedades **de página** para la carpeta o fragmento correspondiente.

   >[!NOTE]
   >
   >Si agrega la configuración de nube a la carpeta principal del fragmento de experiencia, todos los elementos secundarios heredarán la configuración.
   >
   >
   >Si agrega la configuración de nube al propio fragmento de experiencias, todas las variaciones heredan la configuración.

1. Seleccione la ficha **Cloud Services** .

1. En Configuración **del servicio de** nube, seleccione **Adobe Target** en la lista desplegable.

1. 
   >[!NOTE]
   >
   >El formato JSON de una oferta de fragmento de experiencia se puede personalizar. Para ello, defina un componente de fragmento de experiencia del cliente y, a continuación, anote cómo exportar sus propiedades en el modelo de Sling del componente.
   >
   >Consulte el componente principal:
   >
   >[Componentes principales: fragmentos de experiencias](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   En **Adobe Target** , seleccione:

   * la configuración adecuada
   * la opción de formato requerida
   * un espacio de trabajo de Adobe Target
   * si es necesario: el dominio externalizador
   >[!CAUTION]
   >
   >El dominio del externalizador es opcional. Un externalizador de AEM se configura cuando desea que el contenido exportado apunte a un dominio de *publicación* específico. Para obtener más información, consulte [Configuración del Externalizador](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)de vínculos AEM.

   Por ejemplo, para una carpeta:

   ![Carpeta -](assets/xf-target-integration-01.png "Servicios de nubeCarpeta - Servicios de nube")

1. **Guardar y cerrar**.

## Exportación de un fragmento de experiencia a Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Para los recursos de medios, como las imágenes, solo se exporta una referencia a Target. El recurso en sí permanece almacenado en Recursos AEM y se entrega desde la instancia de publicación de AEM.
>
>Debido a esto, el fragmento de experiencias, con todos los recursos relacionados, debe publicarse antes de exportar a Target.

Para exportar un fragmento de experiencia de AEM a Target (después de especificar la Configuración de nube):

1. Vaya a la consola Fragmento de experiencias.
1. Seleccione el fragmento de experiencias que desee exportar a Target.

   >[!NOTE]
   >
   >Debe ser una variación web de fragmento de experiencia.

1. Toque o haga clic en **Exportar a Adobe Target**.

   >[!NOTE]
   >
   >Si el fragmento de experiencias ya se ha exportado, seleccione **Actualizar en Adobe Target**.

1. Toque o haga clic en **Exportar sin publicar** ni **publicar** según sea necesario.

   >[!NOTE]
   >
   >Si selecciona **Publicar** , se publicará el fragmento de experiencia inmediatamente y se enviará a Target.

1. Toque o haga clic en **Aceptar** en el cuadro de diálogo de confirmación.

   El fragmento de experiencia debe estar ahora en Target.

   >[!NOTE]
   >
   >[En la Vista](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) de **lista de la consola y en** Propiedades **se pueden ver varios detalles** de la exportación.

   >[!NOTE]
   >
   >Al ver un fragmento de experiencia en Adobe Target, la *última fecha de modificación* que se ve es la fecha en que se modificó el fragmento por última vez en AEM, no la fecha en que se exportó el fragmento por última vez a Adobe Target.

>[!NOTE]
>
>Como alternativa, puede realizar la exportación desde el editor de páginas mediante comandos comparables en el menú Información [de](/help/sites-authoring/author-environment-tools.md#page-information) página.

## Uso de los fragmentos de experiencia en Adobe Target {#using-your-experience-fragments-in-adobe-target}

Después de realizar las tareas anteriores, el fragmento de experiencia se muestra en la página Ofertas de Target. Consulte la documentación [](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) específica de Target para obtener más información sobre lo que se puede lograr allí.

>[!NOTE]
>
>Al ver un fragmento de experiencia en Adobe Target, la *última fecha de modificación* que se ve es la fecha en que se modificó el fragmento por última vez en AEM, no la fecha en que se exportó el fragmento por última vez a Adobe Target.

## Eliminación de un fragmento de experiencia ya exportado a Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

La eliminación de un fragmento de experiencia que ya se ha exportado a Target puede causar problemas si el fragmento ya se está utilizando en una oferta de Target. Al eliminar el fragmento, la oferta quedaría inutilizable a medida que AEM enviara el contenido del fragmento.

Para evitar tales situaciones:

* Si el fragmento de experiencias no se está utilizando actualmente en una actividad, AEM permite al usuario eliminar el fragmento sin un mensaje de advertencia.
* Si una actividad de Target está utilizando el fragmento de experiencias, aparece un mensaje de error que advierte al usuario de AEM de las posibles consecuencias que tendrá la eliminación del fragmento en la actividad.

   El mensaje de error en AEM no prohíbe al usuario (forzar)eliminar el fragmento de experiencias. Si se elimina el fragmento de experiencias:

   * La oferta de Target con el fragmento de experiencia de AEM puede mostrar un comportamiento no deseado

      * Es probable que la oferta se siga representando, ya que el HTML del fragmento de experiencias se insertó en Target
      * Es posible que las referencias del fragmento de experiencias no funcionen correctamente si los recursos a los que se hace referencia también se eliminan en AEM.
   * Por supuesto, cualquier modificación adicional del fragmento de experiencias es imposible, ya que el fragmento de experiencias ya no existe en AEM.