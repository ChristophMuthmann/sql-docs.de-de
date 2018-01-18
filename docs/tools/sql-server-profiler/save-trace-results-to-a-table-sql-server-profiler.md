---
title: Speichern von Ablaufverfolgungsergebnissen in einer Tabelle (SQL Server Profiler) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
caps.latest.revision: "24"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f411639ced17e80acca493e7e0cd23de6ed5bc8c
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>Speichern von Ablaufverfolgungsergebnissen in einer Tabelle (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In diesem Thema wird beschrieben, wie zum Speichern von Ablaufverfolgungsergebnissen in einer Datenbanktabelle mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-save-trace-results-to-a-table"></a>So speichern Sie Ablaufverfolgungsergebnisse in einer Tabelle  
  
1.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**, und stellen Sie dann eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften**wird angezeigt.  
  
    > [!NOTE]  
    >  Bei der Auswahl von **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**wird das Dialogfeld **Ablaufverfolgungseigenschaften**nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, klicken Sie im Menü **Extras**auf **Optionen**, und deaktivieren Sie das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** .  
  
2.  Geben Sie im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein, und klicken Sie dann auf **In Tabelle speichern**.  
  
3.  Stellen Sie im Dialogfeld **Verbindung mit Server herstellen** eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank her, die die Ablaufverfolgungstabelle enthalten wird.  
  
4.  Geben Sie im Feld **Zieltabelle** in der Liste **Datenbank**eine Datenbank aus.  
  
5.  Wählen Sie in der Liste **Besitzer** den Besitzer für die Ablaufverfolgung aus.  
  
6.  Geben Sie im Feld **Tabelle** den Tabellennamen für die Ablaufverfolgungsergebnisse ein, oder wählen Sie den Namen aus. Klicken Sie auf **OK.**  
  
7.  Aktivieren Sie im Dialogfeld **Ablaufverfolgungseigenschaften** das Kontrollkästchen **Maximale Zeilenzahl festlegen (in Tausend)**, um die maximale Anzahl zu speichernder Zeilen anzugeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
