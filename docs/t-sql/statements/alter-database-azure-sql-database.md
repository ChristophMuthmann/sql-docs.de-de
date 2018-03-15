---
title: ALTER DATABASE (Azure SQL Database) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/13/2018
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
ms.openlocfilehash: 6c303c5abe51eaee2208028ea13991d2d557f1b3
ms.sourcegitcommit: a8311ec5ad8313e85e6989f70c5ff9ef120821d6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Ändert eine [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Ändert den Namen, die Edition und das Dienstziel einer Datenbank, verknüpft einen Pool für elastische Datenbanken und legt Datenbankoptionen fest.  
  
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
    | EDITION = { 'basic' | 'standard' | 'premium' }   
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
                 | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15' }

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
  
 Vollständige Beschreibungen der festgelegten Optionen finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) und [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll.  
  
 CURRENT  
 Legt fest, dass die zurzeit verwendete Datenbank geändert werden soll.  
  
 MODIFY NAME **=***new_database_name*  
 Benennt die Datenbank in den angegebenen Namen *new_database_name* um. Im folgenden Beispiel wird der Name einer Datenbank von `db1` in `db2` geändert:   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

 MODIFY (EDITION **=** ['basic' | 'standard' | 'premium' ])    
 Ändert die Dienstebene der Datenbank. Der Support für „premiumrs“ wurde entfernt. Wenn Sie Fragen haben, wenden Sie sich an den E-Mail-Alias premium-rs@microsoft.com.

Im folgenden Beispiel wird die Edition in `premium` geändert:
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

Wenn die MAXSIZE-Eigenschaft für die Datenbank auf einen Wert außerhalb des gültigen, von der jeweiligen Edition unterstützten Bereichs festgelegt wird, schlägt die Änderung der EDITION-Eigenschaft fehl.  

 MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024…4096] GB)  
 Gibt die maximale Größe der Datenbank an. Die maximale Größe muss dem gültigen Wertsatz für die EDITION-Eigenschaft der Datenbank entsprechen. Eine Änderung der maximalen Datenbankgröße kann auch dazu führen, dass die EDITION-Eigenschaft der Datenbank geändert wird. In der folgenden Tabelle sind die unterstützten MAXSIZE-Werte und die Standardwerte (S) für die Dienstebenen von [!INCLUDE[ssSDS](../../includes/sssds-md.md)] aufgeführt.  
  
|**MAXSIZE**|**Standard**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|  
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
|Von 1024 GB bis 4096 GB in Inkrementen von 256 GB*|–|–|–|–|√|√|  
  
 \* P11 und P15 ermöglichen, dass die Größe von MAXSIZE bis zu 4 TB beträgt, wobei 1024 GB die Standardgröße darstellt.  P11 und P15 können bis zu 4 TB des enthaltenen Speichers ohne Aufpreis verwenden. Im Premium-Tarif ist MAXSIZE von mehr als 1 TB derzeit in folgenden Regionen verfügbar: USA, Osten 2; USA, Westen; USA Gov Virginia; Europa, Westen; Deutschland, Mitte; Asien, Südosten; Australien, Osten; Kanada, Mitte; Kanada, Osten. Weitere Informationen zu derzeitigen Einschränkungen finden Sie unter [Single databases (Einzelne Datenbanken)](https://docs.microsoft.com/azure/sql-database-single-database-resources).  

  
 Die folgenden Regeln gelten für das MAXSIZE-Argument und das EDITION-Argument:  
  
-   Falls angegeben, muss der MAXSIZE-Wert einem gültigen, in der vorherigen Tabelle aufgeführten Wert entsprechen.  
  
-   Wenn EDITION angegeben ist, MAXSIZE jedoch nicht, wird der Standardwert für die Edition verwendet. Wenn EDITION beispielsweise auf die Standard Edition festgelegt und MAXSIZE nicht angegeben ist, wird MAXSIZE automatisch auf 500 MB festgelegt.  
  
-   Wenn weder MAXSIZE noch EDITION angegeben sind, wird EDITION auf „Standard“ (S0) und MAXSIZE auf 250 GB festgelegt.  
 

 MODIFY (SERVICE_OBJECTIVE = \<service-objective>)  
 Gibt die Leistungsebene an. Im folgenden Beispiel wird das Dienstziel einer Premium-Datenbank in `P6` geändert:
 
```  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  
 Für Dienstziele sind die folgenden Werte verfügbar: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11` oder `P15`. Dienstzielbeschreibungen und weitere Informationen zu Größe, Editionen und Dienstzielkombinationen finden Sie unter [Dienst- und Leistungsebenen der Azure SQL-Datenbank](http://msdn.microsoft.com/library/azure/dn741336.aspx). Wenn das angegebene SERVICE_OBJECTIVE von der EDITION nicht unterstützt wird, tritt ein Fehler auf. Zum Ändern des SERVICE_OBJECTIVE-Werts von einer Ebene in eine andere (z. B. von S1 in P1) muss auch der EDITION-Wert geändert werden. Die Unterstützung für PRS-Dienstziele wurde entfernt. Wenn Sie Fragen haben, wenden Sie sich an den E-Mail-Alias premium-rs@microsoft.com. 
  
 MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  
 Wenn Sie eine vorhandene Datenbank zu einem Pool für elastische Datenbanken hinzufügen möchten, müssen Sie das SERVICE_OBJECTIVE der Datenbank auf ELASTIC_POOL festlegen und den Namen des Pools für elastische Datenbanken angeben. Sie können mit dieser Option auch die Datenbank in einen anderen Pool für elastische Datenbanken innerhalb desselben Servers ändern. Weitere Informationen finden Sie unter [Erstellen und Verwalten eines Pools für elastische Datenbanken von SQL-Database](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/). Wenn Sie eine Datenbank aus einem Pool für elastische Datenbanken entfernen möchten, legen Sie mithilfe von ALTER DATABASE das SERVICE_OBJECTIVE-Objekt auf eine einzelne Leistungsebene der Datenbank fest.  

 ADD SECONDARY ON SERVER \<partner_server_name>  
 Erstellt eine georeplizierte sekundäre Datenbank mit dem gleichen Namen auf einem Partnerserver. Dabei wird die lokale Datenbank in eine georeplizierte primäre Datenbank umgewandelt und mit dem asynchronen Replizieren von Daten von der primären in die neue sekundäre Datenbank begonnen. Der Befehl schlägt fehl, wenn auf dem sekundären Server bereits eine Datenbank mit dem gleichen Namen vorhanden ist. Der Befehl wird in der Masterdatenbank auf dem Server ausgeführt, der Host der lokalen Datenbank ist, die zur primären Datenbank wird.  
  
 WITH ALLOW_CONNECTIONS { **ALL** | NO }  
 Wenn ALLOW_CONNECTIONS nicht angegeben ist, wird es standardmäßig auf ALL festgelegt. Wenn ALL festgelegt ist, handelt es sich um eine schreibgeschützte Datenbank, zu der alle Anmeldenamen mit den entsprechenden Berechtigungen eine Verbindung herstellen dürfen.  
  
 WITH SERVICE_OBJECTIVE {  'S0' | 'S1' | 'S2' | 'S3" | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15' }  
 Wenn SERVICE_OBJECTIVE nicht angegeben ist, wird die sekundäre Datenbank auf derselben Dienstebene wie die primäre Datenbank erstellt. Wenn SERVICE_OBJECTIVE angegeben ist, wird die sekundäre Datenbank auf der angegebenen Ebene erstellt. Diese Option unterstützt die Erstellung georeplizierter sekundärer Datenbanken mit kostengünstigeren Servicelevels. Das angegebene SERVICE_OBJECTIVE muss sich in derselben Edition wie die Quelle befinden. So können Sie beispielsweise nicht „S0“ angeben, wenn es sich bei der Edition um eine Premium-Edition handelt.  
  
 ELASTIC_POOL (name = \<elastic_pool_name)  
 Wenn ELASTIC_POOL nicht angegeben ist, wird die sekundäre Datenbank nicht in einem Pool für elastische Datenbanken erstellt. Wenn ELASTIC_POOL angegeben ist, wird die sekundäre Datenbank im angegebenen Pool erstellt.  
  
> [!IMPORTANT]  
>  Der Benutzer, der den Befehl ADD SECONDARY ausführt, muss DBManager auf dem primären Server, db_owner-Mitglied in der lokalen Datenbank und DBManager auf dem sekundären Server sein.  
  
 REMOVE SECONDARY ON SERVER  \<partner_server_name>  
 Entfernt die angegebene georeplizierte sekundäre Datenbank vom angegebenen Server. Der Befehl wird in der Masterdatenbank auf dem Server ausgeführt, der Host der primären Datenbank ist.  
  
> [!IMPORTANT]  
>  Der Benutzer, der den Befehl REMOVE SECONDARY ausführt, muss DBManager auf dem primären Server sein.  
  
 FAILOVER  
 Stuft die sekundäre Datenbank in einer Partnerschaft für die Georeplikation hoch, für die der Befehl ausgeführt wird, damit sie zur primären Datenbank wird, und stuft die aktuelle primäre Datenbank tiefer, sodass diese zur neuen sekundären Datenbank wird. Im Rahmen dieses Prozesses wird der Georeplikationsmodus vorübergehend vom asynchronen in den synchronen Modus umgeschaltet. Während des Failoverprozesses:  
  
1.  Die primäre Datenbank übernimmt keine neuen Transaktionen mehr.  
  
2.  Alle ausstehenden Transaktionen werden in der sekundären Datenbank geleert.  
  
3.  Die sekundäre Datenbank wird zur primären Datenbank und beginnt mit der asynchronen Replikation mit der alten primären/der neuen sekundären Datenbank.  
  
 Durch diese Sequenz wird sichergestellt, dass keine Daten verloren gehen. Der Zeitraum, in dem keine der beiden Datenbanken verfügbar ist, umfasst 0 bis 25 Sekunden. In dieser Zeit werden die Rollen gewechselt. Der gesamte Vorgang sollte nicht mehr als einer Minute in Anspruch nehmen. Wenn die primäre Datenbank bei der Ausgabe dieses Befehls nicht verfügbar ist, schlägt der Befehl fehl, und es wird eine Fehlermeldung angezeigt, dass die primäre Datenbank nicht verfügbar ist. Wenn der Failoverprozess nicht abgeschlossen wird und ins Stocken geraten zu sein scheint, können Sie den Befehl zur Erzwingung des Failovers verwenden und einen Datenverlust in Kauf nehmen. Anschließend, wenn eine Wiederherstellung der verloren gegangenen Daten erforderlich sein sollte, können Sie DevOps (CSS) zur Wiederherstellung der verloren gegangenen Daten aufrufen.  
  
> [!IMPORTANT]  
>  Der Benutzer, der den Befehl FAILOVER ausführt, muss DBManager auf dem primären und dem sekundären Server sein.  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 Stuft die sekundäre Datenbank in einer Partnerschaft für die Georeplikation hoch, für die der Befehl ausgeführt wird, damit sie zur primären Datenbank wird, und stuft die aktuelle primäre Datenbank tiefer, sodass diese zur neuen sekundären Datenbank wird. Verwenden Sie diesen Befehl nur dann, wenn die aktuelle primäre Datenbank nicht mehr verfügbar ist. Er wurde nur für die Notfallwiederherstellung erstellt, wenn die Wiederherstellung der Verfügbarkeit wesentlich und ein Datenverlust akzeptabel ist.  
  
 Während eines erzwungenen Failovers:  
  
1.  Die angegebene sekundäre Datenbank wird sofort zur primären Datenbank und beginnt, neue Transaktionen zu akzeptieren.  
  
2.  Wenn die ursprüngliche primäre Datenbank eine Verbindung zur neuen primären Datenbank wiederherstellen kann, wird eine inkrementelle Sicherung von der ursprünglichen primären Datenbank erstellt. Die ursprüngliche primäre Datenbank wird dann zu einer neuen sekundären Datenbank.  
  
3.  Zur Wiederherstellung der Daten aus dieser inkrementellen Sicherung der ursprünglichen primären Datenbank bindet der Benutzer DevOps/CSS ein.  
  
4.  Wenn es weitere sekundäre Datenbanken gibt, werden diese automatisch so neu konfiguriert, dass sie zu den sekundären Datenbanken der neuen primären Datenbank werden. Dieser Vorgang ist asynchron. Bis zum Abschluss des Vorgangs kann es zu einer Verzögerung kommen. Bis zum Abschluss der Neukonfiguration sind die sekundären Datenbanken weiterhin die sekundären Datenbanken der ursprünglichen primären Datenbank.  
  
> [!IMPORTANT]  
>  Der Benutzer, der den Befehl FORCE_FAILOVER_ALLOW_DATA_LOSS ausführt, muss DBManager auf dem primären und dem sekundären Server sein.  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md), um eine Datenbank zu entfernen.  
  
 Verwenden Sie [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md), um die Größe einer Datenbank zu reduzieren.  
  
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
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. Überprüfen Sie die Bearbeitungsoptionen und ändern Sie diese:

```
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. Verschieben einer Datenbank in einen anderen Pool für elastische Datenbanken  
 Verschiebt eine vorhandene Datenbank in einen Pool mit dem Namen pool1:  
  
```  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. Hinzufügen einer sekundären Datenbank für eine Georeplikation  
 Erstellt die lesbare sekundäre Datenbank db1 auf dem Server `secondaryserver` der Datenbank db1 auf dem lokalen Server.  
  
```  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = ALL )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. Entfernen einer sekundären Datenbank für eine Georeplikation  
 Entfernt die sekundäre Datenbank db1 auf dem Server `secondaryserver`.  
  
```  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. Failover für eine sekundäre Datenbank für eine Georeplikation  
 Stuft die sekundäre Datenbank db1 auf dem Server `secondaryserver` höher, damit sie bei Ausführung auf dem Server `secondaryserver` zur neuen primären Datenbank wird.  
  
```  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE DATABASE &#40;Azure SQL-Datenbank&#41;](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
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
  
  
