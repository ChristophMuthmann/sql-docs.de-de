---
title: Sys. dm_db_missing_index_group_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_group_stats_TSQL
- sys.dm_db_missing_index_group_stats
- dm_db_missing_index_group_stats_TSQL
- dm_db_missing_index_group_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_group_stats dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_group_stats dynamic management view
ms.assetid: c2886986-9e07-44ea-a350-feeac05ee4f4
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4ff5c898645b240431147a7513b232c8b5f919b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbmissingindexgroupstats-transact-sql"></a>sys.dm_db_missing_index_group_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Zusammenfassungsinformationen zu Gruppen fehlender Indizes, außer räumliche Indizes, zurück.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf die Datenbankkapselung auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert.  
    
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**group_handle**|**int**|Identifiziert eine Gruppe fehlender Indizes. Dieser Bezeichner ist innerhalb des Servers eindeutig.<br /><br /> Die anderen Spalten stellen Informationen zu allen Abfragen bereit, für die der Index in der Gruppe als fehlend betrachtet wird.<br /><br /> Eine Indexgruppe enthält nur einen Index.|  
|**unique_compiles**|**bigint**|Anzahl der Kompilierungen und Neukompilierungen, die von dieser Gruppe fehlender Indizes profitieren würden. Zu diesem Spaltenwert können Kompilierungen und Neukompilierungen vieler verschiedener Abfragen beitragen.|  
|**user_seeks**|**bigint**|Die Anzahl von durch Benutzerabfragen verursachten Suchvorgängen, für die der empfohlene Index in der Gruppe hätte verwendet werden können.|  
|**user_scans**|**bigint**|Die Anzahl von durch Benutzerabfragen verursachten Scanvorgängen, für die der empfohlene Index in der Gruppe hätte verwendet werden können.|  
|**last_user_seek**|**datetime**|Das Datum und die Uhrzeit des letzten durch Benutzerabfragen verursachten Suchvorgangs, für den der empfohlene Index in der Gruppe hätte verwendet werden können.|  
|**last_user_scan**|**datetime**|Das Datum und die Uhrzeit des letzten durch Benutzerabfragen verursachten Scanvorgangs, für den der empfohlene Index in der Gruppe hätte verwendet werden können.|  
|**avg_total_user_cost**|**float**|Die durchschnittlichen Kosten der Benutzerabfragen, die durch den Index in der Gruppe reduziert werden könnten.|  
|**avg_user_impact**|**float**|Durchschnittlicher prozentualer Nutzen, der für Benutzerabfragen entstünde, wenn diese Gruppe fehlender Indizes implementiert würde. Der Wert bedeutet, dass die Abfragekosten durchschnittlich um diesen Prozentsatz verringert würden, wenn diese Gruppe fehlender Indizes implementiert würde.|  
|**system_seeks**|**bigint**|Die Anzahl von durch Systemabfragen, beispielsweise Auto Stats-Abfragen, verursachten Suchvorgängen, für die der empfohlene Index in der Gruppe hätte verwendet werden können. Weitere Informationen finden Sie unter [Auto Stats-Ereignisklasse](../../relational-databases/event-classes/auto-stats-event-class.md).|  
|**system_scans**|**bigint**|Die Anzahl von durch Systemabfragen verursachten Scanvorgängen, für die der empfohlene Index in der Gruppe hätte verwendet werden können.|  
|**last_system_seek**|**datetime**|Das Datum und die Uhrzeit des letzten durch Systemabfragen verursachten Systemsuchvorgangs, für den der empfohlene Index in der Gruppe hätte verwendet werden können.|  
|**last_system_scan**|**datetime**|Das Datum und die Uhrzeit des letzten durch Systemabfragen verursachten Systemscanvorgangs, für den der empfohlene Index in der Gruppe hätte verwendet werden können.|  
|**avg_total_system_cost**|**float**|Die durchschnittlichen Kosten der Systemabfragen, die durch den Index in der Gruppe reduziert werden könnten.|  
|**avg_system_impact**|**float**|Durchschnittlicher prozentualer Nutzen, der für Systemabfragen entstünde, wenn diese Gruppe fehlender Indizes implementiert würde. Der Wert bedeutet, dass die Abfragekosten durchschnittlich um diesen Prozentsatz verringert würden, wenn diese Gruppe fehlender Indizes implementiert würde.|  
  
## <a name="remarks"></a>Hinweise  
 Zurückgegebene Informationen **dm_db_missing_index_group_stats** aktualisiert werden bei jeder abfrageausführung, nicht bei jeder Abfragekompilierung oder Neukompilierung. Statistiken zur Verwendung sind nicht persistent und werden nur bis zum Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beibehalten. Datenbankadministratoren sollten regelmäßig Sicherungskopien der Informationen zu fehlenden Indizes erstellen, wenn Sie die Verwendungsstatistiken nach dem Wiederverwenden des Servers beibehalten möchten.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Abfragen dieser dynamischen Verwaltungssicht muss den Benutzern die VIEW SERVER STATE-Berechtigung oder eine Berechtigung, die die VIEW SERVER STATE-Berechtigung impliziert, erteilt werden.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen, wie Sie die **dm_db_missing_index_group_stats** -verwaltungssicht.  
  
### <a name="a-find-the-10-missing-indexes-with-the-highest-anticipated-improvement-for-user-queries"></a>A. Suchen der 10 fehlenden Indizes mit der größten zu erwartenden Verbesserung für Benutzerabfragen  
 Mit der folgenden Abfrage werden in absteigender Reihenfolge die 10 fehlenden Indizes bestimmt, die die größte zu erwartende Gesamtverbesserung für Benutzerabfragen bewirken würden.  
  
```  
SELECT TOP 10 *  
FROM sys.dm_db_missing_index_group_stats  
ORDER BY avg_total_user_cost * avg_user_impact * (user_seeks + user_scans)DESC;  
```  
  
### <a name="b-find-the-individual-missing-indexes-and-their-column-details-for-a-particular-missing-index-group"></a>B. Suchen der einzelnen fehlenden Indizes und ihrer Spaltendetails für eine bestimmte Gruppe fehlender Indizes  
 Mit der folgenden Abfrage werden die fehlenden Indizes bestimmt, aus denen eine bestimmte Gruppe fehlender Indizes besteht, und deren Spaltendetails angezeigt. Für dieses Beispiel lautet das Handle der Gruppe fehlender Indizes 24.  
  
```  
SELECT migs.group_handle, mid.*  
FROM sys.dm_db_missing_index_group_stats AS migs  
INNER JOIN sys.dm_db_missing_index_groups AS mig  
    ON (migs.group_handle = mig.index_group_handle)  
INNER JOIN sys.dm_db_missing_index_details AS mid  
    ON (mig.index_handle = mid.index_handle)  
WHERE migs.group_handle = 24;  
```  
  
 Die Abfrage stellt den Namen der Datenbank, des Schemas und der Tabelle bereit, für die ein Index fehlt. Außerdem werden die Namen der Spalten zurückgegeben, die für den Indexschlüssel verwendet werden sollten. Beim Schreiben der CREATE INDEX-DDL-Anweisung zum Implementieren fehlender Indizes Listen Spalten für Gleichheit zuerst und dann ungleichheitsspalten in der ON \< *Table_name*>-Klausel der CREATE INDEX-Anweisung. Eingeschlossene Spalten sollten in der INCLUDE-Klausel der CREATE INDEX-Anweisung aufgeführt werden. Für eine effektive Reihenfolge der Gleichheitsspalten sortieren Sie sie nach ihrer Selektivität, wobei die selektivsten Spalten zuerst (am weitesten links in der Spaltenliste) aufgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
