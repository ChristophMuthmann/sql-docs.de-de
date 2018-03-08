---
title: Transaktionen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Transactions
- Transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactions [SQL Server]
- transactions [SQL Server], about transactions
- UOW [SQL Server]
- unit of work [SQL Server]
ms.assetid: 1485c375-921a-42af-a871-bb333cc08d3e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 360d2d4d88280a011687dfb3845f1de86513bdc8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="transactions-transact-sql"></a>Transaktionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Eine Transaktion ist eine einzelne Arbeitseinheit. Ist eine Transaktion erfolgreich, wird für alle Datenänderungen, die während der Transaktion vorgenommen wurden, ein Commit ausgeführt, und sie werden dauerhaft in der Datenbank gespeichert. Treten während einer Transaktion Fehler auf, die den Abbruch oder ein Rollback der Transaktion erfordern, werden alle Datenänderungen rückgängig gemacht.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in den folgenden Transaktionsmodi arbeitet:  
  
 Autocommit-Transaktionen  
 Jede einzelne Anweisung ist eine Transaktion.  
  
 Explizite Transaktionen  
 Jede Transaktion wird explizit mit der BEGIN TRANSACTION-Anweisung gestartet und explizit mit einer COMMIT- oder ROLLBACK-Anweisung beendet.  
  
 Implizite Transaktionen  
 Eine neue Transaktion wird implizit gestartet, sobald die vorhergehende Transaktion abgeschlossen ist. Jede Transaktion wird jedoch explizit mit einer COMMIT- oder ROLLBACK-Anweisung beendet.  
  
 Transaktionen mit batchbereich  
 Trifft nur auf MARS (Multiple Active Result Sets) zu; eine explizite oder implizite [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion, die unter einer MARS-Sitzung gestartet wird, wird zu einer Transaktion im Batchbereich. Für eine Transaktion im Batchbereich, für die nach Abschluss des Batches kein Commit oder Rollback ausgeführt wird, wird das Rollback automatisch von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt.  

> [!NOTE] 
> Besondere Aspekte im Zusammenhang mit der Data Warehouse-Produkte finden Sie unter [Transaktionen (SQL Data Warehouse)](transactions-sql-data-warehouse.md).   

## <a name="in-this-section"></a>In diesem Abschnitt  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Stellt die folgenden transaktionsanweisungen bereit:  
  
|||  
|-|-|  
|[BEGIN DISTRIBUTED TRANSACTION](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)|[ROLLBACK TRANSACTION](../../t-sql/language-elements/rollback-transaction-transact-sql.md)|  
|[BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md)|[ROLLBACK WORK](../../t-sql/language-elements/rollback-work-transact-sql.md)|  
|[COMMIT TRANSACTION](../../t-sql/language-elements/commit-transaction-transact-sql.md)|[SAVE TRANSACTION](../../t-sql/language-elements/save-transaction-transact-sql.md)|  
|[COMMIT WORK](../../t-sql/language-elements/commit-work-transact-sql.md)||  
  
## <a name="see-also"></a>Siehe auch  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
