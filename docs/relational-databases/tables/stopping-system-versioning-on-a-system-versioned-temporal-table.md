---
title: Beenden der Versionsverwaltung auf einer versionsverwalteten temporalen Tabelle | Microsoft Dokumentation
ms.custom: 
ms.date: 10/11/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dddd707e-bfb1-44ff-937b-a84c5e5d1a94
caps.latest.revision: "10"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d28ca8dcaae23e9e7c6548dd0c6bc0dcc05d06ac
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stopping-system-versioning-on-a-system-versioned-temporal-table"></a>Beenden der Versionsverwaltung auf einer versionsverwalteten temporalen Tabelle
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Möglicherweise möchten Sie die Versionsverwaltung Ihrer temporalen Tabelle vorübergehend oder dauerhaft beenden.   
Legen Sie zu diesem Zweck die **SYSTEM_VERSIONING** -Klausel, um **OFF**fest.  
  
## <a name="setting-systemversioning--off"></a>Festlegen von SYSTEM_VERSIONING = OFF  
 Beenden Sie die Systemversionsverwaltung, wenn Sie bestimmte Wartungsvorgänge für eine temporale Tabelle ausführen möchten, oder wenn Sie eine Tabelle mit Versionsverwaltung nicht mehr benötigen. Das Ergebnis dieses Vorgangs sind zwei unabhängige Tabellen:  
  
-   Die aktuelle Tabelle mit der Fristdefinition  
  
-   Verlaufstabelle als normale Tabelle  
  
### <a name="important-remarks"></a>Wichtige Hinweise  
  
-   Kein Datenverlust tritt auf, wenn Sie  **SYSTEM_VERSIONING = OFF** festlegen oder den Zeitraum **SYSTEM_TIME** löschen.  
  
-   Wenn Sie **SYSTEM_VERSIONING = OFF** festlegen und den **SYSTEM_TIME** -Zeitraum nicht löschen, wird das System die Aktualisierung der Zeitraumspalten für jeden Einfüge- und Aktualisierungsvorgang fortsetzen. Löschungen in der aktuellen Tabelle sind endgültig.  
  
-   Löschen Sie den **SYSTEM_TIME** -Zeitraum, um die Zeitraumspalten vollständig zu entfernen.  
  
-   Wenn Sie **SYSTEM_VERSIONING = OFF**festlegen, können alle Benutzer, die über ausreichende Berechtigungen verfügen, das Schema und den Inhalt der Verlaufstabelle ändern oder die Verlaufstabelle sogar endgültig löschen.  
  
### <a name="permanently-remove-systemversioning"></a>Dauerhaftes Entfernen von SYSTEM_VERSIONING  
 In diesem Beispiel werden SYSTEM_VERSIONING und die Zeitraumspalten dauerhaft und vollständig entfernt. Das Entfernen der Zeitraumspalten ist optional.  
  
```  
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);   
/*Optionally, DROP PERIOD if you want to revert temporal table to a non-temporal*/   
ALTER TABLE dbo.Department   
DROP PERIOD FOR SYSTEM_TIME;  
  
```  
  
### <a name="temporarily-remove-systemversioning"></a>Vorübergehendes Entfernen von SYSTEM_VERSIONING  
 Dies ist die Liste der Vorgänge, für die die Systemversionsverwaltung auf **OFF**festgelegt werden muss:  
  
-   Entfernen unnötiger Daten aus dem Verlauf (**DELETE** oder **TRUNCATE**)  
  
-   Entfernen von Daten aus der aktuellen Tabelle ohne Versionsverwaltung (**DELETE**, **TRUNCATE**)  
  
-   Partition **SWITCH OUT** aus der aktuellen Tabelle  
  
-   Partition **SWITCH IN** in die Verlaufstabelle  
  
 In diesem Beispiel wird SYSTEM_VERSIONING vorübergehend beendet, um bestimmte Wartungsvorgänge zu erlauben. Wenn Sie Versionsverwaltung als Voraussetzung für die Tabellenwartung vorübergehend beenden, empfehlen wir nachdrücklich, dies für die Datenkonsistenz innerhalb einer Transaktion durchzuführen.  
  
```  
BEGIN TRAN   
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);   
TRUNCATE TABLE [History].[DepartmentHistory]   
WITH (PARTITIONS (1,2))   
ALTER TABLE dbo.Department SET    
(   
SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)   
);   
COMMIT ;  
  
```  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Stopping%20System-Versioning%20on%20a%20System-Version%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Erstellen einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Ändern von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Abfragen von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Ändern vom Schema einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
  
