---
title: ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2e347cc80ec70e765a59364037ace04eed1908ae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Diese Anweisung aktiviert mehrere Einstellungen für die Datenbankkonfiguration auf der Ebene **einzelner Datenbanken**. Sie ist in [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] und in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] verfügbar. Zu diesen Einstellungen zählen die folgenden:  
  
- Löschen des Prozedurcaches.  
- Festlegen des MAXDOP-Parameters auf einen beliebigen Wert (1,2, ...) für die primäre Datenbank, basierend auf dem, was am besten für diese bestimmte Datenbank ist, und Festlegen eines anderen Werts (z.B. 0) für alle verwendeten sekundären Datenbanken (z.B. für Berichtsabfragen).  
- Festlegen des Kardinalitätsschätzungsmodells für den Abfrageoptimierer unabhängig von der Datenbank auf den Kompatibilitätsgrad.  
- Aktivieren oder Deaktivieren der Parameterermittlung auf Datenbankebene.
- Aktivieren oder Deaktivieren der Abfrageoptimierungs-Hotfixes auf Datenbankebene.
- Aktivieren oder Deaktivieren des Identitätscache auf Datenbankebene.
- Aktivieren oder Deaktivieren eines Stubs des kompilierten Plans, der bei der erstmaligen Kompilierung eines Batches im Cache gespeichert werden soll.  
- Aktivieren oder Deaktivieren von Sammlungen von Ausführungsstatistiken für nativ kompilierte T-SQL-Module.
  
 ![Linksymbol](../../database-engine/configure-windows/media/topic-link.gif "Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER DATABASE SCOPED CONFIGURATION  
{        
     {  [ FOR SECONDARY] SET <set_options>  }    
}  
| CLEAR PROCEDURE_CACHE  
| SET < set_options >
[;]    
  
< set_options > ::=    
{  
    MAXDOP = { <value> | PRIMARY}    
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}    
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}    
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
    | OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }
    | XTP_PROCEDURE_EXECUTION_STATISTICS = { ON | OFF } 
    | XTP_QUERY_EXECUTION_STATISTICS = { ON | OFF }     
}  
```  
  
## <a name="arguments"></a>Argumente  
 
FOR SECONDARY  
 
Gibt die Einstellungen für sekundäre Datenbanken an (alle sekundären Datenbanken müssen identische Werte aufweisen).  
  
MAXDOP **=** {\<value> | PRIMARY }  
**\<value>**  
  
Gibt die MAXDOP-Standardeinstellung an, die für Anweisungen verwendet werden sollte. 0 ist der Standardwert und gibt an, dass die Serverkonfiguration stattdessen verwendet wird. Mit der MAXDOP-Einstellung im Datenbankbereich wird der **max. Grad an Parallelität** auf der Serverebene von sp_configure überschrieben (sofern sie nicht auf 0 festgelegt ist). Abfragehinweise können die MAXDOP-Einstellung im Datenbankbereich weiterhin überschreiben, damit bestimmte Abfragen optimiert werden können, für die andere Einstellungen erforderlich sind. All diese Einstellungen werden durch die MAXDOP-Einstellung für die Arbeitsauslastungsgruppe begrenzt.   

Mithilfe der Option Max. Grad an Parallelität kann die Anzahl der Prozessoren beschränkt werden, die bei der Ausführung paralleler Pläne verwendet werden. SQL Server berücksichtigt die Ausführung paralleler Pläne für Abfragen, DDL-Indizierungsoperationen (Datendefinitionssprache, Data Definition Language), parallele Einfügevorgänge, Onlineausführung von ALTER COLUMN, parallele Sammlung von Statistiken sowie die statische und keysetgesteuerte Cursorauffüllung.
 
Informationen zum Festlegen dieser Option auf Instanzebene finden Sie unter [Konfigurieren der Serverkonfigurationsoption „Max. Grad an Parallelität“](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). 

> [!TIP] 
> Fügen Sie den [Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) **MAXDOP** hinzu, um dies auf Abfrageebene zu erreichen.  
  
PRIMARY  
  
Kann nur für die sekundären Datenbanken festgelegt werden, während die betreffende Datenbank die primäre ist, und gibt an, dass diese Konfiguration für die primäre Datenbank festgelegt wird. Wenn sich die Konfiguration für die primäre Datenbank ändert, ändert sich der Wert für die sekundären Datenbanken entsprechend, ohne dass dieser Wert explizit festgelegt werden muss. **PRIMARY** ist die Standardeinstellung für die sekundären Datenbanken.  
  
LEGACY_CARDINALITY_ESTIMATION **=** { ON | **OFF** | PRIMARY }  

Damit können Sie das Kardinalitätsschätzungsmodell für den Abfrageoptimierer unabhängig vom Kompatibilitätsgrad der Datenbank in SQL Server 2012 und früheren Versionen festlegen. Die Standardeinstellung ist **OFF**. Sie legt das Kardinalitätsschätzungsmodell für den Abfrageoptimierer basierend auf dem Kompatibilitätsgrad der Datenbank fest. Das Festlegen dieser Einstellung auf **ON** entspricht der Aktivierung des [Ablaufverfolgungsflags 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

> [!TIP] 
> Fügen Sie den [Abfragehinweis](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) **QUERYTRACEON** hinzu, um dies auf Abfrageebene zu erreichen. Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 müssen Sie den [Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) **USE HINT** hinzufügen, statt das Ablaufverfolgungsflag zu verwenden, um dies auf Abfrageebene zu erreichen. 
  
PRIMARY  
  
Dieser Wert ist nur für sekundäre Datenbanken gültig, während die betreffende Datenbank die primäre ist, und gibt an, dass es sich bei der Einstellung des Kardinalitätsschätzungsmodells für den Abfrageoptimierer für alle sekundären Datenbanken um den für die primäre Datenbank festgelegten Wert handelt. Wenn sich die Konfiguration für die primäre Datenbank im Kardinalitätsschätzungsmodell des Abfrageoptimierers ändert, ändert sich der Wert für die sekundären Datenbanken entsprechend. **PRIMARY** ist die Standardeinstellung für die sekundären Datenbanken.  
  
PARAMETER_SNIFFING **=** { **ON** | OFF | PRIMARY}  

Aktiviert oder deaktiviert die [Parameterermittlung](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing). Der Standardwert ist ON. Dies entspricht dem [Ablaufverfolgungsflag 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Informationen darüber, wie Sie dies auf Abfrageebene erreichen, finden Sie unter dem [Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) **OPTIMIZE FOR UNKNOWN**. Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 ist der [Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) **USE HINT** auch verfügbar, damit dies auf Abfrageebene erreicht werden kann. 
  
PRIMARY  
  
Dieser Wert ist nur für sekundäre Datenbanken gültig, während die betreffende Datenbank primär ist, und gibt an, dass es sich bei dem Wert für diese Einstellung für alle sekundären Datenbanken um den für die primäre Datenbank festgelegten Wert handelt. Wenn sich die Konfiguration für die primäre Datenbank bei der Verwendung der [Parameterermittlung](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing) ändert, ändert sich der Wert für die sekundären Datenbanken entsprechend, ohne dass dieser Wert explizit festgelegt werden muss. Dies ist die Standardeinstellung für die sekundären Datenbanken.  
  
QUERY_OPTIMIZER_HOTFIXES **=** { ON | **OFF** | PRIMARY }  

Aktiviert oder deaktiviert Hotfixes für die Abfrageoptimierung unabhängig vom Kompatibilitätsgrad der Datenbank. Die Standardeinstellung ist **OFF**. Sie deaktiviert Hotfixes für Abfrageoptimierer, die nach der Einführung des höchsten verfügbaren Kompatibilitätsgrads für eine bestimmte Version (post-RTM) veröffentlicht wurden. Ein Festlegen dieser Einstellung auf **ON** entspricht der Aktivierung des [Ablaufverfolgungsflags 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Fügen Sie den [Abfragehinweis](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) **QUERYTRACEON** hinzu, um dies auf Abfrageebene zu erreichen. Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 müssen Sie den [Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) USE HINT hinzufügen, statt das Ablaufverfolgungsflag zu verwenden, um dies auf Abfrageebene zu erreichen.  
  
PRIMARY  
  
Dieser Wert ist nur für sekundäre Datenbanken gültig, während die betreffende Datenbank primär ist, und gibt an, dass es sich bei dem Wert für diese Einstellung für alle sekundären Datenbanken um den für die primäre Datenbank festgelegten Wert handelt. Wenn sich die Konfiguration für die primäre Datenbank ändert, ändert sich der Wert für die sekundären Datenbanken entsprechend, ohne dass dieser Wert explizit festgelegt werden muss. Dies ist die Standardeinstellung für die sekundären Datenbanken.  
  
CLEAR PROCEDURE_CACHE  

Löscht den Cache der Datenbank für die Prozedur bzw. den Prozedurplan. Dieser Vorgang kann in den primären und den sekundären Datenbanken ausgeführt werden.  

IDENTITY_CACHE **=** { **ON** | OFF }  

**Gilt für** : [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

Aktiviert oder deaktiviert den Identitätscache auf Datenbankebene. Der Standardwert ist **ON**. Identitätszwischenspeichern wird verwendet, um die Leistung von INSERT in Tabellen mit Identitätsspalten zu verbessern. Deaktiviert die Option IDENTITY_CACHE, um Lücken in einer Identitätsspalte zu vermeiden, wenn der Server unerwartet neu gestartet oder ein Failover zu einem sekundären Server ausgeführt wird. Diese Option ist mit dem vorhandenen [Ablaufverfolgungsflag 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) vergleichbar. Der einzige Unterschied besteht darin, dass sie auf Datenbankebene und nicht nur auf Serverebene festgelegt werden kann.   

> [!NOTE] 
> Diese Option kann nur für PRIMARY festgelegt werden. Weitere Informationen finden Sie unter [Identitätsspalten](create-table-transact-sql-identity-property.md).  

OPTIMIZE_FOR_AD_HOC_WORKLOADS **=** { ON | **OFF** }  

**Gilt für:** [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] 

Aktiviert oder deaktiviert einen Stub des kompilierten Plans, der bei der erstmaligen Kompilierung eines Batches im Cache gespeichert werden soll. Der Standardwert ist OFF. Sobald die datenbankweite Konfiguration OPTIMIZE_FOR_AD_HOC_WORKLOADS für eine Datenbank aktiviert ist, wird ein Stub des kompilierten Plans zwischengespeichert, wenn ein Batch zum ersten Mal kompiliert wird. Planstubs weisen im Vergleich zur Größe des vollständigen kompilierten Plans einen niedrigeren Speicherbedarf auf.  Wenn ein Batch erneut kompiliert oder ausgeführt wird, wird der Stub des kompilierten Plans entfernt und durch einen vollständigen kompilierten Plan ersetzt.

XTP_PROCEDURE_EXECUTION_STATISTICS  **=** { ON | **OFF** }  

**Gilt für:** [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 

Aktiviert oder deaktiviert die Sammlung von Ausführungsstatistiken auf Modulebene für nativ kompilierte T-SQL-Module in der aktuellen Datenbank. Der Standardwert ist OFF. Die Ausführungsstatistiken werden in [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) wiedergegeben.

Ausführungsstatistiken auf Modulebene für nativ kompilierte T-SQL-Module werden gesammelt, wenn diese Option auf „ON“ festgelegt ist, oder die Sammlung von Statistiken durch [sp_xtp_control_proc_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) aktiviert ist.

XTP_QUERY_EXECUTION_STATISTICS  **=** { ON | **OFF** }  

**Gilt für:** [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

Aktiviert oder deaktiviert die Sammlung von Ausführungsstatistiken auf Anweisungsebene für nativ kompilierte T-SQL-Module in der aktuellen Datenbank. Der Standardwert ist OFF. Die Ausführungsstatistik wird in [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) und im [Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) wiedergegeben.

Ausführungsstatistiken auf Anweisungsebene für nativ kompilierte T-SQL-Module werden gesammelt, wenn diese Option auf „ON“ festgelegt ist, oder die Sammlung von Statistiken durch [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) aktiviert ist.

Weitere Informationen über die Leistungsüberwachung von nativ kompilierten T-SQL-Modulen finden Sie unter [Überwachen der Leistung von systemintern kompilierten gespeicherten Prozeduren](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md).

##  <a name="Permissions"></a> Berechtigungen  
 Macht ALTER ANY DATABASE SCOPE CONFIGURATION   
für die Datenbank erforderlich. Diese Berechtigung kann von einem Benutzer mit CONTROL-Berechtigung für eine Datenbank erteilt werden.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Während Sie sekundäre Datenbanken so konfigurieren können, dass sie verschiedene bereichsbezogene Konfigurationseinstellungen von ihrer primären Datenbank aufweisen, wird für alle sekundären Datenbanken die gleiche Konfiguration verwendet. Für einzelne sekundäre Datenbanken können keine unterschiedlichen Einstellungen konfiguriert werden.  
  
 Durch die Ausführung dieser Anweisung wird der Prozedurcache in der aktuellen Datenbank geleert. Dies bedeutet, dass alle Abfragen erneut kompiliert werden müssen.  
  
 Bei Abfragen für dreiteilige Namen werden die Einstellungen für die aktuelle Datenbankverbindung berücksichtigt. Eine Ausnahme stellen SQL-Module dar (z.B. Prozeduren, Funktionen und Trigger), die im aktuellen Datenbankkontext kompiliert werden, weshalb die Optionen der Datenbank verwendet werden, in der sie sich befinden.  
  
 Das Ereignis ALTER_DATABASE_SCOPED_CONFIGURATION wird als DLL-Ereignis hinzugefügt, mit dem ein DLL-Trigger ausgelöst werden kann. Dieses Ereignis ist der Triggergruppe ALTER_DATABASE_EVENTS untergeordnet.  
 
 Die datenbankweit gültigen Konfigurationseinstellungen werden mit der Datenbank übertragen. Dies bedeutet, dass die vorhandenen Konfigurationseinstellungen bei der Wiederherstellung oder dem Anfügen einer bestimmten Datenbank erhalten bleiben.
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
**MAXDOP**  
  
 Die differenzierten Einstellungen können die globalen Einstellungen überschreiben. Zudem kann die Ressourcenkontrolle alle anderen MAXDOP-Einstellungen begrenzen.  Die Logik für die MAXDOP-Einstellung lautet wie folgt:  
  
-   Der Abfragehinweis überschreibt die Einstellung „sp_configure“ und die datenbankweit gültige Einstellung. Wenn die Ressourcengruppe MAXDOP für die Arbeitsauslastungsgruppe festgelegt ist:  
  
    -   Wenn der Abfragehinweis auf 0 festgelegt ist, wird er von der Einstellung der Ressourcenkontrolle überschrieben.  
  
    -   Wenn der Abfragehinweis nicht auf 0 festgelegt ist, wird er von der Einstellung der Ressourcenkontrolle begrenzt.  
  
-   Die datenbankweit gültige Einstellung überschreibt die Einstellung „sp_configure“ (wenn sie nicht auf 0 festgelegt ist), sofern kein Abfragehinweis vorhanden ist und sie nicht von der Einstellung der Ressourcenkontrolle begrenzt wird.  
  
-   Die Einstellung „sp_configure“ wird von der Einstellung der Ressourcenkontrolle überschrieben.  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 Wenn der Hinweis QUERYTRACEON zur Aktivierung des Legacy-Abfrageoptimierers oder der Hotfixes für den Abfrageoptimierer verwendet wird, bestünde zwischen dem Abfragehinweis und der datenbankweit gültigen Konfigurationseinstellung eine OR-Bedingung. Das heißt, wenn eines davon aktiviert ist, finden die Optionen Anwendung.  
  
**GeoDR**  
  
 Lesbare sekundäre Datenbanken, z.B. Always On-Verfügbarkeitsgruppen und GeoReplication, verwenden den sekundären Wert durch Überprüfung des Datenbankstatus. Obwohl es bei einer erneuten Kompilierung nicht zu einem Failover kommt und die neue primäre Datenbank eigentlich Abfragen aufweist, die Einstellungen für die sekundären Datenbanken verwenden, ist die Idee, dass die Einstellungen zwischen der primären und der sekundären Datenbank nur bei unterschiedlicher Arbeitsauslastung variieren. Daher verwenden die zwischengespeicherten Abfragen die optimalen Einstellungen, während neue Abfragen die neuen, für sie geeigneten Einstellungen auswählen.  
  
**DacFx**  
  
 Da ALTER DATABASE SCOPED CONFIGURATION in Azure SQL-Datenbank und SQL Server ab SQL Server 2016 ein neues Feature ist, das Auswirkungen auf das Datenbankschema hat, können Exporte des Schemas (mit oder ohne Daten) nicht in eine ältere Version von SQL Server wie z.B. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)] importiert werden. Ein Export in ein [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) oder ein [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) aus einer Datenbank von [!INCLUDE[ssSDS](../../includes/sssds-md.md)] oder [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], in der dieses neue Feature verwendet wird, könnte nicht in einen Server der Vorgängerversion importiert werden.  
  
## <a name="metadata"></a>Metadaten  

Die Systemansicht [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) enthält Informationen zu bereichsbezogenen Konfigurationen innerhalb einer Datenbank. Datenbankbezogene Konfigurationsoptionen werden nur in sys.database_scoped_configurations angezeigt, da sie serverweite Standardeinstellungen überschreiben. In der Systemansicht [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) werden nur serverweite Einstellungen angezeigt.  
  
## <a name="examples"></a>Beispiele  
Folgende Beispiele veranschaulichen die Verwendung von ALTER DATABASE SCOPED CONFIGURATION  
  
### <a name="a-grant-permission"></a>A. Erteilen einer Berechtigung  

In diesem Beispiel wird die Berechtigung erteilt, die zum Ausführen von ALTER DATABASE SCOPED CONFIGURATION für den Benutzer     
[Joe] erforderlich ist.  
  
```sql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>B. Festlegen von MAXDOP  

In diesem Beispiel wird in einem Georeplikationsszenario bei einer primären Datenbank MAXDOP = 1 und bei einer sekundären Datenbank MAXDOP = 4 festgelegt.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
In diesem Beispiel wird in einem Georeplikationsszenario der Wert für MAXDOP bei einer sekundären Datenbank auf den gleichen Wert wie für die zugehörige primäre Datenbank festgelegt.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. Festlegen von LEGACY_CARDINALITY_ESTIMATION  

In diesem Beispiel wird LEGACY_CARDINALITY_ESTIMATION in einem Georeplikationsszenario bei einer sekundären Datenbank auf ON festgelegt.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
In diesem Beispiel wird der Wert für LEGACY_CARDINALITY_ESTIMATION in einem Georeplikationsszenario bei einer sekundären Datenbank auf den gleichen Wert wie für die zugehörige primäre Datenbank festgelegt.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>D. Festlegen von PARAMETER_SNIFFING  

In diesem Beispiel wird PARAMETER_SNIFFING in einem Georeplikationsszenario bei einer primären Datenbank auf OFF festgelegt.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
In diesem Beispiel wird PARAMETER_SNIFFING in einem Georeplikationsszenario bei einer primären Datenbank auf OFF festgelegt.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
In diesem Beispiel wird der Wert für PARAMETER_SNIFFING in einem Georeplikationsszenario bei einer sekundären Datenbank auf den gleichen Wert festgelegt wie für die zugehörige primäre Datenbank.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. Festlegen von QUERY_OPTIMIZER_HOTFIXES  

Legt QUERY_OPTIMIZER_HOTFIXES in einem Georeplikationsszenario bei einer primären Datenbank auf ON fest.  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. Leeren des Prozedurcache  

In diesem Beispiel wird der Prozedurcache geleert (dies ist nur bei einer primären Datenbank möglich).  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. Festlegen von IDENTITY_CACHE

**Gilt für**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (das Feature befindet sich in der öffentlichen Vorschau) 

In diesem Beispiel wird der Identitätscache deaktiviert.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. Festlegen von OPTIMIZE_FOR_AD_HOC_WORKLOADS

**Gilt für:** [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

In diesem Beispiel wird ein Stub des kompilierten Plans aktiviert, der bei der erstmaligen Kompilierung eines Batches im Cache gespeichert werden soll.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen

### <a name="maxdop-resources"></a>Ressourcen von MAXDOP 
* [Grad der Parallelität](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [Recommendations and guidelines for the "max degree of parallelism" configuration option in SQL Server (Empfehlungen und Guidelines für die Konfigurationsoption „Max. Grad an Parallelität“ in SQL Server)](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>Ressourcen von LEGACY_CARDINALITY_ESTIMATION    
* [Kardinalitätsschätzung (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator (Optimieren Ihrer Abfragepläne mit der SQL Server 2014-Kardinalitätsschätzung)](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>Ressourcen von PARAMETER_SNIFFING    
* [Parameterermittlung](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* [„I smell a parameter!“](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/)

### <a name="queryoptimizerhotfixes-resources"></a>Ressourcen von QUERY_OPTIMIZER_HOTFIXES    
* [Ablaufverfolgungsflags](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server query optimizer hotfix trace flag 4199 servicing model](https://support.microsoft.com/en-us/kb/974006) (Wartungsmodell für SQL Server-Hotfix für Abfrageoptimierer – Ablaufverfolgungsflag 4199)

## <a name="more-information"></a>Weitere Informationen  
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [Datenbank- und Dateikatalogsichten](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Serverkonfigurationsoptionen](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
 
