---
title: Globale HTL-Objekte
description: Erfahren Sie mehr über aufzählbare Objekte, Java-gestützte Objekte und JavaScript-gestützte Objekte in HTL.
exl-id: ca590b92-f1b3-4e44-a04a-a2c10dff256f
source-git-commit: 88edbd2fd66de960460df5928a3b42846d32066b
workflow-type: ht
source-wordcount: '166'
ht-degree: 100%

---


# Globale HTL-Objekte {#htl-global-objects}

Ohne etwas spezifizieren zu müssen, bietet HTL Zugang zu vielen Objekten, die für Entwickelnde nützlich sind. Diese Objekte kommen zu denen hinzu, die über die [Anwendungs-API](java-use-api.md) eingeführt werden können.

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

Jedes der folgenden Objekte wird durch das entsprechende Java-Objekt unterstützt.

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
