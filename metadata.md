---
solution: Experience Manager
type: Documentation
product: adobe experience manager
git-repo: https://github.com/AdobeDocs/experience-manager-htl.de-DE
index: y
landing-page-name: experience-manager
landing-page-breadcrumb-title: Experience Manager
recommendations: noDisplay
source-git-commit: 50bd3425ac316adf8b4b2560d4782cd1d2efa9c2
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 40%

---


# Metadaten für die interne Verwendung

Das GitHub-Authoring-System definiert Metadaten hierarchisch mit zunehmenden Präzedenzfällen, wie im Folgenden dargestellt:

1. metadata.md
1. IHV
1. Artikel

Die in der Datei „metadata.md“ definierten Metadaten gelten für das gesamte Repository, können jedoch auf Inhaltsverzeichnis- und Artikelebene überschrieben werden. Das Überschreiben der Metadaten sollte auf der niedrigstmöglichen Ebene erfolgen.

Die Metadaten im `experience-manager-core-components.en`-Repository sind das erforderliche Minimum.

metadata.md

* `product`
* `git-repo`
* `index: y`

Wird nicht mehr verwendet:

* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

IHVs

* `sub-product`
* `user-guide-title`

Artikel

* `title`
* `description`
* `index: n` (nur für ältere Komponentenversionen)

