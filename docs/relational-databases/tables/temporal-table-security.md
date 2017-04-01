---
title: "Sicherheit bei temporale Tabellen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 60e5d6f6-a26d-4bba-aada-42e382bbcd38
caps.latest.revision: 9
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Sicherheit bei temporale Tabellen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Um die Sicherheitsaspekte zu verstehen, die für temporale Tabellen relevant sind, ist es wichtig, die Sicherheitsprinzipale zu verstehen, die für die temporalen Tabellen angewendet werden. Sobald Sie mit diesen Sicherheitsprinzipien vertraut sind, sind Sie bereit, sich mit den Sicherheitsfragen zu den **CREATE TABLE**-, **ALTER TABLE**- und **SELECT**-Anweisungen zu befassen.  
  
## Sicherheitsprinzipien  
 Die folgende Tabelle beschreibt die Sicherheitsprinzipien, die für temporäre Tabellen gelten:  
  
|Prinzip|Beschreibung|  
|---------------|-----------------|  
|Das Aktivieren bzw. Deaktivieren der Systemversionsverwaltung erfordert die höchsten Berechtigungen für betroffene Objekte|Das Aktivieren und Deaktivieren von SYSTEM_VERSIONING erfordert die CONTROL-Berechtigung sowohl für die aktuelle Tabelle als auch für die Verlaufstabelle|  
|Verlaufsdaten können nicht direkt geändert werden|Wenn SYSTEM_VERSIONING ON ist, können die Benutzer Verlaufsdaten nicht ändern, unabhängig davon, über welche tatsächlichen Berechtigungen sie für die aktuelle Tabelle oder die Verlaufstabelle verfügen. Das umfasst sowohl Daten- als auch Schemaänderungen|  
|Das Abfragen von Verlaufsdaten erfordert die **SELECT**-Berechtigung für die Verlaufstabelle|Nur weil ein Benutzer über die **SELECT**-Berechtigung für die aktuelle Tabelle verfügt, bedeutet das nicht, dass er über die **SELECT**-Berechtigung für die Verlaufstabelle verfügt.|  
|Überwachungsoberflächenvorgänge wirken sich auf Verlaufstabellen in spezifischen Arten aus:|Die Überwachung von Verlaufstabellen erfasst regelmäßig alle direkten Versuche auf die Daten zuzugreifen (unabhängig davon, ob sie erfolgreich waren oder nicht).<br /><br /> **SELECT** mit der Erweiterung für temporale Abfragen zeigt, dass dieser Vorgang Auswirkungen auf die Verlaufstabelle hatte.<br /><br /> **CREATE/ALTER** temporale Tabellen machen die Information verfügbar, dass Berechtigungsüberprüfungen für die Verlaufstabelle ebenfalls durchgeführt werden. Die Überwachungsdatei enthält einen zusätzlichen Datensatz für die Verlaufstabelle.<br /><br /> DML-Vorgänge auf der aktuellen Tabelle zeigen auf, dass die Verlaufstabelle betroffen war, aber „additional_info“ bietet den erforderlichen Zusammenhang (DML war ein Ergebnis von „system_versioning“).|  
  
## Ausführen von Schemavorgängen  
 Wenn SYSTEM_VERSIONING auf ON festgelegt ist, werden Schemaänderungsvorgänge beschränkt.  
  
### Nicht zulässige ALTER-Schemavorgänge  
  
|Vorgang|aktuelle Tabelle|Verlaufstabelle|  
|---------------|-------------------|-------------------|  
|**DROP TABLE**|Unzulässig|Unzulässig|  
|**ALTER TABLE…SWITCH PARTITION**|Nur SWITCH IN (siehe [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md))|Nur SWITCH OUT (siehe [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md))|  
|**ALTER TABLE…DROP PERIOD**|Unzulässig|-|  
|**ALTER TABLE…ADD PERIOD**|-|Unzulässig|  
  
## Zulässigen ALTER TABLE-Vorgänge  
  
|Vorgang|Aktuell|Verlauf|  
|---------------|-------------|-------------|  
|**ALTER TABLE…REBUILD**|Zulässig (unabhängig)|Zulässig (unabhängig)|  
|**CREATE INDEX**|Zulässig (unabhängig)|Zulässig (unabhängig)|  
|**CREATE STATISTICS**|Zulässig (unabhängig)|Zulässig (unabhängig)|  
  
## Sicherheit der Anweisung CREATE Temporal TABLE  
  
||Erstellen einer neuen Verlaufstabelle|Wiederverwenden einer vorhandenen Verlaufstabelle|  
|-|------------------------------|----------------------------------|  
|Berechtigung erforderlich|**CREATE TABLE**-Berechtigung in der Datenbank<br /><br /> **ALTER**-Berechtigung für die Schemas, in denen die aktuellen Tabellen und Verlaufstabellen erstellt werden|**CREATE TABLE**-Berechtigung in der Datenbank<br /><br /> **ALTER**-Berechtigung für das Schema, in dem die aktuelle Tabelle erstellt wird<br /><br /> **CONTROL**-Berechtigung für die Verlaufstabelle, die als Teil der **CREATE TABLE**-Anweisung zum Erstellen der temporalen Tabelle angegeben wurde|  
|Überwachung|Die Überwachung zeigt, dass Benutzer versucht haben, zwei Objekte zu erstellen. Der Vorgang kann fehlschlagen, entweder aufgrund fehlender Berechtigungen zum Erstellen einer Tabelle in der Datenbank, oder aufgrund fehlender Berechtigungen für das Ändern von Schemas in einer der Tabellen.|Die Überwachung zeigt, dass eine temporale Tabelle erstellt wurde. Der Vorgang kann fehlschlagen, entweder aufgrund fehlender Berechtigungen zum Erstellen einer Tabelle in der Datenbank, aufgrund der fehlenden Berechtigungen zum Ändern des Schemas für die temporale Tabelle, oder aufgrund der fehlenden Berechtigungen für die Verlaufstabelle.|  
  
## Sicherheit der Anweisung ALTER Temporal TABLE SET (SYSTEM_VERSIONING ON/OFF)  
  
||Erstellen einer neuen Verlaufstabelle|Wiederverwenden einer vorhandenen Verlaufstabelle|  
|-|------------------------------|----------------------------------|  
|Berechtigung erforderlich|**CONTROL**-Berechtigung in der Datenbank<br /><br /> **CREATE TABLE**-Berechtigung in der Datenbank<br /><br /> **ALTER**-Berechtigung für die Schemas, in dem die Verlaufstabelle erstellt wird|**CONTROL**-Berechtigung für die ursprüngliche Tabelle, die geändert wird<br /><br /> **CONTROL**-Berechtigung für die Verlaufstabelle, die als Teil der **ALTER TABLE**-Anweisung angegeben wurde|  
|Überwachung|Die Überwachung zeigt, dass die temporale Tabelle geändert und die Verlaufstabelle zur gleichen Zeit erstellt wurde. Der Vorgang kann fehlschlagen, entweder aufgrund fehlender Berechtigungen zum Erstellen einer Tabelle in der Datenbank, aufgrund der fehlenden Berechtigungen zum Ändern des Schemas für die Verlaufstabelle, oder aufgrund der fehlenden Berechtigungen zum Ändern der temporalen Tabelle.|Die Überprüfung zeigt, dass die temporale Tabelle geändert wurde, aber der Vorgang erforderte Zugriff auf die Verlaufstabelle. Der Vorgang kann möglicherweise nicht ausgeführt werden, da Berechtigungen für die Verlaufstabelle oder für die aktuelle Tabelle fehlen.|  
  
## Sicherheit der SELECT-Anweisung  
 **SELECT**-Berechtigung ist unverändert für **SELECT**-Anweisungen, die sich nicht auf die Verlaufstabelle auswirken. Für **SELECT**-Anweisungen, die auf die Verlaufstabelle wirken, ist die **SELECT**-Berechtigung sowohl für die aktuelle als auch für die Verlaufstabelle erforderlich.  
  
## Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20Security%20page).  
  
## Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  