---
title: Globale HTL-Objekte
description: Erfahren Sie mehr über aufzählbare Objekte und Java-unterstützte Objekte in HTL.
exl-id: ca590b92-f1b3-4e44-a04a-a2c10dff256f
index: false
source-git-commit: a496d23277902a5cd573a6a8af770f27b0269f05
workflow-type: ht
source-wordcount: '203'
ht-degree: 100%

---


# Globale HTL-Objekte {#htl-global-objects}

Ohne etwas spezifizieren zu müssen, bietet HTL Zugang zu vielen Objekten, die für Entwickelnde nützlich sind. Diese Objekte sind zusätzlich zu denen vorhanden, die möglicherweise über die [Anwendungs-API](java-use-api.md) eingeführt werden.

>[!NOTE]
>
>Für Entwickelnde, die mit der JSP-Entwicklung in AEM vertraut sind, bietet HTL Zugriff auf alle Objekte, die in JSP üblicherweise verfügbar sind, einschließlich `global.jsp`.

## Aufzählungsobjekte {#enumerable-objects}

Diese Objekte bieten praktischen Zugriff auf häufig verwendete Informationen. Auf ihren Inhalt kann mit der Punktnotation zugegriffen werden, und sie können mit `data-sly-list` oder `data-sly-repeat` durchlaufen werden.

| Variablenname | Beschreibung | Unterstützt durch |
|--- |--- |--- |
| `properties` | Liste der Eigenschaften der aktuellen Ressource | [`org.apache.sling.api.resource.ValueMap`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html) |
| `pageProperties` | Liste der Seiteneigenschaften der aktuellen Seite | [`org.apache.sling.api.resource.ValueMap`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html) |
| `inheritedPageProperties` | Liste der geerbten Seiteneigenschaften der aktuellen Seite | [`org.apache.sling.api.resource.ValueMap`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html) |

## Java-unterstützte Objekte {#java-backed-objects}

Das entsprechende Java-Objekt sichert jedes der folgenden Objekte.

| Variablenname | Beschreibung |
|---|---|
| `component` | `com.day.cq.wcm.api.components.Component` |
| `componentContext` | `com.day.cq.wcm.api.components.ComponentContext` |
| `currentContentPolicy` | `com.day.cq.wcm.api.policies.ContentPolicy` |
| `currentContentPolicyProperties` | `com.day.cq.wcm.api.policies.ContentPolicy` |
| `currentDesign` | `com.day.cq.wcm.api.designer.Design` |
| `currentNode` | `javax.jcr.Node` |
| `currentPage` | `com.day.cq.wcm.api.Page` |
| `currentSession` | `javax.servlet.http.HttpSession` |
| `currentStyle` | `com.day.cq.wcm.api.designer.Style` |
| `designer` | `com.day.cq.wcm.api.designer.Designer` |
| `editContext` | `com.day.cq.wcm.api.components.EditContext` |
| `log` | `org.slf4j.Logger` |
| `out` | `java.io.PrintWriter` |
| `pageManager` | `com.day.cq.wcm.api.PageManager` |
| `reader` | `java.io.BufferedReader` |
| `request` | `org.apache.sling.api.SlingHttpServletRequest` |
| `resolver` | `org.apache.sling.api.resource.ResourceResolver` |
| `resource` | `org.apache.sling.api.resource.Resource` |
| `resourceDesign` | `com.day.cq.wcm.api.designer.Design` |
| `resourcePage` | `com.day.cq.wcm.api.Page` |
| `response` | `org.apache.sling.api.SlingHttpServletResponse` |
| `sling` | `org.apache.sling.api.scripting.SlingScriptHelper` |
| `slyWcmHelper` | `com.adobe.cq.sightly.WCMScriptHelper` |
| `wcmmode` | `com.adobe.cq.sightly.SightlyWCMMode` |
| `xssAPI` | `com.adobe.granite.xss.XSSAPI` |

## JavaScript-unterstützte Objekte {#javascript-backed-objects}

Es ist möglich, die HTL-Logik mit JavaScript zu unterstützen. Die bevorzugte oder empfohlene Methode ist jedoch die Verwendung von [Sling-Modellen](https://sling.apache.org/documentation/bundles/models.html).

>[!NOTE]
>
>[Das JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) gilt nun als veraltet für die Verwendung mit AEM as a Cloud Service. Verwenden Sie stattdessen [das Java Use API](https://experienceleague.adobe.com/de/docs/experience-manager-htl/content/java-use-api).
>
>Weitere Informationen zu veralteten und entfernten Funktionen finden Sie in den [Versionshinweisen zu AEM as a Cloud Service](https://experienceleague.adobe.com/de/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features).
