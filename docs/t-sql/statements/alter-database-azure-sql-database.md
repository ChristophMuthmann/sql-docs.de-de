---
title: ALTER_DATABASE (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 12/20/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a5c22e2ce58189f396835f65748fdbab7ef8f9d5
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Ändert eine [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Ändert den Namen einer Datenbank, die Edition und der Dienst Ziel einer Datenbank, der Join einen elastischen Pool und legt Datenbankoptionen an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name }  
{  
    MODIFY NAME = new_database_name  
  | MODIFY ( <edition_options> [, ... n] )   
  | SET { <option_spec> [ ,... n ] }   
  | ADD SECONDARY ON SERVER <partner_server_name>  
      [WITH ( <add-secondary-option>::= [, ... n] ) ]  
  | REMOVE SECONDARY ON SERVER <partner_server_name>  
  | FAILOVER  
  | FORCE_FAILOVER_ALLOW_DATA_LOSS  
}  
[;] 

<edition_options> ::=   
{  

      MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }    
    | EDITION = { 'basic' | 'standard' | 'premium' | 'premiumrs' }   
    | SERVICE_OBJECTIVE = 
                 {  <service-objective>
                 | { ELASTIC_POOL (name = <elastic_pool_name>) }   
                 }   
}  

<add-secondary-option> ::=  
   {  
      ALLOW_CONNECTIONS = { ALL | NO }  
     | SERVICE_OBJECTIVE =   
                 {  <service-objective> 
                 | { ELASTIC_POOL ( name = <elastic_pool_name>) }   
                 }   
   }  

<service-objective> ::=  { 'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
                 | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15' | 
                 | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' | }

```  
  
```
-- SET OPTIONS AVAILABLE FOR SQL Database  
-- Full descriptions of the set options are available in the topic   
-- ALTER DATABASE SET Options. The supported syntax is listed here.  

<option_spec> ::=   
{  
    <auto_option>   
  | <change_tracking_option> 
  | <cursor_option>   
  | <db_encryption_option>  
  | <db_update_option>   
  | <db_user_access_option>   
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option>   
  | <target_recovery_time_option>   
  | <termination>  
  | <temporal_history_retention>  
}  
  
<auto_option> ::=   
{  
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }   
  | AUTO_SHRINK { ON | OFF }   
  | AUTO_UPDATE_STATISTICS { ON | OFF }   
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  

<change_tracking_option> ::=  
{  
  CHANGE_TRACKING   
   {   
       = OFF  
     | = ON [ ( <change_tracking_option_list > [,...n] ) ]   
     | ( <change_tracking_option_list> [,...n] )  
   }  
}  

   <change_tracking_option_list> ::=  
   {  
       AUTO_CLEANUP = { ON | OFF }   
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }  
   }  

<cursor_option> ::=   
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }   
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
  
<db_update_option> ::=  
    { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
    { RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<parameterization_option> ::=  
    PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
    QUERY_STORE   
    {  
          = OFF   
        | = ON [ ( <query_store_option_list> [,... n] ) ]  
        | ( < query_store_option_list> [,... n] )  
        | CLEAR [ ALL ]  
    }  
}   
  
<query_store_option_list> ::=  
{  
      OPERATION_MODE = { READ_WRITE | READ_ONLY }   
    | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )  
    | DATA_FLUSH_INTERVAL_SECONDS = number   
    | MAX_STORAGE_SIZE_MB = number   
    | INTERVAL_LENGTH_MINUTES = number   
    | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]  
    | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]  
    | MAX_PLANS_PER_QUERY = number  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }  
}  
<sql_option> ::=   
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 100 | 110 | 120 | 130 | 140 }  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  

<temporal_history_retention>  ::=  TEMPORAL_HISTORY_RETENTION { ON | OFF }
```  
  
 Vollständige Beschreibungen der Set-Optionen finden Sie unter [ALTER DATABASE SET-Optionen &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) und [ALTER DATABASE-Kompatibilitätsgrad &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll.  
  
 CURRENT  
 Legt fest, dass die zurzeit verwendete Datenbank geändert werden soll.  
  
 Ändern von Namen **= *** Name der neuen Datenbank*  
 Benennt die Datenbank mit dem angegebenen als Namen *Name der neuen Datenbank*. Im folgende Beispiel ändert den Namen einer Datenbank `db1` auf `db2`:   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

 MODIFY (EDITION  **=**  ['basic' | 'standard' | 'Premium' | 'Premiumrs'])    
 Ändert die Dienstebene der Datenbank an. Im folgende Beispiel ändert die Edition auf `premium`:
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

Änderung der EDITION schlägt fehl, wenn die MAXSIZE-Eigenschaft für die Datenbank auf einen Wert außerhalb des gültigen Bereichs, der von dieser Edition unterstützten festgelegt ist.  

 ÄNDERN (MAXSIZE  **=**  [100 MB | 500 MB | 1 | 1024... 4096] GB)  
 Gibt die maximale Größe der Datenbank an. Die maximale Größe muss dem gültigen Wertsatz für die EDITION-Eigenschaft der Datenbank entsprechen. Eine Änderung der maximalen Datenbankgröße kann auch dazu führen, dass die EDITION-Eigenschaft der Datenbank geändert wird. In der folgenden Tabelle sind die unterstützten MAXSIZE-Werte und die Standardwerte (S) für die Dienstebenen von [!INCLUDE[ssSDS](../../includes/sssds-md.md)] aufgeführt.  
  
|**MAXSIZE**|**Standard**|**S0-S2**|**S3-S12**|**P1-P6 und PRS1 PRS6**|**P11-P15**|  
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (S)|√|√|√|√|  
|5 GB|–|√|√|√|√|  
|10 GB|–|√|√|√|√|  
|20 GB|–|√|√|√|√|  
|30 GB|–|√|√|√|√|  
|40 GB|–|√|√|√|√|  
|50 GB|–|√|√|√|√|  
|100 GB|–|√|√|√|√|  
|150 GB|–|√|√|√|√|  
|200 GB|–|√|√|√|√|  
|250 GB|–|√ (S)|√ (S)|√|√|  
|300 GB|–|√|√|√|√|  
|400 GB|–|√|√|√|√|  
|500 GB|–|√|√|√ (S)|√|  
|750 GB|–|√|√|√|√|  
|1024 GB|–|√|√|√|√ (S)|  
|Von 1024 GB bis zu 4096 GB in Inkrementen von 256 GB *|–|–|–|–|√|√|  
  
 \* P11 und P15 können Sie MAXSIZE mit 1024 GB wird die standardmäßige Größe bis zu 4 TB.  P11 und P15 können bis zu 4 TB Speicher enthalten Aufpreis verwenden. In der Premium-Dienstebene MAXSIZE größer als 1 TB ist zurzeit in der folgenden Regionen verfügbar: uns East2, USA (Westen), uns Gov Virginia, Westeuropa, Deutschland zentralen, Süd Ostasien, Japan OST, Australien Osten, Kanada zentralen und Kanada Osten. Aktuelle Einschränkungen finden Sie unter [einzelner Datenbanken](https://docs.microsoft.com/azure/sql-database-single-database-resources).  

  
 Die folgenden Regeln gelten für das MAXSIZE-Argument und das EDITION-Argument:  
  
-   Die MAXSIZE-Wert, muss Wenn angegeben, einen gültigen Wert in der obigen Tabelle aufgeführten zu sein.  
  
-   Wenn EDITION angegeben ist, MAXSIZE jedoch nicht, wird der Standardwert für die Edition verwendet. Wenn EDITION beispielsweise auf die Standard Edition festgelegt und MAXSIZE nicht angegeben ist, wird MAXSIZE automatisch auf 500 MB festgelegt.  
  
-   Wenn weder MAXSIZE noch EDITION angegeben ist, wird die EDITION, Standard (S0) festgelegt ist, und MAXSIZE auf 250 GB festgelegt.  
 

 Ändern (SERVICE_OBJECTIVE = \<dienstziel >)  
 Gibt die Leistungsebene an. Im folgenden Beispiel wird geändert service Objective einer Premium-Datenbank zu `P6`:
 
```  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  
 Die verfügbaren Werte für dienstziel sind: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `PRS1`, `PRS2`, `PRS4`, und `PRS6`. Dienst dienstzielbeschreibungen und Weitere Informationen über die Größe, Editionen und dienstzielkombinationen finden Sie unter [Azure SQL-Datenbank-Dienstebenen und Leistungsstufen](http://msdn.microsoft.com/library/azure/dn741336.aspx). Wenn der angegebene SERVICE_OBJECTIVE von der EDITION nicht unterstützt wird, wird ein Fehler ausgegeben. Zum Ändern des SERVICE_OBJECTIVE-Werts von einer Ebene in eine andere (z. B. von S1 in P1) muss auch der EDITION-Wert geändert werden.  
  
 Ändern (SERVICE_OBJECTIVE = ELASTISCHE\_POOL (Name = \<Elastic_pool_name >)  
 Um eine vorhandene Datenbank einem elastischen Pool hinzugefügt haben, legen Sie die SERVICE_OBJECTIVE von der Datenbank auf ELASTIC_POOL, und geben Sie den Namen des elastischen Pools. Diese Option können auch um die Datenbank auf einen anderen elastischen Pool innerhalb desselben Servers zu ändern. Weitere Informationen finden Sie unter [erstellen und verwalten Sie einen SQL-Datenbank elastischen Pool](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/). Um eine Datenbank aus einem elastischen Pool entfernen möchten, verwenden Sie ALTER DATABASE für eine einzelne Datenbank-Leistungsstufe der SERVICE_OBJECTIVE festzulegen.  

 ON-SEKUNDÄRSERVER \<Partner_server_name >  
 Erstellt eine sekundäre Datenbank für georeplikation mit dem gleichen Namen auf einem Partnerserver, und machen Sie die lokale Datenbank in eine geografische Replikation Primär und startet asynchron Replizieren von Daten vom primären auf den neuen sekundären. Wenn eine Datenbank mit dem gleichen Namen bereits auf dem sekundären Replikat vorhanden ist, schlägt der Befehl fehl. Der Befehl wird ausgeführt, für die master-Datenbank auf dem Host für die lokalen Datenbank, die das primäre Replikat zum Server.  
  
 MIT ALLOW_CONNECTIONS {ALLE | **KEINE** }  
 Wenn ALLOW_CONNECTIONS nicht angegeben wird, wird er auf keine standardmäßig festgelegt. Wenn sie alle festgelegt ist, ist es eine schreibgeschützte Datenbank, die alle Anmeldenamen mit den entsprechenden Berechtigungen eine Verbindung herstellen kann.  
  
 MIT SERVICE_OBJECTIVE {"S0" | "S1" | "S2" | "S3" | "S4" | "A6" | "S7" | "S9" | "S12" | "P1" | "P2" | "P4" | "P6" | "P11" | "P15" | "PRS1" | "PRS2" | "PRS4" | 'PRS6'}  
 Wenn SERVICE_OBJECTIVE nicht angegeben wird, wird die sekundäre Datenbank auf derselben Dienstebene wie die primäre Datenbank erstellt. Wenn SERVICE_OBJECTIVE angegeben wird, wird die sekundäre Datenbank auf der angegebenen Ebene erstellt. Diese Option unterstützt das Erstellen von georeplizierte mit weniger Aufwand Servicelevels. Der angegebene SERVICE_OBJECTIVE muss in die gleiche Edition wie die Quelle sein. Beispielsweise können Sie S0 angeben, wenn die Edition auf Premium ist.  
  
 ELASTIC_POOL (Name = \<Elastic_pool_name)  
 Wenn ELASTIC_POOL nicht angegeben wird, wird die sekundäre Datenbank nicht in einem elastischen Pool erstellt. Wenn ELASTIC_POOL angegeben wird, wird die sekundäre Datenbank im angegebenen Pool erstellt.  
  
> [!IMPORTANT]  
>  Der Benutzer das Hinzufügen eines sekundären REPLIKATS Befehl ausführt müssen DBManager auf primären Server, muss Mitglied der Db_owner in der lokalen Datenbank und DBManager auf sekundären Server.  
  
 Entfernen eines SEKUNDÄREN ON SERVER \<Partner_server_name >  
 Entfernt die angegebene geografisch repliziert, sekundäre Datenbank auf dem angegebenen Server. Der Befehl ist für die master-Datenbank auf dem Hostserver mit der primären Datenbank ausgeführt.  
  
> [!IMPORTANT]  
>  Der Benutzer die sekundäre entfernen Befehl ausführt, muss auf dem primären Server DBManager sein.  
  
 FAILOVER  
 Stuft die sekundäre Datenbank in die geografische Replikation Partnerschaft auf dem der Befehl ausgeführt wird, um den primären und stuft das aktuelle primäre Replikat, um die neuen sekundären Datenbank werden. Im Rahmen dieses Prozesses ist der geografische Replikation Modus vorübergehend vom asynchronen Modus in den synchronen Modus gewechselt werden. Während des failoverprozesses:  
  
1.  Die primäre beendet neue Transaktionen benötigt.  
  
2.  Alle ausstehende Transaktionen werden auf die sekundäre Datenbank geleert.  
  
3.  Die sekundäre Datenbank wird von der primären und beginnt mit dem alten primären georeplikation asynchrone / die neuen sekundären Datenbank.  
  
 Diese Sequenz wird sichergestellt, dass keine Daten verloren. Der Zeitraum, während, den beiden Datenbanken nicht zur Verfügung stehen, ist Größenordnung von 0-25 Sekunden, während die gewechselt werden. Der gesamte Vorgang sollte nicht mehr als einer Minute dauern. Wenn die primäre Datenbank nicht verfügbar ist, wenn dieser Befehl ausgegeben wird, schlägt der Befehl eine Fehlermeldung an, an, dass die primäre Datenbank nicht verfügbar ist. Wenn während des Failovervorgangs nicht abgeschlossen wird und fixierte angezeigt wird, können Sie verwenden den Befehl zum Erzwingen eines Failovers und Datenverlust - akzeptieren und rufen Sie dann, wenn Sie die verlorenen Daten wiederherstellen müssen Devops (CSS), die verlorenen Daten wiederherzustellen.  
  
> [!IMPORTANT]  
>  Der Benutzer einen Befehl für das FAILOVER ausführt, muss auf dem primären Server und dem sekundären Server DBManager sein.  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 Stuft die sekundäre Datenbank in die geografische Replikation Partnerschaft auf dem der Befehl ausgeführt wird, um den primären und stuft das aktuelle primäre Replikat, um die neuen sekundären Datenbank werden. Verwenden Sie diesen Befehl nur, wenn das aktuelle primäre Replikat nicht mehr verfügbar ist. Es ist nur die Wiederherstellung im Notfall ausgelegt, bei der Wiederherstellung von Verfügbarkeit ist wichtig, und einige Datenverlust akzeptabel ist.  
  
 Bei einem erzwungenen Failover:  
  
1.  Die angegebene sekundäre Datenbank sofort ist die primäre Datenbank und beginnt, neue Transaktionen akzeptiert.  
  
2.  Wenn das ursprüngliche primäre Replikat mit dem neuen primären Replikat herstellen, eine inkrementelle Sicherung wird auf dem ursprünglichen primären übernommen, und das ursprüngliche primäre Replikat wird eine neue sekundäre.  
  
3.  Zum Wiederherstellen von Daten aus dieser inkrementelle Sicherung auf dem alten primären kümmert sich der Benutzer Devops/CSS.  
  
4.  Wenn es zusätzliche sekundärobjekte nutzt sind, werden sie automatisch neu konfiguriert, die dahingehend sekundäre Replikate, der das neue primäre. Dieser Vorgang ist asynchron und möglicherweise gibt es eine Verzögerung bis dieser Vorgang abgeschlossen wurde. Bis zum Abschluss der Neukonfiguration weiterhin die sekundären Datenbanken werden sekundäre Replikate der alten primären.  
  
> [!IMPORTANT]  
>  Der Benutzer die FORCE_FAILOVER_ALLOW_DATA_LOSS-Befehl ausführt, muss auf dem primären Server und dem sekundären Server DBManager sein.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie zum Entfernen einer Datenbank [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
  
 Um die Größe einer Datenbank zu reduzieren, verwenden Sie [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
 Die ALTER DATABASE-Anweisung muss im Autocommitmodus (dem Standardmodus für die Transaktionsverwaltung) ausgeführt werden und ist in einer expliziten oder impliziten Transaktion nicht zugelassen.  
  
 Durch das Löschen des Plancaches wird eine Neukompilierung aller nachfolgenden Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. Für jeden gelöschten Cachespeicher im Plancache enthält das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll folgende Informationsmeldung: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat für den %s-Cachespeicher (Bestandteil des Plancache) %d Leerungen des Cachespeichers gefunden, die von Datenbankwartungs- oder Neukonfigurierungsvorgängen ausgelöst wurden". Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.  
  
 Der Prozedurcache wird in den folgenden Situationen ebenfalls geleert:  
  
-   Die AUTO_CLOSE-Datenbankoption ist für eine Datenbank auf ON festgelegt. Wenn die Datenbank von keiner Benutzerverbindung verwendet wird bzw. keine Benutzerverbindung darauf verweist, versucht der Hintergrundtask, die Datenbank automatisch zu schließen und herunterzufahren.  
  
-   Sie führen mehrere Abfragen für eine Datenbank aus, die über Standardoptionen verfügt. Anschließend wird die Datenbank gelöscht.  
  
-   Sie erstellen das Transaktionsprotokoll für eine Datenbank erfolgreich neu.  
  
-   Sie stellen eine Datenbanksicherung wieder her.  
  
-   Sie trennen eine Datenbank.  
  
## <a name="viewing-database-information"></a>Anzeigen von Datenbankinformationen  
 Sie können Katalogsichten, Systemfunktionen und gespeicherte Systemprozeduren verwenden, um Informationen zu Datenbanken, Dateien und Dateigruppen zurückzugeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Datenbanken können nur durch den Prinzipalanmeldenamen auf Serverebene (vom Bereitstellungsprozess erstellt) oder Mitglieder der Datenbankrolle `dbmanager` geändert werden.  
  
> [!IMPORTANT]  
>  Der Datenbankbesitzer kann die Datenbank nur ändern, wenn er Mitglied der Rolle `dbmanager` ist.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. Überprüfen Sie die editionsoptionen aus, und ändern Sie sie:

```
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. Verschieben einer Datenbank auf einen anderen elastischen pool  
 Verschiebt eine vorhandene Datenbank in einen Pool mit dem Namen pool1:  
  
```  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. Fügen Sie eine sekundäre Georeplikation  
 Erstellt eine nicht lesbare sekundäre Datenbank db1 auf Server `secondaryserver` von der db1 auf dem lokalen Server.  
  
```  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = NO )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. Entfernen Sie eine sekundäre Georeplikation  
 Entfernt die sekundäre Datenbank db1 auf Server `secondaryserver`.  
  
```  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. Failover für die sekundäre Georeplikation  
 Stuft eine sekundäre Datenbank db1 auf Server `secondaryserver` der neuen primären Datenbank, wenn auf dem Server ausgeführt werden `secondaryserver`.  
  
```  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie die Datenbank &#40; Azure SQL-Datenbank &#41;](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Systemdatenbanken](../../relational-databases/databases/system-databases.md)  
  
  
