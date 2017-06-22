---
title: Erstellen einer temporalen Tabelle mit Systemversionsverwaltung | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 05/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21e6d74f-711f-40e6-a8b7-85f832c5d4b3
caps.latest.revision: 20
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a75bde97eddb1b99546ec4d5ff0dbb33340e19e4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="creating-a-system-versioned-temporal-table"></a>Erstellen einer temporalen Tabelle mit Systemversionsverwaltung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Es gibt drei Methoden zum Erstellen einer temporalen Tabelle mit Systemversionsverwaltung, die sich darin unterscheiden, wie die Verlaufstabelle angegeben wird:  
  
-   Temporale Tabelle mit einer anonymen Verlaufstabelle: Sie geben das Schema der aktuellen Tabelle an und lassen eine entsprechende Verlaufstabelle mit einem automatisch generierten Namen vom System erstellen.  
  
-   Temporale Tabelle mit einer Standardverlaufstabelle: Sie geben den Namen des Verlauftabellenschemas und der Tabelle an und lassen vom System eine Verlaufstabelle in diesem Schema erstellen.  
  
-   Temporale Tabelle mit einer vorab erstellten, benutzerdefinierten Verlaufstabelle: Sie erstellen eine Verlaufstabelle, die Ihren Anforderungen am besten entspricht, und verweisen dann beim Erstellen der temporalen Tabelle auf diese Tabelle.  
  
## <a name="creating-a-temporal-table-with-an-anonymous-history-table"></a>Erstellen einer temporalen Tabelle mit einer anonymen Verlaufstabelle  
 Das Erstellen einer temporalen Tabelle mit einer „anonymen“ Verlaufstabelle ist eine praktische Möglichkeit für das schnelle erstellen von Objekten, insbesondere in Prototyp- und Testumgebungen. Es ist auch die einfachste Möglichkeit, eine temporale Tabelle zu erstellen, da keine Parameter in der **SYSTEM_VERSIONING** -Klausel erforderlich sind. Im folgenden Beispiel wird eine neue Tabelle mit aktivierter Systemversionsverwaltung erstellt, ohne den Namen der Verlaufstabelle zu definieren.  
  
```  
CREATE TABLE Department   
(    
     DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)    
WITH (SYSTEM_VERSIONING = ON)   
;  
```  
  
### <a name="important-remarks"></a>Wichtige Hinweise  
  
-   Für eine temporale Tabelle mit Systemversionsverwaltung muss ein Primärschlüssel und genau eine **PERIOD FOR SYSTEM_TIME** mit zwei „datetime2“-Spalten definiert sein, die als **GENERATED ALWAYS AS ROW START / END**deklariert sind.  
  
-   Die **PERIOD** -Spalten dürfen keine NULL-Werte zulassen, auch wenn keine Angabe zur NULL-Zulässigkeit gemacht wurde. Wenn für  **PERIOD** -Spalten explizit angegeben ist, dass NULL-Werte zulässig sind, tritt bei der Anweisung **CREATE TABLE** ein Fehler auf.  
  
-   Das Schema der Verlaufstabelle muss im Hinblick auf Spaltenanzahl, Spaltennamen, Sortierung und Datentypen stets an die aktuelle oder temporale Tabelle angepasst sein.  
  
-   Eine anonyme Verlaufstabelle wird automatisch im gleichen Schema wie die aktuelle oder temporale Tabelle erstellt.  
  
-   Der Name der anonymen Verlaufstabelle weist das folgende Format auf: *MSSQL_TemporalHistoryFor_<Objekt-ID_der_aktuellen_temporalen_Tabelle>_[Suffix]*. Das Suffix ist optional und wird nur hinzugefügt, wenn der erste Teil des Tabellennamens nicht eindeutig ist.  
  
-   Die Verlaufstabelle wird als eine Rowstore-Tabelle erstellt. PAGE-Komprimierung wird angewendet, wenn möglich, andernfalls wird die Verlaufstabelle nicht komprimiert. Einige Tabellenkonfigurationen, z. B. SPARSE-Spalten, lassen beispielsweise keine Komprimierung zu.  
  
-   Für die Verlaufstabelle wird ein gruppierter Standardindex mit einem automatisch generierten Namen im Format *IX_<history_table_name>* erstellt. Der gruppierte Index enthält die **PERIOD**-Spalten (Ende, Anfang).  
  
-   Informationen zum Erstellen der aktuellen Tabelle als speicheroptimierte Tabelle finden Sie unter [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md).  
  
## <a name="creating-a-temporal-table-with-a-default-history-table"></a>Erstellen einer temporalen Tabelle mit einer Standardverlaufstabelle  
 Das Erstellen einer temporalen Tabelle mit einer Standardverlaufstabelle ist eine praktische Möglichkeit, wenn Sie die Benennung steuern möchten, die Verlaufstabelle aber trotzdem mit der Standardkonfiguration vom System erstellt werden soll. Im folgenden Beispiel wird eine neue Tabelle mit aktivierter Systemversionsverwaltung erstellt, wobei der Name der Verlaufstabelle explizit definiert wird.  
  
```  
CREATE TABLE Department   
(    
     DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)     
)   
WITH    
   (   
      SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory)   
   )   
;  
```  
  
### <a name="important-remarks"></a>Wichtige Hinweise  
 Die Verlaufstabelle wird unter Anwendung der gleichen Regeln erstellt, die für das Erstellen einer „anonymen“ Verlaufstabelle gelten. Allerdings gelten die folgenden Regeln speziell für die benannte Verlaufstabelle.  
  
-   Der Schemaname ist für den Parameter **HISTORY_TABLE** obligatorisch.  
  
-   Wenn das angegebene Schema nicht vorhanden ist, tritt bei der Anweisung **CREATE TABLE** ein Fehler auf.  
  
-   Wenn die im Parameter **HISTORY_TABLE** angegebene Tabelle bereits vorhanden ist, wird sie mit der neu erstellten temporalen Tabelle auf [Schemakonsistenz und temporale Datenkonsistenz](http://msdn.microsoft.com/library/dn935015.aspx)verglichen. Wenn Sie eine ungültige Verlaufstabelle angeben, tritt bei der Anweisung **CREATE TABLE** ein Fehler auf.  
  
## <a name="creating-a-temporal-table-with-a-user-defined-history-table"></a>Erstellen einer temporalen Tabelle mit einer benutzerdefinierten Verlaufstabelle  
 Das Erstellen einer temporalen Tabelle mit einer benutzerdefinierten Verlaufstabelle ist eine praktische Möglichkeit, wenn der Benutzer eine Verlaufstabelle mit bestimmten Speicheroptionen und zusätzlichen Indizes festlegen möchte. Im folgenden Beispiel wird eine benutzerdefinierte Verlaufstabelle mit einem Schema erstellt, das auf die zu erstellende temporale Tabelle abgestimmt ist. Für diese benutzerdefinierte Verlaufstabelle werden ein gruppierter Columnstore-Index und ein weiterer nicht gruppierter Rowstore-Index (B-Struktur) für Punktsuchen erstellt. Nach Erstellung der benutzerdefinierten Verlaufstabelle wird die temporale Tabelle mit Systemversionsverwaltung unter Angabe der benutzerdefinierten Verlaufstabelle als Standardverlaufstabelle erstellt.  
  
```  
CREATE TABLE DepartmentHistory   
(    
     DeptID int NOT NULL  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 NOT NULL  
   , SysEndTime datetime2 NOT NULL   
);   
GO   
CREATE CLUSTERED COLUMNSTORE INDEX IX_DepartmentHistory   
   ON DepartmentHistory;   
CREATE NONCLUSTERED INDEX IX_DepartmentHistory_ID_PERIOD_COLUMNS   
   ON DepartmentHistory (SysEndTime, SysStartTime, DeptID);   
GO   
CREATE TABLE Department   
(    
    DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL     
   , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)      
)    
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory))   
;  
```  
  
### <a name="important-remarks"></a>Wichtige Hinweise  
  
-   Wenn Sie analytische Abfragen für die historischen Daten ausführen möchten, die Aggregate oder Fensterfunktionen einsetzen, ist es zum Zwecke der Leistung bei Komprimierung und Abfrage sehr zu empfehlen, einen gruppierten Columnstore als primären Index zu erstellen.  
  
-   Wenn der primäre Anwendungsfall die Datenüberwachung ist (d. h. wenn Sie Verlaufsänderungen für eine bestimmte Zeile in der aktuellen Tabelle suchen möchten), empfiehlt sich die Erstellung einer Rowstore-Verlaufstabelle mit einem gruppierten Index.  
  
-   Die Verlaufstabelle kann keine Primärschlüssel, Fremdschlüssel, eindeutige Indizes, Tabelleneinschränkungen oder Trigger enthalten. Sie kann nicht zur Erfassung von Änderungdaten, zur Änderungsnachverfolgung oder zur Transaktions- oder Mergereplikation konfiguriert werden.  
  
## <a name="alter-non-temporal-table-to-be-system-versioned-temporal-table"></a>Ändern einer nicht temporalen Tabelle in eine temporale Tabelle mit Systemversionsverwaltung  
 Wenn Sie die Systemversionsverwaltung für eine vorhandene Tabelle aktivieren müssen, z. B., wenn Sie eine benutzerdefinierte temporale Lösung zu integrierter Unterstützung migrieren möchten.   
Angenommen, Sie verfügen über eine Gruppe von Tabellen, bei denen die Versionsverwaltung mit Triggern implementiert ist. Die Verwendung temporaler Systemversionsverwaltung ist weniger komplex und bietet zusätzliche Vorteile, z. B.:  
  
-   Unveränderlichen Verlauf  
  
-   Neue Syntax für „Zeitreise“-Abfragen  
  
-   Eine bessere DML-Leistung  
  
-   Minimale Wartungskosten  
  
 Beim Konvertieren einer vorhandenen Tabelle sollten Sie die Verwendung der Klausel **HIDDEN** in Betracht ziehen, um die neuen **PERIOD** -Spalten auszublenden und so Auswirkungen auf vorhandene Anwendungen zu vermeiden, die keine neue Spalten verarbeiten können.  
  
### <a name="adding-versioning-to-non-temporal-tables"></a>Hinzufügen der Versionsverwaltung zu nicht temporalen Tabellen  
 Wenn Sie das Nachverfolgen von Änderungen für eine nicht temporale Tabelle mit den Daten starten möchten, müssen Sie die **PERIOD** -Definition hinzufügen und optional einen Namen für die leere Verlaufstabelle angeben, die SQL Server für Sie erstellt:  
  
```  
CREATE SCHEMA History;   
GO   
ALTER TABLE InsurancePolicy   
   ADD   
      SysStartTime datetime2(0) GENERATED ALWAYS AS ROW START HIDDEN    
           CONSTRAINT DF_SysStart DEFAULT SYSUTCDATETIME()  
      , SysEndTime datetime2(0) GENERATED ALWAYS AS ROW END HIDDEN    
           CONSTRAINT DF_SysEnd DEFAULT CONVERT(datetime2 (0), '9999-12-31 23:59:59'),   
      PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);   
GO   
ALTER TABLE InsurancePolicy   
   SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.InsurancePolicy))   
;  
```  
  
#### <a name="important-remarks"></a>Wichtige Hinweise  
  
-   Das Hinzufügen von Spalten, die keine NULL-Werte zulassen, mit Standardwerten, zu einer vorhandenen Tabelle mit Daten ist in allen Editionen außer SQL Server Enterprise Edition ein Datengrößenvorgang (in SQL Server Enterprise Edition wäre es ein Metadatenvorgang). Bei einer vorhandenen großen Verlaufstabelle mit Daten in SQL Server Standard Edition kann das Hinzufügen einer Nicht-NULL-Spalte ein aufwendiger Vorgang sein.  
  
-   Einschränkungen für Spalten des Zeitraumstarts und -endes müssen sorgfältig gewählt werden:  
  
    -   Der Standardwert für die Startspalte gibt an, ab welchem Zeitpunkt vorhandene Zeilen als gültig betrachtet werden. Es kann kein Zeitpunkt in der Zukunft als datetime-Wert angegeben werden.  
  
    -   Die Endzeit muss als maximaler Wert für eine bestimmte datetime2-Genauigkeit angegeben werden.  
  
-   Durch das Hinzufügen eines Zeitraums wird für die aktuelle Tabelle eine Datenkonsistenzprüfung durchgeführt, um sicherzustellen, dass die Standardwerte für Zeitraumspalten gültig sind.  
  
-   Wenn bei der Aktivierung von **SYSTEM_VERSIONING**eine vorhandene Verlaufstabelle angegeben wird, erfolgt eine Datenkonsistenzprüfung der aktuellen Tabelle und der Verlaufstabelle. Diese Prüfung kann übersprungen werden, indem Sie **DATA_CONISTENCY_CHECK = OFF** als zusätzlichen Parameter angeben.  
  
### <a name="migrate-existing-tables-to-built-in-support"></a>Migrieren von vorhandenen Tabellen zu integrierter Unterstützung  
 Dieses Beispiel zeigt, wie eine vorhandene Lösung basierend auf Triggern zu integrierter temporaler Unterstützung migriert wird. In diesem Beispiel wird angenommen, dass in der aktuellen benutzerdefinierten Lösung die aktuellen und die historischen Daten auf zwei getrennte Benutzertabellen aufgeteilt sind (**ProjectTaskCurrent** und **ProjectTaskHistory**). Wenn Ihre vorhandene Lösung sowohl die aktuellen als auch die historischen Zeilen in einer einzigen Tabelle speichert, sollten Sie die Daten auf zwei Tabellen aufteilen, bevor Sie die in diesem Beispiel gezeigten Migrationsschritte ausführen:  
  
```  
/*Drop trigger on future temporal table*/   
DROP TRIGGER ProjectCurrent_OnUpdateDelete;   
/*Make sure that future period columns are non-nullable*/   
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidFrom] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidTo] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidFrom] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidTo] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskCurrent   
   ADD PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])   
ALTER TABLE ProjectTaskCurrent   
   SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON))   
;  
```  
  
#### <a name="important-remarks"></a>Wichtige Hinweise  
  
-   Durch das Verweisen auf vorhandene Spalten in der **PERIOD** -Definition wird „generated_always_type“ für diese Spalten implizit zu **AS_ROW_START** und **AS_ROW_END** geändert.  
  
-   Durch das Hinzufügen von **PERIOD** wird für die aktuelle Tabelle eine Datenkonsistenzprüfung durchgeführt, um sicherzustellen, dass die vorhandenen Werte für Zeitraumspalten gültig sind.  
  
-   Es wird dringend empfohlen, **SYSTEM_VERSIONING** mit **DATA_CONSISTENCY_CHECK = ON** festzulegen, um Datenkonsistenzprüfungen für die vorhandenen Daten zu erzwingen.  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Creating%20a%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Ändern von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Abfragen von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Ändern vom Schema einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Beenden der Versionsverwaltung auf einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  

