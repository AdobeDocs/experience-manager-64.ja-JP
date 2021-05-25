---
title: SocialUtils のリファクタリング
seo-title: SocialUtils のリファクタリング
description: パッケージ com.adobe.cq.social.ugcbase.SocialUtils は AEM 6.1 で廃止されました
seo-description: パッケージ com.adobe.cq.social.ugcbase.SocialUtils は AEM 6.1 で廃止されました
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
exl-id: ba23188b-a72a-4349-b3e5-0fb50fd6312f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 94%

---

# SocialUtils のリファクタリング {#socialutils-refactoring}

## SocialUtils パッケージの廃止 {#socialutils-package-deprecated}

パッケージ&#x200B;**com.adobe.cq.social.ugcbase.SocialUtils**&#x200B;はAEM 6.1で非推奨（廃止予定）となりました。

以下の各表は、SocialUtils のメソッドの代わりに使用するメソッドのリストです。

## SocialResourceUtilities パッケージ   {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities のメソッド |
|---|
| Boolean checkPermission(ResourceResolver resolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider(Resource resource) |  |
| SocialResourceConfiguration getStorageConfig(Resource resource) |  |
| Resource getUGCResource(Resource userResource) |  |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rrf) | 新規 |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rrf, String resourceTypeHint) | 新規 |
| Resource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| boolean hasModeratePermissions(Resource resource) |  |
| String resourceToACLPath(Resource resource) |  |
| String resourceToUGCStoragePath(Resource resource) | String resourceToUGCPath(Resource resource) に代わるメソッド |
| String UGCToResourcePath(Resource resource) |  |
| String UGCToResourcePath(String ugcPath) | メソッドの署名を変更 |
| String UGCToResourcePath(String ugcPath, ResourceResolver resolver) | 新規 |

| `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilitiesのメソッド |
|---|
| SocialResourceProvider getSocialResourceProvider(Resource resource) | SocialResourceProvider getConfiguredProvider(Resource resource)を置き換えます。 |

## SCFUtilities パッケージ {#scfutilities-package}

| `com.adobe.cq.social.`utilities.scf.api.SCFUtilitesのメソッド |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Page getContainingPage(Resource resource) |
| String getSocialProfileURL(String username, ResourceResolver resolver, Page page) |
| UserProperties getUserProperties(ResourceResolver resolver, String userId) |

## 内部でのみ使用  {#for-internal-use-only}

| boolean canAddNode(Session session, String path) |
|---|
| String createUniqueNameHint(String message) |
| String createUniqueNameHint(String message, int numRandomChars) |
| String generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(String path, ResourceResolver resolver) |
| String getPagePath(Resource resource) |
| String getPagePath(String path) |
| String getResourceTypeForIncludedResource(Resource component, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource resource, String styleProperty, String defaultValue) |
| boolean isResourceOwner(Resource resource) |
| String mapUGCPath(Resource resource) |
| String mapUGCPath(String ugcPath, ResourceResolver resolver) |
| boolean mayPost(ResourceResolver resolver, Resource resource) |
| String prepareUserGeneratedContent(ResourceResolver resolver, String path) |

## 使用できなくなったメソッド  {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, String path, String nodeType) |
|---|
| Resource getResourceAtPath(ResourceResolver resolver, String path) |
| Resource getResourceAtPath(ResourceResolver resolver, String path, String resourceType) |
| Configuration getStorageCloudServiceConfig(Resource resource) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| boolean mayAccessUGC(ResourceResolver resolver) |
