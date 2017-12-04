---
title: "Systemintern kompilierte gespeicherte Prozeduren und deren Ausführung mit SET-Optionen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
caps.latest.revision: "5"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bca46c39dc3e78fcd5ec9c18847707fcd401d9a8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>Systemintern kompilierte gespeicherte Prozeduren und deren Ausführung mit SET-Optionen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Sitzungsoptionen sind in ATOMIC-Blöcken fixiert, wie in [Atomic Blocks (ATOMIC-Blöcken)](atomic-blocks-in-native-procedures.md) beschrieben. Die Ausführung einer gespeicherten Prozedur wird durch die SET-Optionen einer Sitzung nicht beeinflusst, da ATOMIC-Blöcke benötigt werden. Bestimmte SET-Optionen, wie SET NOEXEC und SET SHOWPLAN_XML, bewirken jedoch, dass gespeicherte Prozeduren (einschließlich systemintern kompilierter gespeicherter Prozeduren) nicht ausgeführt werden.   
  
 Wenn eine systemintern kompilierte gespeicherte Prozedur mit einer aktivierten STATISTICS-Option ausgeführt wird, werden Statistiken für die Prozedur als Ganzes und nicht pro Anweisung erfasst. Weitere Informationen finden Sie unter [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md), [SET STATISTICS PROFILE &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-profile-transact-sql.md), [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md) und [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md). Um für systemintern gespeicherte Prozeduren eine Ausführungsstatistik pro Anweisung abzurufen, verwenden Sie für das sp_statement_completed-Ereignis eine Sitzung für erweiterte Ereignisse. Diese startet, nachdem alle Abfragen in der Ausführung einer gespeicherten Prozedur abgeschlossen sind. Weitere Informationen zum Erstellen einer Sitzung für erweiterte Ereignisse finden Sie unter [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md).  
  
 **SHOWPLAN_XML** wird für nativ kompilierte gespeicherte Prozeduren unterstützt. **SHOWPLAN_ALL** und **SHOWPLAN_TEXT** werden bei nativ kompilierten gespeicherten Prozeduren nicht unterstützt.  
  
 **SET FMTONLY** wird bei systemintern kompilierten gespeicherten Prozeduren nicht unterstützt. Verwenden Sie stattdessen [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Systemintern kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
