---
title: ALTER DATABASE SET-Optionen (Transact-SQL) | Microsoft Docs
description: "Informationen Sie zum Festlegen von Datenbankoptionen wie z.B. die automatische Optimierung, Verschlüsselung, Abfragespeicher in einer SQL Server und Azure SQL-Datenbank"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- online database state [SQL Server]
- database options [SQL Server]
- emergency database state [SQL Server]
- databases [SQL Server], options
- read-only databases
- recovery models [SQL Server], switching
- ALTER DATABASE statement, SET options
- offline database state [SQL Server]
- snapshot isolation framework option
- checksums [SQL Server]
- automatic tuning
- SQL plan regression correction
ms.assetid: f76fbd84-df59-4404-806b-8ecb4497c9cc
caps.latest.revision: 159
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 5dbb93a69c6f8194c2d17eb982fae1ba15d4a522
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="alter-database-set-options-transact-sql"></a>ALTER DATABASE SET-Optionen (Transact-SQL) 
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Dieses Thema enthält die ALTER DATABASE-Syntax für das Festlegen von Datenbankoptionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere ALTER DATABASE-Syntax finden Sie unter den folgenden Themen.  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  

-   [ALTER DATABASE &#40; Azure SQL-Datenbank &#41;](alter-database-azure-sql-database.md) 

-   [ALTER DATABASE &#40; Azure SQL Datawarehouse &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)  
  
-   [ALTER DATABASE &#40; Parallel Datawarehouse &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)  
  
Datenbankspiegelung [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], und Kompatibilitätsgrade sind `SET` Optionen jedoch werden in separaten Themen beschrieben wegen ihres Umfangs. Weitere Informationen finden Sie unter [ALTER DATABASE der Datenbankspiegelung &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md), [ALTER DATABASE SET HADR &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-hadr.md), und [ALTER DATABASE-Kompatibilitätsgrad &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]  
>  Viele Database Set-Optionen können für die aktuelle Sitzung konfiguriert werden, mithilfe von [SET-Anweisungen &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md) und werden häufig von Anwendungen konfiguriert, wenn sie eine Verbindung herstellen. Auf Sitzungsebene festgelegt Optionen Außerkraftsetzung der **ALTER DATABASE SET** Werte. Die unten beschriebenen Datenbankoptionen entsprechen Werten, die für Sitzungen festgelegt werden können, von denen explizit keine weiteren Werte für SET-Optionen bereitgestellt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER DATABASE { database_name  | CURRENT }  
SET   
{  
    <optionspec> [ ,...n ] [ WITH <termination> ]   
}  
  
<optionspec> ::=   
{  
    <auto_option>   
  | <automatic_tuning_option>   
  | <change_tracking_option>   
  | <containment_option>   
  | <cursor_option>   
  | <database_mirroring_option>  
  | <date_correlation_optimization_option>  
  | <db_encryption_option>  
  | <db_state_option>  
  | <db_update_option>   
  | <db_user_access_option>   
  | <delayed_durability_option>  
  | <external_access_option>  
  | FILESTREAM ( <FILESTREAM_option> )  
  | <HADR_options>  
  | <mixed_page_allocation_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <recovery_option>  
  | <remote_data_archive_option>  
  | <service_broker_option>  
  | <snapshot_option>  
  | <sql_option>   
  | <target_recovery_time_option>   
  | <termination>  
}  
  
<auto_option> ::=   
{  
    AUTO_CLOSE { ON | OFF }   
  | AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] }   
  | AUTO_SHRINK { ON | OFF }   
  | AUTO_UPDATE_STATISTICS { ON | OFF }   
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  
  
<automatic_tuning_option> ::=  
{  
  AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = { ON | OFF } )
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
  
<containment_option> ::=   
   CONTAINMENT = { NONE | PARTIAL }  
  
<cursor_option> ::=   
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF }   
  | CURSOR_DEFAULT { LOCAL | GLOBAL }   
}  
  
<database_mirroring_option>  
  ALTER DATABASE Database Mirroring  
  
<date_correlation_optimization_option> ::=  
    DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
  
<db_state_option> ::=  
    { ONLINE | OFFLINE | EMERGENCY }  
  
<db_update_option> ::=  
    { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
    { SINGLE_USER | RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=  
    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<external_access_option> ::=  
{  
    DB_CHAINING { ON | OFF }  
  | TRUSTWORTHY { ON | OFF }  
  | DEFAULT_FULLTEXT_LANGUAGE = { <lcid> | <language name> | <language alias> }  
  | DEFAULT_LANGUAGE = { <lcid> | <language name> | <language alias> }  
  | NESTED_TRIGGERS = { OFF | ON }  
  | TRANSFORM_NOISE_WORDS = { OFF | ON }  
  | TWO_DIGIT_YEAR_CUTOFF = { 1753, ..., 2049, ..., 9999 }  
}  
<FILESTREAM_option> ::=  
{  
    NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL   
  | DIRECTORY_NAME = <directory_name>  
}  
<HADR_options> ::=  
    ALTER DATABASE SET HADR  
  
<mixed_page_allocation_option> ::=  
    MIXED_PAGE_ALLOCATION { OFF | ON }  
  
<parameterization_option> ::=  
    PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
    QUERY_STORE   
    {  
          = OFF   
        | = ON [ ( <query_store_option_list> [,...n] ) ]  
        | ( < query_store_option_list> [,...n] )  
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
    | WAIT_STATS_CAPTURE_MODE = [ ON | OFF ]
}  
  
<recovery_option> ::=   
{  
    RECOVERY { FULL | BULK_LOGGED | SIMPLE }   
  | TORN_PAGE_DETECTION { ON | OFF }  
  | PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }  
}  
  
<remote_data_archive_option> ::=  
{  
    REMOTE_DATA_ARCHIVE =  
    {  
        ON ( SERVER = <server_name> ,   
                  {   CREDENTIAL = <db_scoped_credential_name>  
                     | FEDERATED_SERVICE_ACCOUNT =  ON | OFF   
                  }  
               )  
      | OFF  
    }  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | DISABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
  | HONOR_BROKER_PRIORITY { ON | OFF}  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = {ON | OFF }  
}  
<sql_option> ::=   
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 90 | 100 | 110 | 120}  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<target_recovery_time_option> ::=  
    TARGET_RECOVERY_TIME = target_recovery_time { SECONDS | MINUTES }  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll.  
  
 CURRENT  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 `CURRENT`führt die Aktion in der aktuellen Datenbank. `CURRENT`wird für alle Optionen in allen Kontexten nicht unterstützt. Wenn `CURRENT` ein Fehler auftritt, geben Sie den Datenbanknamen ein.  
  
 **\<Auto_option >:: =**  
  
 Steuert automatische Optionen.  
  
 AUTO_CLOSE { ON | OFF }  
 ON  
 Die Datenbank wird ordnungsgemäß heruntergefahren, und ihre Ressourcen werden freigegeben, nachdem der letzte Benutzer die Anwendung beendet hat.  
  
 Die Datenbank wird automatisch wieder geöffnet, wenn ein Benutzer versucht, die Datenbank erneut zu verwenden. Beispielsweise durch Ausgeben einer `USE database_name` Anweisung. Wurde die Datenbank ordnungsgemäß heruntergefahren und ist AUTO_CLOSE auf ON festgelegt, wird sie beim nächsten Start des [!INCLUDE[ssDE](../../includes/ssde-md.md)] erst dann wieder geöffnet, wenn ein Benutzer versucht, die Datenbank zu verwenden.  
  
 OFF  
 Die Datenbank bleibt nach dem Beenden der Verwendung durch den letzten Benutzer geöffnet.  
  
 Die Option AUTO_CLOSE ist sehr nützlich für Desktopdatenbanken, da mit ihrer Hilfe Datenbankdateien wie reguläre Dateien verwaltet werden können. Sie können verschoben, zur Sicherung kopiert oder sogar per E-Mail an andere Benutzer gesendet werden. AUTO_CLOSE ist ein asynchroner Prozess. Das wiederholte Öffnen und Schließen der Datenbank beeinträchtigt nicht die Leistung.  
  
> [!NOTE]  
>  Die AUTO_CLOSE-Option ist nicht verfügbar in einer enthaltenen Datenbank oder auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Der Status dieser Option kann mithilfe der Spalte is_auto_close_on in der sys.databases-Katalogsicht oder der IsAutoClose-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
> [!NOTE]  
>  Ist AUTO_CLOSE auf ON festgelegt, geben einige Spalten in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht sowie die DATABASEPROPERTYEX-Funktion den Wert NULL zurück, da die Datenbank nicht für den Abruf der Daten verfügbar ist. Führen Sie eine USE-Anwendung zum Öffnen der Datenbank aus, um dieses Problem zu beheben.  
  
> [!NOTE]  
>  Für die Datenbankspiegelung muss AUTO_CLOSE deaktiviert sein (OFF).  
  
 Wenn die Datenbank auf AUTOCLOSE = ON festgelegt ist, wird mit einem Vorgang, bei dem das automatische Beenden der Datenbank initiiert wird, der Plancache für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht. Durch das Löschen des Plancaches wird eine Neukompilierung aller nachfolgenden Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 oder höher enthält das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll für jeden geleerten Cachespeicher im Plancache folgende Meldung zur Information: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat für den '%s'-Cachespeicher (Bestandteil des Plancache) %d Leerungen des Cachespeichers gefunden, die von Datenbankwartungs- oder Neukonfigurierungsvorgängen ausgelöst wurden." Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.  
  
 AUTO_CREATE_STATISTICS { ON | OFF }  
 ON  
 Der Abfrageoptimierer erstellt nach Bedarf Statistiken für einzelne Spalten in Abfrageprädikaten, um Abfragepläne und die Abfrageleistung zu verbessern. Diese Statistiken für einzelne Spalten werden erstellt, wenn der Abfrageoptimierer Abfragen kompiliert. Die Statistiken für einzelne Spalten werden nur für Spalten erstellt, die noch nicht der ersten Spalte eines vorhandenen Statistikobjekts entsprechen.  
  
 Der Standardwert ist ON. Für die meisten Datenbanken empfiehlt sich die Verwendung der Standardeinstellung.  
  
 OFF  
 Der Abfrageoptimierer erstellt beim Kompilieren von Abfragen keine Statistiken für einzelne Spalten in Abfrageprädikaten. Das Festlegen dieser Option auf OFF kann zu suboptimalen Abfrageplänen und einer beeinträchtigten Abfrageleistung führen.  
  
 Der Status dieser Option kann mithilfe der is_auto_create_stats_on-Spalte in der sys.databases-Katalogsicht oder der IsAutoCreateStatistics-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 Weitere Informationen finden Sie im Abschnitt "Verwenden der datenbankweiten Statistikoptionen" in [Statistiken](../../relational-databases/statistics/statistics.md).  
  
 INCREMENTAL = ON | OFF  
 Wenn AUTO_CREATE_STATISTICS sowie INCREMENTAL auf ON festgelegt sind, werden automatisch erstellte Statistiken, sofern unterstützt, als inkrementelle Statistiken erstellt. Der Standardwert ist OFF. Weitere Informationen finden Sie unter [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 AUTO_SHRINK { ON | OFF }  
 ON  
 Die Datenbankdateien sind Kandidaten für das periodische Verkleinern.  
  
 Sowohl Daten- als auch Protokolldateien können verkleinert werden. AUTO_SHRINK reduziert die Größe des Transaktionsprotokolls nur, wenn für die Datenbank das SIMPLE-Wiederherstellungsmodell festgelegt ist oder wenn das Protokoll gesichert wird. Ist diese Option auf OFF festgelegt, werden die Datenbankdateien während der periodisch ausgeführten Überprüfung auf nicht verwendeten Speicherplatz nicht automatisch verkleinert.  
  
 Durch die Option AUTO_SHRINK werden Dateien dann verkleinert, wenn mehr als 25 Prozent der Datei aus nicht verwendetem Speicherplatz bestehen. Die Datei wird auf eine Größe verkleinert, bei der 25 Prozent der Datei aus nicht verwendetem Speicherplatz bestehen, oder auf die Größe, mit der die Datei erstellt wurde, je nachdem, welcher Wert größer ist.  
  
 Eine schreibgeschützte Datenbank kann nicht verkleinert werden.  
  
 OFF  
 Die Datenbankdateien werden bei periodischen Prüfungen auf nicht verwendeten Speicherplatz nicht automatisch verkleinert.  
  
 Der Status dieser Option kann mithilfe der is_auto_shrink_on-Spalte in der sys.databases-Katalogsicht oder der IsAutoShrink-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
> [!NOTE]  
>  Die AUTO_SHRINK-Option ist in einer eigenständigen Datenbank nicht verfügbar.  
  
 AUTO_UPDATE_STATISTICS { ON | OFF }  
 ON  
 Gibt an, dass der Abfrageoptimierer Statistiken aktualisiert, wenn sie von einer Abfrage verwendet werden und veraltet sein könnten. Statistiken sind veraltet, wenn die Datenverteilung in der Tabelle oder indizierten Sicht durch die Vorgänge INSERT, UPDATE, DELETE oder MERGE geändert wurde. Der Abfrageoptimierer stellt fest, wann Statistiken veraltet sein könnten, indem er die Anzahl der Datenänderungen seit des letzten Statistikupdates ermittelt und sie mit einem Schwellenwert vergleicht. Der Schwellenwert basiert auf der Anzahl von Zeilen in der Tabelle oder indizierten Sicht.  
  
 Bevor der Abfrageoptimierer eine Abfrage kompiliert und einen zwischengespeicherten Abfrageplan ausführt, sucht er nach veralteten Statistiken. Vor dem Kompilieren einer Abfrage ermittelt der Abfrageoptimierer anhand der Spalten, Tabellen und indizierten Sichten im Abfrageprädikat, welche Statistiken veraltet sein könnten. Vor dem Ausführen eines zwischengespeicherten Abfrageplans überprüft das [!INCLUDE[ssDE](../../includes/ssde-md.md)] , ob der Abfrageplan auf aktuelle Statistiken verweist.  
  
 Die AUTO_UPDATE_STATISTICS-Option gilt für Statistikobjekte, die für Indizes, einzelne Spalten in Abfrageprädikaten und mit der CREATE STATISTICS-Anweisung generierte Statistiken erstellt wurden. Diese Option gilt auch für gefilterte Statistiken.  
  
 Der Standardwert ist ON. Für die meisten Datenbanken empfiehlt sich die Verwendung der Standardeinstellung.  
  
 Verwenden Sie die AUTO_UPDATE_STATISTICS_ASYNC-Option, um anzugeben, ob die Statistiken synchron oder asynchron aktualisiert werden.  
  
 OFF  
 Gibt an, dass der Abfrageoptimierer Statistiken nicht aktualisiert, wenn sie von einer Abfrage verwendet werden und veraltet sein könnten. Das Festlegen dieser Option auf OFF kann zu suboptimalen Abfrageplänen und einer beeinträchtigten Abfrageleistung führen.  
  
 Der Status dieser Option kann mithilfe der is_auto_update_stats_on-Spalte in der sys.databases-Katalogsicht oder der IsAutoUpdateStatistics-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 Weitere Informationen finden Sie im Abschnitt "Verwenden der datenbankweiten Statistikoptionen" in [Statistiken](../../relational-databases/statistics/statistics.md).  
  
 AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
 ON  
 Gibt an, dass Statistikupdates für die AUTO_UPDATE_STATISTICS-Option asynchron sind. Der Abfrageoptimierer wartet nicht, bis Statistikupdates abgeschlossen sind, bevor Abfragen kompiliert werden.  
  
 Das Festlegen dieser Option auf ON hat nur dann Auswirkungen, wenn AUTO_UPDATE_STATISTICS auf ON festgelegt ist.  
  
 Die AUTO_UPDATE_STATISTICS_ASYNC-Option ist standardmäßig auf OFF festgelegt, sodass der Abfrageoptimierer Statistiken synchron aktualisiert.  
  
 OFF  
 Gibt an, dass Statistikupdates für die AUTO_UPDATE_STATISTICS-Option synchron sind. Der Abfrageoptimierer wartet, bis Statistikupdates abgeschlossen sind, bevor Abfragen kompiliert werden.  
  
 Das Festlegen dieser Option auf OFF hat nur dann Auswirkungen, wenn AUTO_UPDATE_STATISTICS auf ON festgelegt ist.  
  
 Der Status der Option kann mithilfe der is_auto_update_stats_async_on-Spalte in der sys.databases-Katalogsicht ermittelt werden.  
  
 Weitere Informationen, die beschreibt, wann synchrone oder asynchrone Statistikupdates verwendet werden sollten, finden Sie im Abschnitt "Verwenden der datenbankweiten Statistikoptionen" in [Statistiken](../../relational-databases/statistics/statistics.md).  
  
 **\<Automatic_tuning_option >:: =**  
 **Gilt für**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  

 Aktiviert oder deaktiviert die `FORCE_LAST_GOOD_PLAN` [Automatische Optimierung](../../relational-databases/automatic-tuning/automatic-tuning.md) Option.  
  
 FORCE_LAST_GOOD_PLAN = {ON | {OFF}  
 ON  
 Die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] erzwingt automatisch auf die letzten bekannten guten Plan die [!INCLUDE[tsql_md](../../includes/tsql_md.md)] Abfragen, in dem neuer SQL-Plan leistungsregressionen verursacht. Die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] fortlaufendes überwacht die abfrageleistung von der [!INCLUDE[tsql_md](../../includes/tsql_md.md)] Abfrage mit dem erzwungenen Plan. Wenn es leistungsverbesserungen gibt der [!INCLUDE[ssde_md](../../includes/ssde_md.md)] wird verwenden weiterhin den letzten bekannten guten Plan. Wenn Leistungsvorteile nicht erkannt werden, die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] erzeugt einen neuen SQL-Plan. Die Anweisung schlägt fehl, wenn der Abfragespeicher nicht aktiviert ist oder wenn es nicht im *Lese-/ Schreibzugriff* Modus.   

 OFF  
 Die [!INCLUDE[ssde_md](../../includes/ssde_md.md)] meldet potenzielle durch Änderungen an SQL-Plan im Abfrage-leistungsregressionen [sys.dm_db_tuning_recommendations](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) anzeigen. Diese Empfehlungen sind jedoch nicht automatisch übernommen. Benutzer kann durch Anwenden von aktiven Empfehlungen und identifiziert Probleme überwachen [!INCLUDE[tsql_md](../../includes/tsql_md.md)] Skripts, die in der Ansicht angezeigt werden. Dies ist der Standardwert.

 **\<Change_tracking_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert Änderungsnachverfolgungsoptionen. Sie können die Änderungsnachverfolgung aktivieren, Optionen festlegen, Optionen ändern und die Änderungsnachverfolgung deaktivieren. Beispiele hierzu finden Sie im Abschnitt "Beispiele" weiter unten in diesem Thema.  
  
 ON  
 Aktiviert die Änderungsnachverfolgung für die Datenbank. Wenn die Änderungsnachverfolgung aktiviert wird, können auch die AUTO CLEANUP-Option und die CHANGE RETENTION-Option festgelegt werden.  
  
 AUTO_CLEANUP = { ON | OFF }  
 ON  
 Die Änderungsnachverfolgungsdaten werden nach der angegebenen Beibehaltungsdauer automatisch entfernt.  
  
 OFF  
 Die Änderungsnachverfolgungsdaten werden nicht aus der Datenbank entfernt.  
  
 CHANGE_RETENTION =*Retention_period* {Tage | STUNDEN | MINUTEN}  
 Gibt die Mindestdauer für die Beibehaltung von Änderungsnachverfolgungsdaten in der Datenbank an. Die Daten werden nur dann entfernt, wenn der Wert für AUTO_CLEANUP ON lautet.  
  
 *Retention_period* ist eine ganze Zahl, die numerische Komponente der Beibehaltungsdauer angibt.  
  
 Die Standardbeibehaltungsdauer beträgt 2 Tage. Die Mindestbeibehaltungsdauer ist 1 Minute. Der Standardtyp für die Beibehaltungsdauer ist Tage.  
  
 OFF  
 Deaktiviert die Änderungsnachverfolgung für die Datenbank. Die Änderungsnachverfolgung muss erst für alle Tabellen deaktiviert werden, bevor sie für die Datenbank deaktiviert werden kann.  
  
 **\<Containment_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert die Einschlussoptionen für Datenbanken.  
  
 CONTAINMENT = {NONE | PARTIELLE}  
 Keine  
 Die Datenbank ist keine eigenständige Datenbank.  
  
 PARTIAL  
 Die Datenbank ist eine eigenständige Datenbank. Wenn für die Datenbank die Replikation, das Aufzeichnen oder das Nachverfolgen von Änderungsdaten aktiviert ist, tritt beim Festlegen des Datenbankeinschlusses auf einen partiellen Einschluss ein Fehler auf. Die Fehlerüberprüfung wird nach einem Fehler beendet. Weitere Informationen zu eigenständigen Datenbanken finden Sie unter [Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md).  
  
> [!NOTE]  
>  Kapselung kann nicht konfiguriert werden, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]. Kapselung ist nicht explizit festgelegt, aber [!INCLUDE[ssSDS](../../includes/sssds-md.md)] enthaltene Funktionen wie z. B. enthaltenen Datenbankbenutzer verwenden können.  
  
 **\<Cursor_option >:: =**  
  
 Steuert Cursoroptionen.  
  
 CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
 ON  
 Alle beim Commit oder Rollback einer Transaktion geöffneten Cursor werden geschlossen.  
  
 OFF  
 Cursor bleiben beim Commit einer Transaktion geöffnet. Beim Rollback einer Transaktion werden alle Cursor geschlossen, sofern sie nicht als INSENSITIVE oder STATIC definiert sind.  
  
 Einstellungen auf Verbindungsebene, die mithilfe der SET-Anweisung festgelegt werden, überschreiben die Standardeinstellung der Datenbank für CURSOR_CLOSE_ON_COMMIT. ODBC- und OLE DB-Clients geben standardmäßig eine SET-Anweisung aus, durch die CURSOR_CLOSE_ON_COMMIT für die Sitzung auf OFF festgelegt wird, wenn sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Weitere Informationen finden Sie unter [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).  
  
 Der Status dieser Option kann mithilfe der Spalte is_cursor_close_on_commit_on in der sys.databases-Katalogsicht oder der IsCloseCursorsOnCommitEnabled-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 CURSOR_DEFAULT { LOCAL | GLOBAL }  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert, ob der Cursorbereich LOCAL oder GLOBAL verwendet.  
  
 LOCAL  
 Wenn LOCAL angegeben wurde und beim Erstellen kein Cursor als GLOBAL definiert wird, ist der Bereich des Cursors lokal für den Batch, die gespeicherte Prozedur oder den Trigger, in dem er erstellt wurde. Der Cursorname ist nur innerhalb dieses Bereichs gültig. Auf den Cursor kann durch lokale Cursorvariablen im Batch, in der gespeicherten Prozedur, im Trigger oder im OUTPUT-Parameter einer gespeicherten Prozedur verwiesen werden. Die Zuordnung des Cursors wird implizit aufgehoben, wenn der Batch, die gespeicherte Prozedur oder der Trigger beendet wird, es sei denn, der Cursor wird in einem OUTPUT-Parameter zurückgegeben. Wenn die Rückgabe in einem OUTPUT-Parameter erfolgt, wird die Zuordnung des Cursors aufgehoben, wenn die Zuordnung der letzten auf ihn verweisenden Variablen aufgehoben wird oder wenn der Cursor den Gültigkeitsbereich verlässt.  
  
 GLOBAL  
 Wenn GLOBAL angegeben wurde und beim Erstellen kein Cursor als LOCAL definiert wird, ist der Bereich des Cursors global für die Verbindung. Auf den Cursornamen kann in jeder gespeicherten Prozedur und in jedem Batch verwiesen werden, die bzw. der von der Verbindung ausgeführt wird.  
  
 Die Zuordnung des Cursors wird implizit nur aufgehoben, wenn die Verbindung getrennt wird. Weitere Informationen finden Sie unter [DECLARE CURSOR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
 Der Status dieser Option kann mithilfe der Spalte is_local_cursor_default in der sys.databases-Katalogsicht oder der IsLocalCursorsDefault-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 **\<Database_mirroring >**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Das argumentbeschreibungen finden Sie unter [ALTER DATABASE der Datenbankspiegelung &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md).  
  
 **\<Date_correlation_optimization_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert die Option DATE_CORRELATION_OPTIMIZATION.  
  
 DATE_CORRELATION_OPTIMIZATION { ON | OFF }  
 ON  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwaltet korrelationsstatistiken zwischen zwei beliebigen Tabellen in der Datenbank, die durch eine FOREIGN KEY-Einschränkung verknüpft sind und **"DateTime"** Spalten.  
  
 OFF  
 Es werden keine Korrelationsstatistiken verwaltet.  
  
 Wenn DATE_CORRELATION_OPTIMIZATION auf ON festgelegt werden soll, darf keine aktive Verbindung mit der Datenbank bestehen, außer der Verbindung, über die die ALTER DATABASE-Anweisung ausgeführt wird. Anschließend werden mehrere Verbindungen unterstützt.  
  
 Die aktuelle Einstellung der Option kann mithilfe der Spalte is_date_correlation_on in der sys.databases-Katalogsicht ermittelt werden.  
  
 **\<Db_encryption_option >:: =**  
  
 Steuert den Status der Datenbankverschlüsselung.  
  
 ENCRYPTION {ON | OFF}  
 Legt fest, ob die Datenbank verschlüsselt (ON) oder nicht verschlüsselt (OFF) werden soll. Weitere Informationen über die datenbankverschlüsselung finden Sie unter [transparente datenverschlüsselung &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md), und [transparente datenverschlüsselung in Azure SQL-Datenbank](../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).  
  
 Wenn die Verschlüsselung auf Datenbankebene aktiviert wird, werden alle Dateigruppen verschlüsselt. Alle neuen Dateigruppen erben die verschlüsselte Eigenschaft. Wenn Dateigruppen in der Datenbank, um festgelegt werden **READ ONLY**, schlägt der datenbankverschlüsselungsvorgang fehl.  
  
 Sie können den Verschlüsselungsstatus der Datenbank anzeigen, indem Sie mit der [dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) -verwaltungssicht.  
  
 **\<Db_state_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert den Status der Datenbank.  
  
 OFFLINE  
 Die Datenbank ist geschlossen, ordnungsgemäß heruntergefahren und als offline gekennzeichnet. Die Datenbank kann nicht geändert werden, während sie als offline gekennzeichnet ist.  
  
 ONLINE  
 Die Datenbank ist geöffnet und kann verwendet werden.  
  
 EMERGENCY  
 Die Datenbank ist als READ_ONLY markiert, die Protokollierung deaktiviert und der Zugriff auf Mitglieder der festen Serverrolle sysadmin beschränkt. Der Status EMERGENCY wird hauptsächlich zu Problembehandlungszwecken verwendet. Beispielsweise kann für eine Datenbank, die aufgrund einer beschädigten Protokolldatei als fehlerverdächtig gekennzeichnet ist, der Status EMERGENCY festgelegt werden. Dadurch wird u. U. für den Systemadministrator der schreibgeschützte Zugriff auf die Datenbank aktiviert. Nur Mitglieder der festen Serverrolle sysadmin können für eine Datenbank den Status NOTFALL festlegen.  
  
> [!NOTE]  
>  **Berechtigungen:** ALTER DATABASE-Berechtigung für die betreffende Datenbank ist erforderlich, um eine Datenbank in den offline- oder notfallstatus Zustand ändern. Die ALTER ANY DATABASE-Berechtigung auf Serverebene ist erforderlich, um eine Datenbank vom Online- in den Offlinestatus zu schalten.  
  
 Der Status dieser Option kann ermittelt werden die Status und "state_desc" Spalten in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht oder der Status-Eigenschaft der [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) Funktion. Weitere Informationen finden Sie unter [Database States](../../relational-databases/databases/database-states.md).  
  
 Für eine Datenbank, die als RESTORING gekennzeichnet ist, kann nicht OFFLINE, ONLINE oder EMERGENCY festgelegt werden. Eine Datenbank kann den Status RESTORING aufweisen, während ein Wiederherstellungsvorgang aktiv ist oder wenn ein Wiederherstellungsvorgang einer Datenbank oder Protokolldatei aufgrund einer beschädigten Sicherungsdatei fehlschlägt.  
  
 **\<Db_update_option >:: =**  
  
 Steuert, ob Updates für die Datenbank zugelassen sind.  
  
 READ_ONLY  
 Benutzer können Daten aus der Datenbank lesen, aber nicht ändern.  
  
> [!NOTE]  
>  Um die Abfrageleistung zu verbessern, sollten Sie vor dem Festlegen einer Datenbank auf READ_ONLY die Statistiken aktualisieren. Wenn weitere Statistiken benötigt werden, nachdem eine Datenbank auf READ_ONLY festgelegt wurde, erstellt das [!INCLUDE[ssDE](../../includes/ssde-md.md)] Statistiken in tempdb. Weitere Informationen zu Statistiken für eine schreibgeschützte Datenbank finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
 READ_WRITE  
 Die Datenbank ist für Lese- und Schreibvorgänge verfügbar.  
  
 Sie müssen über exklusiven Zugriff auf die Datenbank verfügen, um diesen Status zu ändern. Weitere Informationen finden Sie unter der SINGLE_USER-Klausel.  
  
> [!NOTE]  
>  Bei Verbunddatenbanken mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ist SET { READ_ONLY | READ_WRITE } deaktiviert.  
  
 **\<Db_user_access_option >:: =**  
  
 Steuert den Benutzerzugriff auf die Datenbank.  
  
 SINGLE_USER  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Gibt an, dass jeweils nur ein Benutzer auf die Datenbank zugreifen kann. Wenn SINGLE_USER angegeben ist und andere Benutzer mit der Datenbank verbunden sind, wird die ALTER DATABASE-Anweisung blockiert, bis alle Benutzer die Verbindung mit der angegebenen Datenbank trennen. Um dieses Verhalten zu überschreiben, finden Sie unter der WITH \<Termination >-Klausel.  
  
 Die Datenbank verbleibt im SINGLE_USER-Modus, selbst wenn sich der Benutzer, der die Option festgelegt hat, abmeldet. Dadurch kann ein anderer Benutzer (aber nur einer) eine Verbindung mit der Datenbank herstellen.  
  
 Bevor Sie die Datenbank auf SINGLE_USER festlegen, müssen Sie überprüfen, ob die Option AUTO_UPDATE_STATISTICS_ASYNC auf OFF festgelegt ist. Wenn diese Option auf ON festgelegt ist, stellt der Hintergrundthread, der zum Aktualisieren von Statistiken verwendet wird, eine Verbindung mit der Datenbank her, und Sie können im Einzelbenutzermodus nicht auf die Datenbank zugreifen. Fragen Sie zum Anzeigen des Status dieser Option die Is_auto_update_stats_async_on-Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt. Wenn die Option auf ON festgelegt wird, sollten Sie folgende Tasks ausführen:  
  
1.  Legen Sie AUTO_UPDATE_STATISTICS_ASYNC auf OFF fest.  
  
2.  Überprüfen Sie für aktive asynchrone statistikaufträge durch Abfragen der [dm_exec_background_job_queue](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md) -verwaltungssicht.  
  
 Wenn aktive Aufträge vorhanden sind, entweder erlauben, die Aufträge abgeschlossen werden oder beenden Sie sie manuell mit [KILL STATS JOB](../../t-sql/language-elements/kill-stats-job-transact-sql.md).  
  
RESTRICTED_USER  
 RESTRICTED_USER ermöglicht nur Mitgliedern der festen Datenbankrolle db_owner und der festen Serverrollen dbcreator und sysadmin eine Verbindung mit der Datenbank, begrenzt jedoch nicht deren Anzahl. Alle Verbindungen zur Datenbank werden in dem durch die Beendigungsklausel der ALTER DATABASE-Anweisung angegebenen Zeitraum getrennt. Sobald die Datenbank in den Status RESTRICTED_USER gewechselt hat, werden Verbindungsversuche von nicht qualifizierten Benutzern abgelehnt.  
  
MULTI_USER  
 Alle Benutzer, die über die entsprechenden Berechtigungen für die Verbindung mit der Datenbank verfügen, sind zugelassen.  
  
 Der Status dieser Option kann mithilfe der Spalte user_access in der sys.databases-Katalogsicht oder der UserAccess-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 **\<Delayed_durability_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert, ob für Transaktionen ein Commit mit vollständiger oder verzögerter Dauerhaftigkeit ausgeführt wird.  
  
 DISABLED  
 Alle Transaktionen, die auf SET DISABLED folgen, sind vollständig dauerhaft. Alle Dauerhaftigkeitsoptionen, die in einem Atomic-Block oder einer Commitanweisung festgelegt sind, werden ignoriert.  
  
 ALLOWED  
 Alle Transaktionen, die auf SET ALLOWED folgen, sind abhängig von der im Atomic-Block oder der Commitanweisung festgelegten Dauerhaftigkeitsoption entweder vollständig dauerhaft oder verzögert dauerhaft.  
  
 FORCED  
 Alle Transaktionen, die auf SET FORCED folgen, sind verzögert dauerhaft. Alle Dauerhaftigkeitsoptionen, die in einem Atomic-Block oder einer Commitanweisung festgelegt sind, werden ignoriert.  
  
 **\<External_access_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert, ob externe Ressourcen, z. B. Objekte aus einer anderen Datenbank, auf die Datenbank zugreifen können.  
  
 DB_CHAINING { ON | OFF }  
 ON  
 Die Datenbank kann Quelle oder Ziel einer datenbankübergreifenden Besitzverkettung sein.  
  
 OFF  
 Die Datenbank kann nicht an der datenbankübergreifenden Besitzverkettung teilnehmen.  
  
> [!IMPORTANT]  
>  Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erkennt diese Einstellung, wenn die Datenbankübergreifende Besitzverkettung-Serveroption deaktiviert (0 bzw. OFF) ist. Wenn für Datenbankübergreifende Besitzverkettung der Wert 1 (ON) festgelegt ist, können alle Benutzerdatenbanken unabhängig vom Wert dieser Option Teile von datenbankübergreifenden Besitzketten sein. Diese Option wird festgelegt, mit [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Zum Festlegen dieser Option erfordert die CONTROL SERVER-Berechtigung für die Datenbank.  
  
 Die Option DB_CHAINING kann für folgende Systemdatenbanken nicht festgelegt werden: master, model und tempdb.  
  
 Der Status der Option kann mithilfe der Spalte is_db_chaining_on in der sys.databases-Katalogsicht ermittelt werden.  
  
 TRUSTWORTHY { ON | OFF }  
 ON  
 Datenbankmodule (z. B. benutzerdefinierte Funktionen oder gespeicherte Prozeduren), die einen Identitätswechselkontext verwenden, können auf Ressourcen außerhalb der Datenbank zugreifen.  
  
 OFF  
 Datenbankmodule in einem Identitätswechselkontext können nicht auf Ressourcen außerhalb der Datenbank zugreifen.  
  
 TRUSTWORTHY wird auf OFF festgelegt, wenn die Datenbank angefügt wird.  
  
 Standardmäßig ist TRUSTWORTHY für alle Systemdatenbanken mit Ausnahme der msdb-Datenbank auf OFF festgelegt. Für die model-Datenbank und für die tempdb-Datenbank kann der Wert nicht geändert werden. Für die master-Datenbank sollten Sie die Option TRUSTWORTHY niemals auf ON festlegen.  
  
 Zum Festlegen dieser Option erfordert die CONTROL SERVER-Berechtigung für die Datenbank.  
  
 Der Status der Option kann mithilfe der Spalte is_trustworthy_on in der sys.databases-Katalogsicht ermittelt werden.  
  
 DEFAULT_FULLTEXT_LANGUAGE  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Standardsprachenwert für volltextindizierte Spalten an.  
  
> [!IMPORTANT]  
>  Diese Option ist nur zulässig, wenn CONTAINMENT auf PARTIAL festgelegt wurde. Wenn CONTAINMENT auf NONE festgelegt wird, treten Fehler auf.  
  
 DEFAULT_LANGUAGE  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Standardsprache für alle neu erstellten Benutzernamen an. Die Sprache kann durch Bereitstellung der lokalen ID (lcid), des Sprachennamens oder des Sprachenalias angegeben werden. Eine Liste der zulässigen Sprachennamen und Aliase, finden Sie unter [sys.syslanguages &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). Diese Option ist nur zulässig, wenn CONTAINMENT auf PARTIAL festgelegt wurde. Wenn CONTAINMENT auf NONE festgelegt wird, treten Fehler auf.  
  
 NESTED_TRIGGERS  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, ob ein AFTER-Trigger kaskadiert werden kann, d. h., ob er eine Aktion ausführen kann, durch die ein anderer Trigger initiiert wird, der einen weiteren Trigger initiiert usw. Diese Option ist nur zulässig, wenn CONTAINMENT auf PARTIAL festgelegt wurde. Wenn CONTAINMENT auf NONE festgelegt wird, treten Fehler auf.  
  
 TRANSFORM_NOISE_WORDS  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Wird zum Unterdrücken einer Fehlermeldung verwendet, wenn Füllwörter oder Stoppwörter bewirken, dass eine boolesche Operation für eine Volltextabfrage einen Fehler erzeugt. Diese Option ist nur zulässig, wenn CONTAINMENT auf PARTIAL festgelegt wurde. Wenn CONTAINMENT auf NONE festgelegt wird, treten Fehler auf.  
  
 TWO_DIGIT_YEAR_CUTOFF  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt eine ganze Zahl zwischen 1753 und 9999 an, die das Umstellungsjahr für das Interpretieren zweistelliger Jahre als vierstellige Jahre darstellt. Diese Option ist nur zulässig, wenn CONTAINMENT auf PARTIAL festgelegt wurde. Wenn CONTAINMENT auf NONE festgelegt wird, treten Fehler auf.  
  
 **\<FILESTREAM_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Steuert die Einstellungen für FileTables.  
  
 NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
 OFF  
 Nicht transaktionaler Zugriff auf FileTable-Daten ist deaktiviert.  
  
 READ_ONLY  
 FILESTREAM-Daten in FileTables in dieser Datenbank können von nicht transaktionalen Prozessen gelesen werden.  
  
 FULL  
 Der vollständige nicht transaktionale Zugriff auf FILESTREAM-Daten in FileTables ist aktiviert.  
  
 DIRECTORY_NAME =  *\<Directory_name >*  
 Ein Windows-kompatibler Verzeichnisname. Dieser Name sollte für alle Verzeichnisnamen auf Datenbankebene in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz eindeutig sein. Bei Eindeutigkeitsvergleichen wird unabhängig von den Sortiereinstellungen die Groß-/Kleinschreibung nicht beachtet. Diese Option muss vor dem Erstellen einer FileTable in dieser Datenbank festgelegt werden.  
  
 **\<HADR_options >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Finden Sie unter [ALTER DATABASE SET HADR &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-hadr.md).  
  
 **\<Mixed_page_allocation_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)). Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 MIXED_PAGE_ALLOCATION {DEAKTIVIEREN | ON} Steuerelemente kann die Datenbank, ob erste Seiten, die einen gemischten Block für die ersten acht Seiten von einer Tabelle oder eines Indexes mit erstellen.  
  
 OFF  
 Die Datenbank erstellt immer die erste Seiten gleichartigen Blöcken. Dies ist der Standardwert.  
  
 ON  
 Die Datenbank kann die erste Seiten mit gemischten Blöcken erstellen.  
  
 Diese Einstellung ist für alle Systemdatenbanken auf. **Tempdb** ist die einzige Systemdatenbank, die OFF unterstützt.  
  
 **\<PARAMETERIZATION_option >:: =**  
  
 Steuert die Parametrisierungsoption.  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 SIMPLE  
 Abfragen werden basierend auf dem Standardverhalten der Datenbank parametrisiert.  
  
 FORCED  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametrisiert alle Abfragen in der Datenbank.  
  
 Die aktuelle Einstellung der Option kann mithilfe der Spalte is_parameterization_forced in der sys.databases-Katalogsicht ermittelt werden.  
  
 **\<Query_store_options >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 ON | OFF | CLEAR [ ALL ]  
 Steuert, ob der Abfragespeicher in dieser Datenbank aktiviert ist, und steuert außerdem das Entfernen des Inhalts des Abfragespeichers.  
  
ON  
 Der Abfragespeicher aktiviert.  
  
OFF  
 Deaktiviert den Abfragespeicher an.  Dies ist der Standardwert.   
  
CLEAR  
 Entfernen Sie den Inhalt des Abfragespeichers.  
  
OPERATION_MODE  
 Beschreibt den Betriebsmodus des Abfragespeichers. Gültige Werte sind READ_ONLY und READ_WRITE. Im Modus READ_WRITE sammelt und speichert der Abfragespeicher Angaben zum Abfrageplan und statistische Informationen zur Laufzeitausführung. Im Modus READ_ONLY können Informationen aus dem Abfragespeicher gelesen werden, es werden jedoch keine neuen Informationen hinzugefügt. Wenn die maximale Speicherplatzbelegung des Abfragespeichers ausgelastet ist, wird der Betriebsmodus in READ_ONLY geändert.  
  
 CLEANUP_POLICY  
 Beschreibt die Datenaufbewahrungsrichtlinie des Abfragespeichers. STALE_QUERY_THRESHOLD_DAYS bestimmt die Anzahl der Tage, für die die Informationen für eine Abfrage im Abfragespeicher beibehalten wird. STALE_QUERY_THRESHOLD_DAYS weist den Typ **"bigint"**.  
  
 DATA_FLUSH_INTERVAL_SECONDS  
 Bestimmt die Häufigkeit, mit der in den Abfragespeicher geschriebene Daten auf Datenträger gespeichert werden. Um die Leistung zu optimieren, werden durch den Abfragespeicher gesammelte Daten asynchron auf den Datenträger geschrieben. Die Häufigkeit, mit der diese asynchrone Übertragung stattfindet, wird mit dem Argument DATA_FLUSH_INTERVAL_SECONDS konfiguriert. DATA_FLUSH_INTERVAL_SECONDS weist den Typ **"bigint"**.  
  
 MAX_STORAGE_SIZE_MB  
 Bestimmt den Speicherplatz, der vom Abfragespeicher belegt wird. MAX_STORAGE_SIZE_MB-Typ **"bigint"**.  
  
 INTERVAL_LENGTH_MINUTES  
 Bestimmt das Zeitintervall, mit dem statistische Daten zur Laufzeitausführung im Abfragespeicher aggregiert werden. Um die Speicherverwendung zu optimieren, werden die statistischen Daten zur Laufzeitausführung im Speicher für Laufzeitstatistiken über ein festes Zeitfenster aggregiert. Dieses feste Zeitfenster wird mit dem Argument INTERVAL_LENGTH_MINUTES konfiguriert. INTERVAL_LENGTH_MINUTES weist den Typ **"bigint"**.  
  
 SIZE_BASED_CLEANUP_MODE  
 Steuert, ob die Bereinigung automatisch aktiviert wird, wenn die Gesamtmenge der Daten maximalen Größe nähert:  
  
 OFF  
 Größenbasierte Cleanup wird nicht automatisch aktiviert. 
  
 AUTO  
 Größe basierend die Bereinigung wird automatisch aktiviert, wenn Größe auf Datenträger erreicht 90 % der **Max_storage_size_mb**. Größenbasierte Cleanup entfernt zuerst die am wenigsten aufwändigen und ältesten Abfragen. Es hält bei ungefähr 80 % des **Max_storage_size_mb**.  Dies ist der Standardwert für die Konfiguration.  
  
 "Size_based_cleanup_mode"-Typ **Nvarchar**.  
  
 QUERY_CAPTURE_MODE  
 Legt fest, der derzeit aktiven abfrageerfassungsmodus:  
  
 Alle alle Abfragen werden erfasst. Dies ist der Standardwert für die Konfiguration.  Dies ist der Standardwert für die Konfiguration für[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]
  
 Automatische Capture relevanten Abfragen basierend auf der Anzahl und dem Ressourcenverbrauch Ausführung.  Dies ist der Standardwert für die Konfiguration für[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 KEINE stoppen Erfassung neuer Abfragen. Der Abfragespeicher wird fortgesetzt, Kompilier- und Laufzeitstatistiken für Abfragen zu erfassen, die bereits erfasst wurden. Verwenden Sie diese Konfiguration mit Vorsicht, da Sie möglicherweise übersehen, um wichtige Abfragen zu erfassen.  
  
 QUERY_CAPTURE_MODE-Typ **Nvarchar**.  
  
 max_plans_per_query  
 Eine ganze Zahl, die die maximale Anzahl von Plänen darstellt, die für jede Abfrage beibehalten werden. Standardwert ist 200.  
  
 **\<Recovery_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert Datenbankwiederherstellungsoptionen und Datenträger-E/A-Fehlerprüfung.  
  
 FULL  
 Stellt nach einem Medienausfall mithilfe von Transaktionsprotokollsicherungen eine vollständige Wiederherstellung bereit. Falls eine Datendatei beschädigt ist, kann die Medienwiederherstellung alle Transaktionen wiederherstellen, für die ein Commit ausgeführt wurde. Weitere Informationen finden Sie unter [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 BULK_LOGGED  
 Sorgt nach einem Medienfehler für eine Wiederherstellung durch die Kombination der besten Leistung und der geringsten Verwendung von Protokollspeicher für bestimmte umfangreiche Vorgänge oder Massenvorgänge. Weitere Informationen dazu, welche Vorgänge minimal protokolliert werden können, finden Sie unter [das Transaktionsprotokoll &#40; SQLServer &#41; ](../../relational-databases/logs/the-transaction-log-sql-server.md). Bei dem BULK_LOGGED-Wiederherstellungsmodell ist die Protokollierung für diese Vorgänge minimal. Weitere Informationen finden Sie unter [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 SIMPLE  
 Es wird eine einfache Sicherungsstrategie bereitgestellt, die minimalen Protokollspeicherplatz verwendet. Protokollspeicherplatz kann automatisch erneut verwendet werden, wenn er für die Wiederherstellung nach einem Serverfehler nicht mehr benötigt wird. Weitere Informationen finden Sie unter [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
> [!IMPORTANT]  
>  Das Modell der einfachen Wiederherstellung ist einfacher zu verwalten als die anderen beiden Modelle, jedoch auf Kosten eines höheren Datenverlustes, falls eine Datendatei beschädigt ist. Alle Änderungen, die nach der neuesten Datenbank- oder differenziellen Datenbanksicherung durchgeführt wurden, gehen verloren und müssen manuell erneut eingegeben werden.  
  
 Das standardmäßige Wiederherstellungsmodell wird durch das Wiederherstellungsmodell bestimmt die **Modell** Datenbank. Weitere Informationen zum Auswählen des geeigneten Wiederherstellungsmodells finden Sie unter [Wiederherstellungsmodelle &#40; SQLServer &#41; ](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 Der Status dieser Option kann ermittelt werden die **Recovery_model** und **Recovery_model_desc** Spalten in der sys.databases-Katalogsicht oder der Recovery-Eigenschaft der DATABASEPROPERTYEX Funktion.  
  
 TORN_PAGE_DETECTION { ON | OFF }  
 ON  
 Unvollständige Seiten können vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] erkannt werden.  
  
 OFF  
 Unvollständige Seiten können vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht erkannt werden.  
  
> [!IMPORTANT]  
>  Die TORN_PAGE_DETECTION ON | OFF-Syntaxstruktur wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Vermeiden Sie das Verwenden dieser Syntaxstruktur bei neuen Entwicklungsarbeiten, und planen Sie die Änderung von Anwendungen, die diese Syntaxstruktur zurzeit verwenden. Verwenden Sie stattdessen die Option PAGE_VERIFY.  
  
 PAGE_VERIFY { CHECKSUM | TORN_PAGE_DETECTION | NONE }  
 Entdeckt Datenbankseiten, die durch Datenträger-E/A-Pfadfehler beschädigt wurden. Datenträger-E/A-Pfadfehler können die Ursache von Datenbankbeschädigungen sein und werden im Allgemeinen durch Stromausfälle oder Datenträger-Hardwarefehler verursacht, die beim Schreiben der Seite auf den Datenträger auftreten.  
  
 CHECKSUM  
 Berechnet eine Prüfsumme für den Inhalt der gesamten Seite und speichert den Wert im Seitenkopf, wenn eine Seite auf den Datenträger geschrieben wird. Wenn die Seite vom Datenträger gelesen wird, wird die Prüfsumme erneut berechnet und mit dem im Seitenkopf gespeicherten Prüfsummenwert verglichen. Stimmen die Werte nicht überein, wird Fehlermeldung 824 (Hinweis auf einen Prüfsummenfehler) an das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll und an das Windows-Ereignisprotokoll gemeldet. Ein Prüfsummenfehler weist auf ein Problem mit dem E/A-Pfad hin. Um die eigentliche Ursache zu ermitteln, müssen die Hardware, die Firmwaretreiber, das BIOS, die Filtertreiber (z. B. Antivirussoftware) und andere Komponenten des E/A-Pfads untersucht werden.  
  
 TORN_PAGE_DETECTION  
 Speichert ein bestimmtes 2-Bit-Muster für jeden 512-Byte-Sektor in der 8-KB-Datenbankseite und wird im Kopf der Datenbankseite gespeichert, wenn die Seite auf den Datenträger geschrieben wird. Wenn die Seite vom Datenträger gelesen wird, werden die im Seitenkopf gespeicherten zerrissenen Bits mit den tatsächlichen Seitensektorinformationen verglichen. Nicht übereinstimmende Werte weisen darauf hin, dass nur ein Teil der Seite auf den Datenträger geschrieben wurde. In dieser Situation wird Fehlermeldung 824 (Hinweis auf einen Fehler durch eine zerrissene Seite) an das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll und an das Windows-Ereignisprotokoll gemeldet. Zerrissene Seiten werden im Allgemeinen bei der Datenbankwiederherstellung entdeckt, wenn es sich tatsächlich um einen unvollständigen Schreibvorgang für eine Seite handelt. Allerdings können auch andere E/A-Pfadfehler jederzeit eine zerrissene Seite verursachen.  
  
 Keine  
 Schreibvorgänge auf Datenbankseiten erzeugen keinen CHECKSUM- oder TORN_PAGE_DETECTION-Wert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft während eines Lesevorgangs selbst dann keine Prüfsummen oder zerrissenen Seiten, wenn ein CHECKSUM- oder TORN_PAGE_DETECTION-Wert im Seitenkopf vorhanden ist.  
  
 Beachten Sie beim Verwenden der PAGE_VERIFY-Option die folgenden wichtigen Punkte:  
  
-   Der Standardwert ist CHECKSUM.  
  
-   Wenn eine Benutzer- oder Systemdatenbank auf [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder eine höhere Version aktualisiert wird, bleibt der PAGE_VERIFY-Wert (NONE oder TORN_PAGE_DETECTION) erhalten. Sie sollten CHECKSUM verwenden.  
  
    > [!NOTE]  
    >  In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist die Datenbankoption PAGE_VERIFY für die tempdb-Datenbank auf NONE festgelegt und kann nicht geändert werden. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen ist der Standardwert für die Tempdb-Datenbank CHECKSUM für neue Installationen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Bei dem Upgrade einer Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bleibt der Standardwert NONE. Die Option kann geändert werden. Sie sollten CHECKSUM für die tempdb-Datenbank verwenden.  
  
-   TORN_PAGE_DETECTION verwendet zwar weniger Ressourcen, bietet jedoch einen minimalen Teil des Schutzes von CHECKSUM.  
  
-   PAGE_VERIFY kann festgelegt werden, ohne die Datenbank offline zu schalten, zu sperren oder die Parallelität der Datenbank anderweitig zu beeinträchtigen.  
  
-   CHECKSUM und TORN_PAGE_DETECTION schließen sich gegenseitig aus. Beide Optionen können nicht gleichzeitig aktiviert werden.  
  
 Bei Entdecken einer zerrissenen Seite oder eines Prüfsummenfehlers können Sie eine Wiederherstellung ausführen, indem Sie die Daten wiederherstellen oder den Index u. U. neu erstellen, wenn der Fehler auf Indexseiten beschränkt ist. Führen Sie DBCC CHECKDB aus, um bei einem Prüfsummenfehler den Typ der betroffenen Datenbankseite(n) zu bestimmen. Weitere Informationen zu Wiederherstellungsoptionen finden Sie unter [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md). Auch wenn das Datenbeschädigungsproblem durch das Wiederherstellen der Daten behoben wird, sollte die eigentliche Ursache, wie z. B. ein Datenträger-Hardwarefehler, diagnostiziert und baldmöglichst behoben werden, um wiederholte Fehler zu vermeiden.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wiederholt Lesevorgänge, die wegen eines Prüfsummenfehlers, einer zerrissenen Seite oder eines anderen E/A-Fehlers fehlschlagen, vier Mal. Ist der Lesevorgang bei einem dieser Wiederholungsversuche erfolgreich, wird eine Meldung in das Fehlerprotokoll geschrieben, und der Befehl, der den Lesevorgang ausgelöst hat, wird fortgesetzt. Schlagen alle Wiederholungsversuche fehl, schlägt der Befehl mit Fehlermeldung 824 fehl.  
  
 Weitere Informationen zu Prüfsummen, zerrissenen Seiten, lesewiederholungen Nachrichten Fehler 823 und 824 und anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e/a-Überwachungsfunktionen finden Sie in diesem [Microsoft-Website](http://go.microsoft.com/fwlink/?LinkId=47160).  
  
 Die aktuelle Einstellung dieser Option kann ermittelt werden, mithilfe der Page_verify_option-Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht oder der IsTornPageDetectionEnabled-Eigenschaft, der die [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)Funktion.  
  
**\<Remote_data_archive_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Aktiviert oder deaktiviert die Stretch-Datenbank für die Datenbank. Weitere Informationen finden Sie unter [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
REMOTE_DATA_ARCHIVE = {ON (SERVER = \<Servername >, {Anmeldeinformationen = \<Db_scoped_credential_name > | FEDERATED_SERVICE_ACCOUNT = ON | OFF}) | OFF ON  
 Stretch-Datenbank aktiviert für die Datenbank. Weitere Informationen finden Sie zusätzliche erforderliche Komponenten, einschließlich unter [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 **Berechtigungen**. Aktivieren von Stretch-Datenbank für eine Datenbank oder einer Tabelle erfordert Db_owner-Berechtigungen. Stretch-Datenbank für eine Datenbank aktivieren, benötigen Sie außerdem CONTROL DATABASE-Berechtigungen.  
  
SERVER = \<Servername >  
 Gibt die Adresse des Azure-Servers. Enthalten die `.database.windows.net` -Teil des Namens. Beispiel: `MyStretchDatabaseServer.database.windows.net`.  
  
Anmeldeinformationen = \<Db_scoped_credential_name >  
 Gibt die datenbankweite Anmeldeinformationen, die die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verbindung mit dem Azure-Server verwendet. Stellen Sie sicher, dass die Anmeldeinformationen vorhanden ist, bevor Sie diesen Befehl ausführen. Weitere Informationen finden Sie unter [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
FEDERATED_SERVICE_ACCOUNT = ON | AUSSCHALTEN  
 Sie können ein Verbunddienstkonto für den lokalen SQL Server verwenden, um mit der Azure-Remoteserver kommunizieren, wenn alle folgenden Bedingungen zutreffen.  
  
-   Das Dienstkonto, unter dem die SQL Server-Instanz ausgeführt wird, ist ein Domänenkonto.  
  
-   Das Domänenkonto gehört zu einer Domäne, deren Active Directory mit Azure Active Directory verbunden ist.  
  
-   Der Azure-Remoteserver wird konfiguriert, um die Azure Active Directory-Authentifizierung zu unterstützen.  
  
-   Das Dienstkonto, unter dem die SQL Server-Instanz ausgeführt wird, muss auf dem Azure-Remoteserver als ein dbmanager- oder sysadmin-Konto konfiguriert worden sein.  
  
 Wenn Sie ON angeben, kann nicht auch das Argument CREDENTIAL angeben werden. Wenn Sie OFF angeben, müssen Sie das Argument CREDENTIAL angeben.  
  
 OFF  
 Deaktiviert die Stretch-Datenbank für die Datenbank. Weitere Informationen finden Sie unter [Deaktivieren von Stretch Database und Zurückholen von Remotedaten](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).  
  
 Sie können Stretch-Datenbank für eine Datenbank nur deaktivieren, nachdem die Datenbank nicht mehr auf Tabellen enthält, die für Stretch-Datenbank aktiviert sind. Nachdem Sie Stretch-Datenbank deaktivieren, enthalten die Datenmigration beendet und die Abfrageergebnisse nicht mehr Ergebnisse aus Remotetabellen.  
  
 Das Deaktivieren von Stretch wird die Remotedatenbank nicht entfernt werden. Wenn Sie die Remotedatenbank löschen möchten, müssen Sie sie mithilfe des Azure-Verwaltungsportals löschen.  
  
**\<Service_broker_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Steuert die folgenden [!INCLUDE[ssSB](../../includes/sssb-md.md)] Optionen: aktiviert oder deaktiviert die Nachrichtenübermittlung, Festlegen eines neuen [!INCLUDE[ssSB](../../includes/sssb-md.md)] Bezeichner oder Festlegen der konversationsprioritäten auf ON oder OFF.  
  
 ENABLE_BROKER  
 Gibt an, dass [!INCLUDE[ssSB](../../includes/sssb-md.md)] für die angegebene Datenbank aktiviert ist. Die Nachrichtenübermittlung ist gestartet, und das is_broker_enabled-Flag ist in der sys.databases-Katalogsicht auf TRUE festgelegt. Die Datenbank behält den vorhandenen [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Bezeichner bei. Service Broker kann nicht aktiviert werden, während die Datenbank der Prinzipal in einer Datenbank-Spiegelungskonfiguration ist.  
  
> [!NOTE]  
>  ENABLE_BROKER benötigt eine exklusive Datenbanksperre. Wenn Ressourcen in der Datenbank durch andere Sitzungen gesperrt wurden, wartet ENABLE_BROKER, bis die anderen Sitzungen ihre Sperren freigeben. Um [!INCLUDE[ssSB](../../includes/sssb-md.md)] in einer Benutzerdatenbank zu aktivieren, stellen Sie sicher, dass keine anderen Sitzungen auf die Datenbank zugreifen, bevor Sie die Anweisung ALTER DATABASE SET ENABLE_BROKER ausführen. Setzen Sie zum Beispiel die Datenbank in den Einzelbenutzermodus. Um [!INCLUDE[ssSB](../../includes/sssb-md.md)] in der msdb-Datenbank zu aktivieren, beenden Sie zunächst den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agenten, sodass [!INCLUDE[ssSB](../../includes/sssb-md.md)] die erforderliche Sperre abrufen kann.  
  
 DISABLE_BROKER  
 Gibt an, dass [!INCLUDE[ssSB](../../includes/sssb-md.md)] für die angegebene Datenbank deaktiviert ist. Die Nachrichtenübermittlung ist angehalten, und das is_broker_enabled-Flag ist in der sys.databases-Katalogsicht auf FALSE festgelegt. Die Datenbank behält den vorhandenen [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Bezeichner bei.  
  
 NEW_BROKER  
 Gibt an, dass die Datenbank einen neuen Broker-Bezeichner erhalten sollte. Da die Datenbank als neuer Service Broker betrachtet wird, werden alle bestehenden Konversationen in der Datenbank sofort entfernt, ohne Nachrichten über das Beenden des Dialogs zu erstellen. Jede Route, die auf den alten [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Bezeichner verweist, muss mit dem neuen Bezeichner neu erstellt werden.  
  
 ERROR_BROKER_CONVERSATIONS  
 Gibt an, dass die [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Nachrichtenübermittlung aktiviert ist. Dies behält den vorhandenen [!INCLUDE[ssSB](../../includes/sssb-md.md)] Bezeichner für die Datenbank. [!INCLUDE[ssSB](../../includes/sssb-md.md)] beendet alle Konversationen in der Datenbank mit einem Fehler. Auf diese Weise können Anwendungen reguläre Cleanups für bestehende Konversationen ausführen.  
  
 HONOR_BROKER_PRIORITY {ON | OFF}  
 ON  
 Bei Sendevorgängen werden die den Konversationen zugewiesenen Prioritätsstufen berücksichtigt. Nachrichten aus Konversationen mit hohen Prioritätsstufen werden in der Regel vor Nachrichten aus Konversationen mit niedrigen Prioritätsstufen gesendet.  
  
 OFF  
 Sendevorgänge werden so ausgeführt, als ob alle Konversationen die Standardprioritätsstufe haben.  
  
 Änderungen an der HONOR_BROKER_PRIORITY-Option treten bei neuen Dialogfeldern oder Dialogfeldern, in denen keine Nachrichten darauf warten, gesendet zu werden, sofort in Kraft. Bei Dialogfeldern, in denen Nachrichten darauf warten, gesendet zu werden, wenn ALTER DATABASE ausgeführt wird, wird die neue Einstellung erst übernommen, nachdem einige Nachrichten für das Dialogfeld gesendet wurden. Es kann unterschiedlich lange dauern, bis in allen Dialogfeldern die neue Einstellung verwendet wird.  
  
 Die aktuelle Einstellung dieser Eigenschaft wird gemeldet, in der Is_broker_priority_honored-Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.  
  
 **\<Snapshot_option >:: =**  
  
 Bestimmt die Isolationsstufe für Transaktionen.  
  
 ALLOW_SNAPSHOT_ISOLATION { ON| OFF }  
 ON  
 Aktiviert die Momentaufnahmeoption auf Datenbankebene. Wenn die Option aktiviert ist, beginnen DML-Anweisungen mit der Generierung von Zeilenversionen, auch wenn keine Transaktion die Momentaufnahmeisolation verwendet. Sobald diese Option aktiviert ist, können Transaktionen die SNAPSHOT-Transaktionsisolationsstufe angeben. Wenn eine Transaktion auf der SNAPSHOT-Isolationsebene ausgeführt wird, sehen alle Anweisungen eine Momentaufnahme der Daten, wie sie beim Start der Transaktion vorlagen. Greift eine Transaktion, die auf der SNAPSHOT-Isolationsstufe ausgeführt wird, auf Daten in mehreren Datenbanken zu, muss entweder in allen Datenbanken ALLOW_SNAPSHOT_ISOLATION auf ON festgelegt sein oder jede Anweisung in der Transaktion muss Sperrhinweise für alle Verweise in einer FROM-Klausel verwenden, die auf eine Tabelle in einer Datenbank verweisen, bei der ALLOW_SNAPSHOT_ISOLATION auf OFF festgelegt ist.  
  
 OFF  
 Deaktiviert die Momentaufnahmeoption auf Datenbankebene. Transaktionen können die SNAPSHOT-Isolationsstufe für Transaktionen nicht angeben.  
  
 Wenn Sie ALLOW_SNAPSHOT_ISOLATION auf einen neuen Status festlegen (von ON zu OFF oder von OFF zu ON), gibt ALTER DATABASE die Kontrolle erst dann an den Aufrufer zurück, wenn ein Commit aller bestehenden Transaktionen in der Datenbank ausgeführt wurde. Hat die Datenbank bereits den in der ALTER DATABASE-Anweisung angegebenen Status, wird die Kontrolle direkt an den Aufrufer zurückgegeben. Wenn ALTER DATABASE-Anweisung nicht schnell zurückgibt, verwenden Sie [dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) zu bestimmen, ob lang andauernde Transaktionen vorhanden sind. Wird die ALTER DATABASE-Anweisung abgebrochen, bleibt die Datenbank in dem Status, in dem sie sich vor dem Start von ALTER DATABASE befand. Die [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht gibt den Status des Momentaufnahme-Isolationstransaktionen in der Datenbank. Wenn **Snapshot_isolation_state_desc** = IN_TRANSITION_TO_ON, ALTER DATABASE ALLOW_SNAPSHOT_ISOLATION OFF wird, 6 Sekunden angehalten, und wiederholen Sie den Vorgang.  
  
 Sie können den Status von ALLOW_SNAPSHOT_ISOLATION nicht ändern, wenn die Datenbank OFFLINE ist.  
  
 Wenn Sie ALLOW_SNAPSHOT_ISOLATION in einer READ_ONLY-Datenbank festlegen, wird die Einstellung gespeichert, wenn die Datenbank später auf READ_WRITE festgelegt wird.  
  
 Sie können die ALLOW_SNAPSHOT_ISOLATION-Einstellungen für die Datenbanken master, model, msdb und tempdb ändern. Wenn Sie die Einstellung für tempdb ändern, wird die Einstellung jedes Mal beibehalten, wenn die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] beendet und neu gestartet wird. Wenn Sie die Einstellung für model ändern, wird die Einstellung zur Standardeinstellung für alle neu erstellten Datenbanken, mit Ausnahme von tempdb.  
  
 Die Option hat für die Datenbanken master und msdb die Standardeinstellung ON.  
  
 Die aktuelle Einstellung der Option kann mithilfe der Spalte snapshot_isolation_state in der sys.databases-Katalogsicht ermittelt werden.  
  
 READ_COMMITTED_SNAPSHOT { ON | OFF }  
 ON  
 Aktiviert die Option READ COMMITTED-Snapshot auf Datenbankebene. Wenn die Option aktiviert ist, beginnen DML-Anweisungen mit der Generierung von Zeilenversionen, auch wenn keine Transaktion die Momentaufnahmeisolation verwendet. Sobald diese Option aktiviert ist, verwenden Transaktionen, die die Read Committed-Isolationsstufe angeben, anstelle von Sperren die Zeilenversionsverwaltung. Wenn eine Transaktion auf der Read Committed-Isolationsstufe ausgeführt wird, sehen alle Anweisungen eine Momentaufnahme der Daten, wie sie beim Start der Anweisung vorlagen.  
  
 OFF  
 Deaktiviert die Option READ COMMITTED-Snapshot auf Datenbankebene. Transaktionen, die die READ COMMITTED-Isolationsstufe angeben, verwenden Sperren.  
  
 Wenn READ_COMMITTED_SNAPSHOT auf ON oder OFF festgelegt werden soll, dürfen außer der Verbindung, die den ALTER DATABASE-Befehl ausführt, dürfen keine aktiven Verbindungen zur Datenbank bestehen. Die Datenbank muss sich jedoch nicht im Einzelbenutzermodus befinden. Sie können den Status dieser Option nicht ändern, wenn die Datenbank OFFLINE ist.  
  
 Wenn Sie READ_COMMITTED_SNAPSHOT in einer READ_ONLY-Datenbank festlegen, wird die Einstellung beibehalten, wenn die Datenbank später auf READ_WRITE festgelegt wird.  
  
 READ_COMMITTED_SNAPSHOT kann für die Systemdatenbanken master, tempdb oder msdb nicht auf ON festgelegt werden. Wenn Sie die Einstellung für Model ändern, wird die Einstellung der Standard für alle neuen erstellten Datenbanken, mit Ausnahme von Tempdb an.  
  
 Die aktuelle Einstellung der Option kann mithilfe der Spalte is_read_committed_snapshot_on in der sys.databases-Katalogsicht ermittelt werden.  
  
> [!WARNING]  
>  Wenn eine Tabelle erstellt wird, mit **DURABILITY = SCHEMA_ONLY**, und **READ_COMMITTED_SNAPSHOT** wird anschließend mit geändert **ALTER DATABASE**, Daten in der Tabelle gehen verloren.  
  
 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT { ON | OFF }  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ON  
 Wenn die Isolationsstufe für Transaktionen auf eine niedrigere Isolationsstufe als SNAPSHOT festgelegt wird (beispielsweise READ COMMITTED oder READ UNCOMMITTED), werden alle interpretierten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Vorgänge für speicheroptimierte Tabelle unter der Isolationsstufe SNAPSHOT ausgeführt. Dies erfolgt ungeachtet des Umstands, ob die Transaktionsisolationsstufe explizit auf der Sitzungsebene festgelegt ist, oder ob implizit die Standardeinstellung verwendet wird.  
  
 OFF  
 Erhöht nicht die Isolationsstufe für Transaktionen für interpretierte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Vorgänge für speicheroptimierte Tabellen.  
  
 Sie können den Status von MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT nicht ändern, wenn die Datenbank OFFLINE ist.  
  
 Standardmäßig ist die Option auf OFF festgelegt.  
  
 Die aktuelle Einstellung dieser Option kann ermittelt werden die **Is_memory_optimized_elevate_to_snapshot_on** Spalte in der [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.  
  
 **\<Sql_option >:: =**  
  
 Steuert die ANSI-Kompatibilitätsoptionen auf der Datenbankebene.  
  
 ANSI_NULL_DEFAULT { ON | OFF }  
 Legt den Standardwert NULL oder NOT NULL, eine Spalte oder [CLR-benutzerdefinierten Typ](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) für die die NULL-Zulässigkeit nicht explizit in CREATE TABLE oder ALTER TABLE-Anweisung definiert ist. Spalten, die mit Einschränkungen definiert werden, folgen den Einschränkungsregeln, und zwar ungeachtet dieser Einstellung.  
  
 ON  
 Der Standardwert ist NULL.  
  
 OFF  
 Der Standardwert ist NOT NULL.  
  
 Einstellungen auf Verbindungsebene, die mithilfe der SET-Anweisung festgelegt werden, überschreiben die Standardeinstellung der Datenbank für ANSI_NULL_DEFAULT. ODBC- und OLE DB-Clients geben standardmäßig eine SET-Anweisung aus, durch die ANSI_NULL_DEFAULT für die Sitzung auf ON festgelegt wird, wenn sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Weitere Informationen finden Sie unter [SET ANSI_NULL_DFLT_ON &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md).  
  
 Für die ANSI-Kompatibilität wird durch Festlegen der Datenbankoption ANSI_NULL_DEFAULT auf ON der Datenbankstandardwert auf NULL geändert.  
  
 Der Status dieser Option kann mithilfe der Spalte is_ansi_null_default_on in der sys.databases-Katalogsicht oder der IsAnsiNullDefault-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 ANSI_NULLS { ON | OFF }  
 ON  
 Alle Vergleiche mit einem Nullwert ergeben UNKNOWN.  
  
 OFF  
 Vergleiche von Nicht-UNICODE-Werten mit einem Nullwert ergeben TRUE, wenn beide Werte NULL sind.  
  
> [!IMPORTANT]  
>  In einer späteren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ANSI_NULLS immer auf ON festgelegt, und jede Anwendung, für die die Option explizit auf OFF festgelegt wird, löst einen Fehler aus. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
  
 Einstellungen auf Verbindungsebene, die mithilfe der SET-Anweisung festgelegt werden, überschreiben die Standardeinstellung der Datenbank für ANSI_NULLS. ODBC- und OLE DB-Clients geben standardmäßig eine SET-Anweisung aus, durch die ANSI_NULLS für die Sitzung auf ON festgelegt wird, wenn sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Weitere Informationen finden Sie unter [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 SET ANSI_NULLS muss ebenfalls auf ON festgelegt sein, wenn Sie Indizes auf berechneten Spalten oder indizierten Sichten erstellen oder ändern.  
  
 Der Status dieser Option kann mithilfe der Spalte is_ansi_null_on in der sys.databases-Katalogsicht oder der IsAnsiNullsEnabled-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 ANSI_PADDING { ON | OFF }  
 ON  
 Zeichenfolgen werden auf dieselbe Länge aufgefüllt, vor der Konvertierung oder zum Einfügen einer **Varchar** oder **Nvarchar** -Datentyp.  
  
 Nachfolgende Leerzeichen in Zeichenwerten, die eingefügt **Varchar** oder **Nvarchar** Spalten und nachfolgende Nullen in Binärwerten, die eingefügt **Varbinary** Spalten werden nicht abgeschnitten. . Werte werden nicht bis zur Spaltenlänge aufgefüllt.  
  
 OFF  
 Nachfolgende Leerzeichen für **Varchar** oder **Nvarchar** und Nullen für **Varbinary** werden abgeschnitten.  
  
 Ist OFF festgelegt, wirkt sich diese Einstellung nur auf die Definition neuer Spalten aus.  
  
> [!IMPORTANT]  
>  In einer späteren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ANSI_PADDING immer auf ON festgelegt, und jede Anwendung, für die die Option explizit auf OFF festgelegt ist, löst einen Fehler aus. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Es wird empfohlen, für ANSI_PADDING stets den Wert ON festzulegen. ANSI_PADDING muss beim Erstellen oder Bearbeiten von Indizes für berechnete Spalten oder indizierte Sichten auf ON festgelegt sein.  
  
 **Char (*n*) ** und  **binäre (*n*) ** Spalten, die es ermöglichen, für NULL-Werte auf die Länge der Spalte aufgefüllt werden, wenn ANSI_PADDING festgelegt ist auf ON aber nachfolgende Leerzeichen und Nullen werden abgeschnitten, wenn ANSI_PADDING auf OFF festgelegt ist. **Char (*n*) ** und  **binäre (*n*) ** Spalten, die keine NULL-Werte zulassen, werden immer auf die Länge der Spalte aufgefüllt.  
  
 Einstellungen auf Verbindungsebene, die mithilfe der SET-Anweisung festgelegt werden, überschreiben die Standardeinstellung der Datenbank für ANSI_PADDING. ODBC- und OLE DB-Clients geben standardmäßig eine SET-Anweisung aus, durch die ANSI_PADDING für die Sitzung auf ON festgelegt wird, wenn sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Weitere Informationen finden Sie unter [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
 Der Status dieser Option kann mithilfe der Spalte is_ansi_padding_on in der sys.databases-Katalogsicht oder der IsAnsiPaddingEnabled-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 ANSI_WARNINGS { ON | OFF }  
 ON  
 Fehler oder Warnungen werden ausgegeben, wenn Bedingungen wie eine Division durch Null oder Nullwerte in Aggregatfunktionen auftreten.  
  
 OFF  
 Bei Bedingungen wie einer Division durch Null werden keine Warnungen ausgegeben, und Nullwerte werden zurückgegeben.  
  
 SET ANSI_WARNINGS muss auf ON festgelegt sein, wenn Sie Indizes auf berechneten Spalten oder indizierten Sichten erstellen oder ändern.  
  
 Einstellungen auf Verbindungsebene, die mithilfe der SET-Anweisung festgelegt werden, überschreiben die Standardeinstellung der Datenbank für ANSI_WARNINGS. ODBC- und OLE DB-Clients geben standardmäßig eine SET-Anweisung aus, durch die ANSI_WARNINGS für die Sitzung auf ON festgelegt wird, wenn sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Weitere Informationen finden Sie unter [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md).  
  
 Der Status dieser Option kann mithilfe der Spalte is_ansi_warnings_on in der sys.databases-Katalogsicht oder der IsAnsiWarningsEnabled-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 ARITHABORT { ON | OFF }  
 ON  
 Eine Abfrage wird beendet, wenn während der Abfrage ein Überlauffehler oder ein Fehler aufgrund einer Division durch Null auftritt.  
  
 OFF  
 Es wird eine Warnmeldung angezeigt, wenn einer dieser Fehler auftritt. Die Abfrage, der Batch oder die Transaktion wird jedoch so fortgeführt, als sei kein Fehler aufgetreten.  
  
 SET ARITHABORT muss auf ON festgelegt sein, wenn Sie Indizes auf berechneten Spalten oder indizierten Sichten erstellen oder ändern.  
  
 Der Status dieser Option kann mithilfe der Spalte is_arithabort_on in der sys.databases-Katalogsicht oder der IsArithmeticAbortEnabled-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 COMPATIBILITY_LEVEL { 90 | 100 | 110 | 120}  
 Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 CONCAT_NULL_YIELDS_NULL { ON | OFF }  
 ON  
 Das Ergebnis einer Verkettungsoperation ist NULL, wenn einer der Operanden NULL ist. Wenn z. B. die Zeichenfolge "This is" und NULL verkettet wird, ist das Ergebnis NULL statt "This is".  
  
 OFF  
 Der Nullwert wird als leere Zeichenfolge behandelt.  
  
 CONCAT_NULL_YIELDS_NULL muss auf ON festgelegt sein, wenn Sie Indizes auf berechneten Spalten oder indizierten Sichten erstellen oder ändern.  
  
> [!IMPORTANT]  
>  In einer späteren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird CONCAT_NULL_YIELDS_NULL immer auf ON festgelegt, und jede Anwendung, für die die Option explizit auf OFF festgelegt wurde, löst einen Fehler aus. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
  
 Einstellungen auf Verbindungsebene, die mithilfe der SET-Anweisung festgelegt werden, überschreiben die Standardeinstellung der Datenbank für CONCAT_NULL_YIELDS_NULL. ODBC- und OLE DB-Clients geben standardmäßig eine SET-Anweisung aus, durch die CONCAT_NULL_YIELDS_NULL für die Sitzung auf ON festgelegt wird, wenn sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Weitere Informationen finden Sie unter [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
 Der Status dieser Option kann mithilfe der Spalte is_concat_null_yields_null_on in der sys.databases-Katalogsicht oder der IsNullConcat-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 QUOTED_IDENTIFIER { ON | OFF }  
 ON  
 Doppelte Anführungszeichen können nur zum Einschließen von Begrenzungsbezeichnern verwendet werden.  
  
 Alle Zeichenfolgen, die durch doppelte Anführungszeichen begrenzt werden, werden als Objektbezeichner interpretiert. Bezeichner in Anführungszeichen müssen nicht den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Regeln für Bezeichner entsprechen. Sie können Schlüsselwörter darstellen und Zeichen einschließen, die in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Bezeichnern sonst nicht zulässig sind. Ein einfaches Anführungszeichen (’), das zur Literalzeichenfolge selbst gehört, kann durch doppelte Anführungszeichen (’’) dargestellt werden.  
  
 OFF  
 Bezeichner dürfen nicht in Anführungszeichen eingeschlossen werden und müssen allen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Regeln für Bezeichner entsprechen. Literale können in einfache oder doppelte Anführungszeichen eingeschlossen werden.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist es zudem möglich, Bezeichner durch eckige Klammern ([ ]) zu begrenzen. Eckige Klammern als Begrenzungszeichen können jederzeit verwendet werden. Die Einstellung für QUOTED_IDENTIFIER spielt keine Rolle. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 Beim Erstellen einer Tabelle wird die Option QUOTED IDENTIFIER immer als ON in den Metadaten der Tabelle gespeichert, selbst wenn die Option beim Erstellen der Tabelle auf OFF festgelegt war.  
  
 Einstellungen auf Verbindungsebene, die mithilfe der SET-Anweisung festgelegt werden, überschreiben die Standardeinstellung der Datenbank für QUOTED_IDENTIFIER. ODBC- und OLE DB-Clients geben standardmäßig eine SET-Anweisung aus, durch die QUOTED_IDENTIFIER auf ON festgelegt wird, wenn sie eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 Der Status dieser Option kann mithilfe der Spalte is_quoted_identifier_on in der sys.databases-Katalogsicht oder der IsQuotedIdentifiersEnabled-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 NUMERIC_ROUNDABORT { ON | OFF }  
 ON  
 Es wird ein Fehler generiert, wenn ein Genauigkeitsverlust in einem Ausdruck auftritt.  
  
 OFF  
 Bei Genauigkeitsverlusten werden keine Fehlermeldungen generiert, und das Ergebnis wird auf die Genauigkeit der Spalte oder Variablen gerundet, die das Ergebnis speichert.  
  
 NUMERIC_ROUNDABORT muss auf OFF festgelegt sein, wenn Sie Indizes auf berechneten Spalten oder indizierten Sichten erstellen oder ändern.  
  
 Der Status dieser Option kann mithilfe der Spalte is_numeric_roundabort_on in der sys.databases-Katalogsicht oder der IsNumericRoundAbortEnabled-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 RECURSIVE_TRIGGERS { ON | OFF }  
 ON  
 Das rekursive Auslösen von AFTER-Triggern ist zugelassen.  
  
 OFF  
 Nur das direkte rekursive Auslösen von AFTER-Triggern ist nicht zugelassen. Um die indirekte Rekursion von AFTER-Trigger deaktivieren, legen Sie die geschachtelte Trigger Option "Server" auf **0** mit **Sp_configure**.  
  
> [!NOTE]  
>  Nur die direkte Rekursion wird verhindert, wenn RECURSIVE_TRIGGERS auf OFF festgelegt ist. Sie müssen auch die Geschachtelte Trigger-Serveroption auf 0 festlegen, um die indirekte Rekursion zu deaktivieren.  
  
 Der Status dieser Option kann mithilfe der Spalte is_recursive_triggers_on in der sys.databases-Katalogsicht oder der IsRecursiveTriggersEnabled-Eigenschaft der DATABASEPROPERTYEX-Funktion ermittelt werden.  
  
 **\<Target_recovery_time_option >:: =**  
  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Nicht verfügbar in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Gibt die Frequenz indirekter Prüfpunkte auf Basis einzelner Datenbanken an. Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] der Standardwert für neue Datenbanken ist 1 Minute, der die Datenbank wird mithilfe von indirekten Prüfpunkten angibt. Für frühere Versionen ist die Standardeinstellung 0, was bedeutet, dass die Datenbank automatische Prüfpunkte verwendet, deren Frequenz von der Einstellung für Wiederherstellung der Server-Instanz abhängig ist. [!INCLUDE[msCoName](../../includes/msconame-md.md)]empfiehlt eine Minute für die meisten Systeme.  
  
 TARGET_RECOVERY_TIME **=***Zielwiederherstellungszeit* {SECONDS | MINUTES}  
 *target_recovery_time*  
 Gibt die maximale Grenze für die Zeit an, die für die Wiederherstellung der angegebenen Datenbank im Fall eines Fehlers aufgewendet wird.  
  
 SECONDS  
 Gibt an, dass *target_recovery_time* die Anzahl von Sekunden darstellt.  
  
 MINUTES  
 Gibt an, dass *target_recovery_time* die Anzahl von Minuten darstellt.  
  
 Weitere Informationen zu indirekten Prüfpunkten finden Sie unter [Datenbankprüfpunkte &#40; SQLServer &#41; ](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 **MIT \<Beendigung >:: =**  
  
 Gibt an, wann beim Übergang der Datenbank von einem Status in einen anderen für unvollständige Transaktionen ein Rollback ausgeführt werden soll. Wird die Beendigungsklausel ausgelassen, wartet die ALTER DATABASE-Anweisung auf unbestimmte Zeit, wenn keine Sperre für die Datenbank besteht. Es kann nur eine Beendigungsklausel angegeben werden, und diese steht hinter den SET-Klauseln.  
  
> [!NOTE]  
>  Nicht alle Datenbankoptionen verwenden die WITH \<Termination >-Klausel. Weitere Informationen finden Sie in der Tabelle unter "[Festlegen von Optionen](#SettingOptions) der im Abschnitt"Hinweise"in diesem Thema.  
  
 ROLLBACK AFTER *Ganzzahl* [SECONDS] | ROLLBACK SOFORT  
 Gibt an, ob ein Rollback sofort oder nach Ablauf der angegebenen Sekundenzahl ausgeführt werden soll.  
  
 NO_WAIT  
 Gibt an, dass die Anforderung fehlschlägt, wenn diese Änderung des Datenbankstatus oder der Datenbankoption nicht sofort vollständig vorgenommen werden kann, ohne dass darauf gewartet werden muss, dass Transaktionen selbst einen Commit oder Rollback ausführen.  
  
##  <a name="SettingOptions"></a>Festlegen von Optionen  
 Um die aktuelle Einstellungen für Datenbankoptionen abzurufen, verwenden Sie die [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht oder [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)  
  
 Wenn Sie eine Datenbankoption festlegen, tritt die Änderung sofort in Kraft.  
  
 Wenn Sie die Standardwerte einer Datenbankoption für alle neu erstellten Datenbanken ändern möchten, ändern Sie die entsprechende Datenbankoption in der model-Datenbank.  
  
 Nicht alle Datenbankoptionen verwenden die WITH \<Termination >-Klausel oder kann in Kombination mit anderen Optionen angegeben werden. In der folgenden Tabelle sind die Optionen und ihr Options- und Beendigungsstatus aufgeführt.  
  
|Optionskategorie|Kann mit anderen Optionen angegeben werden|Verwenden Sie die WITH können \<Termination >-Klausel|  
|----------------------|-----------------------------------------|---------------------------------------------|  
|\<Db_state_option >|ja|ja|  
|\<Db_user_access_option >|ja|ja|  
|\<Db_update_option >|ja|ja|  
|\<Delayed_durability_option >|ja|ja|  
|\<External_access_option >|ja|Nein|  
|\<Cursor_option >|ja|Nein|  
|\<Auto_option >|ja|Nein|  
|\<Sql_option >|ja|Nein|  
|\<Recovery_option >|ja|Nein|  
|\<Target_recovery_time_option >|Nein|ja|  
|\<Database_mirroring_option >|Nein|Nein|  
|ALLOW_SNAPSHOT_ISOLATION|Nein|Nein|  
|READ_COMMITTED_SNAPSHOT|Nein|ja|  
|MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT|ja|ja|  
|\<Service_broker_option >|ja|Nein|  
|DATE_CORRELATION_OPTIMIZATION|ja|ja|  
|\<Parameterization_option >|ja|ja|  
|\<Change_tracking_option >|ja|ja|  
|\<Db_encryption >|ja|Nein|  
  
 Der Plancache für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird gelöscht, indem eine der folgenden Optionen festgelegt wird:  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY||  
  
 Der Prozedurcache wird auch in den folgenden Szenarien geleert.  
  
-   Die AUTO_CLOSE-Datenbankoption ist für eine Datenbank auf ON festgelegt. Wenn die Datenbank von keiner Benutzerverbindung verwendet wird bzw. keine Benutzerverbindung darauf verweist, versucht der Hintergrundtask, die Datenbank automatisch zu schließen und herunterzufahren.  
  
-   Sie führen mehrere Abfragen für eine Datenbank aus, die über Standardoptionen verfügt. Anschließend wird die Datenbank gelöscht.  
  
-   Eine Datenbank-Momentaufnahme für eine Quelldatenbank wird gelöscht.  
  
-   Sie erstellen das Transaktionsprotokoll für eine Datenbank erfolgreich neu.  
  
-   Sie stellen eine Datenbanksicherung wieder her.  
  
-   Sie trennen eine Datenbank.  
  
 Durch das Löschen des Plancaches wird eine Neukompilierung aller nachfolgenden Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. Für jeden gelöschten Cachespeicher im Plancache enthält das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll folgende Informationsmeldung: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat für den %s-Cachespeicher (Bestandteil des Plancache) %d Leerungen des Cachespeichers gefunden, die von Datenbankwartungs- oder Neukonfigurierungsvorgängen ausgelöst wurden". Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-setting-options-on-a-database"></a>A. Festlegen von Optionen für eine Datenbank  
 Im folgenden Beispiel werden die Optionen für das Wiederherstellungsmodell und die Datenseitenüberprüfung für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank festgelegt.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL PAGE_VERIFY CHECKSUM;  
GO  
  
```  
  
### <a name="b-setting-the-database-to-readonly"></a>B. Festlegen der Datenbank auf READ_ONLY  
 Das Ändern des Status einer Datenbank oder Dateigruppe auf READ_ONLY oder READ_WRITE erfordert den exklusiven Zugriff auf die Datenbank. Im folgenden Beispiel wird die Datenbank auf den `SINGLE_USER`-Modus festgelegt, um exklusiven Zugriff zu erhalten. Anschließend wird in dem Beispiel der Status der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank auf `READ_ONLY` festgelegt und der Zugriff auf die Datenbank an alle Benutzer zurückgegeben.  
  
> [!NOTE]  
>  In diesem Beispiel wird die Beendigungsoption `WITH ROLLBACK IMMEDIATE` in der ersten `ALTER DATABASE`-Anweisung verwendet. Für alle unvollständigen Transaktionen wird ein Rollback ausgeführt, und alle anderen Verbindungen zur [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank werden sofort getrennt.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER  
WITH ROLLBACK IMMEDIATE;  
GO  
ALTER DATABASE AdventureWorks2012  
SET READ_ONLY  
GO  
ALTER DATABASE AdventureWorks2012  
SET MULTI_USER;  
GO  
  
```  
  
### <a name="c-enabling-snapshot-isolation-on-a-database"></a>C. Aktivieren der Momentaufnahmeisolation für eine Datenbank  
 Im folgenden Beispiel wird die Option für das Momentaufnahmeisolations-Framework für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank aktiviert.  
  
```  
USE AdventureWorks2012;  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
-- Check the state of the snapshot_isolation_framework  
-- in the database.  
SELECT name, snapshot_isolation_state,   
    snapshot_isolation_state_desc AS description  
FROM sys.databases  
WHERE name = N'AdventureWorks2012';  
GO  
  
```  
  
 Das Resultset zeigt, dass das Framework für die Momentaufnahmeisolation aktiviert ist.  
  
 |name |snapshot_isolation_state |Beschreibung|  
 |-------------------- |------------------------  |----------|  
 |AdventureWorks2012   |1                        | ON |  
  
### <a name="d-enabling-modifying-and-disabling-change-tracking"></a>D. Aktivieren, Ändern und Deaktivieren der Änderungsnachverfolgung  
 Im folgenden Beispiel wird die Änderungsnachverfolgung für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank aktiviert und die Aufbewahrungsdauer auf `2` Tage festgelegt.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(AUTO_CLEANUP = ON, CHANGE_RETENTION = 2 DAYS);  
```  
  
 Das folgende Beispiel veranschaulicht, wie die Beibehaltungsdauer in `3` Tage geändert wird.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING (CHANGE_RETENTION = 3 DAYS);  
```  
  
 Das folgende Beispiel veranschaulicht, wie die Änderungsnachverfolgung für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank deaktiviert wird.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF;  
```  
  
### <a name="e-enabling-the-query-store"></a>E. Aktivieren des Abfragespeichers  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Im folgenden Beispiel werden der Abfragespeicher aktiviert und Parameter des Abfragespeichers konfiguriert.  
  
```  
ALTER DATABASE AdventureWorks2012  
SET QUERY_STORE = ON   
    (  
      OPERATION_MODE = READ_ONLY   
    , CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 5 )  
    , DATA_FLUSH_INTERVAL_SECONDS = 2000   
    , MAX_STORAGE_SIZE_MB = 10   
    , INTERVAL_LENGTH_MINUTES = 10   
    );  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [ALTER DATABASE-Datenbankspiegelung &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [Statistiken](../../relational-databases/statistics/statistics.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Aktivieren und Deaktivieren der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Sys. data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
  

