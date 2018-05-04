---
title: Filtern von Ereignissen anhand der Ereignisstartzeit (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
- event start times [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: e965579e-d006-41a3-89ec-cfd5398c67d2
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e513313b92af3963541a58a383c6672b4f12b64f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="filter-events-based-on-the-event-start-time-sql-server-profiler"></a>Filtern von Ereignissen nach Ereignisstartzeit (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Sie mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]Ablaufverfolgungsereignisse basierend auf der Ereignisstartzeit filtern.  
  
### <a name="to-filter-an-event-based-on-the-event-start-time"></a>So filtern Sie ein Ereignis basierend auf der Ereignisstartzeit  
  
1.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**, und stellen Sie dann eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften**wird angezeigt.  
  
    > [!NOTE]  
    >  Bei der Auswahl von **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**wird das Dialogfeld **Ablaufverfolgungseigenschaften**nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, klicken Sie im Menü **Extras**auf **Optionen**, und deaktivieren Sie das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** .  
  
2.  Geben Sie im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein.  
  
3.  Geben Sie im Feld **Vorlage verwenden**eine Ablaufverfolgungsvorlage aus.  
  
4.  Geben Sie optional ein Ziel für die Ablaufverfolgungsergebnisse an.  
  
5.  Klicken Sie im Menü **Ereignisauswahl**auf die Spaltenüberschrift **StartTime** . Sie können auch mit der rechten Maustaste auf die Spaltenüberschrift klicken und dann auf **Spaltenfilter bearbeiten** klicken, um das Dialogfeld **Filter bearbeiten** zu starten.  
  
6.  Erweitern Sie **Größer als** oder **Kleiner als**, und geben Sie dann einen **datetime** -Wert in das Feld ein, das unterhalb des Vergleichsoperators angezeigt wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
