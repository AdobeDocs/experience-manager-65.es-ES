---
title: Eventos OSGi para componentes de Communities
description: Se envían eventos OSGi que pueden almacenar en déclencheur a los oyentes asincrónicos
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 5%

---

# Eventos OSGi para componentes de Communities  {#osgi-events-for-communities-components}

## Información general {#overview}

Cuando los miembros interactúan con las funciones de Communities, se envían eventos OSGi que pueden almacenar en déclencheur a los oyentes asincrónicos, como notificaciones o interacción (puntuación e insignias).

El de un componente [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) registra los eventos como `actions` que se producen para una `topic`. SocialEvent incluye un método para devolver un `verb` asociado con la acción. Hay un *n-1* relación entre `actions` y `verbs`.

Para los componentes de Communities incluidos en la versión, las siguientes tablas describen el `verbs` definido para cada `topic` disponible para su uso.

## Temas y verbos {#topics-and-verbs}

[Componente de calendario](calendar-basics-for-developers.md)
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea un evento de calendario |
| AÑADIR | Comentarios de los miembros sobre un evento de calendario |
| ACTUALIZAR | Se edita el evento o comentario del calendario del miembro |
| ELIMINAR | Se elimina el evento o comentario del calendario del miembro |

[Componente Comentarios](essentials-comments.md)
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea un comentario |
| AÑADIR | Respuestas de los miembros al comentario |
| ACTUALIZAR | El comentario del miembro se ha editado |
| ELIMINAR | Se ha eliminado el comentario del miembro |

[Componente Biblioteca de archivos](essentials-file-library.md)
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea una carpeta |
| ADJUNTAR | El miembro carga un archivo |
| ACTUALIZAR | El miembro actualiza una carpeta o un archivo |
| ELIMINAR | El miembro elimina una carpeta o archivo |

[Componente de foro](essentials-forum.md)
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea un tema de foro |
| AÑADIR | Respuestas de los miembros al tema del foro |
| ACTUALIZAR | Se edita el tema o la respuesta del foro del miembro |
| ELIMINAR | Se elimina el tema o la respuesta del foro del miembro |

[Componente de diario](blog-developer-basics.md)
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea un artículo de blog |
| AÑADIR | Comentarios de los miembros en un artículo de blog |
| ACTUALIZAR | Se edita el artículo o comentario del blog del miembro |
| ELIMINAR | Se elimina el artículo o comentario del blog del miembro |

[Componente de control de calidad](qna-essentials.md)
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea una pregunta de control de calidad |
| AÑADIR | El miembro crea una respuesta de control de calidad |
| ACTUALIZAR | Se ha editado la pregunta o respuesta de control de calidad del miembro |
| SELECT | La respuesta del miembro está seleccionada |
| DESELECCIONAR | Se ha anulado la selección de la respuesta del miembro |
| ELIMINAR | Se elimina la pregunta o respuesta de control de calidad del miembro |

[Componente de críticas](reviews-basics.md)
SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descripción** |
|---|---|
| POST | El miembro crea una revisión |
| ACTUALIZAR | Se ha editado la revisión del miembro |
| ELIMINAR | Se ha eliminado la revisión del miembro |

[Componente de clasificación](rating-basics.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descripción** |
|---|---|
| AÑADIR CLASIFICACIÓN | El contenido del miembro se ha clasificado como positivo |
| ELIMINAR CLASIFICACIÓN | El contenido del miembro ha perdido su valoración |

[Componente de votación](essentials-voting.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descripción** |
|---|---|
| AGREGAR VOTO | El contenido del miembro se ha votado arriba |
| ELIMINAR VOTO | El contenido del miembro se ha rechazado. |

**Componentes con moderación habilitada**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descripción** |
|---|---|
| DENEGAR | Se ha denegado el contenido del miembro |
| MARCAR COMO INAPROPIADO | El contenido del miembro está marcado |
| NO MARCAR COMO INAPROPIADO | El contenido del miembro no está marcado |
| ACEPTAR | El moderador aprueba el contenido del miembro |
| CERRAR | El miembro cierra el comentario a las ediciones y respuestas |
| ABRIR | El miembro vuelve a abrir el comentario |

## Eventos de componentes personalizados {#events-for-custom-components}

Para un componente personalizado, la variable [clase abstracta SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) se debe ampliar d para registrar los eventos del componente como `actions`que se producen para una `topic`.

El evento personalizado anularía el método `getVerb()` para que un adecuado `verb`se devuelve para cada `action`. El `verb` devuelto por una acción puede ser uno de uso común (como `POST`) o uno especializado para el componente (como `ADD RATING`). Hay un *n-1* relación entre `actions`y `verbs`.

>[!NOTE]
>
>Asegúrese de que una extensión personalizada esté registrada con una clasificación inferior a cualquier implementación existente en el producto.

### Pseudocódigo para evento de componente personalizado {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activity.streams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
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

## Ejemplo de EventListener para filtrar datos de flujo de actividad {#sample-eventlistener-to-filter-activity-stream-data}

Es posible escuchar eventos con el fin de modificar lo que aparece en el flujo de actividad.

El siguiente ejemplo de pseudocódigo quitará los eventos de DELETE del componente Comentarios del flujo de actividades.

### Pseudocódigo para EventListener {#pseudo-code-for-eventlistener}

Requiere [último paquete de funciones](deploy-communities.md#latestfeaturepack).

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
