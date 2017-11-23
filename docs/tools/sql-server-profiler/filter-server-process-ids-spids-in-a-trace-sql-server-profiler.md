---
title: Filtern von Server-Prozess-IDs (SPIDs) in einer Ablaufverfolgung (SQL Server Profiler) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], traces
- filters [SQL Server], SPIDs
- traces [SQL Server], filters
ms.assetid: f5945c39-be6b-4632-91cb-92066c80e188
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bc5b5a3650b2d5eb646b34ad501d7d911799549
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="filter-server-process-ids-spids-in-a-trace-sql-server-profiler"></a>Filtern von Server-Prozess-IDs (SPIDs) in einer Ablaufverfolgung (SQL Server Profiler)
  In diesem Thema wird das Filtern von Server-Prozess-IDs (SPIDs) in einer Ablaufverfolgung mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]erläutert.  
  
### <a name="to-filter-system-ids-in-a-trace"></a>So filtern Sie System-IDs in einer Ablaufverfolgung  
  
1.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**, und stellen Sie dann eine Verbindung zu einer Instanz von SQL Server her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften**wird angezeigt.  
  
    > [!NOTE]  
    >  Bei der Auswahl von **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**wird das Dialogfeld **Ablaufverfolgungseigenschaften**nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, klicken Sie im Menü **Extras**auf **Optionen**, und deaktivieren Sie das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** .  
  
2.  Geben Sie im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein.  
  
3.  Geben Sie im Feld **Vorlage verwenden**eine Ablaufverfolgungsvorlage aus.  
  
4.  Sie können optional eine Zieldatei oder Zieltabelle angeben, in der die Ablaufverfolgungsergebnisse gespeichert werden.  
  
5.  Klicken Sie auf der Registerkarte **Ereignisauswahl**auf die Spaltenüberschrift **SPID**, um das Dialogfeld **Filter bearbeiten** zu öffnen. Sie können auch mit der rechten Maustaste auf die Spaltenüberschrift klicken und **Spaltenfilter bearbeiten**auswählen. Wenn die **SPID** -Spalte nicht angezeigt wird, überprüfen Sie das Feld **Alle Spalten anzeigen** .  
  
6.  Erweitern Sie im Dialogfeld **Filter bearbeiten** den entsprechenden Vergleichsoperator, und geben Sie eine SPID als Wert für den Vergleich ein.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
