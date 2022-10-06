---
title: Reestructuración de repositorios de comercio electrónico en AEM 6.5
seo-title: E-Commerce Repository Restructuring in AEM 6.5
description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios en AEM 6.5 para comercio electrónico.
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for E-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 2%

---

# Reestructuración de repositorios de comercio electrónico en AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Tal como se describe en el elemento principal [Reestructuración de repositorios en AEM 6.5](/help/sites-deploying/repository-restructuring.md) , los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios en el repositorio que afectan a la solución de comercio electrónico de AEM. Algunos cambios requieren un esfuerzo de trabajo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

## Con actualización a la versión 6.5 {#with-upgrade}

### Datos de Productos, Pedidos, Colecciones, Clasificaciones, Métodos de Envío y Métodos de Pago {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

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
   <td><p>Puede usar un <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Migración diferida</a> para migrar datos de comercio electrónico.</p> <p>Realiza los siguientes pasos:</p>
    <ul>
     <li>ajusta las referencias a la ubicación antigua para que apunten a la nueva ubicación</li>
     <li>mueve el contenido de la ubicación antigua a la nueva ubicación</li>
     <li>elimina la ubicación antigua para activar finalmente el uso de la nueva ubicación en todo el sistema</li>
    </ul> <p>Las ubicaciones que abarca la tarea son:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/Shipping-methods<br /> </li>
    </ul> <p>Para catálogos más grandes, se recomienda ejecutar la tarea de migración del comercio individualmente pasando la siguiente propiedad del sistema Java a AEM:</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Después de la migración AEM debe reiniciarse.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>
