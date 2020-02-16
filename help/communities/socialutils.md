---
title: Refactorización de SocialUtils
seo-title: Refactorización de SocialUtils
description: El paquete com.adobe.cq.social.ugcbase.SocialUtils se dejó de utilizar en AEM 6.1
seo-description: El paquete com.adobe.cq.social.ugcbase.SocialUtils se dejó de utilizar en AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Refactorización de SocialUtils {#socialutils-refactoring}

## Paquete SocialUtils obsoleto {#socialutils-package-deprecated}

El paquete **com.adobe.cq.social.ugcbase.SocialUtils** quedó obsoleto en AEM 6.1.

En las tablas siguientes se enumeran los métodos que se deben utilizar en lugar de los métodos de SocialUtils.

## Paquete SocialResourceUtilities {#socialresourceutilities-package}

| Métodos de com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| Boolean checkPermission(resolución de ResourceResolver, ruta de acceso de cadena, acción de cadena) |  |
| SocialResourceProvider getSocialResourceProvider(recurso de recurso) |  |
| SocialResourceConfiguration getStorageConfig(recurso de recurso) |  |
| Resource getUGCResource(Resource userResource) |  |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rf) | nuevo |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rf, String resourceTypeHint) | nuevo |
| Resource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| boolean hasModeratePermissions(recurso de recurso) |  |
| String resourceToACLPath(recurso de recurso) |  |
| String resourceToUGCStoragePath(recurso de recurso) | reemplaza a String resourceToUGCPath(Resource resource) |
| String UGCToResourcePath(recurso de recurso) |  |
| String UGCToResourcePath(String ugcPath) | firma de método cambiada |
| String UGCToResourcePath(String ugcPath, resolver ResourceResolver) | nuevo |

| Métodos en `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(recurso de recurso) | reemplaza a SocialResourceProvider getConfiguradoProvider(recurso de recurso) |

## Paquete SCFUtilities {#scfutilities-package}

| Métodos en `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String AbsolutDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String AbsolutDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Page getContainerPage(Recurso) |
| String getSocialProfileURL(Nombre de usuario de la cadena, resolución de ResourceResolver, página) |
| UserProperties getUserProperties(resolución de ResourceResolver, cadena userId) |

## For Internal Use Only {#for-internal-use-only}

| boolean canAddNode(Session session, String path) |
|---|
| String createUniqueNameHint(mensaje de cadena) |
| String createUniqueNameHint(Mensaje de cadena, int numRandomChars) |
| String generateRandomString(longitud int) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(Ruta de cadena, resolver ResourceResolver) |
| String getPagePath(recurso de recurso) |
| String getPagePath(Ruta de cadena) |
| String getResourceTypeForIncludedResource(Componente de recurso, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Recurso de recurso, String styleProperty, String defaultValue) |
| booleano isResourceOwner(recurso de recurso) |
| String mapUGCPath(Resource resource) |
| String mapUGCPath(String ugcPath, ResourceResolver resolver) |
| boolean mayPost(ResourceResolver, recurso) |
| String prepareUserGeneratedContent(resolución de ResourceResolver, ruta de acceso de cadena) |

## Métodos que ya no están disponibles {#methods-no-longer-available}

| Node createNode(Resolver de ResourceResolver, ruta de acceso de cadena, String nodeType) |
|---|
| Resource getResourceAtPath(ResourceResolver, resolución de cadena) |
| Resource getResourceAtPath(ResourceResolver, ruta de acceso de cadena, String resourceType) |
| Configuración getStorageCloudServiceConfig(recurso de recurso) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| boolean mayAccessUGC(ResourceResolver, resolución) |

