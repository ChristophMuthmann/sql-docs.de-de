---
title: "'SQL Server:Als veraltet markierte Funktionen'-Objekt | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:Deprecated Features
- performance counters [SQL Server], deprecated features
- deprecation [SQL Server], performance counters
- Deprecated Features object
ms.assetid: e95de9d6-c950-41cd-8aaa-be529c6de198
caps.latest.revision: "61"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 336fea7b5f3ea9fec4dc559933477086f4cca5ed
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-deprecated-features-object"></a>'SQL Server:Als veraltet markierte Funktionen'-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Das „SQLServer:Als veraltet markierte Funktionen“-Objekt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt einen Leistungsindikator bereit, um die als veraltet gekennzeichneten Funktionen zu überwachen. In jedem Fall stellt der Leistungsindikator einen Verwendungszähler bereit, der angibt, wie oft die veraltete Funktion seit dem letzten Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gefunden wurde.  
  
 Die Werte dieser Indikatoren sind auch durch Ausführung folgender Anweisung verfügbar:  
  
```  
SELECT * FROM sys.dm_os_performance_counters   
WHERE object_name = 'SQLServer:Deprecated Features';  
```  

In der folgenden Tabelle wird das SQL Server-Leistungsobjekt **Als veraltet markierte Funktionen** beschrieben.

|**SQL Server-Leistungsindikator „Als veraltet markierte Funktionen“**|Description|  
|-------------|-----------------|  
|**Verwendung**|Funktionsverwendung seit letztem SQL Server-Start.|
  
 In der folgenden Tabelle werden die Instanzen des „SQL Server:Als veraltet markierte Funktionen“-Leistungsindikators beschrieben.  
  
|'SQL Server:Als veraltet markierte Funktionen'-Leistungsindikatorinstanzen|Description|  
|------------------------------------------------------|-----------------|  
|'#' und '##' als Namen von temporären Tabellen und gespeicherten Prozeduren|Ein Bezeichner wurde gefunden, der keine anderen Zeichen als # enthielt. Verwenden Sie mindestens ein zusätzliches Zeichen. Tritt einmal pro Kompilierung auf.|  
|Funktionsaufrufsyntax '::'|Für eine Tabellenwertfunktion wurde die Funktionsaufrufsyntax :: gefunden. Ersetzen Sie die Syntax durch `SELECT column_list FROM` *<Funktionsname>*`()`. Ersetzen Sie beispielsweise `SELECT * FROM ::fn_virtualfilestats(2,1)` durch `SELECT * FROM sys.fn_virtualfilestats(2,1)`. Tritt einmal pro Kompilierung auf.|  
|'@' und Namen, die mit '@@' beginnen, als [!INCLUDE[tsql](../../includes/tsql-md.md)] -Bezeichner|Ein Bezeichner wurde gefunden, der mit @ oder @@ beginnt. @ oder @@ oder Namen, die mit @@ beginnen, dürfen nicht als Bezeichner verwendet werden. Tritt einmal pro Kompilierung auf.|  
|ADDING TAPE DEVICE|Die veraltete Funktionen sp_addumpdevice '**tape**' wurde gefunden. Verwenden Sie stattdessen sp_addumpdevice '**disk**'. Tritt einmal pro Verwendung auf.|  
|ALL-Berechtigung|Gesamtanzahl der gefundenen Vorkommnisse der Syntax GRANT ALL, DENY ALL oder REVOKE ALL. Ändern Sie die Syntax, um einzelne Berechtigungen zu widerrufen. Tritt einmal pro Abfrage auf.|  
|ALTER DATABASE WITH TORN_PAGE_DETECTION|Gesamtanzahl der Verwendungen der veralteten Funktion – der TORN_PAGE_DETECTION-Option von ALTER DATABASE – seit dem Start der Serverinstanz. Verwenden Sie stattdessen die Syntax PAGE_VERIFY. Tritt einmal pro Verwendung in einer DDL-Anweisung auf.|  
|ALTER LOGIN WITH SET CREDENTIAL|Die veraltete Funktionssyntax ALTER LOGIN WITH SET CREDENTIAL oder ALTER LOGIN WITH NO CREDENTIAL wurde gefunden. Verwenden Sie stattdessen die Syntax ADD oder DROP CREDENTIAL. Tritt einmal pro Kompilierung auf.|  
|Azeri_Cyrilllic_90|Ereignis tritt einmal pro Datenbankstart und einmal pro Sortierungsverwendung auf. Planen Sie, Anwendungen zu ändern, die diese Sortierung verwenden.|  
|Azeri_Latin_90|Ereignis tritt einmal pro Datenbankstart und einmal pro Sortierungsverwendung auf. Planen Sie, Anwendungen zu ändern, die diese Sortierung verwenden.|  
|BACKUP DATABASE oder LOG TO TAPE|Die veraltete Funktion BACKUP {DATABASE &#124; LOG} TO TAPE oder BACKUP {DATABASE &#124; LOG} TO *device_that_is_a_tape* wurde gefunden.<br /><br /> Verwenden Sie stattdessen BACKUP {DATABASE &#124; LOG} TO DISK oder BACKUP {DATABASE &#124; LOG} TO *device_that_is_a_disk*. Tritt einmal pro Verwendung auf.|  
|BACKUP DATABASE oder LOG WITH MEDIAPASSWORD|Die veraltete Funktion BACKUP DATABASE WITH MEDIAPASSWORD oder BACKUP LOG WITH MEDIAPASSWORD wurde gefunden. WITH MEDIAPASSWORD darf nicht verwendet werden.|  
|BACKUP DATABASE oder LOG WITH PASSWORD|Die veraltete Funktion BACKUP DATABASE WITH PASSWORD oder BACKUP LOG WITH PASSWORD wurde gefunden. WITH PASSWORD darf nicht verwendet werden.|  
|COMPUTE [BY]|Die Syntax COMPUTE oder COMPUTE BY wurde gefunden. Schreiben Sie die Abfrage um, um GROUP BY mit ROLLUP zu verwenden. Tritt einmal pro Kompilierung auf.|  
|CREATE FULLTEXT CATLOG IN PATH|Eine CREATE FULLTEXT CATLOG-Anweisung mit der IN PATH-Klausel wurde gefunden. Diese Klausel hat in dieser Version von SQL Server keinerlei Auswirkungen. Tritt einmal pro Verwendung auf.|  
|CREATE TRIGGER WITH APPEND|Eine CREATE TRIGGER-Anweisung mit der WITH APPEND-Klausel wurde gefunden. Erstellen Sie stattdessen den ganzen Trigger neu. Tritt einmal pro Verwendung in einer DDL-Anweisung auf.|  
|CREATE_DROP_DEFAULT|Die Syntax CREATE DEFAULT oder DROP DEFAULT wurde gefunden. Schreiben Sie den Befehl unter Verwendung der DEFAULT-Option von CREATE TABLE oder ALTER TABLE um. Tritt einmal pro Kompilierung auf.|  
|CREATE_DROP_RULE|Die Syntax CREATE RULE wurde gefunden. Schreiben Sie den Befehl unter Verwendung von Einschränkungen um. Tritt einmal pro Kompilierung auf.|  
|Datentypen: 'text', 'ntext' oder 'image'|Ein **Text**-, **Ntext**- oder **Image** -Datentyp wurde gefunden. Schreiben Sie Anwendungen so um, dass der Datentyp **varchar(max)** verwendet und die Datentypsyntax **text**, **ntext**und **image** entfernt wird. Tritt einmal pro Abfrage auf.|  
||Die Gesamtzahl der Änderungen des Kompatibilitätsgrads einer Datenbank auf den Wert 80. Planen Sie, vor der nächsten Version die Datenbank und die Anwendung zu aktualisieren. Tritt auch auf, wenn eine Datenbank mit dem Kompatibilitätsgrad 80 gestartet wird.|  
|Datenbank-Kompatibilitätsgrad 100, 110. 120|Die Gesamtzahl der Änderungen des Kompatibilitätsgrads einer Datenbank. Planen Sie, in einer zukünftigen Version die Datenbank und die Anwendung zu aktualisieren. Tritt auch auf, wenn eine Datenbank mit veraltetem Kompatibilitätsgrad gestartet wird.|  
|DATABASE_MIRRORING|Es wurden Verweise für die Datenbankspiegelungsfunktion gefunden. Planen Sie, auf Always On-Verfügbarkeitsgruppen zu aktualisieren. Planen Sie alternativ, zu Protokollversand zu migrieren, wenn Sie eine Edition von SQL Server ausführen, die Always On-Verfügbarkeitsgruppen nicht unterstützt.|  
|database_principal_aliases|Verweise auf die veraltete Funktion sys.database_principal_aliases wurden gefunden. Verwenden Sie anstelle von Aliasen Rollen. Tritt einmal pro Kompilierung auf.|  
|DATABASEPROPERTY|Eine Anweisung hat auf DATABASEPROPERTY verwiesen. Aktualisieren Sie die Anweisung DATABASEPROPERTY auf DATABASEPROPERTYEX. Tritt einmal pro Kompilierung auf.|  
|DATABASEPROPERTYEX('IsFullTextEnabled')|Eine Anweisung hat auf die IsFullTextEnabled-Eigenschaft der Funktion DATABASEPROPERTYEX verwiesen. Der Wert dieser Eigenschaft hat keine Auswirkungen. In Benutzerdatenbanken ist die Volltextsuche standardmäßig aktiviert. Verwenden Sie diese Eigenschaft nicht. Tritt einmal pro Kompilierung auf.|  
|DBCC [UN]PINTABLE|Die Anweisung DBCC PINTABLE oder DBCC UNPINTABLE wurde gefunden. Diese Anweisung hat keine Auswirkungen und sollte entfernt werden. Tritt einmal pro Abfrage auf.|  
|DBCC DBREINDEX|Die Anweisung DBCC DBREINDEX wurde gefunden. Schreiben Sie die Anweisung so um, dass sie die REBUILD-Option von ALTER INDEX verwendet. Tritt einmal pro Abfrage auf.|  
|DBCC INDEXDEFRAG|Die Anweisung DBCC INDEXDEFRAG wurde gefunden. Schreiben Sie die Anweisung so um, dass sie die REORGANIZE-Option von ALTER INDEX verwendet. Tritt einmal pro Abfrage auf.|  
|DBCC SHOWCONTIG|Die Anweisung DBCC SHOWCONTIG wurde gefunden. Fragen Sie sys.dm_db_index_physical_stats nach diesen Informationen ab. Tritt einmal pro Abfrage auf.|  
|DEFAULT-Schlüsselwort als Standardwert|Syntax, die das DEFAULT-Schlüsselwort als Standardwert verwendet, wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Kompilierung auf.|  
|Veralteter Verschlüsselungsalgorithmus|Der veraltete Verschlüsselungsalgorithmus rc4 wird in der nächsten Version von SQL Server entfernt. Nutzen Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie eine Änderung von Anwendungen, in denen sie aktuell verwendet wird. Der RC4-Algorithmus ist schwach und wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höher kann mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden.|  
|Veralteter Hashalgorithmus|Verwenden Sie die MD2-, MD4-, MD5-, SHA- oder SHA1-Algorithmen.|  
|DESX-Algorithmus|Syntax, die den DESX-Verschlüsselungsalgorithmus verwendet, wurde gefunden. Verwenden Sie einen anderen Algorithmus für die Verschlüsselung. Tritt einmal pro Kompilierung auf.|  
|dm_fts_active_catalogs|Der dm_fts_active_catalogs-Leistungsindikator bleibt immer auf dem Wert 0, da einige Spalten der sys.dm_fts_active_catalogs-Sicht nicht als veraltet markiert werden. Um eine veraltete Spalte zu überwachen, verwenden Sie den spaltenspezifischen Leistungsindikator, wie z.B. dm_fts_active_catalogs.is_paused.|  
|dm_fts_active_catalogs.is_paused|Die is_paused-Spalte der dynamischen Verwaltungssicht [sys.dm_fts_active_catalogs](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md) wurde gefunden. Vermeiden Sie die Verwendung dieser Spalte. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|dm_fts_active_catalogs.previous_status|Die previous_status-Spalte der dynamischen Verwaltungssicht sys.dm_fts_active_catalogs wurde gefunden. Vermeiden Sie die Verwendung dieser Spalte. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|dm_fts_active_catalogs.previous_status_description|Die previous_status_description-Spalte der dynamischen Verwaltungssicht sys.dm_fts_active_catalogs wurde gefunden. Vermeiden Sie die Verwendung dieser Spalte. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|dm_fts_active_catalogs.row_count_in_thousands|Die row_count_in_thousands-Spalte der dynamischen Verwaltungssicht sys.dm_fts_active_catalogs wurde gefunden. Vermeiden Sie die Verwendung dieser Spalte. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|dm_fts_active_catalogs.status|Die status-Spalte der dynamischen Verwaltungssicht sys.dm_fts_active_catalogs wurde gefunden. Vermeiden Sie die Verwendung dieser Spalte. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|dm_fts_active_catalogs.status_description|Die status_description-Spalte der dynamischen Verwaltungssicht sys.dm_fts_active_catalogs wurde gefunden. Vermeiden Sie die Verwendung dieser Spalte. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|dm_fts_active_catalogs.worker_count|Die worker_count-Spalte der dynamischen Verwaltungssicht sys.dm_fts_active_catalogs wurde gefunden. Vermeiden Sie die Verwendung dieser Spalte. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|dm_fts_memory_buffers|Der dm_fts_memory_buffers-Leistungsindikator bleibt immer auf dem Wert 0, da die meisten Spalten der sys.dm_fts_memory_buffers-Sicht nicht als veraltet markiert werden. Um die veraltete Spalte zu überwachen, verwenden Sie den spaltenspezifischen Leistungsindikator: dm_fts_memory_buffers.row_count.|  
|dm_fts_memory_buffers.row_count|Die row_count-Spalte der dynamischen Verwaltungssicht [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md) wurde gefunden. Vermeiden Sie die Verwendung dieser Spalte. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|DROP INDEX mit zweiteiligem Namen|Die DROP INDEX-Syntax enthielt die Formatsyntax *table_name.index_name* in DROP INDEX. Ersetzen Sie die Syntax in der DROP INDEX-Anweisung durch die Syntax *index_name* ON *table_name* . Tritt einmal pro Kompilierung auf.|  
|EXT_CREATE_ALTER_SOAP_ENDPOINT|Die CREATE- oder ALTER ENDPOINT-Anweisung mit der FOR SOAP-Option wurde gefunden. Systemeigene XML-Webdienste sind als veraltet markiert. Verwenden Sie stattdessen Windows Communications Foundation (WCF) oder ASP.NET.|  
|EXT_endpoint_webmethods|sys.endpoint_webmethods wurde gefunden. Systemeigene XML-Webdienste sind als veraltet markiert. Verwenden Sie stattdessen Windows Communications Foundation (WCF) oder ASP.NET.|  
|EXT_soap_endpoints|sys.soap_endpoints wurde gefunden. Systemeigene XML-Webdienste sind als veraltet markiert. Verwenden Sie stattdessen Windows Communications Foundation (WCF) oder ASP.NET.|  
|EXTPROP_LEVEL0TYPE|TYPE wurde unter einem level0type gefunden. Verwenden Sie SCHEMA anstelle von level0type und TYPE anstelle von level1type. Tritt einmal pro Abfrage auf.|  
|EXTPROP_LEVEL0USER|Es wurde level0type mit dem Wert USER verwendet und auch ein level1type festgelegt. Verwenden Sie nur USER anstelle von level0type für erweiterte Eigenschaften direkt für einen Benutzer. Tritt einmal pro Abfrage auf.|  
|FASTFIRSTROW|Die Syntax FASTFIRSTROW wurde gefunden. Schreiben Sie die Anweisungen so um, dass sie die Syntax OPTION (FAST *n*) verwenden. Tritt einmal pro Kompilierung auf.|  
|FILE_ID|Die Syntax FILE_ID wurde gefunden. Schreiben Sie die Anweisungen so um, dass sie FILE_IDEX verwenden. Tritt einmal pro Kompilierung auf.|  
|fn_get_sql|Die fn_get_sql-Funktion wurde kompiliert. Verwenden Sie stattdessen sys.dm_exec_sql_text. Tritt einmal pro Kompilierung auf.|  
|fn_servershareddrives|Die fn_servershareddrives-Funktion wurde kompiliert. Verwenden Sie stattdessen sys.dm_io_cluster_shared_drives. Tritt einmal pro Kompilierung auf.|  
|fn_virtualservernodes|Die fn_virtualservernodes-Funktion wurde kompiliert. Verwenden Sie stattdessen sys.dm_os_cluster_nodes. Tritt einmal pro Kompilierung auf.|  
|fulltext_catalogs|Der fulltext_catalogs-Leistungsindikator bleibt immer auf dem Wert 0, da einige Spalten der sys.fulltext_catalogs-Sicht nicht als veraltet markiert werden. Um eine veraltete Spalte zu überwachen, verwenden Sie deren spaltenspezifischen Leistungsindikator, wie z.B. fulltext_catalogs.data_space_id. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|fulltext_catalogs.data_space_id|Die data_space_id-Spalte der [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) -Katalogsicht wurde gefunden. Verwenden Sie diese Spalte nicht. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|fulltext_catalogs.file_id|Die file_id-Spalte der sys.fulltext_catalogs-Katalogsicht wurde gefunden. Verwenden Sie diese Spalte nicht. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|fulltext_catalogs.path|Die path-Spalte der sys.fulltext_catalogs-Katalogsicht wurde gefunden. Verwenden Sie diese Spalte nicht. Tritt jedes Mal auf, wenn die Serverinstanz einen Verweis auf die Spalte erkennt.|  
|FULLTEXTCATALOGPROPERTY('LogSize')|Die LogSize-Eigenschaft der FULLTEXTCATALOGPROPERTY-Funktion wurde gefunden. Vermeiden Sie die Verwendung dieser Eigenschaft.|  
|FULLTEXTCATALOGPROPERTY('PopulateStatus')|Die PopulateStatus-Eigenschaft der FULLTEXTCATALOGPROPERTY-Funktion wurde gefunden. Vermeiden Sie die Verwendung dieser Eigenschaft.|  
|FULLTEXTSERVICEPROPERTY('ConnectTimeout')|Die ConnectTimeout-Eigenschaft der FULLTEXTSERVICEPROPERTY-Funktion wurde gefunden. Vermeiden Sie die Verwendung dieser Eigenschaft.|  
|FULLTEXTSERVICEPROPERTY('DataTimeout')|Die DataTimeout-Eigenschaft der FULLTEXTSERVICEPROPERTY-Funktion wurde gefunden. Vermeiden Sie die Verwendung dieser Eigenschaft.|  
|FULLTEXTSERVICEPROPERTY('ResourceUsage')|Die ResourceUsage-Eigenschaft der FULLTEXTSERVICEPROPERTY-Funktion wurde gefunden. Vermeiden Sie die Verwendung dieser Eigenschaft.|  
|GROUP BY ALL|Gesamtanzahl der gefundenen Vorkommnisse der Syntax GROUP BY ALL. Ändern Sie die Syntax, um nach einzelnen Tabellen zu gruppieren.|  
|Hindi|Ereignis tritt einmal pro Datenbankstart und einmal pro Sortierungsverwendung auf. Planen Sie, Anwendungen zu ändern, die diese Sortierung verwenden. Verwenden Sie stattdessen Indic_General_90.|  
|HOLDLOCK-Tabellenhinweis ohne Klammern||  
|IDENTITYCOL|Die Syntax INDENTITYCOL wurde gefunden. Schreiben Sie die Anweisungen so um, dass sie die $identity-Syntax verwenden. Tritt einmal pro Kompilierung auf.|  
|Indexsicht-Auswahlliste ohne COUNT_BIG(\*)|Die Auswahlliste einer indizierten Aggregatsicht muss den Wert COUNT_BIG (\*) enthalten.|  
|INDEX_OPTION|CREATE TABLE-, ALTER TABLE- oder CREATE INDEX-Syntax ohne Klammern um die Optionen gefunden. Schreiben Sie Anweisung so um, dass sie die aktuelle Syntax verwendet. Tritt einmal pro Abfrage auf.|  
|INDEXKEY_PROPERTY|Die Syntax INDEXKEY_PROPERTY wurde gefunden. Schreiben Sie die Anweisungen so um, dass sie sys.index_columns abfragen. Tritt einmal pro Kompilierung auf.|  
|Indirekte TVF-Hinweise|Das indirekte Anwenden von Tabellenhinweisen auf einen Aufruf einer Tabellenwertfunktion (Table Valued Function, TVF) mit mehreren Anweisungen über eine Sicht wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht mehr unterstützt.|  
|INSERT NULL in TIMESTAMP-Spalten|Ein NULL-Wert wurde in eine TIMESTAMP-Spalte eingefügt. Verwenden Sie stattdessen einen Standardwert. Tritt einmal pro Kompilierung auf.|  
|INSERT_HINTS||  
|Korean_Wansung_Unicode|Ereignis tritt einmal pro Datenbankstart und einmal pro Sortierungsverwendung auf. Planen Sie, Anwendungen zu ändern, die diese Sortierung verwenden.|  
|Lithuanian_Classic|Ereignis tritt einmal pro Datenbankstart und einmal pro Sortierungsverwendung auf. Planen Sie, Anwendungen zu ändern, die diese Sortierung verwenden.|  
|Macedonian|Ereignis tritt einmal pro Datenbankstart und einmal pro Sortierungsverwendung auf. Planen Sie, Anwendungen zu ändern, die diese Sortierung verwenden. Verwenden Sie stattdessen Macedonian_FYROM_90.|  
|MODIFY FILEGROUP READONLY|Die Syntax MODIFY FILEGROUP READONLY wurde gefunden. Schreiben Sie die Anweisungen so um, dass sie die READ_ONLY-Syntax verwenden. Tritt einmal pro Kompilierung auf.|  
|MODIFY FILEGROUP READWRITE|Die Syntax MODIFY FILEGROUP READWRITE wurde gefunden. Schreiben Sie die Anweisungen so um, dass sie die READ_WRITE-Syntax verwenden. Tritt einmal pro Kompilierung auf.|  
|Mehr als zweiteiliger Spaltenname|Eine Abfrage hat in der Spaltenliste einen drei- oder vierteiligen Namen verwendet. Ändern Sie die Abfrage so, dass sie die mit dem Standard kompatiblen zweiteiligen Namen verwendet. Tritt einmal pro Kompilierung auf.|  
|Mehrere Tabellenhinweise ohne Komma|Als Trennzeichen zwischen Tabellenhinweisen wurde ein Leerzeichen verwendet. Verwenden Sie stattdessen ein Komma. Tritt einmal pro Kompilierung auf.|  
|NOLOCK oder READUNCOMMITTED in UPDATE oder DELETE|In der FROM-Klausel einer UPDATE- oder DELETE-Anweisung wurden NOLOCK oder READUNCOMMITTED gefunden. Entfernen Sie die NOLOCK- oder READUNCOMMITTED-Tabellenhinweise aus der FROM-Klausel.|  
|Nicht-ANSI-Operatoren '*=' oder '=\* ' für äußere Joins|Eine Anweisung, die die Joinsyntax '*=' oder '=\* ' verwendet, wurde gefunden. Schreiben Sie Anweisung so um, dass sie die ANSI-Joinsyntax verwendet. Tritt einmal pro Kompilierung auf.|  
|numbered_stored_procedures||  
|numbered_procedure_parameters|Verweise auf die veraltete Funktionsys.numbered_procedure_parameters wurden gefunden. Darf nicht verwendet werden. Tritt einmal pro Kompilierung auf.|  
|numbered_procedures|Verweise auf die veraltete Funktionsys.numbered_procedures wurden gefunden. Darf nicht verwendet werden. Tritt einmal pro Kompilierung auf.|  
|Veraltete RAISEERROR-Syntax|Die veraltete RAISERROR-Syntax (Format: RAISERROR integer string) wurde gefunden. Schreiben Sie Anweisung unter Verwendung der aktuellen RAISERROR-Syntax um. Tritt einmal pro Kompilierung auf.|  
|OLEDB für Ad-hoc-Verbindungen|SQLOLEDB wird nicht als Anbieter unterstützt. Verwenden Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client für Ad-hoc-Verbindungen.|  
|PERMISSIONS|Verweise auf die systeminterne PERMISSIONS-Funktion wurden gefunden. Fragen Sie stattdessen sys.fn_my_permissions ab. Tritt einmal pro Abfrage auf.|  
|ProcNums|Die veraltete ProcNums-Syntax wurde gefunden. Schreiben Sie die Anweisungen um, um die Verweise zu entfernen. Tritt einmal pro Kompilierung auf.|  
|READTEXT|Die Syntax READTEXT wurde gefunden. Schreiben Sie Anwendungen so um, dass der Datentyp **varchar(max)** verwendet und die Datentypsyntax **text** entfernt wird. Tritt einmal pro Abfrage auf.|  
|RESTORE DATABASE oder LOG WITH DBO_ONLY|Die RESTORE ... WITH DBO_ONLY-Syntax wurde gefunden. Verwenden Sie die RESTORE ... RESTRICTED_USER-Syntax.|  
|RESTORE DATABASE oder LOG WITH MEDIAPASSWORD|Die RESTORE ... WITH MEDIAPASSWORD-Syntax wurde gefunden. WITH MEDIAPASSWORD bietet keine hohe Sicherheit und sollte entfernt werden.|  
|RESTORE DATABASE oder LOG WITH PASSWORD|Die RESTORE ... WITH PASSWORD-Syntax wurde gefunden. WITH PASSWORD bietet keine hohe Sicherheit und sollte entfernt werden.|  
|Zurückgeben von Ergebnissen aus Triggern|Dieses Ereignis tritt einmal pro Triggeraufruf auf. Schreiben Sie den Trigger so um, dass er keine Resultsets zurückgibt.|  
|ROWGUIDCOL|Die Syntax ROWGUIDCOL wurde gefunden. Schreiben Sie die Anweisungen so um, dass sie die $rowguid-Syntax verwenden. Tritt einmal pro Kompilierung auf.|  
|SET ANSI_NULLS OFF|Die Syntax SET ANSI_NULLS OFF wurde gefunden. Entfernen Sie diese veraltete Syntax. Tritt einmal pro Kompilierung auf.|  
|SET ANSI_PADDING OFF|Die Syntax SET ANSI_PADDING OFF wurde gefunden. Entfernen Sie diese veraltete Syntax. Tritt einmal pro Kompilierung auf.|  
|SET CONCAT_NULL_YIELDS_NULL OFF|Die Syntax SET CONCAT_NULL_YIELDS_NULL OFF wurde gefunden. Entfernen Sie diese veraltete Syntax. Tritt einmal pro Kompilierung auf.|  
|SET DISABLE_DEF_CNST_CHK|Die Syntax SET DISABLE_DEF_CNST_CHK wurde gefunden. Diese Syntax hat keine Auswirkungen. Entfernen Sie diese veraltete Syntax. Tritt einmal pro Kompilierung auf.|  
|SET FMTONLY ON|Die Syntax SET FMTONLY wurde gefunden. Entfernen Sie diese veraltete Syntax. Tritt einmal pro Kompilierung auf.|  
|SET OFFSETS|Die Syntax SET OFFSETS wurde gefunden. Entfernen Sie diese veraltete Syntax. Tritt einmal pro Kompilierung auf.|  
|SET REMOTE_PROC_TRANSACTIONS|Die Syntax SET REMOTE_PROC_TRANSACTIONS wurde gefunden. Entfernen Sie diese veraltete Syntax. Verwenden Sie stattdessen Verbindungsserver und sp_serveroption.|  
|SET ROWCOUNT|In einer DELETE-, INSERT- oder UPDATE-Anweisung wurde die Syntax SET ROWCOUNT gefunden. Schreiben Sie die Anweisung unter Verwendung von TOP um. Tritt einmal pro Kompilierung auf.|  
|SETUSER|Die Anweisung SET USER wurde gefunden. Verwenden Sie stattdessen EXECUTE AS. Tritt einmal pro Abfrage auf.|  
|sp_addapprole|Die Prozedur sp_addapprole wurde gefunden. Verwenden Sie stattdessen CREATE APPLICATION ROLE. Tritt einmal pro Abfrage auf.|  
|sp_addextendedproc|Die Prozedur sp_addextendedproc wurde gefunden. Verwenden Sie stattdessen CLR. Tritt einmal pro Kompilierung auf.|  
|sp_addlogin|Die Prozedur sp_addlogin wurde gefunden. Verwenden Sie stattdessen CREATE LOGIN. Tritt einmal pro Abfrage auf.|  
|sp_addremotelogin|Die Prozedur sp_addremotelogin wurde gefunden. Verwenden Sie stattdessen Verbindungsserver.|  
|sp_addrole|Die Prozedur sp_addrole wurde gefunden. Verwenden Sie stattdessen CREATE ROLE. Tritt einmal pro Abfrage auf.|  
|sp_addserver|Die Prozedur sp_addserver wurde gefunden. Verwenden Sie stattdessen Verbindungsserver.|  
|sp_addtype|Die Prozedur sp_addtype wurde gefunden. Verwenden Sie stattdessen CREATE TYPE. Tritt einmal pro Kompilierung auf.|  
|sp_adduser|Die Prozedur sp_adduser wurde gefunden. Verwenden Sie stattdessen CREATE USER. Tritt einmal pro Abfrage auf.|  
|sp_approlepassword|Die Prozedur sp_approlepassword wurde gefunden. Verwenden Sie stattdessen ALTER APPLICATION ROLE. Tritt einmal pro Abfrage auf.|  
|sp_attach_db|Die Prozedur sp_attach_db wurde gefunden. Verwenden Sie stattdessen CREATE DATABASE FOR ATTACH. Tritt einmal pro Abfrage auf.|  
|sp_attach_single_file_db|Die Prozedur sp_single_file_db wurde gefunden. Verwenden Sie stattdessen CREATE DATABASE FOR ATTACH_REBUILD_LOG. Tritt einmal pro Abfrage auf.|  
|sp_bindefault|Die Prozedur sp_bindefault wurde gefunden. Verwenden Sie stattdessen das DEFAULT-Schlüsselwort von ALTER TABLE oder CREATE TABLE. Tritt einmal pro Kompilierung auf.|  
|sp_bindrule|Die Prozedur sp_bindrule wurde gefunden. Verwenden Sie stattdessen CHECK-Einschränkungen. Tritt einmal pro Kompilierung auf.|  
|sp_bindsession|Die Prozedur sp_bindsession wurde gefunden. Verwenden Sie stattdessen MARS (Multiple Active Results Sets) oder verteilte Transaktionen. Tritt einmal pro Kompilierung auf.|  
|sp_certify_removable|Die Prozedur sp_certify_removable wurde gefunden. Verwenden Sie stattdessen sp_detach_db. Tritt einmal pro Abfrage auf.|  
|sp_changeobjectowner|Die Prozedur sp_changeobjectowner wurde gefunden. Verwenden Sie stattdessen ALTER SCHEMA oder ALTER AUTHORIZATION. Tritt einmal pro Abfrage auf.|  
|sp_change_users_login|Die Prozedur sp_change_users_login wurde gefunden. Verwenden Sie stattdessen ALTER USER. Tritt einmal pro Abfrage auf.|  
|sp_configure 'allow updates'|Die „allow updates“-Option von sp_configure wurde gefunden. Systemtabellen sind nicht mehr aktualisierbar. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_configure 'disallow results from triggers'|Die „disallow results from triggers“-Option von sp_configure wurde gefunden. Um zu verhindern, dass Trigger Resultsets zurückgeben, legen Sie mit sp_configure die Option auf 1 fest. Tritt einmal pro Abfrage auf.|  
|sp_configure 'ft crawl bandwidth (max)'|Die „ft crawl bandwidth (max)“-Option von sp_configure wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_configure 'ft crawl bandwidth (min)'|Die „ft crawl bandwidth (min)“-Option von sp_configure wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_configure 'ft notify bandwidth (max)'|Die „ft notify bandwidth (max)“-Option von sp_configure wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_configure 'ft notify bandwidth (min)'|Die „ft notify bandwidth (min)“-Option von sp_configure wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_configure 'locks'|Die „locks“-Option von sp_configure wurde gefunden. Sperren sind nicht mehr konfigurierbar. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_configure 'open objects'|Die „open objects“-Option von sp_configure wurde gefunden. Die Anzahl geöffneter Objekte ist nicht mehr konfigurierbar. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_configure 'priority boost'|Die Option „priority boost“ von sp_configure wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf. Verwenden Sie stattdessen die start /high … program.exe-Option von Windows.|  
|sp_configure 'remote proc trans'|Die „remote proc trans“-Option von sp_configure wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_configure 'set working set size'|Die „set working set size“-Option von sp_configure wurde gefunden. Die Workingsetgröße ist nicht mehr konfigurierbar. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_control_dbmasterkey_password|Die gespeicherte Prozedur sp_control_dbmasterkey_password überprüft nicht, ob ein Hauptschlüssel vorhanden ist. Dies wird aus Gründen der Abwärtskompatibilität zugelassen, es wird jedoch eine Warnung angezeigt. Dieses Verhalten ist als veraltet markiert. In einer künftigen Version muss der Hauptschlüssel vorhanden sein, und das Kennwort, das in der gespeicherten Prozedur sp_control_dbmasterkey_password verwendet wird, muss einem der Kennwörter zum Verschlüsseln des Datenbank-Hauptschlüssels entsprechen.|  
|sp_create_removable|Die Prozedur sp_create_removable wurde gefunden. Verwenden Sie stattdessen CREATE DATABASE. Tritt einmal pro Abfrage auf.|  
|sp_db_vardecimal_storage_format|Die Verwendung des Speicherformats **vardecimal** wurde erkannt. Verwenden Sie stattdessen die Datenkomprimierung.|  
|sp_dbcmptlevel|Die Prozedur sp_dbcmptlevel wurde gefunden. Verwenden Sie ALTER DATABASE … SET COMPATIBILITY_LEVEL. Tritt einmal pro Abfrage auf.|  
|sp_dbfixedrolepermission|Die Prozedur sp_dbfixedrolepermission wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_dboption|Die Prozedur sp_dboption wurde gefunden. Verwenden Sie stattdessen ALTER DATABASE und DATABASEPROPERTYEX. Tritt einmal pro Kompilierung auf.|  
|sp_dbremove|Die Prozedur sp_dbremove wurde gefunden. Verwenden Sie stattdessen DROP DATABASE. Tritt einmal pro Abfrage auf.|  
|sp_defaultdb|Die Prozedur sp_defaultdb wurde gefunden. Verwenden Sie stattdessen ALTER LOGIN. Tritt einmal pro Kompilierung auf.|  
|sp_defaultlanguage|Die Prozedur sp_defaultlanguage wurde gefunden. Verwenden Sie stattdessen ALTER LOGIN. Tritt einmal pro Kompilierung auf.|  
|sp_denylogin|Die Prozedur sp_denylogin wurde gefunden. Verwenden Sie stattdessen ALTER LOGIN DISABLE. Tritt einmal pro Abfrage auf.|  
|sp_depends|Die Prozedur sp_depends wurde gefunden. Verwenden Sie stattdessen sys.dm_sql_referencing_entities und sys.dm_sql_referenced_entities. Tritt einmal pro Abfrage auf.|  
|sp_detach_db @keepfulltextindexfile|Das @keepfulltextindexfile-Argument wurde in einer sp_detach_db-Anweisung gefunden. Verwenden Sie dieses Argument nicht.|  
|sp_dropalias|Die Prozedur sp_dropalias wurde gefunden. Ersetzen Sie Aliase durch eine Kombination von Benutzerkonten und Datenbankrollen. Verwenden Sie sp_dropalias, um Aliase in aktualisierten Datenbanken zu entfernen. Tritt einmal pro Kompilierung auf.|  
|sp_dropapprole|Die Prozedur sp_dropapprole wurde gefunden. Verwenden Sie stattdessen DROP APPLICATION ROLE. Tritt einmal pro Abfrage auf.|  
|sp_dropextendedproc|Die Prozedur sp_dropextendedproc wurde gefunden. Verwenden Sie stattdessen CLR. Tritt einmal pro Kompilierung auf.|  
|sp_droplogin|Die Prozedur sp_droplogin wurde gefunden. Verwenden Sie stattdessen DROP LOGIN. Tritt einmal pro Abfrage auf.|  
|sp_dropremotelogin|Die Prozedur sp_dropremotelogin wurde gefunden. Verwenden Sie stattdessen Verbindungsserver.|  
|sp_droprole|Die Prozedur sp_droprole wurde gefunden. Verwenden Sie stattdessen DROP ROLE. Tritt einmal pro Abfrage auf.|  
|sp_droptype|Die Prozedur sp_droptype wurde gefunden. Verwenden Sie stattdessen DROP TYPE.|  
|sp_dropuser|Die Prozedur sp_dropuser wurde gefunden. Verwenden Sie stattdessen DROP USER. Tritt einmal pro Abfrage auf.|  
|sp_estimated_rowsize_reduction_for_vardecimal|Die Verwendung des Speicherformats **vardecimal** wurde erkannt. Verwenden Sie stattdessen Datenkomprimierung und sp_estimate_data_compression_savings.|  
|sp_fulltext_catalog|Die Prozedur sp_fulltext_catalog wurde gefunden. Verwenden Sie stattdessen CREATE/ALTER/DROP FULLTEXT CATALOG. Tritt einmal pro Kompilierung auf.|  
|sp_fulltext_column|Die Prozedur sp_fulltext_column wurde gefunden. Verwenden Sie stattdessen ALTER FULLTEXT INDEX. Tritt einmal pro Kompilierung auf.|  
|sp_fulltext_database|Die Prozedur sp_fulltext_database wurde gefunden. Verwenden Sie stattdessen ALTER DATABASE. Tritt einmal pro Kompilierung auf.|  
|Sp_fulltext_service @action= Clean_up|Die Option clean_up der Prozedur sp_fulltext_service wurde gefunden. Tritt einmal pro Abfrage auf.|  
|sp_fulltext_service @action=connect_timeout|Die Option connect_timeout der Prozedur sp_fulltext_service wurde gefunden. Tritt einmal pro Abfrage auf.|  
|sp_fulltext_service @action=data_timeout|Die Option data_timeout der Prozedur sp_fulltext_service wurde gefunden. Tritt einmal pro Abfrage auf.|  
|sp_fulltext_service @action=resource_usage|Die Option resource_usage der Prozedur sp_fulltext_service wurde gefunden. Diese Option hat keine Funktion. Tritt einmal pro Abfrage auf.|  
|sp_fulltext_table|Die Prozedur sp_fulltext_table wurde gefunden. Verwenden Sie stattdessen CREATE/ALTER/DROP FULLTEXT INDEX. Tritt einmal pro Kompilierung auf.|  
|sp_getbindtoken|Die Prozedur sp_getbindtoken wurde gefunden. Verwenden Sie stattdessen MARS (Multiple Active Results Sets) oder verteilte Transaktionen. Tritt einmal pro Kompilierung auf.|  
|sp_grantdbaccess|Die Prozedur sp_grantdbaccess wurde gefunden. Verwenden Sie stattdessen CREATE USER. Tritt einmal pro Abfrage auf.|  
|sp_grantlogin|Die Prozedur sp_grantlogin wurde gefunden. Verwenden Sie stattdessen CREATE LOGIN. Tritt einmal pro Abfrage auf.|  
|sp_help_fulltext_catalog_components|Die Prozedur sp_help_fulltext_catalog_components wurde gefunden. Diese Prozedur gibt leere Zeilen zurück. Verwenden Sie diese Prozedur nicht. Tritt einmal pro Kompilierung auf.|  
|sp_help_fulltext_catalogs|Die Prozedur sp_help_fulltext_catalogs wurde gefunden. Fragen Sie stattdessen sys.fulltext_catalogs ab. Tritt einmal pro Kompilierung auf.|  
|sp_help_fulltext_catalogs_cursor|Die Prozedur sp_help_fulltext_catalogs_cursor wurde gefunden. Fragen Sie stattdessen sys.fulltext_catalogs ab. Tritt einmal pro Kompilierung auf.|  
|sp_help_fulltext_columns|Die Prozedur sp_help_fulltext_columns wurde gefunden. Fragen Sie stattdessen sys.fulltext_index_columns ab. Tritt einmal pro Kompilierung auf.|  
|sp_help_fulltext_columns_cursor|Die Prozedur sp_help_fulltext_columns_cursor wurde gefunden. Fragen Sie stattdessen sys.fulltext_index_columns ab. Tritt einmal pro Kompilierung auf.|  
|sp_help_fulltext_tables|Die Prozedur sp_help_fulltext_tables wurde gefunden. Fragen Sie stattdessen sys.fulltext_indexes ab. Tritt einmal pro Kompilierung auf.|  
|sp_help_fulltext_tables_cursor|Die Prozedur sp_help_fulltext_tables_cursor wurde gefunden. Fragen Sie stattdessen sys.fulltext_indexes ab. Tritt einmal pro Kompilierung auf.|  
|sp_helpdevice|Die Prozedur sp_helpdevice wurde gefunden. Fragen Sie stattdessen sys.backup_devices ab. Tritt einmal pro Abfrage auf.|  
|sp_helpextendedproc|Die Prozedur sp_helpextendedproc wurde gefunden. Verwenden Sie stattdessen CLR. Tritt einmal pro Kompilierung auf.|  
|sp_helpremotelogin|Die Prozedur sp_helpremotelogin wurde gefunden. Verwenden Sie stattdessen Verbindungsserver.|  
|sp_indexoption|Die Prozedur sp_indexoption wurde gefunden. Verwenden Sie stattdessen ALTER INDEX. Tritt einmal pro Kompilierung auf.|  
|sp_lock|Die Prozedur sp_lock wurde gefunden. Fragen Sie stattdessen sys.dm_tran_locks ab. Tritt einmal pro Abfrage auf.|  
|sp_password|Die Prozedur sp_password wurde gefunden. Verwenden Sie stattdessen ALTER LOGIN. Tritt einmal pro Abfrage auf.|  
|sp_remoteoption|Die Prozedur sp_remoteoption wurde gefunden. Verwenden Sie stattdessen Verbindungsserver.|  
|sp_renamedb|Die Prozedur sp_renamedb wurde gefunden. Verwenden Sie stattdessen ALTER DATABASE. Tritt einmal pro Abfrage auf.|  
|sp_resetstatus|Die Prozedur sp_resetstatus wurde gefunden. Verwenden Sie stattdessen ALTER DATABASE. Tritt einmal pro Abfrage auf.|  
|sp_revokedbaccess|Die Prozedur sp_revokedbaccess wurde gefunden. Verwenden Sie stattdessen DROP USER. Tritt einmal pro Abfrage auf.|  
|sp_revokelogin|Die Prozedur sp_revokelogin wurde gefunden. Verwenden Sie stattdessen DROP LOGIN. Tritt einmal pro Abfrage auf.|  
|sp_srvrolepermission|Die veraltete Prozedur sp_srvrolepermission wurde gefunden. Darf nicht verwendet werden. Tritt einmal pro Abfrage auf.|  
|sp_unbindefault|Die Prozedur sp_unbindefault wurde gefunden. Verwenden Sie stattdessen das DEFAULT-Schlüsselwort in CREATE TABLE- oder ALTER TABLE-Anweisungen. Tritt einmal pro Kompilierung auf.|  
|sp_unbindrule|Die Prozedur sp_unbindrule wurde gefunden. Verwenden Sie anstelle von Regeln CHECK-Einschränkungen. Tritt einmal pro Kompilierung auf.|  
|SQL_AltDiction_CP1253_CS_AS|Ereignis tritt einmal pro Datenbankstart und einmal pro Sortierungsverwendung auf. Planen Sie, Anwendungen zu ändern, die diese Sortierung verwenden.|  
|Zeichenfolgenliterale als Spaltenaliase|Es wurde Syntax mit einer Zeichenfolge gefunden, die in einer SELECT-Anweisung als Spaltenalias verwendet wird, wie z. B. `'string' = expression`. Darf nicht verwendet werden. Tritt einmal pro Kompilierung auf.|  
|sys.sql_dependencies|Verweise auf sys.sql_dependencies wurden gefunden. Verwenden Sie stattdessen sys.sql_expression_dependencies. Tritt einmal pro Kompilierung auf.|  
|sysaltfiles|Verweise auf sysaltfiles wurden gefunden. Verwenden Sie stattdessen sys.master_files. Tritt einmal pro Kompilierung auf.|  
|syscacheobjects|Verweise auf syscacheobjects wurden gefunden. Verwenden Sie stattdessen sys.dm_exec_cached_plans, sys.dm_exec_plan_attributes und sys.dm_exec_sql_text. Tritt einmal pro Kompilierung auf.|  
|syscolumns|Verweise auf syscolumns wurden gefunden. Verwenden Sie stattdessen sys.columns. Tritt einmal pro Kompilierung auf.|  
|syscomments|Verweise auf syscomments wurden gefunden. Verwenden Sie stattdessen sys.sql_modules. Tritt einmal pro Kompilierung auf.|  
|sysconfigures|Verweise auf die sysconfigures-Tabelle wurden gefunden. Verweisen Sie stattdessen auf die sys.sysconfigures-Sicht. Tritt einmal pro Kompilierung auf.|  
|sysconstraints|Verweise auf sysconstraints wurden gefunden. Verwenden Sie stattdessen sys.check_constraints, sys.default_constraints, sys.key_constraints und sys.foreign_keys. Tritt einmal pro Kompilierung auf.|  
|syscurconfigs|Verweise auf syscurconfigs wurden gefunden. Verwenden Sie stattdessen sys.configurations. Tritt einmal pro Kompilierung auf.|  
|sysdatabases|Verweise auf sysdatabases wurden gefunden. Verwenden Sie stattdessen sys.databases. Tritt einmal pro Kompilierung auf.|  
|sysdepends|Verweise auf sysdepends wurden gefunden. Verwenden Sie stattdessen sys.sql_dependencies. Tritt einmal pro Kompilierung auf.|  
|sysdevices|Verweise auf sysdevices wurden gefunden. Verwenden Sie stattdessen sys.backup_devices. Tritt einmal pro Kompilierung auf.|  
|sysfilegroups|Verweise auf sysfilegroups wurden gefunden. Verwenden Sie stattdessen sys.filegroups. Tritt einmal pro Kompilierung auf.|  
|sysfiles|Verweise auf sysfiles wurden gefunden. Verwenden Sie stattdessen sys.database_files. Tritt einmal pro Kompilierung auf.|  
|sysforeignkeys|Verweise auf sysforeignkeys wurden gefunden. Verwenden Sie stattdessen sys.foreign_keys. Tritt einmal pro Kompilierung auf.|  
|sysfulltextcatalogs|Verweise auf sysfulltextcatalogs wurden gefunden. Verwenden Sie stattdessen sys.fulltext_catalogs. Tritt einmal pro Kompilierung auf.|  
|sysindexes|Verweise auf sysindexes wurden gefunden. Verwenden Sie stattdessen sys.indexes, sys.partitions, sys.allocation_units und sys.dm_db_partition_stats. Tritt einmal pro Kompilierung auf.|  
|sysindexkeys|Verweise auf sysindexkeys wurden gefunden. Verwenden Sie stattdessen sys.index_columns. Tritt einmal pro Kompilierung auf.|  
|syslockinfo|Verweise auf syslockinfo wurden gefunden. Verwenden Sie stattdessen sys.dm_tran_locks. Tritt einmal pro Kompilierung auf.|  
|syslogins|Verweise auf syslogins wurden gefunden. Verwenden Sie stattdessen sys.server_principals und sys.sql_logins. Tritt einmal pro Kompilierung auf.|  
|sysmembers|Verweise auf sysmembers wurden gefunden. Verwenden Sie stattdessen sys.database_role_members. Tritt einmal pro Kompilierung auf.|  
|sysmessages|Verweise auf sysmessages wurden gefunden. Verwenden Sie stattdessen sys.messages. Tritt einmal pro Kompilierung auf.|  
|sysobjects|Verweise auf sysobjects wurden gefunden. Verwenden Sie stattdessen sys.objects. Tritt einmal pro Kompilierung auf.|  
|sysoledbusers|Verweise auf sysoledbusers wurden gefunden. Verwenden Sie stattdessen sys.linked_logins. Tritt einmal pro Kompilierung auf.|  
|sysopentapes|Verweise auf sysopentapes wurden gefunden. Verwenden Sie stattdessen sys.dm_io_backup_tapes. Tritt einmal pro Kompilierung auf.|  
|sysperfinfo|Verweise auf sysperfinfo wurden gefunden. Verwenden Sie stattdessen sys.dm_os_performance_counters. stattdessen. Tritt einmal pro Kompilierung auf.|  
|syspermissions|Verweise auf syspermissions wurden gefunden. Verwenden Sie stattdessen sys.database_permissions und sys.server_permissions. Tritt einmal pro Kompilierung auf.|  
|sysprocesses|Verweise auf sysprocesses wurden gefunden. Verwenden Sie stattdessen sys.dm_exec_connections, sys.dm_exec_sessions und sys.dm_exec_requests. Tritt einmal pro Kompilierung auf.|  
|sysprotects|Verweise auf sysprotects wurden gefunden. Verwenden Sie stattdessen sys.database_permissions und sys.server_permissions. Tritt einmal pro Kompilierung auf.|  
|sysreferences|Verweise auf sysreferences wurden gefunden. Verwenden Sie stattdessen sys.foreign_keys. Tritt einmal pro Kompilierung auf.|  
|sysremotelogins|Verweise auf sysremotelogins wurden gefunden. Verwenden Sie stattdessen sys.remote_logins. Tritt einmal pro Kompilierung auf.|  
|sysservers|Verweise auf sysservers wurden gefunden. Verwenden Sie stattdessen sys.servers. Tritt einmal pro Kompilierung auf.|  
|systypes|Verweise auf systypes wurden gefunden. Verwenden Sie stattdessen sys.types. Tritt einmal pro Kompilierung auf.|  
|sysusers|Verweise auf sysusers wurden gefunden. Verwenden Sie stattdessen sys.database_principals. Tritt einmal pro Kompilierung auf.|  
|Tabellenhinweis ohne WITH|Eine Anweisung wurde gefunden, die Tabellenhinweise verwendet, jedoch nicht das WITH-Schlüsselwort. Ändern Sie Anweisungen so, dass sie das Wort WITH einschließen. Tritt einmal pro Kompilierung auf.|  
|Tabellenoption 'text in row'|Verweise auf die Tabellenoption text in row wurden gefunden. Verwenden Sie stattdessen die „large value types out of row“-Option von sp_tableoption. Tritt einmal pro Abfrage auf.|  
|TEXTPTR|Verweise auf die TEXTPTR-Funktion wurden gefunden. Schreiben Sie Anwendungen so um, dass der Datentyp **varchar(max)** verwendet und die Datentypsyntax **text**, **ntext**und **image** entfernt wird. Tritt einmal pro Abfrage auf.|  
|TEXTVALID|Verweise auf die TEXTVALID-Funktion wurden gefunden. Schreiben Sie Anwendungen so um, dass der Datentyp **varchar(max)** verwendet und die Datentypsyntax **text**, **ntext**und **image** entfernt wird. Tritt einmal pro Abfrage auf.|  
|timestamp|Gesamtanzahl der gefundenen Vorkommnisse des veralteten **timestamp** -Datentyps in einer DDL-Anweisung. Verwenden Sie stattdessen den **rowversion** -Datentyp .|  
|UPDATETEXT oder WRITETEXT|Die UPDATETEXT- oder WRITETEXT-Anweisung wurde gefunden. Schreiben Sie Anwendungen so um, dass der Datentyp **varchar(max)** verwendet und die Datentypsyntax **text**, **ntext**und **image** entfernt wird. Tritt einmal pro Abfrage auf.|  
|USER_ID|Verweise auf die USER_ID-Funktion wurden gefunden. Verwenden Sie stattdessen die DATABASE_PRINCIPAL_ID-Funktion. Tritt einmal pro Kompilierung auf.|  
|Verwenden von OLEDB für Verbindungsserver||  
|Vardecimal-Speicherformat|Die Verwendung des Speicherformats **vardecimal** wurde erkannt. Verwenden Sie stattdessen die Datenkomprimierung.|  
|XMLDATA|Die Syntax FOR XML wurde gefunden. Verwenden Sie XSD-Generierung für RAW- und AUTO-Modus. Es gibt keinen Ersatz für den expliziten Modus. Tritt einmal pro Kompilierung auf.|  
|XP_API|Eine Anweisung einer erweiterten gespeicherten Prozedur wurde gefunden. Darf nicht verwendet werden.|  
|xp_grantlogin|Die Prozedur xp_grantlogin wurde gefunden. Verwenden Sie stattdessen CREATE LOGIN. Tritt einmal pro Kompilierung auf.|  
|xp_loginconfig|Die Prozedur xp_loginconfig wurde gefunden. Verwenden Sie stattdessen das IsIntegratedSecurityOnly-Argument von SERVERPROPERTY. Tritt einmal pro Abfrage auf.|  
|xp_revokelogin|Die Prozedur xp_revokelogin wurde gefunden. Verwenden Sie stattdessen ALTER LOGIN DISABLE oder DROP LOGIN. Tritt einmal pro Kompilierung auf.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Als veraltet markierte Funktionen des Datenbankmoduls in SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Als veraltet markierte Funktionen der Volltextsuche in SQL Server 2016](../../relational-databases/search/deprecated-full-text-search-features-in-sql-server-2016.md)   
 [Deprecation Announcement-Ereignisklasse](../../relational-databases/event-classes/deprecation-announcement-event-class.md)   
 [Deprecation Final Support (Ereignisklasse)](../../relational-databases/event-classes/deprecation-final-support-event-class.md)   
 [Nicht mehr unterstützte Datenbankmodul-Funktionalität in SQL Server 2016](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Nicht mehr unterstützte Funktionen der Volltextsuche in SQL Server 2016](http://msdn.microsoft.com/library/70587b3c-cc77-4681-924d-a1df7cdf1517)   
 [Verwenden von SQL Server-Objekten](../../relational-databases/performance-monitor/use-sql-server-objects.md)  
  
  
