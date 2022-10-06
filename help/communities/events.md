---
title: Eventos OSGi para componentes de Communities
seo-title: OSGi Events for Communities Components
description: Se envían eventos OSGi que pueden almacenar en déclencheur a oyentes asincrónicos
seo-description: OSGi events are sent that can trigger asynchronous listeners
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 4%

---

# Eventos OSGi para componentes de Communities  {#osgi-events-for-communities-components}

## Información general {#overview}

Cuando los miembros interactúan con las funciones de Communities, se envían eventos OSGi que pueden almacenar en déclencheur a oyentes asincrónicos, como notificaciones o gamificación (puntuación y distintivo).

Los componentes [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) instance registra los eventos como `actions` que se producen para un `topic`. SocialEvent incluye un método para devolver un `verb` asociado a la acción . Hay un *n-1* relación entre `actions` y `verbs`.

Para los componentes Communities entregados en la versión, las tablas siguientes describen la variable `verbs` definido para cada `topic` disponible para su uso.

## Temas y verbos {#topics-and-verbs}

[Componente de calendario](calendar-basics-for-developers.md)
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descripción** |
|---|---|
| POST | Un miembro crea un evento de calendario |
| AÑADIR | Comentarios de los miembros en un evento de calendario |
| ACTUALIZAR | Se edita el evento o comentario de calendario del miembro |
| ELIMINAR | Se elimina el evento o comentario del calendario del miembro |

[Componente Comentarios](essentials-comments.md)
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descripción** |
|---|---|
| POST | Un miembro crea un comentario |
| AÑADIR | Respuestas de los miembros a las observaciones |
| ACTUALIZAR | Se edita el comentario del miembro |
| ELIMINAR | Se suprime el comentario del miembro |

[Componente Biblioteca de archivos](essentials-file-library.md)
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descripción** |
|---|---|
| POST | Un miembro crea una carpeta |
| ADJUNTAR | Los miembros cargan un archivo |
| ACTUALIZAR | El miembro actualiza una carpeta o un archivo |
| ELIMINAR | El miembro elimina una carpeta o un archivo |

[Componente Foro](essentials-forum.md)
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea un tema de foro |
| AÑADIR | Respuestas de los miembros al tema del foro |
| ACTUALIZAR | Se edita el tema o la respuesta del foro del miembro |
| ELIMINAR | Se elimina el tema o la respuesta del foro del miembro |

[Componente Asiento](blog-developer-basics.md)
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descripción** |
|---|---|
| POST | Un miembro crea un artículo de blog |
| AÑADIR | Comentarios de miembros en un artículo de blog |
| ACTUALIZAR | Se edita el artículo o comentario del blog del miembro |
| ELIMINAR | Se elimina el artículo o comentario del blog de un miembro |

[Componente QnA](qna-essentials.md)
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descripción** |
|---|---|
| POST | Miembro crea una pregunta de QnA |
| AÑADIR | Un miembro crea una respuesta de control de calidad |
| ACTUALIZAR | Se edita la pregunta o respuesta de control de calidad de un miembro |
| SELECT | Se selecciona la respuesta del miembro |
| UNSELECT | Se anula la selección de la respuesta del miembro |
| ELIMINAR | Se suprime la pregunta o respuesta de QnA del Miembro |

[Componente de revisiones](reviews-basics.md)
SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea una revisión |
| ACTUALIZAR | Se edita la revisión del miembro |
| ELIMINAR | Se suprime la revisión de un miembro |

[Componente de clasificación](rating-basics.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descripción** |
|---|---|
| AGREGAR CLASIFICACIÓN | El contenido de un miembro ha aumentado |
| QUITAR CLASIFICACIÓN | El contenido de un miembro ha sido clasificado como inferior |

[Componente de votación](essentials-voting.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descripción** |
|---|---|
| AGREGAR VOTACIÓN | El contenido de los miembros ha sido votado |
| ELIMINAR VOTACIÓN | El contenido de los miembros ha sido rechazado |

**Componentes habilitados para moderación**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descripción** |
|---|---|
| DENEGAR | Se deniega el contenido del miembro |
| INDICADOR INAPROPIADO | El contenido del miembro está marcado |
| LAG-AS-INAPROPIADO | El contenido del miembro no está marcado |
| ACEPTAR | El contenido del miembro es aprobado por el moderador |
| CERRAR | El miembro cierra los comentarios a las ediciones y respuestas |
| ABRIR | El miembro vuelve a abrir el comentario |

## Eventos para componentes personalizados {#events-for-custom-components}

Para un componente personalizado, la variable [Clase abstracta SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) se debe ampliar d para registrar los eventos del componente como `actions`que se producen para un `topic`.

El evento personalizado anularía el método `getVerb()` para que `verb`se devuelve para cada `action`. La variable `verb` devuelta para una acción puede ser de uso común (por ejemplo, `POST`) o uno especializado para el componente (por ejemplo, `ADD RATING`). Hay un *n-1* relación entre `actions`y `verbs`.

>[!NOTE]
>
>Asegúrese de que una extensión personalizada esté registrada con una clasificación inferior a cualquier implementación existente en el producto.

### Pseudocódigo para el evento de componente personalizado {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## Ejemplo de EventListener para filtrar los datos del flujo de actividad {#sample-eventlistener-to-filter-activity-stream-data}

Es posible escuchar eventos para modificar lo que aparece en el flujo de actividad.

El siguiente ejemplo de pseudocódigo eliminará los eventos de DELETE para el componente Comentarios del flujo de actividad.

### Pseudocódigo para EventListener {#pseudo-code-for-eventlistener}

Requiere [último feature pack](deploy-communities.md#latestfeaturepack).

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```
