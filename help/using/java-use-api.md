---
title: HTL-Java-Anwendungs-API
description: Die HTL-Java-Anwendungs-API ermöglicht einer HTL-Datei den Zugriff auf Hilfsmethoden in einer benutzerdefinierten Java-Klasse.
exl-id: 9a9a2bf8-d178-4460-a3ec-cbefcfc09959
source-git-commit: 5e1dce693dc61300530837c996f45d793c0b07e6
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 80%

---


# HTL-Java-Anwendungs-API {#htl-java-use-api}

Die HTL-Java-Anwendungs-API ermöglicht einer HTL-Datei den Zugriff auf Hilfsmethoden in einer benutzerdefinierten Java-Klasse.

## Nutzungsszenario {#use-case}

Die HTL-Java-Anwendungs-API ermöglicht einer HTL-Datei den Zugriff auf Hilfsmethoden in einer benutzerdefinierten Java-Klasse über `data-sly-use`. Diese Methode ermöglicht die Einkapselung aller komplexen Geschäftslogik im Java-Code, während der HTL-Code nur die direkte Markup-Produktion behandelt.

Ein Java-Anwendungs-API-Objekt kann ein einfacher POJO sein, der von einer bestimmten Implementierung über den Standardkonstruktor von POJO instanziiert wird.

Die Anwendungs-API-POJOs können auch eine öffentliche Methode namens init mit der folgenden Signatur bereitstellen:

```java
    /**
     * Initializes the Use bean.
     *
     * @param bindings All bindings available to the HTL scripts.
     **/
    public void init(javax.script.Bindings bindings);
```

Die `bindings`-Zuordnung kann Objekte enthalten, die dem derzeit ausgeführten HTL-Skript, das vom Anwendungs-API-Objekt für die Verarbeitung verwendet werden kann, Kontext bieten.

## Ein einfaches Beispiel {#a-simple-example}

Dieses Beispiel veranschaulicht die Verwendung der Anwendungs-API.

>[!NOTE]
>
>Dieses Beispiel ist vereinfacht, um nur seine Verwendung zu veranschaulichen. In einer Produktionsumgebung empfiehlt Adobe die Verwendung von [Sling-Modellen](https://sling.apache.org/documentation/bundles/models.html).

Starten Sie mit einer HTL-Komponente namens `info,`, die keine Anwendungsklasse hat. Sie besteht aus einer einzelnen Datei namens `/apps/my-example/components/info.html`

```xml
<div>
    <h1>${properties.title}</h1>
    <p>${properties.description}</p>
</div>
```

Fügen Sie Inhalte für diese Komponente hinzu, die bei `/content/my-example/` gerendert werden sollen:

```xml
{
    "sling:resourceType": "my-example/component/info",
    "title": "My Example",
    "description": "This Is Some Example Content."
}
```

Wenn auf diesen Inhalt zugegriffen wird, wird die HTL-Datei ausgeführt. Innerhalb des HTL-Codes wird das Kontextobjekt `properties` verwendet, um auf `title` und `description` der aktuellen Ressource zuzugreifen und sie anzuzeigen. Die Ausgabedatei `/content/my-example.html` lautet:

```html
<div>
    <h1>My Example</h1>
    <p>This Is Some Example Content.</p>
</div>
```

### Hinzufügen einer Anwendungsklasse {#adding-a-use-class}

Die Komponente `info` benötigt in ihrer gegebenen Form keine Anwendungsklasse, um ihre sehr einfache Funktion zu erfüllen. Es gibt jedoch Fälle, in denen Sie Dinge tun müssen, die in HTL nicht möglich sind, und daher eine Anwendungsklasse benötigen. Beachten Sie aber das Folgende:

>[!NOTE]
>
>Eine Anwendungsklasse sollte nur verwendet werden, wenn eine Aktion nicht allein in HTL ausgeführt werden kann.

Angenommen, Sie möchten, dass die Komponente `info` die Eigenschaften `title` und `description` der Ressource anzeigt, jedoch komplett in Kleinschreibung. Da HTL über keine Methode zur Zeichenfolgenkleinschreibung verfügt, können Sie eine Java-Anwendungsklasse hinzufügen und `/apps/my-example/component/info/info.html` wie folgt ändern:

```xml
<div data-sly-use.info="Info">
    <h1>${info.lowerCaseTitle}</h1>
    <p>${info.lowerCaseDescription}</p>
</div>
```

Außerdem wird `/apps/my-example/component/info/Info.java` erstellt.

```java
package apps.my_example.components.info;

import com.adobe.cq.sightly.WCMUsePojo;

public class Info extends WCMUsePojo {
    private String lowerCaseTitle;
    private String lowerCaseDescription;

    @Override
    public void activate() throws Exception {
        lowerCaseTitle = getProperties().get("title", "").toLowerCase();
        lowerCaseDescription = getProperties().get("description", "").toLowerCase();
    }

    public String getLowerCaseTitle() {
        return lowerCaseTitle;
    }

    public String getLowerCaseDescription() {
        return lowerCaseDescription;
    }
}
```

Weitere Einzelheiten finden Sie in den [Javadocs für `com.adobe.cq.sightly.WCMUsePojo`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html).

Sehen wir uns nun die verschiedenen Teile des Codes an.

### Lokale vs. Bundle-Java-Klasse {#local-vs-bundle-java-class}

Die Java-Anwendungsklasse kann auf zwei Arten installiert werden:

* **Lokal** – Bei einer lokalen Installation wird die Java-Quelldatei neben der HTL-Datei im gleichen Repository-Ordner abgelegt. Die Quelle wird bei Bedarf automatisch kompiliert. Es ist kein separater Kompilierungs- oder Paketierungsschritt erforderlich.
* **Bundle** – Bei einer Bundle-Installation muss die Java-Klasse innerhalb eines OSGi-Bundles kompiliert und bereitgestellt werden, wobei der Standard-Bereitstellungsmechanismus von AEM für Bundles verwendet wird (siehe Abschnitt [Bundled Java Class](#bundled-java-class)).

Um zu wissen, welche Methode Sie wann anwenden sollten, sollten Sie diese beiden Punkte beachten:

* Eine **lokale Java-Anwendungsklasse** wird empfohlen, wenn die Anwendungsklasse für die betroffene Komponente spezifisch ist.
* Eine **gebündelte Java-Anwendungsklasse** wird empfohlen, wenn der Java-Code einen Service implementiert, auf den über mehrere HTL-Komponenten zugegriffen wird.

In diesem Beispiel wird eine lokale Installation verwendet.

### Java-Paket ist der Repository-Pfad {#java-package-is-repository-path}

Bei Verwendung einer lokalen Installation muss der Paketname der Anwendungsklasse mit dem Speicherort des Repository-Ordners übereinstimmen. Unterstriche im Paketnamen ersetzen alle Bindestriche im Pfad.

In diesem Fall befindet sich `Info.java` unter `/apps/my-example/components/info`. Daher lautet das Paket `apps.my_example.components.info`:

```java
package apps.my_example.components.info;

import com.adobe.cq.sightly.WCMUsePojo;

public class Info extends WCMUsePojo {

   ...

}
```

>[!NOTE]
>
>Bei der Verwendung von Bindestrichen in den Namen von Repository-Elementen handelt es sich um eine empfohlene Praxis in der AEM-Entwicklung. Bindestriche sind jedoch in Java-Paketnamen ungültig. Daher müssen **alle Bindestriche im Repository-Pfad für den Paketnamen in Unterstriche umgewandelt werden**.

### Erweitern von `WCMUsePojo` {#extending-wcmusepojo}

Es gibt zwar eine Reihe von Möglichkeiten, eine Java-Klasse mit HTL zu integrieren, jedoch besteht die einfachste Möglichkeit darin, die Klasse `WCMUsePojo` zu erweitern. In diesem Beispiel `/apps/my-example/component/info/Info.java`:

```java
package apps.my_example.components.info;

import com.adobe.cq.sightly.WCMUsePojo;

public class Info extends WCMUsePojo

    ...
}
```

### Initialisierung der Klasse {#initializing-the-class}

Wenn die Anwendungsklasse von `WCMUsePojo` erweitert wird, erfolgt die Initialisierung durch Überschreibung der `activate`-Methode, in diesem Fall in `/apps/my-example/component/info/Info.java`

```java
...

public class Info extends WCMUsePojo {
    private String lowerCaseTitle;
    private String lowerCaseDescription;

    @Override
    public void activate() throws Exception {
        lowerCaseTitle = getProperties().get("title", "").toLowerCase();
        lowerCaseDescription = getProperties().get("description", "").toLowerCase();
    }

...

}
```

### Kontext {#context}

Die Methode [aktivieren](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html) wird für gewöhnlich verwendet, um anhand des aktuellen Kontexts (beispielsweise der aktuellen Anforderung und Ressource) die in Ihrem HTL-Code erforderlichen Werte vorab zu berechnen und zu speichern (in Nutzervariablen).

Die Klasse `WCMUsePojo` bietet Zugriff auf denselben Satz von Kontextobjekten, die in einer HTL-Datei verfügbar sind (siehe Dokument [Globale Objekte](global-objects.md)).

In einer Klasse, die `WCMUsePojo` erweitert, können Sie mithilfe ihrer Namen auf Kontextobjekte zugreifen:

[`<T> T get(String name, Class<T> type)`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html)

Alternativ können Sie direkt auf häufig verwendete Kontextobjekte zugreifen, indem Sie die passende Methode in dieser Tabelle verwenden.

| Objekt | Convenience-Methode |
|---|---|
| [`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html) | [`getPageManager()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getPageManager--) |
| [`Page`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html) | [`getCurrentPage()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getCurrentPage--) |
| [`Page`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html) | [`getResourcePage()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getResourcePage--) |
| [`ValueMap`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html) | [`getPageProperties()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getPageProperties--) |
| [`ValueMap`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html) | [`getProperties()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getProperties--) |
| [`Designer`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Designer.html) | [`getDesigner()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getDesigner--) |
| [`Design`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Design.html) | [`getCurrentDesign()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getCurrentDesign--) |
| [`Style`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Style.html) | [`getCurrentStyle()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getCurrentStyle--) |
| [`Component`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html) | [`getComponent()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getComponent--) |
| [`ValueMap`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html) | [`getInheritedProperties()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getInheritedPageProperties--) |
| [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | [`getResource()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getResource--) |
| [`ResourceResolver`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceResolver.html) | [`getResourceResolver()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getResourceResolver--) |
| [`SlingHttpServletRequest`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) | [`getRequest()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getRequest--) |
| [`SlingHttpServletResponse`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) | [`getResponse()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getResponse--) |
| [`SlingScriptHelper`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/scripting/SlingScriptHelper.html) | [`getSlingScriptHelper()`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/sightly/WCMUsePojo.html#getSlingScriptHelper--) |

### Getter-Methoden {#getter-methods}

Sobald die Anwendungsklasse initialisiert ist, wird die HTL-Datei ausgeführt. In dieser Phase wird HTL in der Regel den Status verschiedener Mitgliedsvariablen der Anwendungsklasse abrufen und sie für die Darstellung rendern.

Um den Zugriff auf diese Werte von der HTL-Datei aus zu ermöglichen, müssen Sie benutzerdefinierte Getter-Methoden in der Anwendungsklasse gemäß der folgenden Namenskonvention definieren:

* Eine Methode in der Form `getXyz` stellt in der HTL-Datei eine Objekteigenschaft mit dem Namen `xyz` zur Verfügung.

In der folgenden Beispieldatei `/apps/my-example/component/info/Info.java` führen die Methoden `getTitle` und `getDescription` dazu, dass die Objekteigenschaften `title` und `description` im Kontext der HTL-Datei zugänglich werden.

```java
...

public class Info extends WCMUsePojo {

    ...

    public String getLowerCaseTitle() {
        return lowerCaseTitle;
    }

    public String getLowerCaseDescription() {
        return lowerCaseDescription;
    }
}
```

### Attribut `data-sly-use` {#data-sly-use-attribute}

Das Attribut `data-sly-use` wird verwendet, um die Anwendungsklasse innerhalb Ihres HTL-Codes zu initialisieren. Im Beispiel deklariert das Attribut `data-sly-use` , dass die Klasse `Info` verwendet wird. Sie können nur den lokalen Namen der Klasse verwenden, da Sie eine lokale Installation verwenden (nachdem Sie die Java-Quelldatei im selben Ordner wie die HTL-Datei platziert haben). Wenn Sie eine Bundle-Installation verwenden würden, müssten Sie den voll qualifizierten Klassennamen angeben.

Beachten Sie die Verwendung in diesem Beispiel für `/apps/my-example/component/info/info.html`.

```xml
<div data-sly-use.info="Info">
    <h1>${info.lowerCaseTitle}</h1>
    <p>${info.lowerCaseDescription}</p>
</div>
```

### Lokale Kennung {#local-identifier}

Die Kennung `info` (nach dem Punkt in `data-sly-use.info`) wird in der HTL-Datei verwendet, um die Klasse anzugeben. Diese Kennung erstreckt sich global in der Datei, nachdem sie deklariert wurde. Er ist nicht auf das Element beschränkt, das die Anweisung `data-sly-use` enthält.

Beachten Sie die Verwendung in diesem Beispiel für `/apps/my-example/component/info/info.html`.

```xml
<div data-sly-use.info="Info">
    <h1>${info.lowerCaseTitle}</h1>
    <p>${info.lowerCaseDescription}</p>
</div>
```

### Abrufen der Eigenschaften {#getting-properties}

Die Kennung `info` wird anschließend verwendet, um auf die Objekteigenschaften `title` und `description` zuzugreifen, die mithilfe der Getter-Methoden `Info.getTitle` und `Info.getDescription` zur Verfügung gestellt wurden.

Beachten Sie die Verwendung in diesem Beispiel für `/apps/my-example/component/info/info.html`.

```xml
<div data-sly-use.info="Info">
    <h1>${info.lowerCaseTitle}</h1>
    <p>${info.lowerCaseDescription}</p>
</div>
```

### Ausgabe {#output}

Wenn nun auf `/content/my-example.html` zugegriffen wird, wird die folgende Datei `/content/my-example.html` zurückgegeben.

```xml
<div>
    <h1>my example</h1>
    <p>this is some example content.</p>
</div>
```

>[!NOTE]
>
>Dieses Beispiel wurde vereinfacht, nur um seine Verwendung zu veranschaulichen. In einer Produktionsumgebung empfiehlt Adobe die Verwendung von [Sling-Modellen](https://sling.apache.org/documentation/bundles/models.html).

## Mehr als nur die Grundlagen {#beyond-the-basics}

In diesem Abschnitt werden einige zusätzliche Funktionen vorgestellt, die über das zuvor beschriebene Beispiel hinausgehen.

* Übergabe von Parametern an eine Anwendungsklasse
* Gebündelte Java-Anwendungsklasse

### Weitergeben von Parametern {#passing-parameters}

Parameter können bei der Initialisierung an eine Anwendungsklasse weitergegeben werden.

Weitere Informationen finden Sie in der Dokumentation zur Sling [HTL Scripting Engine](https://sling.apache.org/documentation/bundles/scripting/scripting-htl.html#passing-parameters-to-java-use-objects).

### Gebündelte Java-Klasse {#bundled-java-class}

Bei einer gebündelten Anwendungsklasse muss die Klasse kompiliert, verpackt und in AEM mithilfe des standardmäßigen Verteilungsmechanismus für OSGi-Bundles bereitgestellt werden. Im Gegensatz zu einer lokalen Installation sollte die Paketdeklaration für die Anwendungsklasse normal benannt werden, wie in diesem Beispiel für `/apps/my-example/component/info/Info.java`.

```java
package org.example.app.components;

import com.adobe.cq.sightly.WCMUsePojo;

public class Info extends WCMUsePojo {
    ...
}
```

Außerdem muss die Anweisung `data-sly-use` den voll qualifizierten Klassennamen referenzieren, nicht nur den lokalen Klassennamen wie in diesem Beispiel für `/apps/my-example/component/info/info.html`.

```xml
<div data-sly-use.info="org.example.app.components.info.Info">
  <h1>${info.title}</h1>
  <p>${info.description}</p>
</div>
```
