---
title: "Löschen einer Ablaufverfolgung (Transact-SQL) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5d9eb3c4aeafab2fb6337da5d0bb24c3f4d3b8f7
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="delete-a-trace-transact-sql"></a>Löschen einer Ablaufverfolgung (Transact-SQL)
  In diesem Thema wird beschrieben, wie Sie mithilfe von gespeicherten Prozeduren eine Ablaufverfolgung löschen.  
  
 Ein Beispiel zum Verwenden gespeicherter Prozeduren der Ablaufverfolgung finden Sie unter [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
### <a name="to-delete-a-trace"></a>So löschen Sie eine Ablaufverfolgung  
  
1.  Führen Sie **sp_trace_setstatus** mit **@status = 0** aus, um die Ablaufverfolgung zu beenden.  
  
2.  Führen Sie **sp_trace_setstatus** mit **@status = 2** aus, um die Ablaufverfolgung zu schließen und die zugehörigen Informationen vom Server zu löschen.  
  
> [!NOTE]  
>  Eine Ablaufverfolgung muss beendet werden, bevor sie geschlossen werden kann.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Prozeduren von SQL Server Profiler &#40;SQL Server Profiler&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
