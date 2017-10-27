---
title: Systemintern kompilierte gespeicherte Prozeduren | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b718bafa35ae753eba0064db2af168054fd211ca
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="natively-compiled-stored-procedures"></a>Systemintern kompilierte gespeicherte Prozeduren
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Systemintern kompilierte gespeicherte Prozeduren sind gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozeduren, die in systemeigenen Code kompiliert werden und auf speicheroptimierte Tabellen zugreifen. Systemintern kompilierte gespeicherte Prozeduren ermöglichen die effiziente Ausführung der Abfragen und Geschäftslogik in der gespeicherten Prozedur. Ausführliche Informationen zur systeminternen Kompilierung finden Sie unter [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md). Weitere Informationen zum Migrieren von datenträgerbasierten gespeicherten Prozeduren zu nativ kompilierten gespeicherten Prozeduren finden Sie unter [Migrationsprobleme bei nativ kompilierten gespeicherten Prozeduren](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md).  
  
> [!NOTE]  
>  Ein Unterschied zwischen interpretierten (datenträgerbasierten) gespeicherten Prozeduren und nativ kompilierten gespeicherten Prozeduren besteht darin, dass eine interpretierte gespeicherte Prozedur bei der ersten Ausführung kompiliert wird, während eine nativ kompilierte gespeicherte Prozedur bei der Erstellung kompiliert wird. Bei nativ kompilierten gespeicherten Prozeduren können viele Fehlerbedingungen (arithmetischer Überlauf, Typkonvertierung und bestimmte Bedingungen bei Division durch null) bei der Erstellung festgestellt werden, die zu einem Fehler bei der Erstellung der nativ kompilierten gespeicherten Prozedur führen. Bei interpretierten gespeicherten Prozeduren führen diese Fehlerbedingungen in der Regel zu keinem Fehler, wenn die gespeicherte Prozedur erstellt wird, sondern bei jeder Ausführung.  
  
 Themen in diesem Abschnitt:  
  
-   [Erstellen systemintern kompilierter gespeicherter Prozeduren](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)  
  
-   [ATOMIC-Blöcke](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)  
  
-   [Unterstützte Funktionen für nativ kompilierte T-SQL-Module](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [Unterstützte DDL für nativ kompilierte T-SQL-Module](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [Systemintern kompilierte gespeicherte Prozeduren und deren Ausführung mit SET-Optionen](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [Bewährte Vorgehensweisen für den Aufruf von systemintern kompilierten gespeicherten Prozeduren](../../relational-databases/in-memory-oltp/best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [Überwachen der Leistung von systemintern kompilierten gespeicherten Prozeduren](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [Aufrufen von systemintern kompilierten gespeicherten Prozeduren über Datenzugriffsanwendungen](../../relational-databases/in-memory-oltp/calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  

