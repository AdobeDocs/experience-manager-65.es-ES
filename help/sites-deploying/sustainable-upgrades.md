---
title: Actualizaciones sostenibles
seo-title: Actualizaciones sostenibles
description: Obtenga información sobre actualizaciones sostenibles en AEM 6.4.
seo-description: Obtenga información sobre actualizaciones sostenibles en AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
feature: Actualización
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---


# Actualizaciones sostenibles{#sustainable-upgrades}

## Marco de personalización {#customization-framework}

### Arquitectura (Funcional / Infraestructura / Contenido / Aplicación) {#architecture-functional-infrastructure-content-application}

La función del marco de personalización está diseñada para ayudar a reducir las infracciones en áreas no extensibles del código (como APIS) o contenido (como superposiciones) que no sean fáciles de actualizar.

Existen dos componentes del marco de personalización: la **superficie de API** y la **clasificación de contenido**.

#### Superficie de API {#api-surface}

En versiones anteriores de AEM muchas API se han expuesto a través de Uber Jar. Algunas de estas API no estaban pensadas para ser utilizadas por los clientes, pero estaban expuestas a admitir AEM funcionalidad en varios paquetes. En adelante, las API de Java se marcarán como públicas o privadas para indicar a los clientes qué API pueden utilizar con seguridad en el contexto de las actualizaciones. Otros detalles son:

* Los paquetes de implementación personalizados pueden utilizar las API de Java marcadas como `Public` y hacer referencia a ellas.

* Las API públicas serán compatibles con la instalación de un paquete de compatibilidad.
* El paquete de compatibilidad contendrá una compatibilidad con Uber JAR para garantizar la compatibilidad con versiones anteriores
* Las API de Java marcadas como `Private` solo están pensadas para ser utilizadas por AEM paquetes internos y no deben ser utilizadas por paquetes personalizados.

>[!NOTE]
>
>El concepto de `Private` y `Public` en este contexto no debe confundirse con las nociones Java de clases públicas y privadas.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Clasificaciones de contenido {#content-classifications}

AEM ha utilizado durante mucho tiempo la principal función de superposiciones y fusión de recursos de Sling para permitir a los clientes ampliar y personalizar AEM funcionalidad. La funcionalidad predefinida que alimenta las consolas de AEM y la IU se almacena en **/libs**. Los clientes nunca deben modificar nada debajo de **/libs** pero podrían agregar contenido adicional debajo de **/apps** para superponer y ampliar la funcionalidad definida en **/libs** (consulte Desarrollo con superposiciones para obtener más información). Esto causaba numerosos problemas al actualizar AEM, ya que el contenido en **/libs** podía cambiar, lo que provocaba que la funcionalidad de superposición se interrumpiera de forma inesperada. Los clientes también pueden ampliar los componentes de AEM mediante herencia a través de `sling:resourceSuperType` o simplemente hacer referencia a un componente en **/libs** directamente a través de sling:resourceType. Pueden producirse problemas de actualización similares con casos de uso de referencia y de anulación.

Para que sea más seguro y fácil para los clientes comprender qué áreas de **/libs** son seguras de usar y superponer el contenido en **/libs** se ha clasificado con las siguientes mezclas:

* **Public (granite:PublicArea)** : define un nodo como público para que se pueda superponer, heredar (  `sling:resourceSuperType`) o usar directamente (  `sling:resourceType`). Los nodos situados debajo de /libs marcados como públicos serán seguros de actualizar con la adición de un paquete de compatibilidad. En general, los clientes solo deben aprovechar los nodos marcados como públicos.

* **Abstracto (granite:AbstractArea)** : define un nodo como abstracto. Los nodos se pueden superponer o heredar ( `sling:resourceSupertype`), pero no se deben usar directamente ( `sling:resourceType`).

* **Final (granite:FinalArea)** : define un nodo como final. Los nodos clasificados como finales idealmente no deben superponerse ni heredarse. Los nodos finales se pueden utilizar directamente mediante `sling:resourceType`. Los subnodos bajo el nodo final se consideran internos de forma predeterminada.

* ***Interno (granite:InternalArea)*** *- *Define un nodo como interno. Los nodos clasificados como internos idealmente no deben superponerse, heredarse ni utilizarse directamente. Estos nodos solo están pensados para la funcionalidad interna de AEM

* **Sin anotación** : los nodos heredan la clasificación basada en la jerarquía de árbol. La raíz / es pública de forma predeterminada. **Los nodos con una matriz clasificada como interna o final también deben tratarse como internos.**

>[!NOTE]
>
>Estas políticas solo se aplican contra los mecanismos basados en rutas de búsqueda de Sling. Otras áreas de **/libs** como una biblioteca del lado del cliente pueden marcarse como `Internal`, pero aún pueden utilizarse con la inclusión clientlib estándar. Es importante que un cliente siga respetando la clasificación interna en estos casos.

#### Indicadores de tipo de contenido del CRXDE Lite {#crxde-lite-content-type-indicators}

Las mezclas aplicadas en el CRXDE Lite mostrarán los nodos de contenido y los árboles marcados como `INTERNAL` atenuados. Para `FINAL` solo el icono aparece atenuado. Los elementos secundarios de estos nodos también aparecerán en gris. La funcionalidad Nodo de superposición está deshabilitada en ambos casos.

**Público**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Internas**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Comprobación del estado del contenido**

>[!NOTE]
>
>A partir de AEM 6.5, Adobe recomienda utilizar Pattern Detector para detectar infracciones de acceso al contenido. Los informes de detector de patrones son más detallados, detectan más problemas y reducen la probabilidad de falsos positivos.
>
>Para obtener más información, consulte [Evaluación de la complejidad de la actualización con Pattern Detector](/help/sites-deploying/pattern-detector.md).

AEM 6.5 se enviará con una comprobación de estado para avisar a los clientes si el contenido superpuesto o referenciado se utiliza de forma incompatible con la clasificación de contenido.

La** comprobación de acceso al contenido de Sling/Granite** es una nueva comprobación de estado que supervisa el repositorio para ver si el código de cliente accede incorrectamente a los nodos protegidos en AEM.

Esto analizará **/apps** y normalmente tarda varios segundos en completarse.

Para acceder a esta nueva comprobación de estado, debe hacer lo siguiente:

1. En la pantalla de inicio de AEM, vaya a **Herramientas > Operaciones > Informes de estado**
1. Haga clic en **Comprobación de acceso al contenido de Sling/Granite** como se muestra a continuación:

   ![screen_shot_2017-12-14at5648pm](assets/screen_shot_2017-12-14at55648pm.png)

Una vez completado el análisis, aparecerá una lista de advertencias notificando al usuario final del nodo protegido al que se hace referencia incorrectamente:

![captura de pantalla de informes de salud (2018-2-5health)](assets/screenshot-2018-2-5healthreports.png)

Después de corregir las violaciones, volverá al estado verde:

![captura de pantalla-2018-2-5health-reports-conflicts](assets/screenshot-2018-2-5healthreports-violations.png)

La comprobación de estado muestra la información recopilada por un servicio en segundo plano que comprueba de forma asíncrona siempre que se utiliza una superposición o un tipo de recurso en todas las rutas de búsqueda de Sling. Si las mezclas de contenido se utilizan incorrectamente, se informa de una infracción.
