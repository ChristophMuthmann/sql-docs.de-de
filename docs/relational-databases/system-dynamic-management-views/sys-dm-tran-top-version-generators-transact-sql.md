---
title: sys.dm_tran_top_version_generators (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_tran_top_version_generators
- sys.dm_tran_top_version_generators
- dm_tran_top_version_generators_TSQL
- sys.dm_tran_top_version_generators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_top_version_generators dynamic management view
ms.assetid: cec7809b-ba8a-4df9-b5bb-d4f651ff1a86
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f71613c0c7d65dc690724e2abffed529ab63e4b5
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmtrantopversiongenerators-transact-sql"></a>sys.dm_tran_top_version_generators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine virtuelle Tabelle für die Objekte zurück, die die meisten Versionen im Versionsspeicher erzeugen. **sys.dm_tran_top_version_generators** returns the top 256 aggregated record lengths that are grouped by the **database_id** and **rowset_id**. **sys.dm_tran_top_version_generators** retrieves data by querying the **dm_tran_version_store** virtual table. **sys.dm_tran_top_version_generators** is an inefficient view to run because this view queries the version store, and the version store can be very large. Die Verwendung dieser Funktion wird empfohlen, um die größten Consumer des Versionsspeichers zu suchen.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_tran_top_version_generators**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_tran_top_version_generators  
```  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Datenbank-ID|  
|**rowset_id**|**bigint**|Rowset-ID.|  
|**aggregated_record_length_in_bytes**|**int**|Summe der Datensatzlängen für jedes **Database_id** und **Rowset_id Pair** im Versionsspeicher.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein.  
  
## <a name="remarks"></a>Hinweise  
 Da **dm_tran_top_version_generators** möglicherweise viele Seiten lesen, da überprüft den gesamten Versionsspeicher ausgeführt **dm_tran_top_version_generators** können verhindern, dass System die Leistung.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Testszenario verwendet, in dem vier gleichzeitige Transaktionen, die jeweils durch eine Transaktionssequenznummer (XSN) identifiziert werden, in einer Datenbank ausgeführt werden, für die die Optionen ALLOW_SNAPSHOT_ISOLATION und READ_COMMITTED_SNAPSHOT auf ON festgelegt sind. Die folgenden Transaktionen werden ausgeführt:  
  
-   XSN-57 ist ein Updatevorgang auf der serialisierbaren Isolationsstufe.  
  
-   XSN-58 entspricht XSN-57.  
  
-   XSN-59 ist ein Select-Vorgang auf der Momentaufnahmeisolationsstufe.  
  
-   XSN-60 entspricht XSN-59.  
  
 Die folgende Abfrage wird ausgeführt.  
  
```  
SELECT  
    database_id,  
    rowset_id,  
    aggregated_record_length_in_bytes  
  FROM sys.dm_tran_top_version_generators;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
database_id rowset_id            aggregated_record_length_in_bytes  
----------- -------------------- ---------------------------------  
9           72057594038321152    87  
9           72057594038386688    33  
```  
  
 Die Ausgabe zeigt, dass alle Versionen erstellt werden, mit `database_id``9` und, die die Versionen aus zwei Tabellen zu generieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


