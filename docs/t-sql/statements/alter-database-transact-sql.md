---
title: ALTER DATABASE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b8e96cad90ff94b1f4e8f110d13b87668809606f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert eine Datenbank bzw. die zu dieser Datenbank gehörenden Dateien und Dateigruppen. Fügt einer Datenbank Dateien und Dateigruppen hinzu oder entfernt diese, ändert die Attribute einer Datenbank oder ihrer Dateien und Dateigruppen, ändert die Datenbanksortierung und legt Datenbankoptionen fest. Datenbankmomentaufnahmen können nicht geändert werden. Verwenden Sie zum Ändern von Datenbankoptionen für die Replikation [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
   
 Aufgrund seiner Länge wird die ALTER DATABASE-Syntax in folgende Themen aufgeteilt:  
  
 ALTER DATABASE  
 Das aktuelle Thema behandelt die Syntax zum Ändern des Namens und der Sortierung einer Datenbank.  
  
 [ALTER DATABASE-Optionen für Dateien und Dateigruppen](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
 Stellt die Syntax zum Hinzufügen und Entfernen von Dateien und Dateigruppen in einer Datenbank sowie zum Ändern der Datei- und Dateigruppenattribute bereit.  
  
 [ALTER DATABASE SET-Optionen](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
 Stellt die Syntax zum Ändern der Datenbankattribute mithilfe der SET-Optionen von ALTER DATABASE bereit.  
  
 [ALTER DATABASE-Datenbankspiegelung](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)  
 Stellt die Syntax für die SET-Optionen von ALTER DATABASE bereit, die sich auf die Datenbankspiegelung beziehen.  
  
 [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)  
 Stellt die Syntax der ALTER DATABASE-Optionen für [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] zum Konfigurieren einer sekundären Datenbank auf einem sekundären Replikat einer Always On-Verfügbarkeitsgruppe bereit.  
  
 [ALTER DATABASE-Kompatibilitätsgrad](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
 Stellt die Syntax für die SET-Optionen von ALTER DATABASE in Bezug auf die Kompatibilitätsgrade von Datenbanken bereit.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
Informationen zu Azure SQL-Datenbank finden Sie unter [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md).  
Informationen zu Azure SQL Data Warehouse finden Sie unter [ALTER DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
Informationen zu Parallel Data Warehouse finden Sie unter [ALTER DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).
  
## <a name="syntax"></a>Syntax  
  
```  
-- SQL Server Syntax  
ALTER DATABASE { database_name  | CURRENT }  
{  
    MODIFY NAME = new_database_name   
  | COLLATE collation_name  
  | <file_and_filegroup_options>  
  | <set_database_options>  
}  
[;]  
  
<file_and_filegroup_options >::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  
  
<set_database_options>::=  
  <optionspec>::=   
  <auto_option> ::=   
  <change_tracking_option> ::=  
  <cursor_option> ::=   
  <database_mirroring_option> ::=   
  <date_correlation_optimization_option> ::=  
  <db_encryption_option> ::=  
  <db_state_option> ::=  
  <db_update_option> ::=  
  <db_user_access_option> ::=  <delayed_durability_option> ::=  <external_access_option> ::=  
  <FILESTREAM_options> ::=  
  <HADR_options> ::=    
  <parameterization_option> ::=  
  <query_store_options> ::=  
  <recovery_option> ::=   
  <service_broker_option> ::=  
  <snapshot_option> ::=  
  <sql_option> ::=   
  <termination> ::=  
  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll.  
  
> [!NOTE]  
>  Diese Option ist in einer eigenständigen Datenbank nicht verfügbar.  
  
 CURRENT  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Legt fest, dass die zurzeit verwendete Datenbank geändert werden soll.  
  
 MODIFY NAME **=***new_database_name*  
 Benennt die Datenbank in den angegebenen Namen *new_database_name* um.  
  
 COLLATE *collation_name*  
 Gibt die Sortierung für die Datenbank an. *collation_name* kann entweder der Name einer Windows-Sortierung oder ein SQL-Sortierungsname sein. Wenn keine Sortierung angegeben ist, wird der Datenbank die Sortierung der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugewiesen.  
  
 Beim Erstellen von Datenbanken mit einer von der Standardsortierung abweichenden Sortierung folgen die Daten in der Datenbank immer der angegebenen Sortierung. Bei der Erstellung einer eigenständigen Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die internen Kataloginformationen mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Standardsortierung **Latin1_General_100_CI_AS_WS_KS_SC** verwaltet.  
  
 Weitere Informationen zu den Windows- und SQL-Sortierungsnamen finden Sie unter [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).  
  
 **\<delayed_durability_option> ::=**  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Weitere Informationen finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) und [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md).  
  
 **\<file_and_filegroup_options>::=**  
 Weitere Informationen finden Sie unter [ALTER DATABASE-Optionen FILE und FILEGROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md), um Datenbanken zu entfernen.  
  
 Verwenden Sie [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md), um die Größe einer Datenbank zu reduzieren.  
  
 Die ALTER DATABASE-Anweisung muss im Autocommitmodus (dem Standardmodus für die Transaktionsverwaltung) ausgeführt werden und ist in einer expliziten oder impliziten Transaktion nicht zugelassen.  
  
 Der Status einer Datenbankdatei (z. B. online oder offline) wird unabhängig vom Status der Datenbank verwaltet. Weitere Informationen finden Sie im Abschnitt [Dateistatus](../../relational-databases/databases/file-states.md). Der Status der Dateien in einer Dateigruppe bestimmt die Verfügbarkeit der gesamten Dateigruppe. Damit eine Dateigruppe verfügbar ist, müssen alle Dateien in der Dateigruppe online sein. Ist eine Dateigruppe offline, verursacht jeder Versuch, über eine SQL-Anweisung auf die Dateigruppe zuzugreifen, einen Fehler. Wenn Sie Abfragepläne für SELECT-Anweisungen erstellen, vermeidet der Abfrageoptimierer nicht gruppierte Indizes und indizierte Sichten, die sich in Offlinedateigruppen befinden. Dadurch wird ein erfolgreiches Ausführen der Anweisungen ermöglicht. Enthält die Offlinedateigruppe jedoch den Heap oder gruppierten Index der Zieltabelle, schlagen die SELECT-Anweisungen fehl. Auch alle INSERT-, UPDATE- oder DELETE-Anweisungen, die eine Tabelle mit einem Index in einer Offlinedateigruppe ändern, schlagen fehl.  
  
 Wenn eine Datenbank sich im Status RESTORING befindet, erzeugen die meisten ALTER DATABASE-Anweisungen einen Fehler. Eine Ausnahme bildet das Festlegen von Datenbank-Spiegelungsoptionen. Eine Datenbank kann den Status RESTORING aufweisen, während ein Wiederherstellungsvorgang aktiv ist oder wenn ein Wiederherstellungsvorgang einer Datenbank oder Protokolldatei aufgrund einer beschädigten Sicherungsdatei fehlschlägt.  
  
 Der Plancache für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird gelöscht, indem eine der folgenden Optionen festgelegt wird.  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY|PAGE_VERIFY|  
  
 Durch das Löschen des Plancaches wird eine Neukompilierung aller nachfolgenden Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. Für jeden gelöschten Cachespeicher im Plancache enthält das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll folgende Informationsmeldung: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat für den %s-Cachespeicher (Bestandteil des Plancache) %d Leerungen des Cachespeichers gefunden, die von Datenbankwartungs- oder Neukonfigurierungsvorgängen ausgelöst wurden". Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.  
  
 Der Prozedurcache wird in den folgenden Situationen ebenfalls geleert:  
  
-   Die AUTO_CLOSE-Datenbankoption ist für eine Datenbank auf ON festgelegt. Wenn die Datenbank von keiner Benutzerverbindung verwendet wird bzw. keine Benutzerverbindung darauf verweist, versucht der Hintergrundtask, die Datenbank automatisch zu schließen und herunterzufahren.  
  
-   Sie führen mehrere Abfragen für eine Datenbank aus, die über Standardoptionen verfügt. Anschließend wird die Datenbank gelöscht.  
  
-   Eine Datenbank-Momentaufnahme für eine Quelldatenbank wird gelöscht.  
  
-   Sie erstellen das Transaktionsprotokoll für eine Datenbank erfolgreich neu.  
  
-   Sie stellen eine Datenbanksicherung wieder her.  
  
-   Sie trennen eine Datenbank.  
  
## <a name="changing-the-database-collation"></a>Ändern der Datenbanksortierung  
 Bevor Sie auf eine Datenbank eine andere Sortierung anwenden, stellen Sie sicher, dass die folgenden Bedingungen erfüllt sind:  
  
-   Die Datenbank wird derzeit nur von Ihnen verwendet.  
  
-   Von der Sortierung der Datenbank hängt kein schemagebundenes Objekt ab.  
  
     Wenn die folgenden Objekte, die von der Datenbanksortierung abhängen, in der Datenbank vorhanden sind, schlägt die ALTER DATABASE*database_name*COLLATE-Anweisung fehl. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt eine Fehlermeldung für jedes Objekt zurück, das die ALTER-Aktion blockiert:  
  
    -   Benutzerdefinierte Funktionen und Sichten, die mit SCHEMABINDING erstellt wurden.  
  
    -   Berechnete Spalten.  
  
    -   CHECK-Einschränkungen.  
  
    -   Tabellenwertfunktionen, die Tabellen mit Zeichenspalten zurückgeben, deren Sortierungen von der Standardsortierung der Datenbank geerbt wurden.  
  
     Abhängigkeitsinformationen für nicht schemagebundene Entitäten werden automatisch aktualisiert, wenn die Sortierung der Datenbank geändert wird.  
  
 Durch das Ändern der Sortierung der Datenbank werden keine Duplikate von Systemnamen für die Datenbankobjekte erstellt. Wenn durch die geänderte Sortierung doppelte Namen entstehen, verursachen die folgenden Namespaces möglicherweise einen Fehler bei der Änderung der Datenbanksortierung:  
  
-   Objektnamen wie z. B. der Name einer Prozedur, einer Tabelle, eines Triggers oder einer Sicht  
  
-   Schemanamen;  
  
-   Prinzipale wie z. B. eine Gruppe, eine Rolle oder ein Benutzer  
  
-   Namen skalarer Typen wie z. B. der Name eines system- oder benutzerdefinierten Typs  
  
-   Namen von Volltextkatalogen  
  
-   Spalten- oder Parameternamen in einem Objekt  
  
-   Indexnamen in einer Tabelle  
  
Durch doppelte Namen, die durch die neue Sortierung entstanden sind, schlägt die ALTER-Aktion fehl. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt eine Fehlermeldung zurück, in der der Namespace angegeben wird, in dem das Duplikat gefunden wurde.  
  
## <a name="viewing-database-information"></a>Anzeigen von Datenbankinformationen  
 Sie können Katalogsichten, Systemfunktionen und gespeicherte Systemprozeduren verwenden, um Informationen zu Datenbanken, Dateien und Dateigruppen zurückzugeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-name-of-a-database"></a>A. Ändern des Namens einer Datenbank  
 Im folgenden Beispiel wird der Name der Datenbank `AdventureWorks2012` in `Northwind` geändert.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
### <a name="b-changing-the-collation-of-a-database"></a>B. Ändern der Datenbanksortierung  
 Im folgenden Beispiel wird die Datenbank `testdb` mit der `SQL_Latin1_General_CP1_CI_A`S-Sortierung erstellt. Danach wird die Sortierung der Datenbank `testdb` in `COLLATE French_CI_AI` geändert.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE master;  
GO  
  
CREATE DATABASE testdb  
COLLATE SQL_Latin1_General_CP1_CI_AS ;  
GO  
  
ALTER DATABASE testDB  
COLLATE French_CI_AI ;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
- [ALTER DATABASE &#40;Azure SQL-Datenbank&#41;](alter-database-azure-sql-database.md)  
- [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
- [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
- [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
- [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
- [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
- [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
- [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
- [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
- [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
- [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
- [Systemdatenbanken](../../relational-databases/databases/system-databases.md)  
  
