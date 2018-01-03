---
title: Speichern von Ablaufverfolgungsergebnissen in einer Datei (SQL Server Profiler) | Microsoft Docs
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
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e347edc4a3e442cd7422e7b9e18829c14fdfeb7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="save-trace-results-to-a-file-sql-server-profiler"></a>Speichern von Ablaufverfolgungsergebnissen in einer Datei (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In diesem Thema wird beschrieben, wie zum Speichern von Ablaufverfolgungsergebnissen in einer Datei mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-save-trace-results-to-a-file"></a>So speichern Sie Ablaufverfolgungsergebnisse in einer Datei  
  
1.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**, und stellen Sie dann eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften**wird angezeigt.  
  
    > [!NOTE]  
    >  Bei der Auswahl von **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**wird das Dialogfeld **Ablaufverfolgungseigenschaften**nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, klicken Sie im Menü **Extras**auf **Optionen**, und deaktivieren Sie das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** .  
  
2.  Geben Sie im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein.  
  
3.  Aktivieren Sie das Kontrollkästchen **In Datei speichern** .  
  
     Das Dialogfeld **Speichern unter**wird angezeigt.  
  
4.  Geben Sie im Dialogfeld **Speichern unter**den Pfad und den Dateinamen an. Klicken Sie auf **Speichern.**  
  
    > [!NOTE]  
    >  Stellen Sie sicher, dass der SQL Server-Dienst die entsprechenden Berechtigungen hat, um in eine Datei im angegebenen Verzeichnis zu schreiben.  
  
5.  Geben Sie im Dialogfeld **Ablaufverfolgungseigenschaften** die maximale Dateigröße in das Textfeld **Maximale Dateigröße festlegen (MB)** ein. Der Standardwert ist 5 MB.  
  
6.  Geben Sie optional die folgenden Optionen an:  
  
    -   Aktivieren Sie das Kontrollkästchen **Dateirollover aktivieren** , damit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] neue Dateien für Ablaufverfolgungsdaten erstellt, wenn die maximale Dateigröße erreicht wird. Diese Option ist standardmäßig aktiviert.  
  
    -   Aktivieren Sie das Kontrollkästchen **Ablaufverfolgungsdaten von Serverprozessen** , um sicherzustellen, dass der Server jedes Ablaufverfolgungsereignis aufzeichnet.  
  
        > [!NOTE]  
        >  Wenn **Ablaufverfolgungsdaten von Serverprozessen**deaktiviert ist, zeichnet der Server keine Ereignisse auf, falls dadurch die Leistung erheblich beeinträchtigt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
