---
title: Die HTL-Spezifikation
description: Ausführliche Informationen zur Syntax finden Sie in der HTL-Spezifikation.
exl-id: c0657476-4db6-4fad-ad87-9252b5003237
source-git-commit: addc69e4b4e56a9b1c5f91ce9af26fa2d326d981
workflow-type: ht
source-wordcount: '134'
ht-degree: 100%

---


# Die HTL-Spezifikation {#htl-specification}

Die HTML Template Language (HTL) ist das bevorzugte und empfohlene Server-seitige Vorlagensystem für HTML.

## HTL-Ebenen {#layers}

Sie können HTL in AEM durch eine Reihe von Ebenen definieren.

1. **[HTL-Spezifikation](https://github.com/adobe/htl-spec)** – HTL ist eine plattformunabhängige Open-Source-Spezifikation, die von interessierten Personen frei implementiert werden kann. Seine Spezifikationen werden in seinem GitHub-Repository gepflegt.
1. **[Sling HTL Scripting Engine](https://sling.apache.org/documentation/bundles/scripting/scripting-htl.html)** – Das `Sling`-Projekt hat die Referenzimplementierung von HTL erstellt, die von AEM verwendet wird. Die Dokumentation wird vom `Sling`-Projekt verwaltet.
1. **[AEM-Erweiterungen](aem-extensions.md)** – AEM baut auf der `Sling` HTL Scripting Engine auf, um Entwickelnden praktische, AEM-spezifische Funktionen zu bieten. Diese Erweiterungen sind im Rahmen dieser Dokumentation dokumentiert.

Folgen Sie den obigen Links zu den entsprechenden Dokumentationen für alle von AEM verwendeten HTL-Ebenen.
