---
title: Reestructuración de repositorios de comercio electrónico en AEM 6.5
description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios de AEM 6.5 para E-Commerce.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 835ee49e-9248-5578-a60a-15c097807178
    internal-label: Upgrading
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 9%
---
# Reestructuración de repositorios de comercio electrónico en AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Como se describe en la página principal [Reestructuración del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a la solución AEM E-Commerce. Algunos cambios requieren esfuerzo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

## Con actualización a 6.5 {#with-upgrade}

### Datos de productos, pedidos, colecciones, clasificaciones, métodos de envío y métodos de pago {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Puede utilizar una tarea <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Migración diferida</a> para migrar datos de E-Commerce.</p> <p>Realiza los siguientes pasos:</p>
    <ul>
     <li>ajusta las referencias a la ubicación antigua para que apunten a la nueva ubicación</li>
     <li>mueve contenido de la ubicación antigua a la nueva</li>
     <li>elimina la ubicación antigua para activar finalmente el uso de la nueva ubicación en todo el sistema</li>
    </ul> <p>Las ubicaciones que abarca la tarea son las siguientes:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>Para catálogos más grandes, Adobe recomienda ejecutar la tarea de migración comercial de forma individual pasando la siguiente propiedad del sistema Java™ a AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Después de la migración, reinicie AEM.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>
