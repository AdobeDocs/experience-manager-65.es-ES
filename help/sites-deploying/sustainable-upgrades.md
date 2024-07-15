---
title: Actualizaciones sostenibles
description: Obtenga información acerca de las actualizaciones sostenibles en Adobe Experience Manager 6.4.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Actualizaciones sostenibles{#sustainable-upgrades}

## Marco de personalización {#customization-framework}

### Arquitectura (funcional/infraestructura/contenido/aplicación)  {#architecture-functional-infrastructure-content-application}

La función Marco de personalización está diseñada para ayudar a reducir las infracciones en áreas no ampliables del código (como las API) o en contenido (como las superposiciones) que no son compatibles con la actualización.

Hay dos componentes en el marco de personalización: la **superficie de API** y la **clasificación de contenido**.

#### Superficie API {#api-surface}

En versiones anteriores de Adobe Experience Manager AEM (), muchas API se exponían a través de Uber Jar. AEM Algunas de estas API no estaban pensadas para que las usaran los clientes, sino que estuvieron expuestas a la funcionalidad de soporte de los paquetes de informes de forma conjunta. En adelante, las API de Java™ se marcarán como Públicas o Privadas para indicar a los clientes qué API son seguras de usar en el contexto de las actualizaciones. Otros detalles específicos incluyen:

* Los paquetes de implementación personalizada pueden usar y hacer referencia a las API de Java™ marcadas como `Public`.

* Las API públicas son compatibles con la instalación de un paquete de compatibilidad.
* El paquete de compatibilidad contiene una compatibilidad con Uber JAR para garantizar la compatibilidad con versiones anteriores
* AEM Las API de Java™ marcadas como `Private` están pensadas para que solo las usen los paquetes internos, no los paquetes personalizados, y solo los usen los paquetes internos.

>[!NOTE]
>
>El concepto de `Private` y `Public` en este contexto no debe confundirse con las nociones de Java™ de clases públicas y privadas.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Clasificaciones de contenido {#content-classifications}

AEM AEM Durante mucho tiempo, ha utilizado el principio de superposiciones y la fusión de recursos de Sling para permitir a los clientes ampliar y personalizar la funcionalidad de la. AEM La funcionalidad predefinida que alimenta las consolas y la interfaz de usuario de la se almacena en **/libs**. Los clientes nunca modificarán nada por debajo de **/libs**, pero podrían agregar contenido adicional por debajo de **/apps** para superponer y ampliar la funcionalidad definida en **/libs** (consulte Desarrollo con superposiciones para obtener más información). AEM Esto aún causaba numerosos problemas al actualizar el contenido de **/libs**, ya que la funcionalidad de superposición podría cambiar y romperse de formas inesperadas. AEM Los clientes también pueden ampliar los componentes de la a través de la herencia mediante `sling:resourceSuperType` o simplemente hacer referencia a un componente de **/libs** directamente a través de sling:resourceType. Pueden producirse problemas de actualización similares con los casos de uso de referencia y anulación.

Para que sea más seguro y fácil para los clientes comprender qué áreas de **/libs** son seguras de usar y superponer, el contenido de **/libs** se ha clasificado con los siguientes mixins:

* **Public (granite:PublicArea)**: define un nodo como público para que se pueda superponer, heredar ( `sling:resourceSuperType`) o utilizar directamente ( `sling:resourceType`). Los nodos debajo de /libs marcados como Public son seguros para actualizar con la adición de un Paquete de compatibilidad. En general, los clientes solo deben utilizar nodos marcados como Public.

* **Abstracto (granite:AbstractArea)**: define un nodo como abstracto. Los nodos se pueden superponer o heredar ( `sling:resourceSupertype`), pero no se pueden usar directamente ( `sling:resourceType`).

* **Final (granite:FinalArea)**: Define un nodo como final. Los nodos clasificados como finales no se deben superponer ni heredar. Los nodos finales se pueden usar directamente mediante `sling:resourceType`. Los subnodos bajo el nodo final se consideran internos de forma predeterminada.

* ***Interno (granite:InternalArea)*** *- *Define un nodo como interno. Los nodos clasificados como internos no deben superponerse, heredarse ni utilizarse directamente. AEM Estos nodos solo están pensados para la funcionalidad interna de los entornos de trabajo de los que se puede acceder a

* **Sin anotación**: los nodos heredan la clasificación según la jerarquía del árbol. La raíz / es de forma predeterminada pública. **Los nodos con un nodo principal clasificado como Interno o Final también se tratarán como Interno.**

>[!NOTE]
>
>Estas políticas solo se aplican a los mecanismos basados en rutas de búsqueda de Sling. Otras áreas de **/libs**, como una biblioteca del lado del cliente, pueden marcarse como `Internal`, pero podrían utilizarse con la inclusión clientlib estándar. Es importante que un cliente siga respetando la clasificación interna en estos casos.

#### Indicadores de tipo de contenido de CRXDE Lite {#crxde-lite-content-type-indicators}

Las mezclas aplicadas en CRXDE Lite muestran nodos de contenido y árboles que están marcados como `INTERNAL` como atenuados (atenuados). Para `FINAL`, solo el icono está atenuado. Los elementos secundarios de estos nodos también aparecen atenuados. La funcionalidad Nodo de superposición está desactivada en ambos casos.

**Público**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interno**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Comprobación de estado del contenido**

>[!NOTE]
>
>AEM A partir de la versión 6.5, Adobe recomienda utilizar Pattern Detector para detectar infracciones de acceso al contenido. Los informes de detector de patrones son más detallados, detectan más problemas y reducen la probabilidad de falsos positivos.
>
>Para obtener más información, consulte [Evaluación de la complejidad de la actualización con Pattern Detector](/help/sites-deploying/pattern-detector.md).

AEM La versión 6.5 se envía con una comprobación de estado para alertar a los clientes de si el contenido superpuesto o referenciado se utiliza de una manera incoherente con la clasificación de contenido.

AEM La** Comprobación de acceso al contenido de Sling/Granite** es una nueva comprobación de estado que supervisa el repositorio para ver si el código de cliente accede incorrectamente a los nodos protegidos en el.

Esto explora **/apps** y, por lo general, tarda varios segundos en completarse.

Para acceder a esta nueva comprobación de estado, haga lo siguiente:

1. AEM En la pantalla de inicio de la, vaya a **Herramientas > Operaciones > Informes de estado**
1. Haga clic en **Comprobación de acceso al contenido de Sling/Granite**.

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Una vez finalizado el análisis, aparece una lista de advertencias que notifican al usuario final del nodo protegido al que se hace referencia incorrectamente:

![screenshot-2018-2-5health reports](assets/screenshot-2018-2-5healthreports.png)

Después de corregir las infracciones, vuelve al estado verde:

![captura de pantalla-2018-2-5informes de estado-violaciones](assets/screenshot-2018-2-5healthreports-violations.png)

La comprobación de estado muestra información recopilada por un servicio en segundo plano que comprueba asincrónicamente cada vez que se utiliza una superposición o un tipo de recurso en todas las rutas de búsqueda de Sling. Si los mixins de contenido se utilizan incorrectamente, informa de una infracción.
