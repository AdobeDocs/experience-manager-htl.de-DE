---
title: Geschichte von HTL
description: Für Personen, die schon lange mit AEM arbeiten, enthält dieses Dokument Hintergrundinformationen zu HTL, zu dessen Ablösung von JSP und zur Änderung des früheren Namens Sightly.
exl-id: 00985b35-2130-4946-959a-0a09a34a0f05
source-git-commit: c6bb6f0954ada866cec574d480b6ea5ac0b51a3f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 41%

---


# Geschichte von HTL {#history-of-htl}

Für Personen, die schon lange mit AEM arbeiten, enthält dieses Dokument Hintergrundinformationen zu HTL, zu dessen Ablösung von JSP und zur Änderung des früheren Namens Sightly.

## Zuvor als Sightly bezeichnet {#sightly}

HTML Template Language (HTL) ist das bevorzugte und empfohlene Server-seitige Vorlagensystem für HTML in Adobe Experience Manager. Sie ersetzt JSP (JavaServer Pages), das in früheren Versionen von AEM verwendet wurde.

## HTL über JSP {#htl-over-jsp}

Adobe empfiehlt für neue AEM Projekte die Verwendung der HTML-Vorlagensprache. Der Grund dafür ist, dass es im Vergleich zu JSP mehrere Vorteile bietet. Bei bestehenden Projekten macht eine Migration jedoch nur Sinn, wenn abschätzbar ist, dass dies weniger aufwändig ist, als die vorhandenen JSPs für die kommenden Jahre zu verwalten.

Der Wechsel zu HTL ist nicht notwendigerweise eine Alles-oder-Nichts-Wahl, da in HTL geschriebene Komponenten mit in JSP oder ESP geschriebenen Komponenten kompatibel sind. Dieser Ansatz bedeutet, dass vorhandene Projekte HTL für neue Komponenten ohne Probleme verwenden können, während JSP für vorhandene Komponenten beibehalten wird.

HTL-Dateien können sogar in derselben Komponente zusammen mit JSPs und ESPs verwendet werden. Das folgende Beispiel zeigt in **Zeile 1**, wie eine HTL-Datei aus einer JSP-Datei eingeschlossen wird, und in **Zeile 2**, wie eine JSP-Datei aus einer HTL-Datei eingeschlossen werden kann:

```xml
<cq:include script="template.html"/>
<sly data-sly-include="template.jsp"/>
```

## Häufig gestellte Fragen {#frequently-asked-questions}

Erfahrene Entwickler, die neu bei HTL sind, stellen häufig die folgenden Fragen:

### Weist HTL Einschränkungen auf, die bei JSP nicht vorhanden sind? {#limitations}

HTL weist im Vergleich zu JSP keine Einschränkungen auf, da das, was mit JSP durchgeführt werden kann, auch mit HTL erreichbar sein sollte. HTL ist in verschiedener Hinsicht jedoch grundsätzlich strenger als JSP. Was in einer einzelnen JSP-Datei erreicht werden kann, muss möglicherweise in eine Java-Klasse oder eine JavaScript-Datei unterteilt werden, um in HTL erreichbar zu sein. Dieser Ansatz ist jedoch im Allgemeinen wünschenswert, um eine gute Trennung der Bedenken zwischen Logik und Markup sicherzustellen.

### Werden JSP-Tag-Bibliotheken durch HTL unterstützt? {#tag-libraries}

Nein. Wie jedoch im Abschnitt [Laden von Client-Bibliotheken](getting-started.md#loading-client-libraries) des Dokuments &quot;Erste Schritte&quot;gezeigt, weisen die Anweisungen &quot;template&quot;und &quot;call&quot;ein ähnliches Muster auf.

### Können die HTL-Funktionen für ein AEM-Projekt erweitert werden? {#extended}

Nein. HTL verfügt über leistungsfähige Erweiterungsmechanismen für die Wiederverwendung von Logik (die [Anwendungs-API](#use-api-for-accessing-logic)) und von Markup (die Template- und Call-Anweisungen), die zur Modularisierung des Codes von Projekten genutzt werden können.

### Was sind die Hauptvorteile von HTL im Vergleich zu JSP? {#benefits}

Sicherheit und Projekteffizienz sind die wichtigsten Vorteile, die in der [Übersicht](overview.md) beschrieben werden.

### Werden JavaServer-Seiten (JSP) entfernt? {#go-away}

Nein. Es gibt keine Pläne, JSP einzustellen.

## Was verbirgt sich hinter einem Namen? {#what-is-in-a-name}

In AEM 6.0 und 6.1 hieß HTL **Sightly**. Adobe hat sie in **HTML-Vorlagensprache** oder **HTL** umbenannt, um klarzustellen, wofür die Spezifikation steht, und um sie allgemein an die Namensrichtlinien für Adobe anzupassen. Diese Namensänderung wurde im August 2016 wirksam und gilt für AEM Version 6.0 und höher.

>[!NOTE]
>
>Diese Namensänderung wirkt sich nicht auf den Code oder die API aus, daher ist die Kompatibilität nicht betroffen. Weitere Informationen finden Sie in diesem Ankündigungsvideo](https://helpx.adobe.com/de/experience-manager/how-to/announce-htl.html).[

Weitere Informationen zu HTL finden Sie im Leitfaden [Erste Schritte mit der HTML-Vorlagensprache (HTL)](overview.md).
