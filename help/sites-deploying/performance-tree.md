---
title: Árbol de rendimiento
seo-title: Performance Tree
description: Obtenga información sobre los pasos que deben seguirse para solucionar problemas de rendimiento en AEM.
seo-description: Learn about the steps that need to be taken in order to troubleshoot performance issues in AEM.
uuid: ab0624f7-6b39-4255-89e0-54c74b54cd98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 5febbb1e-795c-49cd-a8f4-c6b4b540673d
exl-id: f2f968b8-b21c-487d-bc0d-ed60903bc4bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 5%

---

# Árbol de rendimiento{#performance-tree}

## Ámbito {#scope}

El diagrama siguiente pretende proporcionar instrucciones sobre los pasos que se deben seguir para solucionar los problemas de rendimiento. Se divide en 5 secciones para facilitar la lectura.

Cada paso del diagrama está vinculado a un recurso de documentación o a una recomendación.

## Requisitos previos y supuestos {#prerequisites-and-assumptions}

Se supone que un problema de rendimiento se observa en una página determinada (ya sea una consola AEM o una página web) y se puede reproducir de forma coherente. Antes de iniciar la investigación, es necesario disponer de una forma de probar o supervisar el rendimiento.

El análisis comienza en el paso 0. El objetivo es determinar qué entidad (Dispatcher, host externo o AEM) es responsable del problema de rendimiento y luego determinar qué área (servidor o red) debe investigarse.

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
   <td><strong>Etapa</strong></td>
   <td><strong>Título</strong></td>
   <td><strong>Medios</strong></td>
  </tr>
  <tr>
   <td><strong>Etapa 0</strong></td>
   <td>Analizar el flujo de solicitud</td>
   <td><p>Se puede utilizar el análisis de solicitud HTTP estándar en el navegador para analizar el flujo de solicitudes. Para obtener más información sobre cómo hacer esto en Chrome, consulte:<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading</a><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing"><br /> https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 2</strong></td>
   <td>¿Las solicitudes proceden de hosts externos?</td>
   <td>Se puede utilizar el análisis de solicitud HTTP estándar en el navegador para analizar el flujo de solicitudes. Consulte los vínculos anteriores sobre cómo hacerlo en Chrome.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 3</strong></td>
   <td>¿Se pueden almacenar en caché las solicitudes?</td>
   <td>Para obtener más información sobre las solicitudes almacenables en caché y los consejos generales de optimización del rendimiento de Dispatcher, consulte <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Optimización del rendimiento de Dispatcher</a>.</td>
  </tr>
  <tr>
   <td><strong>Etapa 4</strong></td>
   <td>¿Las solicitudes provienen de Dispatcher?</td>
   <td><p>Marque la <a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#debugging">Documentación de depuración de Dispatcher</a> para ver si las solicitudes se almacenan en la caché correctamente.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 5</strong></td>
   <td>¿Dispatcher está intentando autenticar cada solicitud a través de AEM?</td>
   <td>Compruebe si el despachante envía <code>HEAD</code> solicitudes a AEM para autenticación antes de enviar el recurso almacenado en caché. Para ello, busque <code>HEAD</code> solicitudes en la AEM <code>access.log</code>. Para obtener más información, consulte <a href="/help/sites-deploying/configure-logging.md">Registro</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 6</strong></td>
   <td>¿La ubicación geográfica de Dispatcher está lejos de los usuarios?</td>
   <td>Acerque Dispatcher a los usuarios.</td>
  </tr>
  <tr>
   <td><strong>Etapa 7</strong></td>
   <td>¿Está bien la capa de red de Dispatcher?</td>
   <td><br /> Investigue la capa de red para detectar problemas de saturación y latencia.<p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 8</strong></td>
   <td>¿La lentitud se puede reproducir con una instancia local?</td>
   <td><br /> <p>Uso <a href="/help/sites-developing/tough-day.md">Día duro</a> para replicar las condiciones del "mundo real" desde las instancias de producción. Si esto no es realista para la pendiente del desarrollo, asegúrese de probar la instancia de producción (o una instancia de ensayo idéntica) en un contexto de red diferente.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 9</strong></td>
   <td>¿La ubicación geográfica del servidor está lejos de los usuarios?</td>
   <td>Acerque el servidor a los usuarios.</td>
  </tr>
  <tr>
   <td><strong>Pasos 10 y 29</strong></td>
   <td>Investigar capa de red</td>
   <td><p>Investigue la capa de red para detectar problemas de saturación y latencia.</p> <p>Para el nivel de creación, se recomienda que la latencia no supere los 100 milisegundos.</p> <p>Para obtener más información sobre sugerencias de optimización del rendimiento, consulte <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">esta página</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 11</strong></td>
   <td>Acercar el servidor o agregar uno por región</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 12</strong></td>
   <td>Resolución de problemas del servidor AEM</td>
   <td>Consulte los siguientes subpasos del diagrama para obtener más información.</td>
  </tr>
  <tr>
   <td><strong>Etapa 13</strong></td>
   <td>Comprobar los requisitos de hardware</td>
   <td>Consulte la documentación en <a href="/help/managing/hardware-sizing-guidelines.md">Pautas para el tamaño del hardware</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 14</strong></td>
   <td>Compruebe las causas frecuentes de los problemas de rendimiento</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 15</strong></td>
   <td>Buscar solicitudes lentas</td>
   <td><p>Puede comprobar la existencia de solicitudes lentas analizando la variable <code>request.log</code> o utilizando <code>rlog.jar</code>.</p> <p>Para obtener más información sobre el uso de rlog.jar, consulte esta página.</p> <p>Consulte <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">Uso de rlog.jar para encontrar solicitudes con largos tiempos de duración</a>.<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 16</strong></td>
   <td>Servidor de perfiles</td>
   <td><p>Para obtener información sobre las herramientas de creación de perfiles que puede utilizar con AEM, consulte <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">Herramientas para monitorizar y analizar el rendimiento</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 17</strong></td>
   <td>Buscar métodos lentos en la creación de perfiles</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 18</strong></td>
   <td>Situaciones comunes de creación de perfiles</td>
   <td>Consulte <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">Análisis de escenarios específicos</a> en la sección Optimización del rendimiento .<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 19</strong></td>
   <td>CPU del 100%</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://helpx.adobe.com/experience-manager/6-3/sites-deploying/monitoring-and-maintaining.html#MonitoringPerformance</a></td>
  </tr>
  <tr>
   <td><strong>Etapa 20</strong></td>
   <td>Memoria insuficiente</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">Memoria insuficiente</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">Mi aplicación genera errores de memoria insuficiente</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html">Analizar problemas de memoria en Helpx.</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 21</strong></td>
   <td>E/S de disco</td>
   <td><p>Consulte la <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">E/S de disco</a> en la documentación de Monitoreo y Mantenimiento.</p> </td>
  </tr>
  <tr>
   <td><strong>Pasos 22 y 22.1</strong></td>
   <td>Relación de caché</td>
   <td>Consulte <a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">Cálculo de la proporción de caché de Dispatcher</a>.<br /> <br /> </td>
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
     <li><a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">Sugerencias de ajuste de rendimiento</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">Configuración del rendimiento</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">Ajuste del rendimiento del repositorio</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Etapa 25</strong></td>
   <td>Flujos de trabajo en ejecución</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">Procesamiento De Flujo De Trabajo Simultáneo</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">Configuración de la cola para un flujo de trabajo específico</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">Depuración regular de instancias de flujo de trabajo</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">Flujos de trabajo transitorios</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 26</strong></td>
   <td>Infraestructura de MSM</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">Prácticas recomendadas del administrador de varios sitios</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 27</strong></td>
   <td>Ajuste de recursos</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">Servicio de sincronización de recursos</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">Varias instancias de DAM</a></li>
     <li>Artículos sobre consejos de rendimiento <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">here</a> y <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">here</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 28</strong></td>
   <td>Sesiones no cerradas</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">Comprobación de sesiones JCR no cerradas</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 30</strong></td>
   <td>Acerque el despachante (añada uno por "región"?)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 31</strong></td>
   <td>Usar CDN delante de Dispatcher</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Utilizar Dispatcher con una CDN</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 32</strong></td>
   <td>Utilice la administración de sesiones en el nivel de Dispatcher para descargar AEM servidor</td>
   <td><p><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement">Habilitar sesiones seguras</a></p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 33</strong></td>
   <td>Hacer que las solicitudes se almacenen en caché</td>
   <td>
    <ol>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html">Configuración general de Dispatcher</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache">Configuración de la caché de Dispatcher</a></li>
    </ol> <p>Cómo mejorar la proporción de caché; hacer que las solicitudes se puedan almacenar en caché (prácticas recomendadas de Dispatcher)</p> <p>Además, tenga en cuenta los siguientes ajustes para optimizar las configuraciones de almacenamiento en caché<br /> </p>
    <ol>
     <li>Establezca una regla de no caché para solicitudes HTTP que no sean de GET</li>
     <li>Configurar cadenas de consulta que no se pueden almacenar en caché</li>
     <li>No almacene en caché las URL con extensiones que faltan</li>
     <li>Encabezados de autenticación de caché (posible desde la versión 4.1.10 de Dispatcher)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 34</strong></td>
   <td>Actualización de la versión de Dispatcher</td>
   <td><p>Puede descargar la última versión de Dispatcher en esta ubicación:</p> <p><a href="https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html">Seguir vínculo</a></p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 35</strong></td>
   <td>Configurar Dispatcher</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html">Configuración de Dispatcher</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 36</strong></td>
   <td>Comprobar invalidación de caché</td>
   <td><br />
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment">Invalidación de caché para el nivel de Author;</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance">Invalidación de caché para el nivel de publicación.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Pasos 37 y 38</strong></td>
   <td>Carga diferida</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">Consulte la sesión de Gem sobre AEM rendimiento web.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 39</strong></td>
   <td>Utilice la preconexión para reducir la sobrecarga de conexión</td>
   <td>Consulte la sesión de Gem indicada anteriormente. Además, la documentación adicional se preconecta en W3c:<a href="https://www.w3.org/TR/resource-hints/#dfn-preconnect"> https://www.w3.org/TR/resource-hints/#dfn-preconnect</a></td>
  </tr>
  <tr>
   <td><strong>Pasos 40 y 41</strong><br /> </td>
   <td>Tiempo de latencia y respuesta de los hosts externos</td>
   <td>Investigue la latencia y el tiempo de respuesta de los hosts externos.</td>
  </tr>
  <tr>
   <td><strong>Pasos 45<br /> y 47</strong><br /> </td>
   <td>Uso de HTTP/2</td>
   <td>Consulte la sesión de Gem para ver los pasos 37, 38 y 39. Además, consulte <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">this</a> publicación en el foro sobre compatibilidad con HTTP/2.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 49</strong></td>
   <td>Reducir tamaño de carga útil</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Habilitar Gzip</a> y <a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">reducir el tamaño de la imagen</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Pasos 42 y 43</strong></td>
   <td>Mantener vivo</td>
   <td><p>¿Es la variable <code>Keep-Alive</code> presente en las diferentes solicitudes para reutilizar conexiones? De lo contrario, significaría que cada solicitud conduce a otro establecimiento de conexión, que introduce una sobrecarga innecesaria. (Análisis de solicitudes HTTP estándar en el explorador)</p> <p>Puede comprobar la <a href="/help/sites-administering/proxy-jar.md">Herramienta Servidor proxy</a> para comprobar la existencia de conexiones Keep-Alive.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 44</strong></td>
   <td>¿Cuántas solicitudes se realizan?</td>
   <td>Realice un análisis de solicitud HTTP estándar en el explorador.</td>
  </tr>
  <tr>
   <td><strong>Etapa 46</strong></td>
   <td>Reducir el número de solicitudes</td>
   <td>
    <ol>
     <li>Concatenar recursos (imágenes, sprites CSS, JSON, etc.)<br /> </li>
     <li>Integración de Clientlibs:
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">Creación de carpetas de la biblioteca del cliente</a> - consulte el encabezado Uso de la incrustación para minimizar las solicitudes</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 48</strong></td>
   <td>¿Cuál es el tamaño de la carga útil?</td>
   <td>Análisis de solicitud HTTP estándar en el explorador</td>
  </tr>
  <tr>
   <td><strong>Pasos 50 y 51</strong></td>
   <td>Bloqueo de código JS</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">https://docs.adobe.com/ddc/en/gems/aem-web-performance.html</a></td>
  </tr>
 </tbody>
</table>
