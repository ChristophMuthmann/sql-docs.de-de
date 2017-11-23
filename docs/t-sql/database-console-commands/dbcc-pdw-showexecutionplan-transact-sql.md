---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
caps.latest.revision: "12"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1429ba18470b0881065bb0a851ff09faecd181c3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Zeigt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ausführungsplan für eine Abfrage ausgeführt wird, bei einer bestimmten [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Compute-Knoten oder Knoten "Zugriffssteuerung". Hiermit können Sie um Leistungsprobleme bei Abfragen zu beheben, während Abfragen auf den Serverknoten und den Knoten "Zugriffssteuerung" ausgeführt werden.
  
Sobald Sie Leistungsprobleme bei Abfragen für SMP verstanden werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abfragen, die auf den Serverknoten ausgeführt werden. Es gibt mehrere Möglichkeiten zum Verbessern der Leistung. Beispielsweise die Vorgehensweisen zum Verbessern der abfrageleistung auf den Serverknoten mit mehreren Spalte werden Statistiken erstellt, nicht gruppierte Indizes erstellen oder verwenden Abfragehinweise.
  
![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
Die Syntax für SQLServer:

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Syntax Azure Parallel Datawarehouse:
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *distribution_id*  
 Der Bezeichner für die Verteilung, die den Abfrageplan ausgeführt wird. Dies ist eine ganze Zahl und kann nicht NULL sein. Verwendet beim Abzielen auf [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 *pdw_node_id*  
 Der Bezeichner für den Knoten, der den Abfrageplan ausgeführt wird. Dies ist eine ganze Zahl und kann nicht NULL sein. Verwendet, wenn eine Anwendung abzielt.  
  
 *SPID*  
 Bezeichner für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sitzung, die den Abfrageplan ausgeführt wird. Dies ist eine ganze Zahl und kann nicht NULL sein.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
Erfordert die VIEW-SERVER-STATE-Berechtigung auf dem Gerät.
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>Beispiele:[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. DBCC PDW_SHOWEXECUTIONPLAN grundlegende Syntax  
 Bei der Ausführung unter einem [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Instanz ist, ändern Sie die obige Abfrage, um auch die Distribution_id auszuwählen.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
Dadurch wird die Spid für jedes aktiv ausgeführten Verteilung zurückgegeben. Wenn Sie wissen würden, welche Verteilung 1 in Sitzung 375 ausgeführt wurde, führen Sie den folgenden Befehl aus.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>B. DBCC PDW_SHOWEXECUTIONPLAN grundlegende Syntax  
 Die Abfrage, die zu lang ausgeführt wird ist entweder mit einem DMS Plan oder SQL-Abfrage-Plan-Operation abgefragt.  
  
Wenn die Abfrage eine DMS-Abfrageoperation Plan ausgeführt wird, können Sie die folgende Abfrage, zum Abrufen einer Liste der Knoten-IDs und Sitzungs-IDs für Schritte, die nicht abgeschlossen sind.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
Verwenden Sie auf Grundlage der Ergebnisse der vorherigen Abfrage Sql_spid und Pdw_node_id als Parameter für DBCC PDW_SHOWEXEUCTIONPLAN. Der folgende Befehl zeigt z. B. den Ausführungsplan für Pdw_node_id 201001 und Sql_spid 375.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>Siehe auch
[DBCC PDW_SHOWPARTITIONSTATS &#40; Transact-SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40; Transact-SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)
