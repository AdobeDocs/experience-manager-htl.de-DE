---
solution: Experience Manager
type: Documentation
product: adobe experience manager
git-repo: https://github.com/AdobeDocs/experience-manager-htl.de-DE
index: y
recommendations: noDisplay
source-git-commit: 22f62868df0fcfc558e5d62434dde843a9f3ca83
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 40%

---


# Metadaten für die interne Verwendung

Das GitHub-Authoring-System definiert Metadaten hierarchisch, wobei die Präzedenzebenen, wie im Folgenden dargestellt, zunehmen:

1. metadata.md
1. IHV
1. Artikel

Die in der Datei &quot;metadata.md&quot;definierten Metadaten gelten für das gesamte Repository, können jedoch auf den Ebenen &quot;ToC&quot;und &quot;article&quot;überschrieben werden. Das Überschreiben der Metadaten sollte auf der niedrigstmöglichen Ebene erfolgen.

Die Metadaten im `experience-manager-core-components.en` -Repository sind das erforderliche Minimum.

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

