---
title: Verwalten von FileTables | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: blob
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], security
- FileTables [SQL Server], managing access
ms.assetid: 93af982c-b4fe-4be0-8268-11f86dae27e1
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e59931627ce7c22ccb799f048f04bc77edd49fec
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="manage-filetables"></a>Verwalten von FileTables
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Beschreibt allgemeine administrative Tasks zum Verwalten von FileTables.  
  
##  <a name="HowToEnumerate"></a> Vorgehensweise: Abrufen einer Liste von FileTables und verbundenen Objekten  
 Um eine Liste von FileTables abzurufen, fragen Sie eine der folgenden Katalogsichten ab:  
  
-   [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
  
-   [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) (Überprüfen Sie den Wert der **is_filetable**-Spalte.)  
  
```sql  
SELECT * FROM sys.filetables;  
GO  
  
SELECT * FROM sys.tables WHERE is_filetable = 1;  
GO  
```  
  
 Um eine Liste der systemdefinierten Objekte abzurufen, die bei der Erstellung der zugeordneten FileTables erstellt wurden, fragen Sie die Katalogsicht [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md) ab.  
  
```sql  
SELECT object_id, OBJECT_NAME(object_id) AS 'Object Name'  
FROM sys.filetable_system_defined_objects;  
GO  
```  
  
##  <a name="BasicsDisabling"></a> Deaktivieren und erneutes Aktivieren von nicht transaktionalem Zugriff auf Datenbankebene  
 Um den exklusiven Zugriff zu erhalten, der für bestimmte administrative Tasks erforderlich ist, müssen Sie möglicherweise nicht transaktionalen Zugriff vorübergehend deaktivieren.  
  
 **Verhalten der ALTER DATABASE-Anweisung beim Ändern der Ebene von nicht transaktionalem Zugriff**  
  
-   Wenn Sie nicht transaktionalen Zugriff auf READ_ONLY oder OFF festgelegt haben, gibt der ALTER DATABASE-Befehl kein Steuerelement an den Benutzer zurück, solange offene Dateihandles vorhanden sind, die mit dem angeforderten Vorgang in Konflikt stehen. Bei folgenden Dateihandles treten Konflikte mit diesem Vorgang auf:  
  
    -   Bei allen offenen Dateihandles beim Festlegen des Zugriffs auf **NONE**.  
  
    -   Alle offenen Dateihandles für Schreibzugriff beim Festlegen des Zugriffs auf **READ_ONLY**.  
  
     Informationen zum Abbrechen von offenen Dateihandles finden Sie unter [Abbrechen von einer FileTable zugeordneten offenen Dateihandles](#BasicsKilling) .  
  
     Wenn der ALTER DATABASE-Befehl abgebrochen wird oder mit einem Timeout endet, wird die Ebene des transaktionalen Zugriffs nicht geändert.  
  
-   Wenn Sie die ALTER DATABASE-Anweisung mit einer WITH-\<Termination>-Klausel aufrufen (ROLLBACK AFTER integer [ SECONDS ] | ROLLBACK IMMEDIATE | NO_WAIT), werden alle geöffneten nicht transaktionalen Dateihandles abgebrochen.  
  
> [!WARNING]  
>  Durch das Abbrechen geöffneter Dateihandles verlieren Benutzer möglicherweise nicht gespeicherte Daten. Dieses Verhalten ist mit dem Verhalten des Dateisystems selbst konsistent.  
  
 **Auswirkungen des Deaktivierens von nicht transaktionalem Zugriff**  
  
 Das Ändern der Ebene von nicht transaktionalem Zugriff auf Datenbankebene hat die folgenden Auswirkungen auf die FileTable-Verzeichnisse unter dem Verzeichnis auf Datenbankebene:  
  
-   Wenn der Zugriff auf **NONE**festgelegt ist, kann auf alle FileTable-Verzeichnisse und ihre Inhalte nicht mehr zugegriffen werden. Zudem sind sie nicht mehr sichtbar.  
  
-   Wenn der Zugriff auf **READ_ONLY**festgelegt ist, sind alle FileTable-Verzeichnisse und ihre Inhalte ebenfalls schreibgeschützt.  
  
 Das Deaktivieren von FILESTREAM auf Instanzebene hat die folgenden Auswirkungen auf Verzeichnisse auf Datenbankebene in dieser Instanz und die FileTable-Verzeichnisse darunter:  
  
-   Keines der Verzeichnisse auf Datenbankebene auf der Instanz ist sichtbar, wenn FILESTREAM auf Instanzebene deaktiviert ist.  
  
###  <a name="HowToDisable"></a> Vorgehensweise: Deaktivieren und erneutes Aktivieren von nicht transaktionalem Zugriff auf Datenbankebene  
 Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 **So deaktivieren Sie vollständigen nicht transaktionalen Zugriff**  
 Rufen Sie die **ALTER DATABASE** -Anweisung auf, und legen Sie den Wert von **NON_TRANSACTED_ACCESS** auf **READ_ONLY** oder **OFF**fest.  
  
```sql  
-- Disable write access.  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = READ_ONLY );  
GO  
  
-- Disable non-transactional access.  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = OFF );  
GO  
```  
  
 **So aktivieren Sie vollständigen nicht transaktionalen Zugriff erneut**  
 Rufen Sie die **ALTER DATABASE** -Anweisung auf, und legen Sie den Wert von **NON_TRANSACTED_ACCESS** auf **FULL**fest.  
  
```sql  
ALTER DATABASE database_name  
SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL );  
GO  
```  
  
###  <a name="visible"></a> Vorgehensweise: Sicherstellen der Sichtbarkeit der FileTables in einer Datenbank  
 Ein Verzeichnis auf Datenbankebene und die FileTable-Verzeichnisse darunter sind sichtbar, wenn alle folgenden Bedingungen zutreffen:  
  
1.  FILESTREAM ist auf Instanzebene aktiviert.  
  
2.  Nicht transaktionaler Zugriff ist auf Datenbankebene aktiviert.  
  
3.  Ein gültiges Verzeichnis wurde auf Datenbankebene angegeben.  
  
##  <a name="BasicsEnabling"></a> Deaktivieren und erneutes Aktivieren des FileTable-Namespaces auf Tabellenebene  
 Durch Deaktivieren des FileTable-Namespaces werden alle systemdefinierten Einschränkungen und Trigger deaktiviert, die mit der FileTable erstellt wurden. Dies ist in Situationen hilfreich, in denen eine FileTable in großem Umfang mit [!INCLUDE[tsql](../../includes/tsql-md.md)] -Vorgängen ohne den Aufwand der FileTable-Semantikerzwingung neu organisiert werden müssen. Durch diese Vorgänge kann die FileTable jedoch in einem inkonsistenten Status belassen werden, und das erneute Aktivieren des FileTable-Namespaces kann verhindert werden.  
  
 Das Deaktivieren eines FileTable-Namespaces führt zu folgenden Ergebnissen:  
  
-   FileTable-Spalten und -Daten werden nicht physisch aus der Tabelle gelöscht.  
  
-   Das FileTable-Verzeichnis und die enthaltenen Dateien und Verzeichnisse verschwinden aus dem Dateisystem und sind für Datei-E/A-Zugriff nicht verfügbar.  
  
-   Systemdefinierte FileTable-Spalten können nicht gelöscht und neu erstellt werden, sie verhalten sich jedoch bei DML-Vorgängen wie normale Spalten.  
  
-   Offene Dateihandles verhindern, dass die FileTable-Einschränkungen deaktiviert werden, da für diesen Vorgang eine Schemasperre für die Tabelle erforderlich ist.  
  
-   Die Erzwingung der gesamten FileTable-Semantik, einschließlich systemdefinierter Einschränkungen und Trigger, wird nach dem Deaktivieren des FileTable-Namespaces beendet.  
  
 Das erneute Aktivieren eines FileTable-Namespaces führt zu folgenden Ergebnissen:  
  
-   Die FileTable wird auf Konsistenz überprüft. Werden Inkonsistenzen festgestellt, wird ein Fehler ausgelöst, und die FileTable bleibt deaktiviert. Andernfalls wird die FileTable erneut aktiviert.  
  
-   Die Erzwingung der FileTable-Semantik, einschließlich systemdefinierter Einschränkungen und Trigger, wird wiederhergestellt.  
  
-   Das FileTable-Verzeichnis und die enthaltenen Dateien und Verzeichnisse werden im Dateisystem sichtbar und stehen zum Datei-E/A-Zugriff zur Verfügung.  
  
###  <a name="HowToEnableNS"></a> Vorgehensweise: Deaktivieren und erneutes Aktivieren des FileTable-Namespaces auf Tabellenebene  
 Rufen Sie die ALTER TABLE-Anweisung mit der Option **{ ENABLE | DISABLE } FILETABLE_NAMESPACE** auf.  
  
 **So deaktivieren Sie den FileTable-Namespace**  
 ```sql  
ALTER TABLE filetable_name  
DISABLE FILETABLE_NAMESPACE;  
GO  
```  
  
 **So aktivieren Sie den FileTable-Namespace erneut**  
 ```sql  
ALTER TABLE filetable_name  
ENABLE FILETABLE_NAMESPACE;  
GO  
```  
  
##  <a name="BasicsKilling"></a> Abbrechen von einer FileTable zugeordneten offenen Dateihandles  
 Durch das Öffnen von Handles für Dateien, die in einer FileTable gespeichert sind, kann der exklusive Zugriff verhindert werden, der für bestimmte administrative Tasks erforderlich ist. Um dringende Tasks zu aktivieren, müssen Sie möglicherweise geöffnete Dateihandles, die einer oder mehreren FileTables zugeordnet sind, abbrechen.  
  
> [!WARNING]  
>  Durch das Abbrechen geöffneter Dateihandles verlieren Benutzer möglicherweise nicht gespeicherte Daten. Dieses Verhalten ist mit dem Verhalten des Dateisystems selbst konsistent.  
  
###  <a name="HowToListOpen"></a> Vorgehensweise: Abrufen einer Liste von einer FileTable zugeordneten offenen Dateihandles  
 Rufen Sie die Katalogsicht [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md) ab.  
  
```sql  
SELECT * FROM sys.dm_filestream_non_transacted_handles;  
GO  
```  
  
###  <a name="HowToKill"></a> Vorgehensweise: Abbrechen von einer FileTable zugeordneten offenen Dateihandles  
 Rufen Sie die gespeicherte Prozedur [sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md) mit den entsprechenden Argumenten auf, um alle offenen Dateihandles in der Datenbank oder FileTable oder ein bestimmtes Handle abzubrechen.  
  
```sql  
USE database_name;  
  
-- Kill all open handles in all the filetables in the database.  
EXEC sp_kill_filestream_non_transacted_handles;  
GO  
  
-- Kill all open handles in a single filetable.  
EXEC sp_kill_filestream_non_transacted_handles @table_name = 'filetable_name';  
GO  
  
-- Kill a single handle.  
EXEC sp_kill_filestream_non_transacted_handles @handle_id = integer_handle_id;  
GO  
```  
  
###  <a name="HowToIdentifyLocks"></a> Vorgehensweise: Identifizieren der von FileTables abgehaltenen Sperren  
 Die meisten von FileTables abgehaltenen Sperren entsprechen Dateien, die von Anwendungen geöffnet wurden.  
  
 **So identifizieren Sie geöffnete Dateien und die zugeordneten Sperren**  
 Verknüpfen Sie das **request_owner_id**-Feld in der dynamischen Verwaltungssicht [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) mit dem **fcb_id**-Feld in [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md). In einigen Fällen entspricht die Sperre nicht einem einzigen geöffneten Dateihandle.  
  
```sql  
SELECT opened_file_name  
FROM sys.dm_filestream_non_transacted_handles  
WHERE fcb_id IN  
    ( SELECT request_owner_id FROM sys.dm_tran_locks );  
GO  
```  
  
##  <a name="BasicsSecurity"></a> FileTable-Sicherheit  
 Die in FileTables gespeicherten Dateien und Verzeichnisse werden nur von SQL Server-Sicherheit gesichert. Tabellen- und spaltenbasierte Sicherheit wird für Dateisystemzugriff sowie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff erzwungen. Windows-Dateisystemsicherheits-APIs und ACL-Einstellungen werden nicht unterstützt.  
  
 Die für FILESTREAM-Dateigruppen und -Container geltenden Sicherheits- und Zugriffsberechtigungen gelten auch für FileTables, da die Dateidaten als FILESTREAM-Spalte in der FileTable gespeichert werden.  
  
 **FileTable-Sicherheit und Transact-SQL-Zugriff**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] Zugriff auf Daten in FileTables wird auf dieselbe Weise wie eine beliebige andere Tabelle gesichert. Entsprechende Sicherheitsüberprüfungen auf Tabellen- und Spaltenebene werden für alle Vorgänge ausgeführt, die auf die Daten zugreifen oder sie ändern.  
  
 **FileTable-Sicherheit und Dateisystemzugriff**  
 Zum Öffnen eines Handles für eine Datei oder ein Verzeichnis, die bzw. das in der FileTable gespeichert ist, sind für Dateisystem-APIs entsprechende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Berechtigungen für die gesamte Zeile in der FileTable (Tabellenebenenberechtigung) erforderlich. Wenn der Benutzer nicht über die entsprechende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Berechtigung für eine Spalte in der FileTable verfügt, wird der Dateisystemzugriff verweigert.  
  
##  <a name="OtherBackup"></a> Sicherung und FileTables  
 Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Sichern einer FileTable verwenden, werden die FILESTREAM-Daten zusammen mit den strukturierten Daten in der Datenbank gesichert Wenn Sie die FILESTREAM-Daten nicht zusammen mit relationalen Daten sichern möchten, können Sie eine Teilsicherung durchführen, um die FILESTREAM-Dateigruppen auszuschließen.  
  
 **Transaktionskonsistenz von FileTable-Sicherungen**  
  
 Viele Verwaltungsprogramme und Vorgänge (einschließlich Sicherung, Protokollsicherung und Transaktionsreplikation) lesen transaktional konsistente Daten, indem sie die Transaktionsprotokolle lesen. Derzeit werden als Teil einer Transaktion alle aktualisierten FILESTREAM-Daten gelesen. Wenn nicht transaktionaler Zugriff nicht auf Datenbankebene aktiviert ist, arbeiten diese Programme und Vorgänge mit vollständiger Transaktionskonsistenz.  
  
 Wenn jedoch vollständiger nicht transaktionaler Zugriff aktiviert ist, könnte eine FileTable Daten enthalten, die später aktualisiert wurden (über ein nicht transaktionales Update) als die Transaktion, die das Programm oder der Prozess aus dem Transaktionsprotokoll liest. Das heißt, dass eine Wiederherstellung einer bestimmten Transaktion zu einem bestimmten Zeitpunkt FILESTREAM-Daten enthalten kann, die aktueller als die betreffende Transaktion sind. Dies ist das erwartete Verhalten, wenn nicht transaktionale Updates in FileTables zulässig sind.  
  
##  <a name="Monitor"></a> SQL Server Profiler und FileTables  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler kann Vorgänge zum Öffnen und Schließen von Dateien in Windows in der Ablaufverfolgungsausgabe für in einer FileTable gespeicherte Dateien aufzeichnen.  
  
##  <a name="OtherAuditing"></a> Überwachung und FileTables  
 Eine FileTable kann genau wie jede andere Tabelle überwacht werden. Win32-Zugriffsmuster sind jedoch keine satzbasierten Vorgänge. Eine einzelne Aktion im Dateisystem wird in mehrere Transact-SQL-DML-Vorgänge umgesetzt. Das Öffnen einer Datei in Microsoft Word wird beispielsweise in mehrere open/close/create/rename/delete-Vorgänge und entsprechende Transact-SQL-DML-Aktivitäten umgesetzt. Dies führt zu ausführlichen Überwachungsdatensätzen in Situationen, in denen es schwierig ist, Datensätze zwischen Dateisystemaktionen und entsprechenden Transact-SQL-DML-Überwachungsdatensätzen zu korrelieren.  
  
##  <a name="OtherDBCC"></a> DBCC und FileTables  
 Sie können die Einschränkungen für eine FileTable, einschließlich systemdefinierter Einschränkungen, mithilfe von DBCC CHECKCONSTRAINTS überprüfen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [FileTable-Kompatibilität mit anderen SQL Server-Funktionen](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)   
 [FileTable-DDL, Funktionen, gespeicherte Prozeduren und Sichten](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
