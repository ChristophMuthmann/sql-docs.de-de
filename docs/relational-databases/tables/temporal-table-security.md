---
title: Sicherheit bei temporalen Tabellen | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 02/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 60e5d6f6-a26d-4bba-aada-42e382bbcd38
caps.latest.revision: 9
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f73cdc0f3a240e3d4c795fd67c2913b99748de4a
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="temporal-table-security"></a>Sicherheit bei temporale Tabellen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Um die Sicherheitsaspekte zu verstehen, die für temporale Tabellen relevant sind, ist es wichtig, die Sicherheitsprinzipale zu verstehen, die für die temporalen Tabellen angewendet werden. Sobald Sie mit diesen Sicherheitsprinzipien vertraut sind, sind Sie bereit, sich mit den Sicherheitsfragen zu den **CREATE TABLE**-, **ALTER TABLE**- und **SELECT** -Anweisungen zu befassen.  
  
## <a name="security-principles"></a>Sicherheitsprinzipien  
 Die folgende Tabelle beschreibt die Sicherheitsprinzipien, die für temporäre Tabellen gelten:  
  
|Prinzip|Beschreibung|  
|---------------|-----------------|  
|Das Aktivieren bzw. Deaktivieren der Systemversionsverwaltung erfordert die höchsten Berechtigungen für betroffene Objekte|Das Aktivieren und Deaktivieren von SYSTEM_VERSIONING erfordert die CONTROL-Berechtigung sowohl für die aktuelle Tabelle als auch für die Verlaufstabelle|  
|Verlaufsdaten können nicht direkt geändert werden|Wenn SYSTEM_VERSIONING ON ist, können die Benutzer Verlaufsdaten nicht ändern, unabhängig davon, über welche tatsächlichen Berechtigungen sie für die aktuelle Tabelle oder die Verlaufstabelle verfügen. Das umfasst sowohl Daten- als auch Schemaänderungen|  
|Das Abfragen von Verlaufsdaten erfordert die **SELECT** -Berechtigung für die Verlaufstabelle|Nur weil ein Benutzer über die **SELECT** -Berechtigung für die aktuelle Tabelle verfügt, bedeutet das nicht, dass er über die **SELECT** -Berechtigung für die Verlaufstabelle verfügt.|  
|Überwachungsoberflächenvorgänge wirken sich auf Verlaufstabellen in spezifischen Arten aus:|Die Überwachung von Verlaufstabellen erfasst regelmäßig alle direkten Versuche auf die Daten zuzugreifen (unabhängig davon, ob sie erfolgreich waren oder nicht).<br /><br /> **SELECT** mit der Erweiterung für temporale Abfragen zeigt, dass dieser Vorgang Auswirkungen auf die Verlaufstabelle hatte.<br /><br /> **CREATE/ALTER** temporale Tabellen machen die Information verfügbar, dass Berechtigungsüberprüfungen für die Verlaufstabelle ebenfalls durchgeführt werden. Die Überwachungsdatei enthält einen zusätzlichen Datensatz für die Verlaufstabelle.<br /><br /> DML-Vorgänge auf der aktuellen Tabelle zeigen auf, dass die Verlaufstabelle betroffen war, aber „additional_info“ bietet den erforderlichen Zusammenhang (DML war ein Ergebnis von „system_versioning“).|  
  
## <a name="performing-schema-operations"></a>Ausführen von Schemavorgängen  
 Wenn SYSTEM_VERSIONING auf ON festgelegt ist, werden Schemaänderungsvorgänge beschränkt.  
  
### <a name="disallowed-alter-schema-operations"></a>Nicht zulässige ALTER-Schemavorgänge  
  
|Vorgang|aktuelle Tabelle|Verlaufstabelle|  
|---------------|-------------------|-------------------|  
|**DROP TABLE**|Unzulässig|Unzulässig|  
|**ALTER TABLE…SWITCH PARTITION**|Nur SWITCH IN (siehe [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md))|Nur SWITCH OUT (siehe [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md))|  
|**ALTER TABLE…DROP PERIOD**|Unzulässig|-|  
|**ALTER TABLE…ADD PERIOD**|-|Unzulässig|  
  
## <a name="allowed-alter-table-operations"></a>Zulässigen ALTER TABLE-Vorgänge  
  
|Vorgang|Aktuell|Verlauf|  
|---------------|-------------|-------------|  
|**ALTER TABLE…REBUILD**|Zulässig (unabhängig)|Zulässig (unabhängig)|  
|**CREATE INDEX**|Zulässig (unabhängig)|Zulässig (unabhängig)|  
|**CREATE STATISTICS**|Zulässig (unabhängig)|Zulässig (unabhängig)|  
  
## <a name="security-of-the-create-temporal-table-statement"></a>Sicherheit der Anweisung CREATE Temporal TABLE  
  
||Erstellen einer neuen Verlaufstabelle|Wiederverwenden einer vorhandenen Verlaufstabelle|  
|-|------------------------------|----------------------------------|  
|Berechtigung erforderlich|**CREATE TABLE** -Berechtigung in der Datenbank<br /><br /> **ALTER** -Berechtigung für die Schemas, in denen die aktuellen Tabellen und Verlaufstabellen erstellt werden|**CREATE TABLE** -Berechtigung in der Datenbank<br /><br /> **ALTER** -Berechtigung für das Schema, in dem die aktuelle Tabelle erstellt wird<br /><br /> **CONTROL** -Berechtigung für die Verlaufstabelle, die als Teil der **CREATE TABLE** -Anweisung zum Erstellen der temporalen Tabelle angegeben wurde|  
|Überwachung|Die Überwachung zeigt, dass Benutzer versucht haben, zwei Objekte zu erstellen. Der Vorgang kann fehlschlagen, entweder aufgrund fehlender Berechtigungen zum Erstellen einer Tabelle in der Datenbank, oder aufgrund fehlender Berechtigungen für das Ändern von Schemas in einer der Tabellen.|Die Überwachung zeigt, dass eine temporale Tabelle erstellt wurde. Der Vorgang kann fehlschlagen, entweder aufgrund fehlender Berechtigungen zum Erstellen einer Tabelle in der Datenbank, aufgrund der fehlenden Berechtigungen zum Ändern des Schemas für die temporale Tabelle, oder aufgrund der fehlenden Berechtigungen für die Verlaufstabelle.|  
  
## <a name="security-of-the-alter-temporal-table-set-systemversioning-onoff-statement"></a>Sicherheit der Anweisung ALTER Temporal TABLE SET (SYSTEM_VERSIONING ON/OFF)  
  
||Erstellen einer neuen Verlaufstabelle|Wiederverwenden einer vorhandenen Verlaufstabelle|  
|-|------------------------------|----------------------------------|  
|Berechtigung erforderlich|**CONTROL** -Berechtigung in der Datenbank<br /><br /> **CREATE TABLE** -Berechtigung in der Datenbank<br /><br /> **ALTER** -Berechtigung für die Schemas, in dem die Verlaufstabelle erstellt wird|**CONTROL** -Berechtigung für die ursprüngliche Tabelle, die geändert wird<br /><br /> **CONTROL** -Berechtigung für die Verlaufstabelle, die als Teil der **ALTER TABLE** -Anweisung angegeben wurde|  
|Überwachung|Die Überwachung zeigt, dass die temporale Tabelle geändert und die Verlaufstabelle zur gleichen Zeit erstellt wurde. Der Vorgang kann fehlschlagen, entweder aufgrund fehlender Berechtigungen zum Erstellen einer Tabelle in der Datenbank, aufgrund der fehlenden Berechtigungen zum Ändern des Schemas für die Verlaufstabelle, oder aufgrund der fehlenden Berechtigungen zum Ändern der temporalen Tabelle.|Die Überprüfung zeigt, dass die temporale Tabelle geändert wurde, aber der Vorgang erforderte Zugriff auf die Verlaufstabelle. Der Vorgang kann möglicherweise nicht ausgeführt werden, da Berechtigungen für die Verlaufstabelle oder für die aktuelle Tabelle fehlen.|  
  
## <a name="security-of-select-statement"></a>Sicherheit der SELECT-Anweisung  
 **SELECT** -Berechtigung ist unverändert für **SELECT** -Anweisungen, die sich nicht auf die Verlaufstabelle auswirken. Für **SELECT** -Anweisungen, die auf die Verlaufstabelle wirken, ist die **SELECT** -Berechtigung sowohl für die aktuelle als auch für die Verlaufstabelle erforderlich.  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20Security%20page)  
  
## <a name="see-also"></a>Siehe auch  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

