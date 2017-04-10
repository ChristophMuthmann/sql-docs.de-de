---
title: "Partitionierung mit tempor&#228;ren Tabellen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
caps.latest.revision: 11
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 11
---
# Partitionierung mit tempor&#228;ren Tabellen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Sie können die Partitionierung unabhängig voneinander für die aktuelle und die Verlaufstabelle verwenden. Ohne Systemversionsverwaltung können mittels Partitionierung jedoch keine Dateninhalte geändert werden.  
  
> [!NOTE]  
>  Partitionierung ist eine Funktion der Enterprise Edition.  
  
-   **Aktuelle Tabelle:**  
  
    -   **SWITCH IN** für die aktuelle Tabelle kann zum Laden und Abfragen von Daten verwendet werden, solange **SYSTEM_VERSIONING** mit **ON** aktiviert ist.  
  
    -   **SWITCH OUT** ist nicht zulässig, wenn **SYSTEM_VERSIONING** aktiviert ist (**ON**).  
  
-   **Verlaufstabelle:**  
  
    -   **SWITCH OUT** kann über die Verlaufstabelle ausgeführt werden, solange **SYSTEM_VERSIONING** aktiviert ist (**ON**), um Teile der Verlaufsdaten zu löschen, die nicht mehr relevant sind.  
  
    -   **SWITCH IN** ist nicht zulässig, solange **SYSTEM_VERSIONING** aktiviert ist (**ON**), da es die Konsistenz temporaler Daten beeinträchtigen kann.  
  
## Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Partitioning%20with%20Temporal%20Tables%20page).  
  
## Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Sicherheit bei temporale Tabellen](../../relational-databases/tables/temporal-table-security.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  