---
title: Extrahieren eines Skripts aus einer Ablaufverfolgung (SQL Server Profiler) | Microsoft-Dokumentation
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
- scripts [SQL Server], traces
- extracting script from trace [SQL Server]
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1a6b1c13fce71dc29f332e1b85abfca0378f6f2b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>Extrahieren eines Skripts aus einer Ablaufverfolgung (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird das Extrahieren von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Ereignissen aus einer Ablaufverfolgungsdatei oder -tabelle sowie das Speichern in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skriptdatei mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]beschrieben.  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>So extrahieren Sie ein Transact-SQL-Skript aus einer Ablaufverfolgungsdatei oder -tabelle  
  
1.  Öffnen Sie eine Ablaufverfolgungsdatei oder -tabelle, die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ereignisse enthält, die Sie in einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skriptdatei speichern möchten. Weitere Informationen finden Sie unter [Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) oder den Optimierungsratgeber von [Öffnen einer Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)die richtigen Ereignisse und Spalten aufgezeichnet werden.  
  
2.  Zeigen Sie im Menü **Datei** auf **Exportieren**, zeigen Sie auf **SQL Server-Ereignisse extrahieren**, und klicken Sie dann auf **Transact-SQL-Ereignisse extrahieren**.  
  
3.  Geben Sie im Dialogfeld **Speichern unter** einen Namen für die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Datei ein, und klicken Sie dann auf **Speichern**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
