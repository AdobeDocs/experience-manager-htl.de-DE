---
title: AEM-Erweiterungen
description: AEM bietet Erweiterungen der HTL-Spezifikation, die Sie als Entwickler AEM können.
exl-id: d78cb84d-f958-45e2-9c6c-df86a68277d5
source-git-commit: ebeac25c38b81c92011c163c7860688f43547a7d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 64%

---

# AEM-Erweiterungen {#aem-extensions}

Ähnlich wie die [Apache Sling-Erweiterungen der HTL-Spezifikation](https://sling.apache.org/documentation/bundles/scripting/scripting-htl.html#extensions-of-the-htl-specification-1) bietet AEM einige zusätzliche Ausdrucksoptionen, die die Arbeit mit AEM-Konzepten direkt in den HTL-Skripten etwas erleichtern.

## i18n {#i18n}

Die gleichen [drei zusätzlichen Optionen](https://sling.apache.org/documentation/bundles/scripting/scripting-htl.html#i18n) wie in Apache Sling können zusammen mit `i18n` verwendet werden:

* `locale`
* `hint`
* `basename`

In AEM wird die [Internationalisierungsunterstützung](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/developing/components/internationalization/i18n-dev) für HTL jedoch mit Hilfe der API aus dem `com.day.cq.i18n`-Paket implementiert.

## `data-sly-include` {#data-sly-include}

In AEM kann `data-sly-include` eine zusätzliche Option `wcmmode` annehmen, die den [WCM-Modus](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/WCMMode.html) für das enthaltene Skript steuert. Die zulässigen Werte sind die Namen der verfügbaren Aufzählungskonstanten.

## `data-sly-resource` {#data-sly-resource}

Zusätzlich zu Pfaden und `Resources` kann das `data-sly-resource`-Blockelement auch mit [`Maps`](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Map.html) oder [`Records` arbeiten.](https://github.com/apache/sling-org-apache-sling-scripting-sightly-runtime/blob/master/src/main/java/org/apache/sling/scripting/sightly/Record.java) Bei beiden Ansätzen muss die Eigenschaft von `resourceName` als Zeichenfolge angegeben werden. Der Wert wird verwendet, um eine [Synthetische Ressource](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/org/apache/sling/api/resource/SyntheticResource.html) zu erstellen, die im Rendering-Kontext enthalten ist. Die übrigen Eigenschaften der `Record` oder der `Map`, die an `data-sly-resource` übergeben werden, werden als normale `Resource`-Eigenschaften verwendet. Wenn die Eigenschaft `sling:resourceType` in dieser Zuordnung fehlt, wird davon ausgegangen, dass der Ressourcentyp entweder der Wert der Ausdrucksoption `resourceType` [3} oder der Ressourcentyp der aktuellen Ressource ist, die das Rendering auslöst.](https://github.com/adobe/htl-spec/blob/1.4/SPECIFICATION.md#229-resource)

Unter Berücksichtigung der folgenden Zuordnungs-/Datensatz-Eigenschaften, die im Skriptbereich als `map` verfügbar sind:

```javascript
{
    resourceName: "myText",
    "sling:resourceType": "core/wcm/components/text/v2/text",
    "text": "Hello World!"
}
```

Und bei der folgenden Aufschlüsselung:

```html
<div class="outer" data-sly-resource="${map}"></div>
```

Folgende Ausgabe wird erwartet:

```html
<div class="outer">
    <div class="myText">
        <div data-cmp-data-layer="{&quot;text-e58d65c472&quot;:{&quot;@type&quot;:&quot;core/wcm/components/text/v2/text&quot;,&quot;xdm:text&quot;:&quot;<p>Hello world!</p>&quot;}}" id="text-e58d65c472" class="cmp-text">
            <p>Hello world!</p>
        </div>
  </div>
</div>
```
