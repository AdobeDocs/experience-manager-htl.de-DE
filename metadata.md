---
solution: Experience Manager
type: Documentation
git-repo: https://github.com/AdobeDocs/experience-manager-htl.en
index: true
landing-page-name: experience-manager
landing-page-breadcrumb-title: AEM
recommendations: noDisplay
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
usetq: true
source-git-commit: d9500886a302eafb90cb5ece6dec09849acd7ae2
workflow-type: tm+mt
source-wordcount: 86
ht-degree: 2%

---


# Metadaten für die interne Verwendung

Das GitHub-Authoring-System definiert Metadaten hierarchisch mit zunehmenden Präzedenzfällen, wie im Folgenden dargestellt:

1. metadata.md
1. toC
1. Artikel

Die in der Datei „metadata.md“ definierten Metadaten gelten für das gesamte Repository, können jedoch auf Inhaltsverzeichnis- und Artikelebene überschrieben werden. Jede Überschreibung der Metadaten sollte auf der niedrigstmöglichen Ebene erfolgen.

Die Metadaten im `experience-manager-core-components.en`-Repository sind das erforderliche Minimum.

metadata.md

* `product`
* `git-repo`
* `index: true`

Wird nicht mehr verwendet:

* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

toCS

* `sub-product`
* `user-guide-title`

Artikel

* `title`
* `description`
* `index: false` (nur für frühere Versionen von Komponenten)

