---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9d1a4659deeab00589a09e66d885d7f7005f7a43
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Zeigt die Größe und Anzahl der Zeilen für jede Partition einer Tabelle in eine [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Datenbank.
  
![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ *Database_name* . [ *Schema_name* ]. | *Schema_name* . ] *Table_name*  
 Der ein-, zwei- oder dreiteiligen Name der Tabelle angezeigt werden.  Für zwei oder dreiteiligen Tabellennamen, Spaltennamen, der Name müssen in doppelte Anführungszeichen eingeschlossen werden (""). Verwenden Anführungszeichen ein einteiliger Tabellenname ist optional.  
  
## <a name="permissions"></a>Berechtigungen
Erfordert **VIEW SERVER STATE** Berechtigung.
  
## <a name="result-sets"></a>Resultsets  
Dies ist die Ergebnisse des Befehls DBCC PDW_SHOWPARTITIONSTATS.
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|partition_number|int|Partitionsnummer.|  
|used_page_count|bigint|Anzahl der Seiten, die für die Daten verwendet.|  
|reserved_page_count|bigint|Anzahl der Seiten, die die Partition zugeordnet.|  
|row_count|bigint|Anzahl der Zeilen in der Partition.|  
|pdw_node_id|int|Knoten für die Daten zu berechnen.|  
|distribution_id|int|Verteilungs-Id für die Daten.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>A. Beispiele für DBCC PDW_SHOWPARTITIONSTATS die grundlegende Syntax  
Die folgenden Beispiele zeigen die verwendeter Speicherplatz und die Anzahl der Zeilen von Partition für die FactInternetSales-Tabelle in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] Datenbank.
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>Siehe auch
[DBCC PDW_SHOWEXECUTIONPLAN &#40; Transact-SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40; Transact-SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)  
  

