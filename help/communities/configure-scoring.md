---
title: Elementos esenciales de puntuación e insignias
seo-title: Scoring and Badges Essentials
description: Información general sobre las características Puntuación e insignias
seo-description: Scoring and Badges feature overview
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Elementos esenciales de puntuación e insignias {#scoring-and-badges-essentials}

La función de puntuación e insignias de AEM Communities permite identificar y recompensar a los miembros de la comunidad.

Los detalles de configuración de la función se describen en

* [Puntuación y distintivos de comunidades](/help/communities/implementing-scoring.md)

Esta página contiene detalles técnicos adicionales:

* Cómo: [mostrar un distintivo](#displaying-badges) como imagen o texto
* Cómo activar la función extensiva [registro de depuración](#debug-log-for-scoring-and-badging)
* Cómo: [acceder a UGC](#ugc-for-scoring-and-badging) relacionado con la puntuación y el distintivo

>[!CAUTION]
>
>La estructura de implementación visible en CRXDE Lite está sujeta a cambios.

## Visualización de distintivos {#displaying-badges}

Si un distintivo se muestra como texto o imagen se controla en el lado del cliente en la plantilla HBS.

Por ejemplo, busque `this.isAssigned` in `/libs/social/forum/components/hbs/topic/list-item.hbs`:

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

Si el valor es True, isAssigned indica que el distintivo se ha asignado a una función y que el distintivo debe mostrarse como texto.

Si es false, is Assigned indica que el distintivo se concedió por una puntuación ganada y que el distintivo debe mostrarse como una imagen.

Cualquier cambio en este comportamiento debe realizarse en un script personalizado (anulación o superposición). Consulte [Personalización del lado del cliente](/help/communities/client-customize.md).

## Registro de depuración para puntuación e identificación {#debug-log-for-scoring-and-badging}

Para depurar la puntuación y el distintivo, se puede configurar un archivo de registro personalizado. El contenido de este archivo de registro se puede proporcionar al servicio de atención al cliente si se producen problemas con la función.

Para obtener instrucciones detalladas, visite [Crear un archivo de registro personalizado](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

Para configurar rápidamente un archivo slinglog:

1. Acceda a la **Compatibilidad con registros de la consola web de Adobe Experience Manager**, por ejemplo

   * https://localhost:4502/system/console/slinglog

1. Seleccionar **Añadir nuevo registrador**

   1. Seleccionar `DEBUG` para **Nivel de registro**

   1. Introduzca un nombre para **Archivo de registro**, por ejemplo

      * logs/scoring-debug.log
   1. Introducir dos **Logger** Entradas (clase) (usando `+` icon)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. Seleccione **Guardar**



![debug-scoring-log](assets/debug-scoring-log.png)

Para ver las entradas de registro:

* Desde la consola web

   * En el **Estado** menú
   * Seleccionar **Archivos de registro**
   * Busque el nombre del archivo de registro, como `scoring-debug`

* En el disco local del servidor

   * El archivo de registro se encuentra en &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*nombre-archivo-registro*>.log

   * Por ejemplo, `.../crx-quickstart/logs/scoring-debug.log`. 

![registro de puntuación](assets/scoring-log.png)

## UGC para puntuación e identificación {#ugc-for-scoring-and-badging}

Es posible ver el UGC relacionado con la puntuación y el distintivo cuando el SRP elegido es JSRP o MSRP, pero no ASRP. (Si no conoce estos términos, consulte [Almacenamiento de contenido de comunidad](/help/communities/working-with-srp.md) y [Resumen del proveedor de recursos de almacenamiento](/help/communities/srp.md).)

Las descripciones para acceder a los datos de puntuación y distintivos utilizan JSRP, ya que el UGC es fácilmente accesible mediante [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP en autor**: la experimentación en el entorno de creación da como resultado un CGU que solo es visible desde el entorno de creación.

**JSRP en publicación**: del mismo modo, si realiza pruebas en el entorno de publicación, será necesario acceder a un CRXDE Lite con privilegios administrativos en una instancia de publicación. Si la instancia de publicación se ejecuta en [modo de producción](/help/sites-administering/production-ready.md) (nosamplecontent runmode), será necesario [habilitar CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

La ubicación base de UGC en JSRP es `/content/usergenerated/asi/jcr/`.

### API de puntuación e identificación {#scoring-and-badging-apis}

Las siguientes API están disponibles para su uso:

* [com.adobe.cq.social.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.social.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

Los últimos Javadocs para el paquete de funciones instalado están disponibles para los desarrolladores desde el repositorio de Adobe. Consulte [Uso de Maven para comunidades: Javadocs](/help/communities/maven.md#javadocs).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

### Configuración de ejemplo {#example-setup}

AEM Las capturas de pantalla de los datos del repositorio proceden de la configuración de la puntuación y el distintivo para un foro en dos sitios de diferentes:

1. AEM Un sitio *con* un id único (sitio de la comunidad creado con el asistente):

   * Uso del sitio Tutorial de introducción (participación) creado durante la [tutorial de introducción](/help/communities/getting-started.md)
   * Busque el nodo de la página del foro

      `/content/sites/engage/en/forum/jcr:content`

   * Añadir propiedades de puntuación e insignias

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * Busque el nodo del componente del foro

      `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Añadir propiedad para mostrar distintivos

      `allowBadges = true`

   * Un usuario inicia sesión, crea un tema de foro y se le otorga una insignia de bronce


1. AEM Un sitio *sin* un id único:

   * Uso del [Guía de componentes de la comunidad](/help/communities/components-guide.md)
   * Busque el nodo de la página del foro

      `/content/community-components/en/forum/jcr:content`

   * Añadir propiedades de puntuación e insignias

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * Busque el nodo del componente del foro

      `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Añadir propiedad para mostrar distintivos

      `allowBadges = true`

   * Un usuario inicia sesión, crea un tema de foro y se le otorga una insignia de bronce


1. A un usuario se le asigna un distintivo de moderador mediante cURL :

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   Como un usuario ha obtenido dos insignias de bronce y se le ha concedido una insignia de moderador, así es como aparece el usuario con su entrada en el foro.

   ![moderador](assets/moderator.png)

>[!NOTE]
>
>Este ejemplo no sigue estas prácticas recomendadas:
>
>* Los nombres de las reglas de puntuación deben ser únicos a nivel global; no deben terminar con el mismo nombre.
>
>  Un ejemplo de lo que *no* para hacer:
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* AEM Creación de imágenes de insignias únicas para diferentes sitios de


### UGC de puntuación de acceso {#access-scoring-ugc}

Uso del [API](#scoring-and-badging-apis) se prefiere.

Para fines de investigación, con JSRP como ejemplo, la carpeta base que contiene puntuaciones es

* `/content/usergenerated/asi/jcr/scoring`

El nodo secundario de `scoring` es el nombre de la regla de puntuación. Por lo tanto, una práctica recomendada es que los nombres de reglas de puntuación en un servidor sean únicos a nivel global.

Para el sitio de Geometrixx Engage, el usuario y su puntuación se encuentran en una ruta construida con el nombre de la regla de puntuación, el ID de sitio de la comunidad ( `engage-ba81p`), un id único y el id del usuario :

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Para el sitio de guía de componentes de la comunidad, el usuario y su puntuación se encuentran en una ruta construida con el nombre de la regla de puntuación, un ID predeterminado ( `default-site`), un id único y el id del usuario :

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

La puntuación se almacena en la propiedad `scoreValue_tl` que solo pueden contener un valor o hacer referencia indirectamente a atomicCounter.

![access-scoring-ugc](assets/access-scoring-ugc.png)

### UGC de insignias de acceso {#access-badging-ugc}

Uso del [API](#scoring-and-badging-apis) se prefiere.

Para fines de investigación, utilizando JSRP para el ejemplo, la carpeta base que contiene información sobre insignias asignadas o concedidas es

* `/content/usergenerated/asi/jcr`

Seguido de la ruta al perfil del usuario, que termina en una carpeta de distintivos, como:

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Insignia otorgada {#awarded-badge}

![granted-badging-ugc](assets/access-badging-ugc.png)

#### Insignia asignada {#assigned-badge}

![assigned-badge](assets/assigned-badge.png)

## Información adicional {#additional-information}

Para mostrar una lista ordenada de miembros basada en puntos:

* [Función de clasificación](/help/communities/functions.md#leaderboard-function) para su inclusión en un sitio de comunidad o plantilla de grupo.
* [Componente de clasificación](/help/communities/enabling-leaderboard.md), el componente destacado de la función Tabla de posiciones, para la creación de páginas.
