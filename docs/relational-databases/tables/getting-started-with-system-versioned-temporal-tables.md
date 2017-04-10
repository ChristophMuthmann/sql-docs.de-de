---
title: "Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/28/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
caps.latest.revision: 12
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 12
---
# Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Je nach Szenario können Sie neue temporale Tabellen mit Systemversionsverwaltung erstellen oder vorhandene ändern, indem Sie dem vorhandenen Tabellenschema temporale Attribute hinzufügen.   
Wenn die Daten in der temporalen Tabelle geändert werden, erstellt das System einen Versionsverlauf, transparent für Anwendungen und Endbenutzer. Folglich erfordert das Arbeiten mit temporalen Tabellen mit Systemversionsverwaltung keine Änderungen an der Art, wie die Tabelle geändert wird oder wie der neueste (tatsächliche) Status der Daten abgefragt wird.   
Neben den regulären DML-Anweisungen und Abfragen ermöglichen temporale Tabellen durch erweiterte Transact-SQL-Syntax auch praktische und einfache Möglichkeiten, aus dem Datenverlauf Erkenntnisse zu gewinnen.   
Jeder Tabelle mit Systemversionsverwaltung wird einer Verlaufstabelle zugewiesen. Dies ist für die Benutzer jedoch vollständig transparent, es sei denn, sie möchten die Arbeitsauslastungsleistung oder den Speicherplatzbedarf optimieren, indem sie zusätzliche Indizes erstellen oder verschiedene Speicheroptionen auswählen.    
Das folgende Diagramm veranschaulicht den üblichen Arbeitsablauf bei temporalen Tabellen mit Systemversionsverwaltung:   
![Getting Started with Temporal](../../relational-databases/tables/media/getting-started-with-temporal.png "Getting Started with Temporal")  
  
 Dieses Thema ist in folgende fünf Unterthemen unterteilt:  
  
-   [Erstellen einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
-   [Ändern von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
-   [Abfragen von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
-   [Ändern vom Schema einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
-   [Beenden der Versionsverwaltung auf einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
## Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Getting%20Started%20with%20System-Versioned%20Temporal%20Tables%20page).  
  
## Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Sicherheit bei temporale Tabellen](../../relational-databases/tables/temporal-table-security.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  