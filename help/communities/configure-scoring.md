---
title: Elementos esenciales de puntuación e insignias
description: Obtenga información sobre cómo la función de puntuación e insignias de las comunidades de Adobe Experience Manager identifica y premia a los miembros de la comunidad.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Elementos esenciales de puntuación e insignias {#scoring-and-badges-essentials}

La función de puntuación e insignias de AEM Communities identifica y recompensa a los miembros de la comunidad.

Los detalles de configuración de la función se describen en

* [Puntuación y distintivos de comunidades](/help/communities/implementing-scoring.md)

Esta página contiene detalles técnicos adicionales:

* Cómo [mostrar una insignia](#displaying-badges) como imagen o texto
* Activar el registro de depuración [extenso](#debug-log-for-scoring-and-badging)
* Cómo [acceder a UGC](#ugc-for-scoring-and-badging) en relación con la puntuación y el distintivo

>[!CAUTION]
>
>La estructura de implementación visible en CRXDE Lite está sujeta a cambios.

## Visualización de distintivos {#displaying-badges}

Si un distintivo se muestra como texto o imagen se controla en el lado del cliente en la plantilla HBS.

Por ejemplo, busque `this.isAssigned` en `/libs/social/forum/components/hbs/topic/list-item.hbs`:

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

Si el valor es True, `isAssigned` indica que el distintivo se asignó a un rol y el distintivo debe mostrarse como texto.

Si es falso, `isAssigned` indica que el distintivo se otorgó por una puntuación ganada y el distintivo debe mostrarse como una imagen.

Cualquier cambio en este comportamiento debe realizarse en un script personalizado (anulación o superposición). Consulte [Personalización del lado del cliente](/help/communities/client-customize.md).

## Registro de depuración para puntuación e identificación {#debug-log-for-scoring-and-badging}

Para depurar la puntuación y el distintivo, se puede configurar un archivo de registro personalizado. El contenido de este archivo de registro se puede proporcionar al servicio de atención al cliente si se producen problemas con la función.

Para obtener instrucciones detalladas, visite [Crear un archivo de registro personalizado](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

Para configurar rápidamente un archivo slinglog:

1. Obtenga acceso a la **compatibilidad con registros de la consola web de Adobe Experience Manager**, por ejemplo

   * https://localhost:4502/system/console/slinglog

1. Seleccionar **Agregar nuevo registrador**

   1. Seleccionar `DEBUG` para **Nivel de registro**

   1. Escriba un nombre para **Archivo de registro**, por ejemplo

      * logs/scoring-debug.log

   1. Escriba dos entradas de **Logger** (clase) (usando el icono `+`)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`

   1. Seleccionar **Guardar**

![registro de puntuación de depuración](assets/debug-scoring-log.png)

Para ver las entradas de registro:

* Desde la consola web

   * En el menú **Estado**
   * Seleccionar **archivos de registro**
   * Busque el nombre de su archivo de registro, como `scoring-debug`

* En el disco local del servidor

   * El archivo de registro se encuentra en &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * Por ejemplo, `.../crx-quickstart/logs/scoring-debug.log`

![registro de puntuación](assets/scoring-log.png)

## UGC para puntuación e identificación {#ugc-for-scoring-and-badging}

Es posible ver el UGC relacionado con la puntuación y el distintivo cuando el SRP elegido es JSRP o MSRP, pero no ASRP. (Si no está familiarizado con estos términos, consulte [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md) y [Información general sobre el proveedor de recursos de almacenamiento](/help/communities/srp.md)).

Las descripciones para acceder a los datos de puntuación e insignias utilizan JSRP, ya que se puede acceder fácilmente al UGC con [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP en Author**: la experimentación en el entorno de Author genera un UGC que solo es visible desde el entorno de Author.

**JSRP en la publicación**: de manera similar, si realiza pruebas en el entorno de publicación, es necesario tener acceso a un CRXDE Lite con privilegios administrativos en una instancia de publicación. Si la instancia de publicación se está ejecutando en [modo de producción](/help/sites-administering/production-ready.md) (modo de ejecución nosamplecontent), es necesario [habilitar el CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

La ubicación base de UGC en JSRP es `/content/usergenerated/asi/jcr/`.

### API de puntuación e identificación {#scoring-and-badging-apis}

Las siguientes API están disponibles para su uso:

* [com.adobe.cq.social.scoring.api en 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es)
* [com.adobe.cq.social.badging.api en 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es)

Los últimos Javadocs para el paquete de funciones instalado están disponibles para los desarrolladores desde el repositorio de Adobe. Ver [Uso de Maven para comunidades: Javadocs](/help/communities/maven.md#javadocs).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

### Configuración de ejemplo {#example-setup}

AEM Las capturas de pantalla de los datos del repositorio proceden de la configuración de la puntuación y el distintivo para un foro en dos sitios de diferentes:

1. AEM Un sitio de la comunidad *con* tiene un identificador único (sitio de la comunidad creado mediante el asistente):

   * Uso del sitio Tutorial de introducción (interacción) creado durante el [tutorial de introducción](/help/communities/getting-started.md)
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

   * Para mostrar insignias, agregue la propiedad

     `allowBadges = true`

   * Un usuario inicia sesión, crea un tema de foro y se le otorga una insignia de bronce

1. AEM Un sitio *sin* tiene un ID único:

   * Usando la [guía de componentes de la comunidad](/help/communities/components-guide.md)
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

   * Para mostrar insignias, agregue la propiedad

     `allowBadges = true`

   * Un usuario inicia sesión, crea un tema de foro y se le otorga una insignia de bronce

1. A un usuario se le asigna un distintivo de moderador mediante cURL :

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   Como un usuario ha obtenido dos insignias de bronce y se le ha otorgado una insignia de moderador, el usuario aparece con su entrada en el foro de la siguiente manera:

   ![moderador](assets/moderator.png)

>[!NOTE]
>
>Este ejemplo no sigue estas prácticas recomendadas:
>
>* Los nombres de las reglas de puntuación deben ser únicos a nivel global; no deben terminar con el mismo nombre.
>
>  Un ejemplo de lo que *no* debe hacer:
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* AEM Creación de imágenes de insignias únicas para diferentes sitios de

### UGC de puntuación de acceso {#access-scoring-ugc}

Se prefiere el uso de [API](#scoring-and-badging-apis).

Para fines de investigación, con JSRP como ejemplo, la carpeta base que contiene puntuaciones es

* `/content/usergenerated/asi/jcr/scoring`

El nodo secundario de `scoring` es el nombre de la regla de puntuación. Por lo tanto, una práctica recomendada es que los nombres de reglas de puntuación en un servidor sean únicos a nivel global.

Para el sitio de Geometrixx Engage, el usuario y su puntuación se encuentran en una ruta construida con el nombre de la regla de puntuación, el ID del sitio de la comunidad ( `engage-ba81p`), un ID único y el ID del usuario:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Para el sitio de guía de componentes de la comunidad, el usuario y su puntuación se encuentran en una ruta construida con el nombre de la regla de puntuación, un identificador predeterminado ( `default-site`), un identificador único y el identificador del usuario:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

La puntuación se almacena en la propiedad `scoreValue_tl`, que solo puede contener un valor o hacer referencia indirectamente a atomicCounter.

![access-scoring-ugc](assets/access-scoring-ugc.png)

### UGC de insignias de acceso {#access-badging-ugc}

Se prefiere el uso de [API](#scoring-and-badging-apis).

Para fines de investigación, utilizando JSRP para el ejemplo, la carpeta base que contiene información sobre insignias asignadas o concedidas es

* `/content/usergenerated/asi/jcr`

Seguido de la ruta al perfil del usuario, que termina en una carpeta de distintivos, como:

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Insignia otorgada {#awarded-badge}

![granted-badging-ugc](assets/access-badging-ugc.png)

#### Insignia asignada {#assigned-badge}

![insignia asignada](assets/assigned-badge.png)

## Información adicional {#additional-information}

Para mostrar una lista ordenada de miembros basada en puntos:

* [Función de tabla de clasificación](/help/communities/functions.md#leaderboard-function) para su inclusión en un sitio de comunidad o plantilla de grupo.
* [Componente de tabla de posiciones](/help/communities/enabling-leaderboard.md), el componente destacado de la función de tabla de posiciones, para la creación de páginas.
