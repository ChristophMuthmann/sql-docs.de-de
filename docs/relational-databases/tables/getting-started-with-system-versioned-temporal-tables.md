---
title: Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 456602d6543527b1826dc21f93859f75629fd1a1
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="getting-started-with-system-versioned-temporal-tables"></a>Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Je nach Szenario können Sie neue temporale Tabellen mit Systemversionsverwaltung erstellen oder vorhandene ändern, indem Sie dem vorhandenen Tabellenschema temporale Attribute hinzufügen.   
Wenn die Daten in der temporalen Tabelle geändert werden, erstellt das System einen Versionsverlauf, transparent für Anwendungen und Endbenutzer. Folglich erfordert das Arbeiten mit temporalen Tabellen mit Systemversionsverwaltung keine Änderungen an der Art, wie die Tabelle geändert wird oder wie der neueste (tatsächliche) Status der Daten abgefragt wird.   
Neben den regulären DML-Anweisungen und Abfragen ermöglichen temporale Tabellen durch erweiterte Transact-SQL-Syntax auch praktische und einfache Möglichkeiten, aus dem Datenverlauf Erkenntnisse zu gewinnen.   
Jeder Tabelle mit Systemversionsverwaltung wird einer Verlaufstabelle zugewiesen. Dies ist für die Benutzer jedoch vollständig transparent, es sei denn, sie möchten die Arbeitsauslastungsleistung oder den Speicherplatzbedarf optimieren, indem sie zusätzliche Indizes erstellen oder verschiedene Speicheroptionen auswählen.    
Das folgende Diagramm veranschaulicht den üblichen Arbeitsablauf bei temporalen Tabellen mit Systemversionsverwaltung:   
![Erste Schritte mit Temporal](../../relational-databases/tables/media/getting-started-with-temporal.png "Getting Started with Temporal")  
  
 Dieses Thema ist in folgende fünf Unterthemen unterteilt:  
  
-   [Erstellen einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
-   [Ändern von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
-   [Abfragen von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
-   [Ändern vom Schema einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
-   [Beenden der Versionsverwaltung auf einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Getting%20Started%20with%20System-Versioned%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Sicherheit bei temporale Tabellen](../../relational-databases/tables/temporal-table-security.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
