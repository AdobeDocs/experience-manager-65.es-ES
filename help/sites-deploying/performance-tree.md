---
title: Árbol de rendimiento
description: AEM Obtenga información acerca de los pasos que se deben seguir para solucionar problemas de rendimiento en las soluciones de problemas de la.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: f2f968b8-b21c-487d-bc0d-ed60903bc4bf
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 9%

---

# Árbol de rendimiento{#performance-tree}

## Ámbito {#scope}

El diagrama siguiente tiene por objeto proporcionar instrucciones sobre los pasos que se deben seguir para solucionar los problemas de rendimiento. Se divide en cinco secciones para facilitar la lectura.

Cada paso del diagrama está vinculado a un recurso de documentación o a una recomendación.

## Requisitos previos y suposiciones {#prerequisites-and-assumptions}

AEM Se supone que se observa un problema de rendimiento en una página determinada (ya sea una consola de o una página web) y que se puede reproducir de forma coherente. Tener una forma de probar o monitorear el rendimiento es un requisito previo antes de comenzar la investigación.

El análisis comienza en el paso 0. AEM El objetivo es determinar qué entidad (Dispatcher, host externo o red) es responsable del problema de rendimiento y, a continuación, determinar qué área (servidor o red) debe investigarse.

### Sección 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### Sección 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### Sección 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### Sección 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### Sección 5 {#section-4}

![chlimage_1-107](assets/chlimage_1-107.png)

## Vínculos de referencia {#reference-links}

<table>
 <tbody>
  <tr>
   <td><strong>Paso</strong></td>
   <td><strong>Título</strong></td>
   <td><strong>Recursos</strong></td>
  </tr>
  <tr>
   <td><strong>Etapa 0</strong></td>
   <td>Analizar flujo de solicitudes</td>
   <td><p>Puede utilizar el análisis de solicitud HTTP estándar en el explorador para analizar el flujo de solicitud. Para obtener más información sobre cómo realizar este análisis en Chrome, consulte:<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developer.chrome.com/docs/devtools/</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 2</strong></td>
   <td>¿Las solicitudes provienen de hosts externos?</td>
   <td>Puede utilizar el análisis de solicitud HTTP estándar en el explorador para analizar el flujo de solicitud. Consulte los vínculos anteriores sobre cómo realizar este análisis en Chrome.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 3</strong></td>
   <td>¿Se pueden almacenar en caché las solicitudes?</td>
   <td>Para obtener más información sobre las solicitudes almacenables en caché y los consejos generales de optimización del rendimiento de Dispatcher, consulte <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Optimización del rendimiento de Dispatcher</a>.</td>
  </tr>
  <tr>
   <td><strong>Etapa 4</strong></td>
   <td>¿Las solicitudes provienen de Dispatcher?</td>
   <td><p>Para ver si las solicitudes se almacenan en caché correctamente, consulte la <a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#debugging">Documentación de depuración de Dispatcher</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 5</strong></td>
   <td>AEM ¿Dispatcher está intentando autenticar cada solicitud a través de la?</td>
   <td>Compruebe si Dispatcher envía <code>HEAD</code> AEM solicitudes de autenticación para la autenticación antes de enviar el recurso almacenado en caché. Buscar: <code>HEAD</code> AEM solicitudes en la lista de <code>access.log</code>. Para obtener más información, consulte <a href="/help/sites-deploying/configure-logging.md">Registro</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 6</strong></td>
   <td>¿La ubicación geográfica de Dispatcher está lejos de los usuarios?</td>
   <td>Acerque Dispatcher a los usuarios.</td>
  </tr>
  <tr>
   <td><strong>Etapa 7</strong></td>
   <td>¿Es correcta la capa de red de Dispatcher?</td>
   <td><br /> Investigue la capa de red para ver si hay problemas de saturación y latencia.<p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 8</strong></td>
   <td>¿La lentitud es reproducible con una instancia local?</td>
   <td><br /> <p>Uso <a href="/help/sites-developing/tough-day.md">Día difícil</a> para replicar condiciones "reales" desde las instancias de producción. Si este escenario no es realista para el espacio de desarrollo, asegúrese de probar la instancia de producción (o una instancia de ensayo idéntica) en un contexto de red diferente.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 9</strong></td>
   <td>¿La ubicación geográfica del servidor está lejos de los usuarios?</td>
   <td>Acerque el servidor a los usuarios.</td>
  </tr>
  <tr>
   <td><strong>Pasos 10 y 29</strong></td>
   <td>Investigar la capa de red</td>
   <td><p>Investigue la capa de red para ver si hay problemas de saturación y latencia.</p> <p>Para el nivel de creación, se recomienda que la latencia no supere los 100 milisegundos.</p> <p>Para obtener más información sobre sugerencias de optimización de rendimiento, consulte <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">esta página</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 11</strong></td>
   <td>Acercar el servidor o agregar uno por región</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 12</strong></td>
   <td>AEM Solución de problemas del servidor de</td>
   <td>Consulte los siguientes pasos secundarios en el diagrama para obtener más información.</td>
  </tr>
  <tr>
   <td><strong>Etapa 13</strong></td>
   <td>Compruebe los requisitos de hardware</td>
   <td>Consulte la documentación de <a href="/help/managing/hardware-sizing-guidelines.md">Directrices de tamaño de hardware</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 14</strong></td>
   <td>Buscar causas frecuentes de problemas de rendimiento</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 15</strong></td>
   <td>Buscar solicitudes lentas</td>
   <td><p>Puede comprobar las solicitudes lentas analizando la variable <code>request.log</code> o utilizando <code>rlog.jar</code>.</p> <p>Para obtener más información sobre el uso de rlog.jar, consulte esta página.</p> <p>Consulte <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">Busque solicitudes con tiempos de duración largos mediante rlog.jar.</a>.<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 16</strong></td>
   <td>Servidor de perfiles</td>
   <td><p>AEM Para obtener información sobre las herramientas de creación de perfiles que puede utilizar con los informes de perfiles, consulte <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">Herramientas para monitorizar y analizar el rendimiento</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 17</strong></td>
   <td>Buscar métodos lentos en la creación de perfiles</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 18</strong></td>
   <td>Situaciones comunes de creación de perfiles</td>
   <td>Consulte <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">Análisis de escenarios específicos</a> en la sección Optimización de rendimiento.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 19</strong></td>
   <td>CPU al 100%</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es</a></td>
  </tr>
  <tr>
   <td><strong>Etapa 20</strong></td>
   <td>Memoria insuficiente</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">Memoria insuficiente</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">Mi aplicación genera errores de memoria insuficiente</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html">Analice los problemas de memoria.</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 21</strong></td>
   <td>E/S de disco</td>
   <td><p>Consulte la <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">E/S de disco</a> de la documentación de Monitorización y mantenimiento.</p> </td>
  </tr>
  <tr>
   <td><strong>Pasos 22 y 22.1</strong></td>
   <td>Proporción de caché</td>
   <td>Consulte <a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">Calcular la proporción de caché de Dispatcher</a>.<br /> <br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 23</strong></td>
   <td>Consultas lentas</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Prácticas recomendadas para consultas e indexación</a></td>
  </tr>
  <tr>
   <td><strong>Etapa 24</strong></td>
   <td>Ajuste del repositorio</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">Consejos de ajuste de rendimiento</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">Configurar para el rendimiento</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">Ajuste del rendimiento del repositorio</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Etapa 25</strong></td>
   <td>Flujos de trabajo en ejecución</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">Procesamiento de flujo de trabajo simultáneo</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">Configurar la cola para un flujo de trabajo específico</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">Depuración regular de instancias de flujo de trabajo</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">Flujos de trabajo transitorios</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 26</strong></td>
   <td>Infraestructura de MSM</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">Prácticas recomendadas para administradores de varios sitios</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 27</strong></td>
   <td>Ajuste de recursos</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">Servicio de sincronización de recursos</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">Varias instancias de DAM</a></li>
     <li>Artículo de consejos de rendimiento <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">aquí</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 28</strong></td>
   <td>Sesiones sin cerrar</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">Comprobación de sesiones JCR sin cerrar</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 30</strong></td>
   <td>¿Desea acercar Dispatcher (agregue uno por "región"?)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 31</strong></td>
   <td>Usar CDN delante de Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Uso de Dispatcher con una CDN</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 32</strong></td>
   <td>AEM Para descargar el servidor de, utilice la administración de sesiones en el nivel de Dispatcher</td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement">Activar sesiones seguras</a></p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 33</strong></td>
   <td>Hacer que las solicitudes sean almacenables en caché</td>
   <td>
    <ol>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es">Configuración general de Dispatcher</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache">Configurar la caché de Dispatcher</a></li>
    </ol> <p>Cómo mejorar la proporción de caché; hacer que las solicitudes puedan almacenarse en caché (prácticas recomendadas de Dispatcher)</p> <p>Además, tenga en cuenta la siguiente configuración para optimizar las configuraciones de almacenamiento en caché<br /> </p>
    <ol>
     <li>Establezca una regla sin caché para la solicitud HTTP que no sea de GET</li>
     <li>Configurar las cadenas de consulta para que no se puedan almacenar en caché</li>
     <li>No almacenar en caché las direcciones URL con extensiones faltantes</li>
     <li>Encabezados de autenticación en caché (posible desde la versión 4.1.10 de Dispatcher)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 34</strong></td>
   <td>Actualizar la versión de Dispatcher</td>
   <td><p>Puede descargar la versión más reciente de Dispatcher en esta ubicación:</p> <p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html">Seguir vínculo</a></p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 35</strong></td>
   <td>Configurar Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html">Configuración de Dispatcher</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 36</strong></td>
   <td>Comprobar invalidación de caché</td>
   <td><br />
    <ul>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment">Invalidación de caché para el nivel de Author;</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance">Invalidación de caché para el nivel de publicación.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Pasos 37 y 38</strong></td>
   <td>Carga diferida</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">AEM Consulte la Sesión Gem sobre rendimiento web de la.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 39</strong></td>
   <td>Utilice la preconexión para reducir la sobrecarga de conexión</td>
   <td>Consulte la sesión de Gem anterior. Además, documentación adicional previa a la conexión en W3c:<a href="https://html.spec.whatwg.org/#linkTypes"> https://html.spec.whatwg.org/#linkTypes</a></td>
  </tr>
  <tr>
   <td><strong>Pasos 40 y 41</strong><br /> </td>
   <td>Latencia y tiempo de respuesta de hosts externos</td>
   <td>Investigue la latencia y el tiempo de respuesta de los hosts externos.</td>
  </tr>
  <tr>
   <td><strong>Pasos 45<br /> y 47</strong><br /> </td>
   <td>Uso de HTTP/2</td>
   <td>Consulte la Sesión Gem para ver los pasos 37, 38 y 39. Además, consulte <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">esta</a> publicación en el foro sobre compatibilidad con HTTP/2.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 49</strong></td>
   <td>Reducir tamaño de carga útil</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Habilitar Gzip</a> y <a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">reducir el tamaño de la imagen</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Pasos 42 y 43</strong></td>
   <td>Keep-Alive</td>
   <td><p>Es el <code>Keep-Alive</code> encabezado presente en las diferentes solicitudes para reutilizar conexiones? De lo contrario, significaría que cada solicitud conduce a otro establecimiento de conexión, lo que introduce gastos generales innecesarios. (Análisis de solicitudes HTTP estándar en el explorador)</p> <p>Puede consultar la <a href="/help/sites-administering/proxy-jar.md">Herramienta Servidor Proxy</a> para comprobar las conexiones de mantenimiento activo.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 44</strong></td>
   <td>¿Cuántas solicitudes se realizan?</td>
   <td>Realizar análisis de solicitudes HTTP estándar en el explorador.</td>
  </tr>
  <tr>
   <td><strong>Etapa 46</strong></td>
   <td>Reducción del número de solicitudes</td>
   <td>
    <ol>
     <li>Concatenar recursos (imágenes, sprites CSS, JSON)<br /> </li>
     <li>Incrustar Clientlibs:
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">Creación de carpetas de biblioteca de cliente</a> : consulte encabezado Usar la incrustación para minimizar las solicitudes</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 48</strong></td>
   <td>¿Cuál es el tamaño de la carga útil?</td>
   <td>Análisis de solicitudes HTTP estándar en el explorador</td>
  </tr>
  <tr>
   <td><strong>Pasos 50 y 51</strong></td>
   <td>Bloqueo de código JS</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html</a></td>
  </tr>
 </tbody>
</table>
