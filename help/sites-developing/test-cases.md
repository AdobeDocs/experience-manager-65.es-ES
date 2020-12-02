---
title: Definición de los casos de prueba
seo-title: Definición de los casos de prueba
description: Los casos de prueba deben basarse en los casos de uso y en la especificación detallada de los requisitos
seo-description: Los casos de prueba deben basarse en los casos de uso y en la especificación detallada de los requisitos
uuid: daaa5370-bcd3-45a6-9974-f9b5af6a1529
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: f01eb2aa-6891-4f5d-8a4a-43fc1534c222
docset: aem65
translation-type: tm+mt
source-git-commit: da08613be784f43ad3e3c3652b7e015640a48a9d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Definición de los casos de prueba{#defining-your-test-cases}

Los casos de prueba deben basarse en:

**Casos de uso**

* Definen la funcionalidad requerida en términos de interacción entre los actores (funciones que inician determinadas acciones) y el sistema.
* El cliente debe definir los casos de uso.

**Especificación detallada de requisitos**

* Deben probarse todos los requisitos funcionales y de rendimiento.

Los ensayos deberán definir claramente:

* Requisitos previos; estas pueden abarcar sistemas, configuraciones o experiencia de prueba específicos.
* Medidas que deben seguirse; en un nivel de detalle adecuado.
* Resultados esperados.
* Criterios claros para aprobar o fallar.

El cliente potencial de automatizar los casos de prueba es obviamente atractivo ya que puede eliminar tareas repetitivas.

## Pruebas manuales versus automatizadas {#manual-versus-automated-tests}

Sin embargo, la automatización de los casos de prueba es una inversión importante, por lo que deben considerarse algunos aspectos:

* Requiere tiempo, esfuerzo y experiencia para configurar y configurar.
* Si el navegador está basado, existe un mayor riesgo de que se produzcan problemas al instalar las actualizaciones; requerir más tiempo para corregir.
* Sólo realmente factible para grandes proyectos.
* Es bueno cuando se generan varias versiones para pruebas o en el plan de versiones a largo plazo.

## Prueba de aspectos específicos {#testing-specific-aspects}

Cuando se realizan pruebas AEM algunos detalles específicos son de particular interés:

**Entornos de creación y publicación**

Aunque, abarcado en [Entornos](/help/sites-developing/the-basics.md#environments), vale la pena destacar un factor decisivo de AEM con respecto a las pruebas.

Debe considerar AEM como dos aplicaciones:

* el entorno *Autor*
Esta instancia permite a los autores introducir y publicar contenido.
Esto tiene un conjunto pequeño (er) y predecible de usuarios, para los que es crucial una funcionalidad y un rendimiento específicos.

* el entorno *Publish*
Esta instancia presenta el sitio web en su forma publicada para el acceso de los visitantes.
Generalmente, este grupo de usuarios es mayor, ya que el volumen de tráfico no siempre es 100% predecible. El rendimiento sigue siendo crucial cuando se responde a las solicitudes. También se debe considerar el almacenamiento en caché y el equilibrio de carga.

Aunque el mismo software como tal:

* servir para diferentes propósitos
* tener diferentes requisitos en cuanto a funcionalidad y rendimiento
* están configuradas de forma diferente
* se ajustan por separado
* cada uno tendrá su propio conjunto de pruebas de aceptación

En otras palabras, deben someterse a pruebas por separado y con diferentes casos de prueba.

**Personalización**

Al probar la personalización, cada caso de uso individual debe repetirse utilizando varias cuentas de usuario para probar el comportamiento.

También se debe comprobar el comportamiento correcto del almacenamiento en caché.

**El despachante**

La mayoría de los proyectos instalarán Dispatcher para almacenamiento en caché y equilibrio de carga.

La prueba es difícil (el almacenamiento en caché se realiza en varios niveles y en varias ubicaciones) y debe realizarse en forma de caja negra. Los aspectos clave para probar son:

* **Con**
precisión, asegúrese de que el visitante del sitio web vea las actualizaciones de contenido.

* **Asegúrese**
continuamente de que el sitio web siga estando disponible cuando se cierre un servidor.

* ****
ClustersClusters se utilizan para proporcionar:

   * ****
FailoverSi un servidor falla, otros servidores del clúster se harán cargo del procesamiento.

   * **El equilibrio**
PerformanceLoad con failover completo aumenta el rendimiento de un clúster.
Cuando se utiliza para un proyecto de cliente, se debe probar el clúster para confirmar el funcionamiento correcto de la configuración.

## Prueba de software de terceros {#testing-third-party-software}

Cualquier software de terceros interconectado a AEM será referenciado en las Especificaciones detalladas de requisitos.

Todas las pruebas requeridas (según el ámbito definido) deben analizarse y obtenerse pruebas limpias.
