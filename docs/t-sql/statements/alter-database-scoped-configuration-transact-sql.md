---
title: ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: "32"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9638d94c2bd6f461650b15f96c7a75c95eaeb861
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Diese Anweisung ermöglicht es, mehrere Konfigurationseinstellungen der Datenbank an die **einzelne Datenbank** Ebene. Diese Anweisung steht in [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Diese Einstellungen sind:  
  
- Löschen des Prozedurcaches.  
- Legen Sie den MAXDOP-Parameter auf einen beliebigen Wert (1,2,...), für die primäre Datenbank basierend auf was am besten für diese bestimmte Datenbank, und legen Sie einen anderen Wert (z. B. 0) für alle verwendeten sekundären Datenbanken (z. B. für Berichtsabfragen).  
- Festlegen des Kardinalitätsschätzungsmodells für den Abfrageoptimierer unabhängig von der Datenbank auf den Kompatibilitätsgrad.  
- Aktivieren oder Deaktivieren der Parameterermittlung auf Datenbankebene.
- Aktivieren oder Deaktivieren der Abfrageoptimierungs-Hotfixes auf Datenbankebene.
- Aktivieren oder Deaktivieren der Identitäts-Cache auf Datenbankebene.
- Aktivieren Sie oder deaktivieren Sie einen Stub des kompilierten Plans im Cache gespeichert werden, wenn ein Batch zum ersten Mal kompiliert wird.    
  
 ![Symbol "Verknüpfung"](../../database-engine/configure-windows/media/topic-link.gif "Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
}  
```  
  
## <a name="arguments"></a>Argumente  
 
FÜR SEKUNDÄRE OBJEKTE  
 
Gibt die Einstellungen für die sekundären Datenbanken (alle sekundäre Datenbanken müssen die identische Werte haben).  
  
MAXDOP  **=**  {\<Wert > | PRIMÄRE}  
**\<value>**  
  
Gibt die Standard-MAXDOP festlegen, die für Anweisungen verwendet werden soll. 0 ist der Standardwert und gibt an, dass die Serverkonfiguration stattdessen verwendet werden soll. Der MAXDOP im Datenbankbereich überschreibt (es sei denn, es auf 0 festgelegt ist) die **Max. Grad an Parallelität** auf Serverebene von Sp_configure festgelegt. Abfragehinweise können weiterhin die Datenbank überschreiben MAXDOP begrenzt, um bestimmte Abfragen optimieren, die andere Einstellung benötigen. All diese Einstellungen werden durch die MAXDOP, legen Sie für die Arbeitsauslastungsgruppe begrenzt.   

Mithilfe der Option Max. Grad an Parallelität kann die Anzahl der Prozessoren beschränkt werden, die bei der Ausführung paralleler Pläne verwendet werden. SQL Server betrachtet die Ausführung paralleler Pläne für Abfragen, Data Definition Language (DDL) Indexvorgänge, parallele Einfügevorgänge, onlineausführung von alter Spalten-, parallele statistikdatensammlung und statische und keysetgesteuerte cursorauffüllung.
 
Um diese Option auf Instanzebene festzulegen, finden Sie unter [Konfigurieren der max Degree of Parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). 

> [!TIP] 
> Fügen Sie hierzu auf der abfragenebene der **MAXDOP** [-Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md).  
  
PRIMARY  
  
Kann nur festgelegt werden, für die protokollsicherungskopien verfügbar, während die Datenbank in der primären Datenbank und gibt an, dass die Konfiguration der einen Satz für die primäre sein wird. Wenn die Konfiguration für die primäre geändert wird, den Wert auf den sekundären Replikaten zu ändern, wird entsprechend ohne die Notwendigkeit zum Festlegen von der sekundären Replikaten Wert explizit. **PRIMÄRE** ist die Standardeinstellung für den sekundären Replikaten.  
  
LEGACY_CARDINALITY_ESTIMATION  **=**  {ON | **OFF** | PRIMÄRE}  

Können Sie das Query Optimizer kardinalitätsschätzungsmodell auf die SQL Server 2012 und früheren Version unabhängig vom Kompatibilitätsgrad der Datenbank festgelegt. Die Standardeinstellung ist **OFF**, welche legt das kardinalitätsschätzungsmodell für Abfrage Abfrageoptimierer auf den Kompatibilitätsgrad der Datenbank basierend. Wenn dieser **ON** entspricht der Aktivierung von [Ablaufverfolgungsflag 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

> [!TIP] 
> Fügen Sie hierzu auf der abfragenebene der **"QueryTraceOn"** [-Abfragehinweis](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 können hierfür auf Abfrageebene, Hinzufügen der **verwenden Hinweis** [-Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) anstatt mithilfe des Ablaufverfolgungsflags. 
  
PRIMARY  
  
Dieser Wert ist nur gültig für sekundäre Replikate, während die Datenbank in der primären Datenbank und gibt an, dass der Wert für die primäre Abfrageoptimierer Modell Einstellung für die kardinalitätsschätzung für alle sekundären Datenbanken wird. Wenn die Konfiguration auf dem primären Replikat für das kardinalitätsschätzungsmodell für Abfrage Abfrageoptimierer ändert, wird der Wert auf den sekundären Replikaten entsprechend geändert. **PRIMÄRE** ist die Standardeinstellung für den sekundären Replikaten.  
  
PARAMETER_SNIFFING  **=**  { **ON** | DEAKTIVIEREN | PRIMÄRE}  

Aktiviert oder deaktiviert die [parameterermittlung](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing). Der Standardwert ist ON. Dies entspricht dem [Ablaufverfolgungsflag 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Zu diesem Zweck auf Abfrageebene finden Sie unter der **OPTIMIZE FOR UNKNOWN** [-Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md). Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 dafür auf Abfrageebene, zu der **verwenden Hinweis** [-Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) ist auch verfügbar. 
  
PRIMARY  
  
Dieser Wert ist nur gültig für sekundäre Replikate, während die Datenbank in der primären Datenbank und gibt an, dass der Wert für diese Einstellung auf alle sekundären Datenbanken für den primären festgelegte Wert. Wenn die Konfiguration auf dem primären Replikat für die Verwendung von [parameterermittlung](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing) ändert, der Wert auf den sekundären Replikaten ändert sich entsprechend ohne die Notwendigkeit zum Festlegen der sekundären Replikate Wert explizit. Dies ist die Standardeinstellung für den sekundären Replikaten.  
  
QUERY_OPTIMIZER_HOTFIXES  **=**  {ON | **OFF** | PRIMÄRE}  

Aktiviert oder deaktiviert Hotfixes für die abfrageoptimierung unabhängig vom Kompatibilitätsgrad der Datenbank. Die Standardeinstellung ist **OFF**, die deaktiviert zurückgreifen abfrageoptimierungs-Hotfixes, die freigegeben wurden, nachdem die höchste verfügbare Kompatibilitätsgrad für eine bestimmte Version eingeführt wurde (Post-RTM). Wenn dieser **ON** entspricht der Aktivierung von [Ablaufverfolgungsflag 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).   

> [!TIP] 
> Fügen Sie hierzu auf der abfragenebene der **"QueryTraceOn"** [-Abfragehinweis](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 können hierfür auf Abfrageebene, Hinzufügen der verwenden Hinweis [-Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) anstatt mithilfe des Ablaufverfolgungsflags.  
  
PRIMARY  
  
Dieser Wert ist nur gültig für sekundäre Replikate, während die Datenbank in der primären Datenbank und gibt an, dass der Wert für diese Einstellung auf alle sekundären Datenbanken für den primären festgelegte Wert ist. Wenn die Konfiguration für die primäre geändert wird, den Wert auf den sekundären Replikaten geändert Wert entsprechend ohne die Notwendigkeit zum Festlegen der sekundären Datenbanken explizit. Dies ist die Standardeinstellung für den sekundären Replikaten.  
  
LÖSCHEN PROCEDURE_CACHE  

Löscht den Prozedurcache (Plan) für die Datenbank an. Dies kann sowohl auf dem primären und den sekundären Replikaten ausgeführt werden.  

IDENTITY_CACHE  **=**  { **ON** | {OFF}  

**Gilt für**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] und[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Aktiviert oder deaktiviert die Identitäts-Cache auf Datenbankebene. Die Standardeinstellung ist **ON**. Zwischenspeichern von Identität dient zum Verbessern der Leistung von INSERT auf Tabellen mit Identitätsspalten. Deaktivieren Sie die IDENTITY_CACHE-Option, um Lücken in den Werten einer Identitätsspalte in Fällen, in dem der Server wird unerwartet neu gestartet oder ein Failover zu einem sekundären Server, zu vermeiden. Diese Option ist vergleichbar mit der vorhandenen [Trace-Flag 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), außer dass es auf Datenbankebene, statt nur auf Serverebene festgelegt werden kann.   

> [!NOTE] 
> Diese Option kann nur für den primären festgelegt werden. Weitere Informationen finden Sie unter [Identitätsspalten](create-table-transact-sql-identity-property.md).  

OPTIMIZE_FOR_AD_HOC_WORKLOADS  **=**  {ON | **OFF** }  

**Gilt für:** [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

Aktiviert oder deaktiviert einen Stub des kompilierten Plans im Cache gespeichert werden, wenn ein Batch zum ersten Mal kompiliert wird. Der Standardwert ist OFF. Sobald die datenbankweite Konfiguration für eine Datenbank, die ein Stub des kompilierten Plans OPTIMIZE_FOR_AD_HOC_WORKLOADS aktiviert ist, die in der Cache bei einem Batch gespeichert werden, wird zum ersten Mal kompiliert. Plan-Stubs müssen einen weniger Speicher beansprucht im Vergleich zu der Größe des vollständigen kompilierten Plans.  Wenn ein Batch kompiliert oder erneut ausgeführt wird, werden Stub des kompilierten Plans entfernt und durch einen vollständigen kompilierten Plan ersetzt.

##  <a name="Permissions"></a> Berechtigungen  
 Erfordert ALTER alle Datenbank-BEREICHSKONFIGURATION   
in der Datenbank. Diese Berechtigung kann von einem Benutzer mit CONTROL-Berechtigung für eine Datenbank erteilt werden.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Sie können konfigurieren, dass sekundäre Datenbanken, um verschiedene Bereichsbezogene Konfigurationseinstellungen von ihren primären aufweisen, verwenden alle sekundäre Datenbanken die gleiche Konfiguration. Andere Einstellungen können nicht für einzelne sekundäre Replikate konfiguriert werden.  
  
 Diese Anweisung ausführen, löscht der Prozedurcache in der aktuellen Datenbank, das bedeutet, dass alle Abfragen neu kompiliert.  
  
 Für Namensabfragen mit 3 Teilen die Einstellungen für die aktuelle datenbankverbindung für die Abfrage wird berücksichtigt, außer für SQL-Module (z. B. Prozeduren, Funktionen und Trigger), die im aktuellen Datenbankkontext kompiliert werden, und verwendet daher die Optionen von der Datenbank, in denen sie sich befinden.  
  
 Das Ereignis ALTER_DATABASE_SCOPED_CONFIGURATION wird als ein DDL-Ereignis hinzugefügt, die zum Auslösen eines DDL-Triggers verwendet werden kann. Dies ist ein untergeordnetes Element der Gruppe "ALTER_DATABASE_EVENTS Trigger".  
 
 Datenbankweit gültige Konfiguration wie die Einstellungen mit der Datenbank übernommen. Dies bedeutet, dass bei eine bestimmte Datenbank wiederhergestellt oder angefügt wird, die vorhandenen Konfigurationseinstellungen bleiben.
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
**MAXDOP**  
  
 Die präzisen Einstellungen können die globale Konfigurationen überschreiben und diese Ressourcenkontrolle kann cap MAXDOP-Einstellungen.  Die Logik für die MAXDOP-Einstellung lautet wie folgt:  
  
-   Abfragehinweis überschreibt Sp_configure und die Datenbank als Bereich festlegen. Wenn die Ressourcengruppe MAXDOP für die Arbeitsauslastungsgruppe festgelegt ist:  
  
    -   Wenn Sie der Abfragehinweis auf 0 festgelegt ist, wird sie durch die Ressourcenkontrolle festlegen überschrieben.  
  
    -   Wenn Sie der Abfragehinweis nicht 0 ist, ist wird durch die Ressourcenkontrolle festlegen Obergrenze.  
  
-   Die DB Bereich festlegen (es sei denn, es 0 ist) überschreibt die Sp_configure-Einstellung aus, es sei denn, es ein Abfragehinweis wird und Obergrenze ist, durch die Ressourcenkontrolle festlegen.  
  
-   Die Sp_configure-Einstellung wird von der Einstellung der Ressourcenkontrolle überschrieben.  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 Wenn "QueryTraceOn" Hinweis verwendet wird, um die ältere Abfrageoptimierer oder Hotfixes für Abfrageoptimierer zu aktivieren, wäre es eine OR-Bedingung zwischen den Abfragehinweis und die datenbankweite Konfiguration festlegen, d. h., wenn entweder aktiviert ist, gelten die Optionen.  
  
**GeoDR**  
  
 Lesbare sekundäre Datenbanken, z. B. AlwaysOn-Verfügbarkeitsgruppen und GeoReplication, verwenden Sie den sekundären Wert durch Überprüfen des Zustands der Datenbank. Obwohl Recompile findet kein Failover statt und technisch das neue primäre hat Abfragen, die die Einstellungen für die sekundären verwenden, ist die Vorstellung, dass die Einstellung zwischen primären und sekundären nur unterschiedlich sein, wenn die arbeitsauslastung besteht aus verschiedenen und daher die zwischengespeicherte Abfragen verwenden die optimalen Einstellungen an, während Sie neue Abfragen die neuen Einstellungen auswählen, die für sie geeignet sind.  
  
**DacFx**  
  
 Da ALTER_DATABASE SCOPED ist CONFIGURATION ein neues Feature in Azure SQL-Datenbank und SQL Server ab SQL Server 2016, wirkt sich auf das Datenbankschema Exporte des Schemas (mit oder ohne Daten) werden möglicherweise nicht in einer älteren Version von SQL Server importiert werden z. B. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]. Z. B. ein Export in eine [DACPAC-Datei](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) oder ein [bacpac-Datei](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) aus einer [!INCLUDE[ssSDS](../../includes/sssds-md.md)] oder [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] dieser neuen Funktion verwendeten wären nicht in der Lage, in einen Server der Vorgängerversion importiert werden sollen.  
  
## <a name="metadata"></a>Metadaten  

Die [Sys. database_scoped_configurations &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) Systemsicht enthält Informationen zu diesen Bereich Konfigurationen innerhalb einer Datenbank. Datenbankbezogene Konfigurationsoptionen erscheinen nur in Sys. database_scoped_configurations, überschreibungen, um serverweite Standardeinstellungen sind. Die [sys.configurations &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) Systemsicht zeigt nur die serverweite Einstellungen.  
  
## <a name="examples"></a>Beispiele  
Diese Beispiele veranschaulichen die Verwendung von ALTER DATABASE SCOPED CONFIGURATION  
  
### <a name="a-grant-permission"></a>A. GRANT-Berechtigung  

In diesem Beispiel wird die Berechtigung zum Ausführen von ALTER DATABASE SCOPED CONFIGURATION     
Benutzer [Joe].  
  
```sql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>B. Festlegen von MAXDOP  

In diesem Beispiel wird MAXDOP = 1 für eine primäre Datenbank und die MAXDOP = 4 für eine sekundäre Datenbank in einem Szenario für die geografische Replikation.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
In diesem Beispiel wird MAXDOP für eine sekundäre Datenbank identisch sein, da es für die primäre Datenbank in einem Szenario für die geografische Replikation festgelegt ist.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. Legen Sie die LEGACY_CARDINALITY_ESTIMATION  

In diesem Beispiel legt LEGACY_CARDINALITY_ESTIMATION auf ON fest, für eine sekundäre Datenbank in einem Szenario für die geografische Replikation.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
In diesem Beispiel wird für eine sekundäre Datenbank LEGACY_CARDINALITY_ESTIMATION, wie es für die primäre Datenbank in einem Szenario für die geografische Replikation ist.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>D. PARAMETER_SNIFFING festlegen  

In diesem Beispiel werden PARAMETER_SNIFFING für eine primäre Datenbank in einem Szenario für die geografische Replikation auf OFF festgelegt.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
In diesem Beispiel werden PARAMETER_SNIFFING für eine primäre Datenbank in einem Szenario für die geografische Replikation auf OFF festgelegt.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
In diesem Beispiel wird PARAMETER_SNIFFING für die sekundäre Datenbank an, wie es auf der primären Datenbank in einem Szenario für die geografische Replikation ist.  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. QUERY_OPTIMIZER_HOTFIXES festlegen  

QUERY_OPTIMIZER_HOTFIXES auf ON festgelegt, für eine primäre Datenbank in einem Szenario für die geografische Replikation.  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. Löschen des Prozedurcaches  

Dieses Beispiel löscht den Prozedurcache (nur für eine primäre Datenbank möglich).  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. IDENTITY_CACHE festlegen

**Gilt für**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (Feature steht in der öffentlichen Vorschau) 

In diesem Beispiel wird der Identitäts-Cache deaktiviert.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. OPTIMIZE_FOR_AD_HOC_WORKLOADS festlegen

**Gilt für:** [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

In diesem Beispiel ermöglicht einen Stub des kompilierten Plans im Cache gespeichert werden, wenn ein Batch zum ersten Mal kompiliert wird.

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen

### <a name="maxdop-resources"></a>MAXDOP-Ressourcen 
* [Grad der Parallelität](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [Empfehlungen und Richtlinien für die Konfigurationsoption "Max. Grad an Parallelität" in SQL Server](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>LEGACY_CARDINALITY_ESTIMATION-Ressourcen    
* [Kardinalitätsschätzung (SQLServer)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator (Optimieren Ihrer Abfragepläne mit der SQL Server 2014-Kardinalitätsschätzung)](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>PARAMETER_SNIFFING Ressourcen    
* [Parameterermittlung](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* ["Ich Geruchs Parameter!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/)

### <a name="queryoptimizerhotfixes-resources"></a>QUERY_OPTIMIZER_HOTFIXES Ressourcen    
* [Ablaufverfolgungsflags](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server Query Optimizer Hotfix Trace Flag 4199 Wartungsmodell](https://support.microsoft.com/en-us/kb/974006)

## <a name="more-information"></a>Weitere Informationen  
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [Datenbanken und Dateikatalogsichten](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Serverkonfigurationsoptionen für den](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
 
