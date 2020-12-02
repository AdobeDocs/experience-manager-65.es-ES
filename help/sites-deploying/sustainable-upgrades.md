---
title: Upgrades sostenibles
seo-title: Upgrades sostenibles
description: Obtenga información sobre actualizaciones sostenibles en AEM 6.4.
seo-description: Obtenga información sobre actualizaciones sostenibles en AEM 6.4.
uuid: 80673076-624b-4308-8233-129cb4422bd5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: e35c9352-f0d5-4db5-b88f-0720af8f6883
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# Actualizaciones sostenibles{#sustainable-upgrades}

## Customization Framework {#customization-framework}

### Arquitectura (Funcional / Infraestructura / Contenido / Aplicación) {#architecture-functional-infrastructure-content-application}

La función Customization Framework está diseñada para ayudar a reducir las infracciones en áreas no extensibles del código (como APIS) o en el contenido (como las superposiciones) que no son fáciles de actualizar.

Existen dos componentes del marco de personalización: la **superficie de API** y la **clasificación del contenido**.

#### Superficie de API {#api-surface}

En versiones anteriores de AEM muchas API se han expuesto a través de Uber Jar. Algunas de estas API no estaban destinadas a ser utilizadas por los clientes, pero estaban expuestas a admitir la funcionalidad AEM en varios paquetes. A partir de ahora, las API de Java se marcarán como públicas o privadas para indicar a los clientes qué API son seguras de usar en el contexto de las actualizaciones. Otros detalles específicos incluyen:

* Las API de Java marcadas como `Public` se pueden usar y hacer referencia a ellas mediante paquetes de implementación personalizados.

* Las API públicas serán retrocompatibles con la instalación de un paquete de compatibilidad.
* El paquete de compatibilidad contendrá una compatibilidad con Uber JAR para garantizar la compatibilidad con versiones anteriores
* Las API de Java marcadas como `Private` sólo están pensadas para ser utilizadas por AEM paquetes internos y no deben ser utilizadas por paquetes personalizados.

>[!NOTE]
>
>El concepto de `Private` y `Public` en este contexto no debe confundirse con las nociones de Java de las clases públicas y privadas.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Clasificaciones de contenido {#content-classifications}

AEM ha utilizado durante mucho tiempo el principal de las superposiciones y la fusión de recursos de Sling para permitir a los clientes ampliar y personalizar AEM funcionalidad. La funcionalidad predefinida que alimenta las consolas de AEM y la interfaz de usuario se almacena en **/libs**. Los clientes nunca modificarán nada debajo de **/libs** pero podrían agregar contenido adicional debajo de **/apps** para superponer y ampliar la funcionalidad definida en **/libs** (consulte Desarrollar con superposiciones para obtener más información). Esto causaba numerosos problemas al actualizar AEM, ya que el contenido de **/libs** podía cambiar, lo que ocasionaba que la funcionalidad de superposición se dañara de forma inesperada. Los clientes también pueden extender AEM componentes mediante herencia mediante `sling:resourceSuperType` o simplemente hacer referencia a un componente en **/libs** directamente mediante sling:resourceType. Se podrían producir problemas de actualización similares con casos de uso de referencia y anulación.

A fin de que sea más seguro y fácil para los clientes comprender qué áreas de **/libs** son seguras de usar y superponer el contenido en **/libs** se ha clasificado con las siguientes mezclas:

* **Public (granite:PublicArea)** : define un nodo como público para que pueda superponerse, heredarse (  `sling:resourceSuperType`) o utilizarse directamente (  `sling:resourceType`). Los nodos situados debajo de /libs marcados como Público serán seguros para la actualización con la adición de un paquete de compatibilidad. En general, los clientes solo deben aprovechar los nodos marcados como Público.

* **Abstracto (granite:AbstractArea)** : define un nodo como abstracto. Los nodos pueden superponerse o heredarse ( `sling:resourceSupertype`) pero no deben usarse directamente ( `sling:resourceType`).

* **Final (granite:FinalArea)** : define un nodo como final. Los nodos clasificados como finales idealmente no deben superponerse ni heredarse. Los nodos finales se pueden utilizar directamente mediante `sling:resourceType`. Los subnodos bajo el nodo final se consideran internos de forma predeterminada.

* ***Interno (granite:InternalArea)*** *- *Define un nodo como interno. Los nodos clasificados como internos idealmente no deben superponerse, heredarse ni utilizarse directamente. Estos nodos solo están diseñados para la funcionalidad interna de AEM

* **Sin anotación** : los nodos heredan la clasificación basada en la jerarquía de árbol. El parámetro / root es de forma predeterminada Public. **Los nodos con un padre clasificado como interno o final también se tratarán como internos.**

>[!NOTE]
>
>Estas directivas solo se aplican a los mecanismos basados en rutas de búsqueda Sling. Otras áreas de **/libs** como una biblioteca del lado del cliente se pueden marcar como `Internal`, pero se pueden seguir utilizando con la inclusión de clientlib estándar. Es importante que un cliente siga respetando la clasificación interna en estos casos.

#### Indicadores de tipo de contenido del CRXDE Lite {#crxde-lite-content-type-indicators}

Las mezclas aplicadas en el CRXDE Lite mostrarán los nodos de contenido y los árboles marcados como `INTERNAL` atenuados. Para `FINAL` sólo el icono aparece atenuado. Los elementos secundarios de estos nodos también aparecerán en gris. La funcionalidad Nodo de superposición está deshabilitada en ambos casos.

**Público**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interno**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Comprobación del estado del contenido**

>[!NOTE]
>
>A partir de AEM 6.5, Adobe recomienda utilizar el detector de patrones para detectar infracciones de acceso al contenido. Los informes del detector de patrones son más detallados, detectan más problemas y reducen la probabilidad de falsos positivos.
>
>Para obtener más información, consulte [Evaluación de la complejidad de la actualización con el detector de patrones](/help/sites-deploying/pattern-detector.md).

AEM 6.5 se enviará con una comprobación de estado para avisar a los clientes si el contenido superpuesto o referenciado se utiliza de manera incompatible con la clasificación de contenido.

La** comprobación de acceso al contenido de Sling/Granite** es una nueva comprobación de estado que supervisa el repositorio para ver si el código del cliente accede incorrectamente a los nodos protegidos en AEM.

Esto analizará **/apps** y generalmente tarda varios segundos en completarse.

Para acceder a este nuevo chequeo, debe hacer lo siguiente:

1. En la pantalla de inicio de AEM, vaya a **Herramientas > Operaciones > Informes de estado**
1. Haga clic en la **Comprobación de acceso al contenido de Sling/Granite** como se muestra a continuación:

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Una vez finalizado el análisis, aparecerá una lista de advertencias notificando al usuario final del nodo protegido al que se hace referencia incorrectamente:

![captura de pantalla-2018-2-5curthreports](assets/screenshot-2018-2-5healthreports.png)

Después de corregir las infracciones, volverá a su estado verde:

![captura de pantalla-2018-2-5health-reports-conflicts](assets/screenshot-2018-2-5healthreports-violations.png)

La comprobación de estado muestra la información recopilada por un servicio en segundo plano que comprueba asincrónicamente siempre que se utiliza una superposición o un tipo de recurso en todas las rutas de búsqueda de Sling. Si las mezclas de contenido se utilizan incorrectamente, se produce una infracción.
