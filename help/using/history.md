---
title: Geschichte von HTL
description: Für Personen, die schon lange mit AEM arbeiten, enthält dieses Dokument Hintergrundinformationen zu HTL, zu dessen Ablösung von JSP und zur Änderung des früheren Namens Sightly.
exl-id: 00985b35-2130-4946-959a-0a09a34a0f05
source-git-commit: addc69e4b4e56a9b1c5f91ce9af26fa2d326d981
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 96%

---


# Geschichte von HTL {#history-of-htl}

Für Personen, die schon lange mit AEM arbeiten, enthält dieses Dokument Hintergrundinformationen zu HTL, zu dessen Ablösung von JSP und zur Änderung des früheren Namens Sightly.

## Zuvor als Sightly bezeichnet {#sightly}

HTML Template Language (HTL) ist das bevorzugte und empfohlene Server-seitige Vorlagensystem für HTML in Adobe Experience Manager. Sie ersetzt JSP (JavaServer Pages), das in früheren Versionen von AEM verwendet wurde.

## HTL über JSP {#htl-over-jsp}

Adobe empfiehlt, für neue AEM-Projekte die HTML Template Language zu verwenden. Der Grund dafür ist, dass sie im Vergleich zu JSP mehrere Vorteile bietet. Bei bestehenden Projekten macht eine Migration jedoch nur Sinn, wenn abschätzbar ist, dass dies weniger aufwändig ist, als die vorhandenen JSPs für die kommenden Jahre zu verwalten.

Der Wechsel zu HTL ist nicht zwangsläufig eine Alles-oder-Nichts-Entscheidung, da in HTL geschriebene Komponenten mit in JSP oder ESP geschriebenen Komponenten kompatibel sind. Dieser Ansatz bedeutet, dass vorhandene Projekte HTL problemlos für neue Komponenten und gleichzeitig JSP für vorhandene Komponenten verwenden können.

HTL-Dateien können sogar in derselben Komponente zusammen mit JSPs und ESPs verwendet werden. Im folgenden Beispiel wird in **Zeile 1** gezeigt, wie eine HTL-Datei aus einer JSP-Datei eingeschlossen wird, und in **Zeile 2**, wie eine JSP-Datei aus einer HTL-Datei eingeschlossen werden kann:

```xml
<cq:include script="template.html"/>
<sly data-sly-include="template.jsp"/>
```

## Häufig gestellte Fragen {#frequently-asked-questions}

Erfahrene AEM-Entwickelnde, die HTL gerade erst kennenlernen, stellen häufig die folgenden Fragen:

### Weist HTL Einschränkungen auf, die es bei JSP nicht gibt? {#limitations}

HTL weist im Vergleich zu JSP keine Einschränkungen auf. Was mit JSP erledigt werden kann, sollte auch mit HTL erreichbar sein. HTL ist jedoch in mehreren Aspekten strenger als JSP. Was in einer einzigen JSP-Datei erreicht werden kann, muss in HTL möglicherweise in eine Java-Klasse oder eine JavaScript-Datei aufgeteilt werden, um es zu erreichen. Dieser Ansatz ist jedoch generell erwünscht, um eine entsprechende Trennung von Belangen zwischen der Logik und dem Markup sicherzustellen.

### Werden JSP-Tag-Bibliotheken durch HTL unterstützt? {#tag-libraries}

Nein. Aber wie im Abschnitt [Laden von Client-Bibliotheken](getting-started.md#loading-client-libraries) des Dokuments zu den ersten Schritten gezeigt, bieten die Template- und Call-Anweisungen ein ähnliches Muster.

### Können die HTL-Funktionen für ein AEM-Projekt erweitert werden? {#extended}

Nein. HTL verfügt über leistungsfähige Erweiterungsmechanismen für die Wiederverwendung von Logik (die [Anwendungs-API](#use-api-for-accessing-logic)) und von Markup (die Template- und Call-Anweisungen), die zur Modularisierung des Codes von Projekten genutzt werden können.

### Was sind die Hauptvorteile von HTL im Vergleich zu JSP? {#benefits}

Sicherheit und Projekteffizienz sind die Hauptvorteile, die in der [Übersicht](overview.md) näher erläutert werden.

### Wird es JavaServer-Seiten (JSP) irgendwann nicht mehr geben? {#go-away}

Nein. Es liegen keine Pläne zur Einstellung von JSP vor.

## Was verbirgt sich hinter einem Namen? {#what-is-in-a-name}

In AEM 6.0 und 6.1 wurde die HTL **Sightly** genannt. Adobe hat sie in **HTML Template Language** oder kurz **HTL** umbenannt, um klarzustellen, wofür die Spezifikation gedacht ist, und um sich die Namensrichtlinien von Adobe im Allgemeinen anzupassen. Diese Namensänderung wurde im August 2016 wirksam und gilt für AEM Version 6.0 und höher.

>[!NOTE]
>
>Diese Namensänderung wirkt sich weder auf den Code noch auf die API aus. Daher ist die Kompatibilität nicht beeinträchtigt.

<!-- LINK IS 404
For more information, watch [this announcement video](https://helpx.adobe.com/experience-manager/how-to/announce-htl.html). -->

Weitere Informationen über HTL finden Sie im [Leitfaden für die ersten Schritte mit der HTML Templating Language (HTL)](overview.md).
