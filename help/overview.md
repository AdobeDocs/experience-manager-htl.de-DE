---
title: HTL-Übersicht
description: Erfahren Sie, wie AEM die HTML-Vorlagensprache (HTL) unterstützt, um ein produktives Web-Framework auf Unternehmensebene anzubieten, das die Sicherheit erhöht und Personen ohne Java-Kenntnisse, die HTML entwickeln, eine bessere Beteiligung an AEM-Projekten ermöglicht.
exl-id: 5d06ff25-d681-4b95-8375-c28a8364eb7e
source-git-commit: 5ab1275c984135fe946f36905bbc979cf19edd80
workflow-type: ht
source-wordcount: '711'
ht-degree: 100%

---


# Übersicht {#overview}

Die HTML-Vorlagensprache (HTL), die durch Adobe Experience Manager (AEM) unterstützt wird, bietet ein hoch produktives Webframework auf Unternehmensebene, das die Sicherheit erhöht und es HTML-Entwicklern ohne Java-Kenntnissen ermöglicht, besser an AEM-Projekten teilhaben zu können.

Die [in AEM 6.0 eingeführte](history.md) HTML Template Language ist das bevorzugte und empfohlene Server-seitige Vorlagensystem für HTML in AEM. Die HTML-Vorlagensprache unterstützt Web-Entwickler, die zuverlässige Unternehmens-Websites erstellen müssen, dabei, die Sicherheit und die Entwicklungseffizienz zu erhöhen.

## Erhöhte Sicherheit {#increased-security}

Die HTML Template Language erhöht die Sicherheit von Websites, die sie in ihrer Implementierung verwenden, im Vergleich zu den meisten anderen Template-Systemen, da HTL in der Lage ist, automatisch das richtige kontextbezogene Escaping auf alle Variablen anzuwenden, die an die Präsentationsebene ausgegeben werden. HTL ermöglicht dies, da sie die HTML-Syntax versteht, und verwendet dieses Wissen zum Anpassen des erforderlichen Escapings für Ausdrücke auf der Grundlage ihrer Position im Markup. Dies führt beispielsweise dazu, dass Ausdrücke, die in `href`- oder `src`-Attributen stehen, anders behandelt werden als Ausdrücke, die in anderen Attributen oder anderswo stehen.

Auch wenn dasselbe Ergebnis mit Vorlagensprachen wie JSP erzielt werden kann, muss dort der Entwickler manuell sicherstellen, dass jede Variable entsprechend maskiert wird. Da ein einzelner Wegfall oder Fehler hinsichtlich der angewendeten Maskierung potenziell ausreichen kann, um eine Sicherheitslücke beim Cross-Site-Scripting (XSS) zu verursachen, haben wir uns dafür entschieden, diese Aufgabe mit HTL zu automatisieren. Bei Bedarf können Entwickler weiterhin eine andere Maskierung für die Ausdrücke angeben. Mit HTL entspricht das Standardverhalten mit höherer Wahrscheinlichkeit dem gewünschten Verhalten, wobei die Fehlerwahrscheinlichkeit reduziert wird.

## Vereinfachte Entwicklung {#simplified-development}

Die HTML-Vorlagensprache lässt sich einfach erlernen und ihre Funktionen sind zweckgebunden, um sicherzustellen, dass sie einfach und gezielt bleibt. Sie verfügt über leistungsstarke Mechanismen für das Strukturieren von Markup und das Aufrufen der Logik. Zugleich erzwingt sie immer die strenge Trennung von Belangen zwischen Markup und Logik. Bei der HTL an sich handelt es sich um den Standard HTML5, da sie Ausdrücke und Datenattribute verwendet, um das Markup mit dem gewünschten dynamischen Verhalten mit Anmerkungen zu versehen. Sie unterbricht demnach nicht die Gültigkeit des Markups und sorgt dafür, dass es weiterhin lesbar bleibt. Beachten Sie, dass die Auswertung der Ausdrücke und Datenattribute vollständig Server-seitig erfolgt und auf der Client-Seite nicht sichtbar ist, wo jedes gewünschte JavaScript-Framework ohne Störung verwendet werden kann. 

Durch diese Funktionen können HTML-Entwickler ohne Java-Kenntnisse und nur mit geringen produktspezifischen Kenntnissen HTL-Vorlagen bearbeiten, wodurch sie Teil des Entwicklungsteams sein und die Zusammenarbeit mit den Java-Entwicklerexperten optimieren können. Zudem können sich Java-Entwickler wiederum auf den Back-End-Code konzentrieren und müssen sich nicht um HTML kümmern.

## Reduzierte Kosten {#reduced-costs}

Erhöhte Sicherheit, vereinfachte Entwicklung und verbesserte Team-Zusammenarbeit führen bei AEM-Projekten zu geringerem Aufwand, schnellerer Markteinführung (TTM) und niedrigeren Gesamtbetriebskosten (TCO).

Konkret wurde bei der Neuimplementierung der Website Adobe.com mit der HTML-Vorlagensprache beobachtet, dass Kosten und Dauer des Projekts um etwa 25 % reduziert werden konnten.

![Effizienzsteigerung und Kostensenkung](assets/chlimage_1.png)

Das obige Diagramm zeigt die folgenden, potenziell durch HTL ermöglichten Verbesserungen hinsichtlich der Effizienz:

* **HTML/CSS/JS:** Da die HTML-Entwickler HTL-Vorlagen direkt bearbeiten können, müssen die Front-End-Designs nicht mehr getrennt vom AEM-Projekt implementiert werden, sondern können direkt in den tatsächlichen AEM-Komponenten implementiert werden. Dies reduziert mühevolle wiederholte Durchgänge mit den Java-Entwicklerexperten.
* **JSP/HTL:** Da für HTL an sich keinerlei Java-Kenntnisse erforderlich sind und darin zu schreiben unkompliziert ist, kann jeder Entwickler mit HTML-Fachwissen die Vorlagen bearbeiten.
* **Java:** Dank der eindeutigen und einfach zu verwendenden durch HTL bereitgestellten Anwendungs-API ist die Schnittstelle mit der Geschäftslogik klarer gestaltet, wovon die Java-Entwicklung insgesamt profitiert.

## Einführungsvideo {#video}

Das folgende Video aus einer [AEM Gems-Sitzung](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-introduction-to-htl.html?lang=de) gibt einen Überblick über den Zweck von HTL sowie Implementierungsbeispiele.

>[!VIDEO](https://video.tv.adobe.com/v/19504/?quality=9)

Bitte beachten Sie, dass sich das Video auf HTL unter [seinem früheren Namen, Sightly](history.md), bezieht.

## Nächste Schritte {#next-steps}

Nachdem Sie nun die Ziele und Vorteile von HTL kennen, können Sie sich mit der Sprache vertraut machen, indem Sie das Dokument [Erste Schritte mit der HTML-Vorlagensprache](getting-started.md) lesen.