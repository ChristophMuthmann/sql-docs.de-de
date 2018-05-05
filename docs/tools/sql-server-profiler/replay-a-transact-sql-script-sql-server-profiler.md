---
title: Wiedergeben eines Transact-SQL-Skripts (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bfda646b7bd7211067bb146ff31d95bcd3662ccc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Wiedergeben eines Transact-SQL-Skripts (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Verwenden Sie beim Testen von möglichen Lösungen für ein Leistungsproblem [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , um [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts wiederzugeben, und vergleichen Sie die Leistung vor und nach dem Ändern.  
  
### <a name="to-replay-a-transact-sql-script"></a>So geben Sie ein Transact-SQL-Skript wieder  
  
1.  Zeigen Sie im Menü **Datei** auf **Öffnen**, und klicken Sie dann auf **Skriptdatei**.  
  
2.  Wählen Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skriptdatei aus, die Sie öffnen möchten. Stellen Sie sicher, dass das [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript die zum Wiedergeben erforderlichen Ereignisse enthält. Weitere Informationen finden Sie unter [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
3.  Klicken Sie im Menü **Wiedergeben** auf **Start**, und stellen Sie eine Verbindung mit dem Server her, auf dem das Skript wiedergegeben werden soll.  
  
4.  Überprüfen Sie im Dialogfeld **Wiedergabekonfiguration** die Einstellungen, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Wiedergeben von Ablaufverfolgungen](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
