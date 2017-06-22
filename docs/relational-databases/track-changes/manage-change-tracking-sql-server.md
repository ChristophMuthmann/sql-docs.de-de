---
title: "Verwalten der Änderungsnachverfolgung (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tracking data changes [SQL Server]
- change tracking [SQL Server], overhead
- change tracking [SQL Server]
- change tracking [SQL Server], managing
ms.assetid: 94a8d361-e897-4d6d-9a8f-1bb652e7a850
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6a29f384995058da7b4beef3edc3dac37e3e616
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="manage-change-tracking-sql-server"></a>Verwalten der Änderungsnachverfolgung (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Änderungsnachverfolgung verwaltet wird. Außerdem werden die Vorgehensweisen zum Konfigurieren der Sicherheit und zum Ermitteln der Auswirkungen der Änderungsnachverfolgung auf Speicherung und Leistung beschrieben.  
  
## <a name="managing-change-tracking"></a>Verwalten der Änderungsnachverfolgung  
 In den nachfolgenden Abschnitten sind Katalogsichten, Berechtigungen und Einstellungen aufgeführt, die für die Verwaltung der Änderungsnachverfolgung relevant sind.  
  
### <a name="catalog-views"></a>Katalogsichten  
 Zur Festlegung, für welche Tabellen und Datenbanken die Änderungsnachverfolgung aktiviert ist, können Sie die folgenden Katalogsichten verwenden:  
  
-   [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)  
  
-   [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
 Zusätzlich werden in der [sys.internal_tables](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) -Katalogsicht die internen Tabellen aufgeführt, die bei aktivierter Änderungsnachverfolgung für eine Benutzertabelle erstellt werden.  
  
### <a name="security"></a>Sicherheit  
 Für den Zugriff auf Änderungsnachverfolgungsinformationen mit den [Änderungsnachverfolgungsfunktionen](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)muss der Prinzipal über die folgenden Berechtigungen verfügen:  
  
-   SELECT-Berechtigung mindestens für die wichtigsten Schlüsselspalten der änderungsnachverfolgten Tabelle zur abgefragten Tabelle.  
  
-   VIEW CHANGE TRACKING-Berechtigung für die Tabelle, für die Änderungen abgerufen werden. Die VIEW CHANGE TRACKING-Berechtigung ist aus folgenden Gründen erforderlich:  
  
    -   Datensätze der Änderungsnachverfolgung beinhalten Informationen zu gelöschten Zeilen, insbesondere zu den Primärschlüsselwerten der gelöschten Zeilen. Einem Prinzipal kann die SELECT-Berechtigung für eine änderungsnachverfolgte Tabelle erteilt worden sein, nachdem einige vertrauliche Daten gelöscht wurden. In diesem Fall sollte der Prinzipal nicht mit der Änderungsnachverfolgung auf die gelöschten Informationen zugreifen können.  
  
    -   Änderungsnachverfolgungsinformationen können Informationen darüber enthalten, welche Spalten mit Updatevorgängen geändert wurden. Einem Prinzipal kann die Berechtigung für eine Spalte verweigert werden, die vertrauliche Informationen enthält. Da jedoch Änderungsnachverfolgungsinformationen verfügbar sind, kann der Prinzipal weiterhin feststellen, dass ein Spaltenwert aktualisiert wurde, aber er kann den Wert der Spalte nicht ermitteln.  
  
## <a name="understanding-change-tracking-overhead"></a>Grundlegendes zum Aufwand der Änderungsnachverfolgung  
 Wenn die Änderungsnachverfolgung für eine Tabelle aktiviert ist, wirkt sich dies auf einige Verwaltungsvorgänge aus. In der folgenden Tabelle sind die Vorgänge und Auswirkungen aufgeführt, die Sie berücksichtigen sollten.  
  
|Vorgang|Aktivierte Änderungsnachverfolgung|  
|---------------|-------------------------------------|  
|DROP TABLE|Alle Änderungsnachverfolgungsinformationen für die gelöschte Tabelle werden entfernt.|  
|ALTER TABLE DROP CONSTRAINT|Ein Versuch, die PRIMARY KEY-Einschränkung zu löschen, schlägt fehl. Die Änderungsnachverfolgung muss deaktiviert werden, damit eine PRIMARY KEY-Einschränkung gelöscht werden kann.|  
|ALTER TABLE DROP COLUMN|Ist eine gelöschte Spalte Bestandteil des Primärschlüssels, kann die Spalte nicht gelöscht werden, unabhängig von der Änderungsnachverfolgung.<br /><br /> Ist die gelöschte Spalte kein Bestandteil des Primärschlüssels, kann die Spalte gelöscht werden. Es sollte jedoch zuerst die Auswirkung auf eine beliebige Anwendung, die diese Daten synchronisiert, verstanden werden. Ist die Spaltenänderungsnachverfolgung für die Tabelle aktiviert, kann die Spalte trotzdem als Bestandteil der Änderungsnachverfolgungsinformationen zurückgegeben werden. Die Anwendung ist für die Behandlung der gelöschten Spalte zuständig.|  
|ALTER TABLE ADD COLUMN|Wird der änderungsnachverfolgten Tabelle eine neue Spalte hinzugefügt, wird das Hinzufügen der Spalte nicht verfolgt. Nur die Updates und Änderungen, die an der neuen Spalte vorgenommen werden, werden nachverfolgt.|  
|ALTER TABLE ALTER COLUMN|Datentypänderungen einer Nicht-Primärschlüsselspalte werden nicht nachverfolgt.|  
|ALTER TABLE SWITCH|Der Partitionswechsel schlägt fehl, wenn für eine oder beide Tabellen die Änderungsnachverfolgung aktiviert ist.|  
|DROP INDEX oder ALTER INDEX DISABLE|Der Index, der den Primärschlüssel erzwingt, kann nicht gelöscht oder deaktiviert werden.|  
|TRUNCATE TABLE|Das Abschneiden einer Tabelle kann für eine Tabelle ausgeführt werden, für die die Änderungsnachverfolgung aktiviert ist. Die mit dem Vorgang gelöschten Zeilen werden von dem Vorgang jedoch nicht nachverfolgt, und die minimale gültige Version wird aktualisiert. Führt eine Anwendung eine Versionsprüfung durch, ergibt die Prüfung, dass die Version zu alt ist und dass eine erneute Initialisierung erforderlich ist. Dies ist identisch mit der Deaktivierung der Änderungsnachverfolgung und der anschließenden erneuten Aktivierung für die Tabelle.|  
  
 Die Verwendung der Änderungsnachverfolgung führt aufgrund der Änderungsnachverfolgungsinformationen, die im Rahmen des Vorgangs gespeichert werden, zu erhöhtem Aufwand für DML-Vorgänge.  
  
### <a name="effects-on-dml"></a>Auswirkungen auf DML  
 Die Änderungsnachverfolgung wurde optimiert, um den Verwaltungsaufwand für DML-Vorgänge zu minimieren. Der mit der Verwendung der Änderungsnachverfolgung für eine Tabelle verbundene schrittweise Verwaltungsaufwand ist mit dem Aufwand vergleichbar, der entsteht, wenn ein Index für eine Tabelle erstellt wird und beibehalten werden muss.  
  
 Für jede mit einem DML-Vorgang geänderte Zeile wird der internen Änderungsnachverfolgungstabelle eine Zeile hinzugefügt. Die Auswirkung dieses Vorgangs hängt von verschiedenen Faktoren ab, wie z. B. Folgendem:  
  
-   Anzahl der Primärschlüsselspalten  
  
-   In der Benutzertabellenzeile geänderte Datenmenge  
  
-   Anzahl der Vorgänge, die in einer Transaktion ausgeführt werden  
  
 Die Verwendung der Momentaufnahmeisolation wirkt sich auch auf die Leistung für alle DML-Vorgänge aus, unabhängig davon, ob die Änderungsnachverfolgung aktiviert ist oder nicht.  
  
### <a name="effects-on-storage"></a>Auswirkungen auf die Speicherung  
 Änderungsnachverfolgungsdaten werden in den folgenden Typen von internen Tabellen gespeichert:  
  
-   Interne Änderungstabelle  
  
     Es gibt eine interne Änderungstabelle für jede Benutzertabelle, für die die Änderungsnachverfolgung aktiviert ist.  
  
-   Interne Transaktionstabelle  
  
     Es gibt eine interne Transaktionstabelle für die Datenbank.  
  
 Diese internen Tabellen beeinflussen die Speicheranforderungen folgendermaßen:  
  
-   Für jede Änderung einer Zeile in der Benutzertabelle wird der internen Änderungstabelle eine Zeile hinzugefügt. Diese Zeile verfügt über einen geringen festen Aufwand zuzüglich eines variablen Aufwands entsprechend der Größe der Primärschlüsselspalten. Die Zeile kann optionale, von einer Anwendung festgelegte Kontextinformationen enthalten. Wenn Spaltennachverfolgung aktiviert ist, werden für jede geänderte Spalte 4 Byte in der Nachverfolgungstabelle benötigt.  
  
-   Für jede Transaktion, für die ein Commit ausgeführt wurde, wird einer internen Transaktionstabelle eine Zeile hinzugefügt.  
  
 Wie bei anderen internen Tabellen auch können Sie den für die Änderungsnachverfolgungstabelle verwendeten Speicher mit der gespeicherten Prozedur [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) festlegen. Die Namen der internen Tabellen können mit der [sys.internal_tables](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) -Katalogsicht abgerufen werden, wie im nachfolgenden Beispiel dargestellt.  
  
```tsql  
sp_spaceused 'sys.change_tracking_309576141'  
sp_spaceused 'sys.syscommittab'  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Datenbankeigenschaften &#40;ChangeTracking-Seite&#41;](../../relational-databases/databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)   
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Informationen zur Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [Arbeiten mit Änderungsdaten &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  

