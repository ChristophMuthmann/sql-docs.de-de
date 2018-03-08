---
title: Sp_tables (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_tables
- sp_tables_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_tables
ms.assetid: 787a2fa5-87a1-49bd-938b-6043c245f46b
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 95a0bae2722c519cea3e1dac14c633fe582ed5a8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sptables-transact-sql"></a>sp_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Liste von Objekten zurück, die in der aktuellen Umgebung abgefragt werden können. Dies bedeutet jede Tabelle oder Sicht, mit Ausnahme von Synonymobjekten.  
  
> [!NOTE]  
>  Um den Namen des Basisobjekts eines Synonyms zu bestimmen, Fragen den [sys.synonyms](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md) -Katalogsicht angezeigt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_tables [ [ @table_name = ] 'name' ]   
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @table_type = ] "type" ]   
     [ , [@fUsePattern = ] 'fUsePattern'];  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@table_name=** ] **"***Namen***"**  
 Die Tabelle zum Zurückgeben von Kataloginformationen. *Namen* ist **nvarchar(384)**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden unterstützt.  
  
 [  **@table_owner=** ] **"***Besitzer***"**  
 Der Tabellenbesitzer für die Tabelle zum Zurückgeben von Kataloginformationen. *Besitzer* ist **nvarchar(384)**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden unterstützt. Wenn der Besitzer nicht angegeben ist, werden die Standardregeln für die Sichtbarkeit von Tabellen des zugrunde liegenden DBMS angewendet.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die Spalten einer Tabelle zurückgegeben, wenn der aktuelle Benutzer diese Tabelle mit dem angegebenen Namen besitzt. Falls der Besitzer nicht angegeben ist und der aktuelle Benutzer keine Tabelle mit dem angegebenen Namen besitzt, wird nach einer Tabelle mit dem angegebenen Namen gesucht, deren Besitzer der Datenbankbesitzer ist. Falls vorhanden, werden die Spalten dieser Tabelle zurückgegeben.  
  
 [  **@table_qualifier=** ] **"***Qualifizierer***"**  
 Der Name des Tabellenqualifizierers. *qualifier* ist vom Datentyp **sysname**und hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*Qualifizierer***.** *Besitzer***.** *Namen*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
 [ **,** [  **@table_type=** ] **""***Typ***"**, **"**Typ **'"** ]  
 Eine Liste mit Werten, getrennt durch Kommas, zum Abrufen von Informationen zu allen Tabellen des angegebenen Tabellentyps. Dazu gehören **Tabelle**, **SYSTEMTABLE**, und **Ansicht**. *Typ* ist **varchar(100)**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Jeder Tabellentyp muss in einfache Anführungszeichen und der gesamte Parameter in doppelte Anführungszeichen eingeschlossen werden. Für Tabellentypen müssen Großbuchstaben verwendet werden. Wenn SET QUOTED_IDENTIFIER auf ON festgelegt ist, müssen alle einfachen Anführungszeichen in doppelte Anführungszeichen geändert werden, und der gesamte Parameter muss in einfache Anführungszeichen eingeschlossen werden.  
  
 [  **@fUsePattern =** ] **"***fUsePattern***"**  
 Bestimmt, ob der Unterstrich (_), das Prozentzeichen (%) und eckige Klammern ([ oder ]) als Platzhalterzeichen interpretiert werden. Gültige Werte sind 0 (Mustervergleich ist deaktiviert) und 1 (Mustervergleich ist aktiviert). *fUsePattern* ist vom Datentyp **bit**. Der Standardwert ist 1.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Tabelle der Name des Prozedurqualifizierers. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Dieses Feld kann den Wert NULL annehmen.|  
|**TABLE_OWNER**|**sysname**|Name des Tabellenbesitzers. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], diese Spalte dar, der Name des Datenbankbenutzers, der die Tabelle erstellt. Dieses Feld gibt immer einen Wert zurück.|  
|**TABELLENNAME**|**sysname**|Tabellenname. Dieses Feld gibt immer einen Wert zurück.|  
|**TABLE_TYPE**|**varchar(32)**|Tabelle, Systemtabelle oder Sicht.|  
|**"HINWEISE"**|**varchar(254)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt für diese Spalte keinen Wert zurück.|  
  
## <a name="remarks"></a>Hinweise  
 Für maximale Interoperabilität sollte der Gatewayclient nur den SQL-92-Standard zum SQL-Mustervergleich (die Platzhalterzeichen % und _) voraussetzen.  
  
 Die Privileginformationen zum Lese- und Schreibzugriff des aktuellen Benutzers für eine bestimmte Tabelle werden nicht immer geprüft. Deshalb ist der Zugriff nicht sichergestellt. Dieses Resultset enthält nicht nur Tabellen und Sichten, sondern auch Synonyme und Aliasnamen für Gateways zu DBMS-Produkten, die diese Typen unterstützen. Wenn das Serverattribut **ACCESSIBLE_TABLES** ist Y in das Resultset für **Sp_server_info**, nur die Tabellen, die vom aktuellen Benutzer zugegriffen werden können, werden zurückgegeben.  
  
 **Sp_tables** entspricht **SQLTables** in ODBC. Die zurückgegebenen Ergebnisse sind sortiert, indem **TABLE_TYPE**, **TABLE_QUALIFIER**, **TABLE_OWNER**, und **TABLE_NAME**.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>A. Zurückgeben einer Liste von Objekten, die in der aktuellen Umgebung abgefragt werden können  
 Das folgende Beispiel gibt eine Liste von Objekten, die Abfragen in der aktuellen Umgebung werden können.  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="b-returning-information-about-the-tables-in-a-specified-schema"></a>B. Zurückgeben von Informationen zu den Tabellen in einem angegebenen Schema  
 Im folgenden Beispiel werden Informationen zu den Tabellen zurückgegeben, die zum `Person`-Schema in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank gehören.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_tables   
   @table_name = '%',  
   @table_owner = 'Person',  
   @table_qualifier = 'AdventureWorks2012';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>C. Zurückgeben einer Liste von Objekten, die in der aktuellen Umgebung abgefragt werden können  
 Das folgende Beispiel gibt eine Liste von Objekten, die Abfragen in der aktuellen Umgebung werden können.  
  
```  
EXEC sp_tables ;  
```  
  
### <a name="d-returning-information-about-the-tables-in-a-specified-schema"></a>D. Zurückgeben von Informationen zu den Tabellen in einem angegebenen Schema  
 Das folgende Beispiel gibt Informationen zu den Dimensionstabellen in der `AdventureWorksPDW201` Datenbank.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_tables   
   @table_name = 'Dim%',  
   @table_owner = 'dbo',  
   @table_qualifier = 'AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys.Synonyms &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

