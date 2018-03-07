---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c564a6debb9c110cb41f8fc90a7cc1c0c5a01f7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Zeigt die Anzahl der Zeilen, reservierte Speicherplatz und Speicherplatz für eine bestimmte Tabelle oder für alle Tabellen in einem [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Datenbank.
  
![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ *database_name* . [ *schema_name* ] . | *schema_name* . ] *table_name*  
 Der ein-, zwei- oder dreiteiligen Name der Tabelle angezeigt werden. Für zwei oder dreiteiligen Tabellennamen, Spaltennamen, der Name müssen in doppelte Anführungszeichen eingeschlossen werden (""). Verwenden Anführungszeichen ein einteiliger Tabellenname ist optional. Wenn kein Tabellenname angegeben wird, werden die Informationen für die aktuelle Datenbank angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die VIEW SERVER STATE-Berechtigung.
  
## <a name="result-sets"></a>Resultsets  
Dies ist das Resultset für alle Tabellen.
  
|Column|Datentyp|Description|  
|------------|---------------|-----------------|  
|reserved_space|bigint|Für die Datenbank, in KB belegter Gesamtspeicherplatz.|  
|data_space|bigint|Speicherplatz für Daten in KB verwendet wird.|  
|index_space|bigint|Speicherplatz für Indizes in KB verwendet wird.|  
|unused_space|bigint|Speicherplatz, der den reservierten Speicherplatz Teil und wird nicht verwendet, in KB ist.|  
|pdw_node_id|int|Computeknoten, der für die Daten verwendet wird.|  
  
Dies ist das Resultset für eine Tabelle.
  
|Column|Datentyp|Description|Bereich|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|Anzahl der Zeilen.||  
|reserved_space|bigint|Gesamtspeicherplatz, der für das Objekt, in KB reserviert ist.||  
|data_space|bigint|Speicherplatz verwendet wird, für die Daten in KB.||  
|index_space|bigint|Speicherplatz für Indizes in KB verwendet wird.||  
|unused_space|bigint|Speicherplatz, der den reservierten Speicherplatz Teil und wird nicht verwendet, in KB ist.||  
|pdw_node_id|int|Computeknoten, die für die Speicherplatzverwendung reporting verwendet wird.||  
|distribution_id|int|Verteilung, die für die Speicherplatzverwendung reporting verwendet wird.|Wert ist 1 für replizierte Tabellen.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. DBCC PDW_SHOWSPACEUSED grundlegende Syntax  
In den folgenden Beispielen zeigen die Anzahl der Zeilen, die reserviert Speicherplatz auf Datenträger auf verschiedene Weisen anzuzeigen und Speicherplatz verwendet wird, indem Sie die FactInternetSales-Tabelle in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] Datenbank.
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. Anzeigen des von allen Tabellen in der aktuellen Datenbank verwendeten Speicherplatzes  
 Das folgende Beispiel zeigt den Speicherplatz reserviert und verwendet, die von allen Benutzertabellen und Systemtabellen in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] Datenbank.  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>Siehe auch
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
