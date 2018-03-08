---
title: sys.dm_tran_current_transaction (Transact-SQL) | Microsoft Docs
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
- sys.dm_tran_current_transaction
- sys.dm_tran_current_transaction_TSQL
- dm_tran_current_transaction_TSQL
- dm_tran_current_transaction
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_current_transaction dynamic management view
ms.assetid: 75d5697d-b390-4963-99b8-fa0b4244a40c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 37deeb2752cc1e96c5c3ddc0719d2f71dce2283a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmtrancurrenttransaction-transact-sql"></a>sys.dm_tran_current_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine einzelne Zeile zurück, in der die Statusinformationen der Transaktion in der aktuellen Sitzung angezeigt werden.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_tran_current_transaction**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_tran_current_transaction  
```  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**transaction_id**|**bigint**|Transaktions-ID der aktuellen Momentaufnahme.|  
|**transaction_sequence_num**|**bigint**|Sequenznummer der Transaktion, die die Datensatzversion generiert.|  
|**transaction_is_snapshot**|**bit**|Der Momentaufnahmeisolationsstatus. Dieser Wert beträgt 1, wenn die Transaktion unter der Momentaufnahmeisolation gestartet wird. Anderenfalls ist der Wert 0.|  
|**first_snapshot_sequence_num**|**bigint**|Niedrigste Transaktionssequenznummer der Transaktionen, die beim Erstellen einer Momentaufnahme aktiviert waren. Bei der Ausführung einer Momentaufnahmetransaktion wird eine Momentaufnahme aller zu diesem Zeitpunkt aktiven Transaktionen erstellt. Für NonSnapshot-Transaktionen wird in dieser Spalte 0 angezeigt.|  
|**last_transaction_sequence_num**|**bigint**|Globale Sequenznummer. Dieser Wert stellt die letzte Transaktionssequenznummer dar, die vom System generiert wurde.|  
|**first_useful_sequence_num**|**bigint**|Globale Sequenznummer. Dieser Wert stellt die älteste Transaktionssequenznummer der Transaktion dar, die über Zeilenversionen verfügt, die im Versionsspeicher beibehalten werden müssen. Zeilenversionen, die von früheren Transaktionen erstellt wurden, können entfernt werden.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Testszenario verwendet, in dem vier gleichzeitige Transaktionen, die jeweils durch eine Transaktionssequenznummer (XSN) identifiziert werden, in einer Datenbank ausgeführt werden, für die die Optionen ALLOW_SNAPSHOT_ISOLATION und READ_COMMITTED_SNAPSHOT auf ON festgelegt sind. Die folgenden Transaktionen werden ausgeführt:  
  
-   XSN-57 ist ein Updatevorgang auf der serialisierbaren Isolationsstufe.  
  
-   XSN-58 entspricht XSN-57.  
  
-   XSN-59 ist ein Select-Vorgang auf der Momentaufnahmeisolationsstufe.  
  
-   XSN-60 entspricht XSN-59.  
  
 Die folgende Abfrage wird im Bereich jeder Transaktion ausgeführt.  
  
```  
SELECT   
    transaction_id  
   ,transaction_sequence_num  
   ,transaction_is_snapshot  
   ,first_snapshot_sequence_num  
   ,last_transaction_sequence_num  
   ,first_useful_sequence_num  
  FROM sys.dm_tran_current_transaction;  
```  
  
 Im Folgenden wird das Ergebnis für XSN-59 aufgeführt.  
  
```  
transaction_id       transaction_sequence_num transaction_is_snapshot  
-------------------- ------------------------ -----------------------  
9387                 59                       1                         
  
first_snapshot_sequence_num last_transaction_sequence_num  
--------------------------- -----------------------------  
57                               61                        
  
first_useful_sequence_num  
-------------------------  
57  
```  
  
 Die Ausgabe zeigt an, dass es sich bei XSN-59 um eine Momentaufnahmetransaktion handelt, die XSN-57 als die erste Transaktion verwendet, die beim Start von XSN-59 aktiviert war. Dies bedeutet, dass XSN-59 Daten liest, für die von Transaktionen, deren Transaktionssequenznummer niedriger ist als XSN-57, ein Commit ausgeführt wurde.  
  
 Im Folgenden wird das Ergebnis für XSN-57 aufgeführt.  
  
```  
transaction_id       transaction_sequence_num transaction_is_snapshot  
-------------------- ------------------------ -----------------------  
9295                 57                       0  
  
first_snapshot_sequence_num last_transaction_sequence_num  
--------------------------- -----------------------------  
NULL                        61  
  
first_useful_sequence_num  
-------------------------  
57  
```  
  
 Da XSN-57 keine Momentaufnahmetransaktion ist, weist `first_snapshot_sequence_num` den Wert `NULL` auf.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


