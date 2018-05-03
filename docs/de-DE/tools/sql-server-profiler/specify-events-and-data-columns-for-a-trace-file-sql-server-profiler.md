---
title: Angeben von Ereignissen und Datenspalten für eine Ablaufverfolgungsdatei (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- adding events
- traces [SQL Server], data columns
- deleting events
- removing events
- traces [SQL Server], events
ms.assetid: 7da715a3-2f03-4063-b6a4-20fd7b44e675
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45184a8741296f43b29029776741def6704a6aaf
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="specify-events-and-data-columns-for-a-trace-file-sql-server-profiler"></a>Angeben von Ereignissen und Datenspalten für eine Ablaufverfolgungsdatei (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In diesem Artikel wird beschrieben, wie Ereignisklassen und Datenspalten mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] angegeben werden.  
  
### <a name="to-specify-events-and-data-columns-for-a-trace"></a>So geben Sie Ereignisse und Datenspalten für eine Ablaufverfolgung an  
  
1.  Klicken Sie im Dialogfeld **Ablaufverfolgungseigenschaften** oder **Eigenschaften der Ablaufverfolgungsvorlage** auf die Registerkarte **Ereignisauswahl** .  
  
     Die Registerkarte **Ereignisauswahl** enthält ein Rastersteuerelement. Bei dem Rastersteuerelement handelt es sich um eine Tabelle, die alle bei der Ablaufverfolgung zu berücksichtigenden Ereignisklassen enthält. Die Tabelle enthält für jede Ereignisklasse eine Zeile. Die Ereignisklassen können sich leicht voneinander unterscheiden. Dies hängt vom Typ und der Version des Servers ab, zu dem eine Verbindung besteht. Die Ereignisklassen werden in der Spalte **Events**des Rasters identifiziert und nach Ereigniskategorie gruppiert. In den übrigen Spalten sind die Datenspalten aufgeführt, die für jede Ereignisklasse zurückgegeben werden können.  
  
2.  Klicken Sie im Dialogfeld **Ereignisauswahl**das Rastersteuerelement, um Ereignisse und Datenspalten zur Ablaufverfolgungsdatei hinzuzufügen oder aus ihr zu entfernen.  
  
3.  Um Ereignisse aus der Ablaufverfolgung zu entfernen, deaktivieren Sie das Kontrollkästchen in der **Ereignisse** -Spalte für jede Ereignisklasse.  
  
4.  Um Ereignisse in einer Ablaufverfolgung einzuschließen, aktivieren Sie das Kontrollkästchen in der **Ereignisse** -Spalte für jede Ereignisklasse, oder aktivieren Sie eine Datenspalte, die sich auf ein Ereignis bezieht.  
  
> [!IMPORTANT]  
>  Wenn die Ablaufverfolgung mit Systemmonitordaten abhängig wird, müssen die Datenspalten **Startzeit** und **Beendigungszeit** in der Ablaufverfolgung eingeschlossen sein.  
  
 Wenn Sie eine Ereignisklasse einschließen, wird auch jede zugeordnete Datenspalte in die Ablaufverfolgung aufgenommen, wenn Sie das Kontrollkästchen aktiviert haben, das mit einem Ereignis korrespondiert. Wenn Sie das Kontrollkästchen für eine bestimmte Spalte aktiviert haben, wird nur diese Spalte in die Ablaufverfolgung aufgenommen.  
  
1.  Um Datenspalten aus einer Ereignisklasse zu entfernen, deaktivieren Sie die Kontrollkästchen der Datenspalte in der Ereignisklassenzeile, oder klicken Sie mit der rechten Maustaste auf den Spaltenheader, und wählen Sie die Option **Spaltenauswahl aufheben** aus.  
  
2.  Wenden Sie optional Filter auf die Ablaufverfolgung an. Weitere Informationen finden Sie unter [Filtern von Ereignissen in einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
