---
title: Migrieren von Triggern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2f151fa00c2e92ef1509ea2c6d7d93e8c8d2c69
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="migrating-triggers"></a>Migrieren von Triggern
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In diesem Thema werden DDL-Trigger und speicheroptimierte Tabellen erläutert.  
  
 DML-Trigger werden für speicheroptimierte Tabellen unterstützt, aber nur mit dem Triggerereignis FOR | AFTER. Ein Beispiel finden Sie unter [Implementieren von UPDATE mit FROM oder Unterabfragen](../../relational-databases/in-memory-oltp/implementing-update-with-from-or-subqueries.md). 
  
 LOGON-Trigger sind Trigger zum Auslösen von LOGON-Ereignissen. LOGON-Trigger wirken sich nicht auf speicheroptimierte Tabellen aus.  
  
## <a name="ddl-triggers"></a>DDL-Trigger  
 DDL-Trigger sind Trigger, die ausgelöst werden, wenn eine CREATE-, ALTER-, DROP-, GRANT-, DENY-, REVOKE- oder UPDATE STATISTICS-Anweisung für die Datenbank oder den Server ausgeführt wird, für die oder den sie definiert wurde.  
  
 Sie können keine speicheroptimierten Tabellen erstellen, wenn die Datenbank oder der Server über mindestens einen DDL-Trigger verfügt, der für CREATE_TABLE oder eine beliebige Ereignisgruppe definiert wurde, in der das Ereignis enthalten ist. Sie können keine speicheroptimierte Tabelle löschen, wenn die Datenbank oder der Server über mindestens einen DDL-Trigger verfügt, der für DROP_TABLE oder eine beliebige Ereignisgruppe definiert wurde, in der das Ereignis enthalten ist.  
  
 Systemintern kompilierte gespeicherte Prozeduren können nicht erstellt werden, wenn mindestens ein DDL-Trigger für CREATE_PROCEDURE, DROP_PROCEDURE oder eine beliebige Ereignisgruppe definiert wurde, in der diese Ereignisse enthalten sind.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Migrieren zu In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
