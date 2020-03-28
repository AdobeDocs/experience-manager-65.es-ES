---
title: Eventos OSGi para componentes de comunidades
seo-title: Eventos OSGi para componentes de comunidades
description: Se envían eventos OSGi que pueden activar oyentes asincrónicos
seo-description: Se envían eventos OSGi que pueden activar oyentes asincrónicos
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Eventos OSGi para componentes de comunidades {#osgi-events-for-communities-components}

## Información general {#overview}

Cuando los miembros interactúan con las funciones de Communities, se envían eventos OSGi que pueden activar oyentes asincrónicos, como notificaciones o gamificación (puntuación y distintivo).

La instancia [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) de un componente registra los eventos `actions` que se producen para un `topic`. SocialEvent incluye un método para devolver un `verb` asociado a la acción. Hay una relación *n-1* entre `actions` y `verbs`.

Para los componentes Communities entregados en la versión, en las tablas siguientes se describe la `verbs` definición de cada uno de los componentes disponibles para `topic` su uso.

## Temas y verbos {#topics-and-verbs}

[Calendario Componente](calendar-basics-for-developers.md)SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un evento de calendario |
| AÑADIR | comentarios de miembros en un evento de calendario |
| ACTUALIZAR | se edita el evento o comentario del calendario del miembro |
| ELIMINAR | se elimina el evento o comentario del calendario del miembro |

[Componente](essentials-comments.md)ComentariosSocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un comentario |
| AÑADIR | respuestas de los miembros al comentario |
| ACTUALIZAR | se edita el comentario del miembro |
| ELIMINAR | se elimina el comentario del miembro |

[Componente](essentials-file-library.md)Biblioteca de archivosSocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea una carpeta |
| ATTACH | miembro carga un archivo |
| ACTUALIZAR | Un miembro actualiza una carpeta o un archivo |
| ELIMINAR | elimina una carpeta o un archivo |

[Foro Componente](essentials-forum.md)SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un tema del foro |
| AÑADIR | respuestas de los miembros al tema del foro |
| ACTUALIZAR | se edita el tema o la respuesta del foro del miembro |
| ELIMINAR | se elimina el tema o la respuesta del foro del miembro |

[Componente](blog-developer-basics.md)HistorialSocialEvent `topic`= com/adobe/cq/social/historial

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea un artículo de blog |
| AÑADIR | comentarios de miembros en un artículo de blog |
| ACTUALIZAR | se edita el artículo o comentario del blog del miembro |
| ELIMINAR | se elimina el artículo o comentario del blog del miembro |

[QnA Component](qna-essentials.md)SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea una pregunta QnA |
| AÑADIR | miembro crea una respuesta de QnA |
| ACTUALIZAR | se edita la pregunta o la respuesta de control de calidad del miembro |
| SELECCIONAR | la respuesta del miembro está seleccionada |
| DESSELECCIONAR | se anula la selección de la respuesta del miembro |
| ELIMINAR | se elimina la pregunta o la respuesta de control de calidad del miembro |

[Reseñas del componente](reviews-basics.md)SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descripción** |
|---|---|
| POST | miembro crea revisión |
| ACTUALIZAR | se edita la revisión del miembro |
| ELIMINAR | se elimina la revisión del miembro |

[Componente](rating-basics.md)de clasificación SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descripción** |
|---|---|
| AÑADIR CLASIFICACIÓN | el contenido del miembro se ha valorado |
| QUITAR CLASIFICACIÓN | el contenido del miembro se ha reducido |

[Componente](essentials-voting.md)de votaciónSocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descripción** |
|---|---|
| AÑADIR VOTACIÓN | el contenido de los miembros ha sido votado |
| ELIMINAR VOTACIÓN | el contenido de los miembros ha sido rechazado |

**Componentes** habilitados para moderaciónSocialEvent `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descripción** |
|---|---|
| DENEGAR | se deniega el contenido del miembro |
| INDICADOR COMO INAPROPIADO | se marca el contenido del miembro |
| DESALOG-AS-INAPROPIADO | el contenido del miembro no está marcado |
| ACEPTAR | el moderador aprueba el contenido del miembro |
| CERRAR | el miembro cierra los comentarios a las ediciones y las respuestas |
| ABRIR | miembro vuelve a abrir el comentario |

## Eventos para componentes personalizados {#events-for-custom-components}

Para un componente personalizado, la clase [abstracta](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) SocialEvent debe ampliarse para registrar los eventos del componente `actions`que se producen para un `topic`.

El evento personalizado anularía el método `getVerb()` para que `verb`se devuelva un valor apropiado para cada `action`. El `verb` resultado de una acción puede ser uno de uso común (como `POST`) o uno especializado para el componente (como `ADD RATING`). Hay una relación *n-1* entre `actions`y `verbs`.

>[!NOTE]
>
>Asegúrese de que una extensión personalizada esté registrada con una clasificación inferior a cualquier implementación existente en el producto.

### Pseudocódigo para el Evento de componentes personalizados {#pseudo-code-for-custom-component-event}

[org.osgi.service.evento.Evento](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.social.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystream.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystream.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

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

## Ejemplo de EventListener para filtrar datos de flujo de Actividad {#sample-eventlistener-to-filter-activity-stream-data}

Es posible escuchar eventos para modificar lo que aparece en el flujo de actividad.

El siguiente ejemplo de pseudocódigo eliminará los eventos ELIMINAR para el componente Comentarios del flujo de actividad.

### Pseudocódigo para EventListener {#pseudo-code-for-eventlistener}

Requiere el paquete [de funciones](deploy-communities.md#latestfeaturepack)más reciente.

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

