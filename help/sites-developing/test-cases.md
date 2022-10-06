---
title: Definición de los casos de prueba
seo-title: Defining your Test Cases
description: Los casos de prueba deben basarse en los casos de uso y en la especificación detallada de los requisitos
seo-description: Your test cases should be based upon the use cases and the detailed requirements specification
uuid: daaa5370-bcd3-45a6-9974-f9b5af6a1529
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: f01eb2aa-6891-4f5d-8a4a-43fc1534c222
docset: aem65
exl-id: c09cde0d-401c-437f-9ec8-a0530c1312d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Definición de los casos de prueba{#defining-your-test-cases}

Los casos de prueba deben basarse en:

**Casos de uso**

* Definen la funcionalidad necesaria en términos de la interacción entre Actors (roles que inician ciertas acciones) y el sistema.
* El cliente debe definir los casos de uso.

**Especificación de requisitos detallados**

* Deben probarse todos los requisitos funcionales y de rendimiento.

Los ensayos deben definir claramente:

* Requisitos previos pueden abarcar sistemas, configuraciones o experiencia de prueba específicos.
* Medidas que deben adoptarse; en un nivel de detalle adecuado.
* Resultados esperados.
* Criterios claros para aprobar o fallar.

La perspectiva de automatizar los casos de prueba es obviamente atractiva, ya que puede eliminar tareas repetitivas.

## Pruebas manuales y automatizadas {#manual-versus-automated-tests}

Sin embargo, la automatización de los casos de prueba es una inversión importante, por lo que deben tenerse en cuenta ciertos aspectos:

* Se necesita tiempo, esfuerzo y experiencia para configurar y configurar.
* Si el explorador se basa en , existe un mayor riesgo de problemas cuando se instalan las actualizaciones del explorador; requiere más tiempo para corregir.
* Sólo realmente factible para grandes proyectos.
* Positivo cuando se generan varias versiones, ya sea para pruebas o en el plan de versiones a largo plazo.

## Prueba de aspectos específicos {#testing-specific-aspects}

A la hora de realizar pruebas AEM algunos detalles específicos son de particular interés:

**Creación y publicación de entornos**

Aunque, se incluye en [Entornos](/help/sites-developing/the-basics.md#environments) vale la pena destacar un factor decisivo de AEM con respecto a los ensayos.

Debe considerar AEM como dos aplicaciones:

* el *Autor* entorno Esta instancia permite a los autores introducir y publicar contenido.
Esto tiene un conjunto pequeño (más) y predecible de usuarios, para los que la funcionalidad y el rendimiento específicos son cruciales.

* el *Publicación* entorno Esta instancia presenta el sitio web en su formulario publicado para el acceso de los visitantes.
Normalmente, este grupo de usuarios es mayor, ya que el volumen de tráfico no siempre es 100 % predecible. El rendimiento sigue siendo crucial: al responder a las solicitudes. También se debe considerar el almacenamiento en caché y el equilibrio de carga.

Aunque el mismo software como tal:

* sirven para diferentes propósitos
* tienen diferentes requisitos en cuanto a funcionalidad y rendimiento
* están configuradas de forma diferente
* se afinan por separado
* cada uno tendrá su propio conjunto de pruebas de aceptación

En otras palabras, deben someterse a pruebas por separado y con diferentes casos de prueba.

**Personalización**

Al probar la personalización, cada caso de uso individual debe repetirse utilizando varias cuentas de usuario para probar el comportamiento.

El almacenamiento en caché también debe comprobarse para comprobar el comportamiento correcto.

**Dispatcher**

La mayoría de los proyectos instalarán Dispatcher para el almacenamiento en caché y el equilibrio de carga.

Las pruebas son difíciles (el almacenamiento en caché se realiza en varios niveles y en varias ubicaciones) y deben realizarse en forma de caja negra. Los aspectos clave para probar son:

* **Precisión**
asegúrese de que el visitante del sitio web vea las actualizaciones de contenido.

* **Continuidad**
asegúrese de que el sitio web siga disponible cuando se cierre un servidor.

* **Clústeres**
Los clústeres se utilizan para proporcionar:

   * **Failover**
Si un servidor falla, otros servidores del clúster se harán cargo del procesamiento.

   * **Rendimiento**
El equilibrio de carga con failover completo aumenta el rendimiento de un clúster.
Cuando se utiliza para un proyecto de cliente, se debe probar el clúster para confirmar el funcionamiento correcto de la configuración.

## Prueba de software de terceros {#testing-third-party-software}

Se hará referencia a cualquier software de terceros que interactúe con AEM en las Especificaciones detalladas de los requisitos.

Todas las pruebas necesarias (dependiendo del ámbito definido) deben analizarse y obtenerse pruebas limpias.
