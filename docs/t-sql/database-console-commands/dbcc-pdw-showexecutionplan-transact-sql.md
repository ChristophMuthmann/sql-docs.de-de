---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/16/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 384177035c1b80127ca3d33967e2fc12b6878157
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Zeigt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ausführungsplan für eine Abfrage an, die auf einem bestimmten [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]- oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Computeknoten oder -Steuerknoten ausgeführt wird. Verwenden Sie diese Funktion zum Behandeln von Problemen mit der Abfrageleistung, während Abfragen auf Compute- oder Steuerknoten ausgeführt werden.
  
Sobald Sie verstanden haben, wodurch Leistungsprobleme bei Abfragen für SMP-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfragen auf den Computeknoten entstehen, können Sie diese Probleme auf verschiedene Weisen verbessern. Beispielsweise können Sie die Abfrageleistung auf Computeknoten verbessern, indem Sie Statistiken mit mehreren Spalten oder nicht gruppierte Indizes erstellen bzw. Abfragehinweise verwenden.
  
![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
Syntax für SQL Server:

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Syntax für Azure Parallel Data Warehouse:
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *distribution_id*  
 Bezeichner für die Verteilung, die den Abfrageplan ausführt. Dabei handelt es sich um einen Integer, der nicht NULL sein kann. Dieser Bezeichner wird verwendet, wenn für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] entwickelt wird.  
  
 *pdw_node_id*  
 Bezeichner für den Knoten, der den Abfrageplan ausführt. Dabei handelt es sich um einen Integer, der nicht NULL sein kann. Wird verwendet, wenn eine Anwendung entwickelt wird.  
  
 *spid*  
 Bezeichner für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sitzung, die den Abfrageplan ausführt. Dabei handelt es sich um einen Integer, der nicht NULL sein kann.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung auf [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
Erfordert die VIEW-SERVER-STATE-Berechtigung auf die Anwendung.
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. Grundlegende DBCC-PDW_SHOWEXECUTIONPLAN-Syntax  
 Wenn Sie die obenstehende Abfrage auf einer [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]-Instanz ausführen, müssen Sie diese verändern, um auch distribution_id auszuwählen.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
Dadurch wird für jede aktiv ausgeführte Verteilung eine SPID zurückgegeben. Wenn Sie gerne wissen möchten, was Verteilung 1 in Sitzung 375 ausgeführt hat, können Sie den folgenden Befehl ausführen.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>B. Grundlegende DBCC-PDW_SHOWEXECUTIONPLAN-Syntax  
 Die Abfrage, die zu lange ausgeführt wird, führt entweder einen Vorgang für einen DMS-Abfrageplan oder für einen SQL-Abfrageplan aus.  
  
Wenn die Abfrage einen Vorgang für einen DMS-Abfrageplan ausführt. können Sie die folgende Abfrage verwenden, um eine Liste der Knoten- und Sitzungs-IDs für noch nicht abgeschlossene Schritte abzufragen.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
Verwenden Sie anhand des Ergebnisses der vorherigen Abfrage sql_spid und pdw_node_id als Parameter für DBCC PDW_SHOWEXEUCTIONPLAN. Beispielsweise zeigt das folgende Beispiel den Ausführungsplan für pdw_node_id 201001 und sql_spid 375.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>Siehe auch
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)
