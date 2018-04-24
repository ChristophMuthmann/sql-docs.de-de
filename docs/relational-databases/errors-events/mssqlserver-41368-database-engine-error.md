---
title: MSSQLSERVER_41368 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: e2aded8bf29e77ff4239528790b3b8745dd97d3a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver41368"></a>MSSQLSERVER_41368
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|41368|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|Meldungstext|Der Zugriff auf speicheroptimierte Tabellen mit der READ COMMITTED-Isolationsstufe wird nur für Autocommittransaktionen unterstützt. Er wird nicht für explizite oder implizite Transaktionen unterstützt. Geben Sie eine unterstützte Isolationsstufe für die speicheroptimierte Tabelle mithilfe eines Tabellentipps wie WITH (SNAPSHOT) an.|  
  
## <a name="explanation"></a>Erklärung  
Der Zugriff auf speicheroptimierte Tabellen mit der READ COMMITTED-Isolationsstufe wird nur für Autocommittransaktionen unterstützt. Weitere Informationen finden Sie unter [Transaktionen mit In-Memory-Tabellen und Prozeduren](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md).  
  
Wenn Sie unter Verwendung einer expliziten Transaktion, die mit BEGIN TRANSACTION gestartet wurde, oder einer impliziten Transaktion auf eine speicheroptimierte Tabelle zugreifen, während IMPLICIT_TRANSACTIONS auf ON festgelegt ist, wird die READ COMMITTED-Isolationsstufe nicht unterstützt.  
  
## <a name="user-action"></a>Benutzeraktion  
Verwenden Sie für den Tabellenzugriff die SNAPSHOT-Isolationsstufe, wenn Sie von einer expliziten oder impliziten READ COMMITTED-Transaktion auf eine speicheroptimierte Tabelle zugreifen. Dazu können Sie den Tabellenhinweis WITH (SNAPSHOT) verwenden (weitere Informationen finden Sie unter [Transaktionen mit In-Memory-Tabellen und Prozeduren](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)) oder die Datenbankoption MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT auf ON festlegen (weitere Informationen finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql.md)).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
