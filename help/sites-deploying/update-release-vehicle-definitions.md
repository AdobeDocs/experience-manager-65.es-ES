---
title: Actualizar definiciones del vehículo de lanzamiento
seo-title: Actualizar definiciones del vehículo de lanzamiento
description: Este artículo detalla los distintos tipos de versiones de AEM, incluidas las versiones completas, los paquetes de funciones y los paquetes de servicios.
seo-description: Este artículo detalla los distintos tipos de versiones de AEM, incluidas las versiones completas, los paquetes de funciones y los paquetes de servicios.
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# Definiciones del vehículo de la versión de actualización de AEM{#update-release-vehicle-definitions}

Este documento incluye detalles sobre los distintos tipos de versiones de Adobe Experience Manager (AEM), incluidas versiones completas, paquetes de funciones y paquetes de servicios que Adobe ofrece a sus clientes.

>[!Note]
>
>Para consultar la programación de versiones de actualizaciones de AEM, consulte la guía de versiones de actualizaciones de [AEM](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

## Versión completa {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>Definición</strong></td>
   <td>
    <ul>
     <li>Versión programada</li>
     <li>Admite rutas de actualización para versiones específicas, que se define en las notas de la versión</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Asignación de nombres</strong></td>
   <td>
    <ul>
     <li>Los números de versión de las versiones principales aumentan según la fórmula X+1.Y.Z. </li>
     <li>Los números de versión de versiones menores aumentan según la fórmula X.Y+1.Z</li>
    </ul> <p>Si X es el número de versión principal, Y es el número de versión secundario y Z el número de parche.</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusiones</strong></td>
   <td>
    <ul>
     <li>Nuevas funciones</li>
     <li>Mejoras</li>
     <li>Correcciones de errores</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentación</strong></td>
   <td>
    <ul>
     <li>Las notas de la versión están disponibles en el portal de documentación</li>
     <li>La documentación sobre funciones, mejoras y correcciones de errores está disponible en el portal de documentación</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Anual</td>
  </tr>
  <tr>
   <td><strong>Disponibilidad e instalación</strong></td>
   <td>
    <ul>
     <li>Se entrega como un instalador de producto independiente</li>
     <li>Disponible en el sitio web de licencias y en el sitio web de licencias de servicios gestionados</li>
     <li>Puede requerir la migración del repositorio de contenido</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nivel de prueba</strong></td>
   <td>Totalmente validado por el control de calidad</td>
  </tr>
 </tbody>
</table>

## Paquete de servicio {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definición</strong></td>
   <td>
    <ul>
     <li>Versión programada</li>
     <li>Actualmente, no se puede revertir</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Asignación de nombres</strong></td>
   <td>
    <ul>
     <li>El número de revisión es un número de un solo dígito</li>
     <li>Después de la instalación, aumentará el dígito del parche del número de versión instalado, según la fórmula X.Y.Z.SPx</li>
     <li>Si X es el número de versión principal, Y es el número de versión secundario y Z el número de parche. x es el número del Service Pack.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Inclusiones</strong></td>
   <td>
    <ul>
     <li>Nuevas funciones</li>
     <li>Mejoras</li>
     <li>Correcciones de errores</li>
     <li>Paquetes de funciones de interés común (si los hay)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentación</strong></td>
   <td>
    <ul>
     <li>Notas de la versión disponibles en el portal de documentación</li>
     <li>Documentación sobre funciones, mejoras y correcciones de errores en el portal de documentación</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Trimestral</td>
  </tr>
  <tr>
   <td><strong>Disponibilidad e instalación</strong></td>
   <td>
    <ul>
     <li>Entregado como paquete</li>
     <li>Disponible en Uso compartido de paquetes</li>
     <li>Requiere una instalación funcional existente</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nivel de prueba</strong></td>
   <td>
    <ul>
     <li>Se validó el control de calidad de todas las correcciones</li>
     <li>Sentido general del paquete con ejecuciones de automatización</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Paquete de correcciones acumulativas  {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Definición</strong></td>
   <td>
    <ul>
     <li>Modelo de entrega única de correcciones de liberación</li>
     <li>Paquete de contenido agregado que contiene el paquete de contenido de componentes individuales</li>
     <li>Los archivos CFP son la sustitución de las correcciones rápidas y no se incluyen mejoras.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Asignación de nombres</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>Si X es el número de versión principal, Y es el número de versión secundario y Z el número de parche. x es el número acumulado del Service Pack.</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusiones</strong></td>
   <td><p>CFP es un paquete de correcciones acumulativo que contiene correcciones de todos los componentes en fechas especificadas. Por ejemplo, si un cliente aplica CFP3, entonces CFP3 = CFP1 + CFP2.</p> </td>
  </tr>
  <tr>
   <td><strong>Documentación</strong></td>
   <td>Notas de la versión disponibles en el portal de documentación</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Cuateralmente</td>
  </tr>
  <tr>
   <td><strong>Disponibilidad e instalación</strong></td>
   <td>
    <ul>
     <li>Entregado como paquete</li>
     <li>Disponible en Uso compartido de paquetes</li>
     <li>Depende del Service Pack más reciente lanzado</li>
     <li>La PCP es independiente. Los clientes no tienen por qué preocuparse por encontrar o resolver dependencias. CFP debe instalarse en el Service Pack más reciente.</li>
     <li>CFP se puede instalar como un paquete único, lo que mejora la experiencia del cliente.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nivel de prueba</strong></td>
   <td>Control de calidad validado a nivel de integración y pruebas de regresión</td>
  </tr>
 </tbody>
</table>

## Paquete de correcciones acumulativas Oak {#oak-cumulative-fix-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definición</strong></td>
   <td>
    <ul>
     <li>Similar a un CFP estándar, pero solo contiene correcciones relacionadas con Oak</li>
     <li>COFP es independiente (sin dependencias). Los clientes no tienen por qué preocuparse por encontrar o resolver dependencias. [1]</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Asignación de nombres</strong></td>
   <td>oak &lt;version&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusiones</strong></td>
   <td>COFP es un paquete acumulativo de correcciones que contiene correcciones de todos los componentes Oak para una versión 1.x específica. Por ejemplo, si el cliente aplica COHF 1.x.3, entonces COHF 1.x.3. = COHF 1.x.1 + COHF 1.x.2.</td>
  </tr>
  <tr>
   <td><strong>Documentación</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td><p>Según sea necesario</p> </td>
  </tr>
  <tr>
   <td><strong>Disponibilidad e instalación</strong></td>
   <td>
    <ul>
     <li>El proceso de instalación de COFP se ha simplificado para mejorar la experiencia del cliente. (Los clientes solo pueden instalar un paquete único para todos los componentes).</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nivel de prueba</strong></td>
   <td><p>Control de calidad validado</p> </td>
  </tr>
 </tbody>
</table>

## Corrección urgente {#hot-fix}

<table>
 <tbody>
  <tr>
   <td><strong>Definición</strong></td>
   <td><p>Paquete que incluye uno o más archivos creados para resolver un defecto del producto que degrada significativamente los servicios esenciales o que afecta significativamente a las operaciones comerciales. </p> </td>
  </tr>
  <tr>
   <td><strong>Asignación de nombres</strong></td>
   <td>cq-&lt;Versión&gt;-hotfix-&lt;id. de revisión&gt;-&lt;versión de revisión&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusiones</strong></td>
   <td>Incluye correcciones para un problema específico</td>
  </tr>
  <tr>
   <td><strong>Documentación</strong></td>
   <td>Las notas de la versión de las revisiones públicas solo están disponibles en función de la solicitud del cliente a través del portal de asistencia de AEM.</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Según sea necesario</td>
  </tr>
  <tr>
   <td><strong>Disponibilidad e instalación</strong></td>
   <td>
    <ul>
     <li>Entregado como paquete</li>
     <li>Disponible en Uso compartido de paquetes</li>
     <li>Depende del Service Pack más reciente lanzado</li>
     <li>La mayoría de las correcciones rápidas son independientes, a menos que se especifiquen. Puede instalarse en cualquier orden. Puede verificarse mediante la ficha Detalles de uso compartido de paquetes del elemento Dependencias.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nivel de prueba</strong></td>
   <td>
    <ul>
     <li>Validado por el Servicio de atención al cliente</li>
     <li>Las correcciones rápidas de AEM no se benefician del mismo nivel de garantía de calidad que los Service Packs o las versiones de productos. Por lo tanto, primero deben validarse en un entorno de ensayo como parte de los procesos de implementación de calidad.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Superposición {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>Definición</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Asignación de nombres</strong></td>
   <td>superposición-&lt;ID del vale&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusiones</strong></td>
   <td>Corrección de errores de un archivo JS o JSP</td>
  </tr>
  <tr>
   <td><strong>Documentación</strong></td>
   <td>Ninguna</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Según sea necesario</td>
  </tr>
  <tr>
   <td><strong>Disponibilidad e instalación</strong></td>
   <td>
    <ul>
     <li>Entregado como paquete por el Servicio de atención al cliente de AEM</li>
     <li>No necesariamente se incluye en los Service Packs o en las versiones completas</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nivel de prueba</strong></td>
   <td>Validado por el Servicio de atención al cliente</td>
  </tr>
 </tbody>
</table>

## Paquete de funciones {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definición</strong></td>
   <td>
    <ul>
     <li>Los paquetes de funciones son funcionalidades adicionales y se entregan a través de Service Packs. Si una versión de AEM ha lanzado su último Service Pack, Adobe no proporcionará ningún paquete de funciones para él en el futuro.</li>
     <li>Los programas PDF contienen mejoras del producto, programadas para una versión posterior del producto, pero entregadas con antelación según la decisión de la Administración de productos de Adobe.</li>
     <li>Las funciones siempre se combinan con la siguiente versión principal y, a continuación, se adaptan a la versión de AEM requerida por el cliente</li>
     <li>Los paquetes de funciones de Interés común y GA se combinan en el siguiente Service Pack</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Asignación de nombres</strong></td>
   <td>cq-&lt;Versión&gt;-featurepack-&lt;Id. de funciones&gt;-&lt;versión de funciones&gt;-&lt;versión de funciones&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusiones</strong></td>
   <td>
    <ul>
     <li>Nuevas funciones</li>
     <li>Mejoras</li>
     <li>Correcciones de errores (actualizaciones de productos incrementales)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentación</strong></td>
   <td>La documentación está disponible en helpx.adobe.com.</td>
  </tr>
  <tr>
   <td><strong>Cadence</strong></td>
   <td>Varía con el área de producto</td>
  </tr>
  <tr>
   <td><strong>Disponibilidad e instalación</strong></td>
   <td>
    <ul>
     <li>Entregado mediante Service Packs</li>
     <li>Disponible en Uso compartido de paquetes. Los clientes aceptan los términos y condiciones de Adobe a través del uso compartido de paquetes.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Nivel de prueba</strong></td>
   <td>Los paquetes de funciones de disponibilidad general están validados por el control de calidad</td>
  </tr>
 </tbody>
</table>

* [1]: Las correcciones OAK no se entregan como correcciones rápidas individuales. Sin embargo, se incluyen en la corrección urgente Acumulative Oak posterior. Si es necesario, se puede poner a disposición una compilación de diagnóstico sobre el último COFP. La condición previa es que el cliente tenga la última COFP en ejecución. Las compilaciones de diagnóstico solo proporcionan el mismo nivel de garantía de calidad que una corrección urgente. Por lo tanto, no proporcionan el mismo nivel de garantía de calidad que un paquete de correcciones acumulativo, un Service Pack o una versión del producto. La corrección final se entrega con la siguiente CFP.

