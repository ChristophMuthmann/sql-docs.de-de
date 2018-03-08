---
title: Speichern von Deadlock Graphs (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
caps.latest.revision: "26"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0aaa9c41b63479eda21bf1f0e862639c50160495
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>Speichern von Deadlock Graphs (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie ein Deadlock Graph mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] gespeichert wird. Deadlock Graphs werden als XML-Dateien gespeichert.  
  
## <a name="save-deadlock-graph-events-separately"></a>Separates Speichern von Deadlock Graph-Ereignissen  
  
1. Wählen Sie im Menü **Datei** die Option **Neue Ablaufverfolgung** aus, und stellen Sie dann eine Verbindung mit einer Instanz von SQL Server her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften** wird angezeigt.  
  
    > [!NOTE]  
    >  Wenn Sie **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** auswählen, wird das Dialogfeld **Ablaufverfolgungseigenschaften** nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, wählen Sie im Menü **Extras** **Optionen** aus und deaktivieren das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**.  
  
2. Geben Sie im Dialogfeld **Ablaufverfolgungseigenschaften** im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein.  
  
3. Wählen Sie in der Liste **Vorlage verwenden** eine Nachverfolgungsvorlage aus, auf der die Nachverfolgung basieren soll. Wenn Sie keine Vorlage verwenden möchten, wählen Sie **Leer** aus.  
  
4. Führen Sie eines der folgenden Verfahren aus:  
  
    -   Aktivieren Sie das Kontrollkästchen **In Datei speichern**, um die Ablaufverfolgung in einer Datei aufzuzeichnen. Geben Sie einen Wert für **Maximale Dateigröße festlegen**an.  
  
         Optional aktivieren Sie die Kontrollkästchen **Dateirollover aktivieren** und **Ablaufverfolgungsdaten von Serverprozessen** . 
  
    -   Aktivieren Sie das Kontrollkästchen **In Tabelle speichern**, um die Ablaufverfolgung in einer Datenbanktabelle aufzuzeichnen.  
  
         Wählen Sie optional **Maximale Zeilenzahl festlegen** aus, und geben Sie einen Wert an.  
  
5. Aktivieren Sie optional das Kontrollkästchen **Beendigungszeit für Ablaufverfolgung aktivieren** , und geben Sie das Datum und die Uhrzeit zum Beenden der Ablaufverfolgung an. 
  
6. Wählen Sie die Registerkarte **Ereignisauswahl** aus.  
  
7. Erweitern Sie in der **Events**-Datenspalte die **Sperren**-Ereigniskategorie, und aktivieren Sie das Kontrollkästchen **Deadlock Graph**. Falls die Ereigniskategorie **Sperren** nicht verfügbar ist, aktivieren Sie das Kontrollkästchen **Alle Ereignisse anzeigen**, damit sie angezeigt wird.  
  
     Die Registerkarte **Ereignisextraktionseinstellungen** wird dem Dialogfeld **Ablaufverfolgungseigenschaften** hinzugefügt.  
  
8. Wählen Sie auf der Registerkarte **Ereignisextraktionseinstellungen** die Option **Deadlock-XML-Ereignisse separat speichern** aus.  
  
9. Geben Sie im Dialogfeld **Speichern unter** den Namen der Datei ein, in der Sie die Deadlock Graph-Ereignisse speichern möchten.  
  
10. Wählen Sie **Alle Deadlock-XML-Batches in einer einzelnen Datei** aus, um alle Deadlock Graph-Ereignisse in einer einzelnen XML-Datei zu speichern. Wählen Sie alternativ **Jeder Deadlock-XML-Batch in einer eigenen Datei** aus, um für jeden Deadlock Graph eine neue XML-Datei zu erstellen.  
  
 Nach dem Speichern der Deadlockdatei können Sie sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnen. Weitere Informationen finden Sie unter [Öffnen, Anzeigen und Drucken einer Deadlockdatei &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/open-view-and-print-a-deadlock-file-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Analysieren von Deadlocks mit SQL Server Profiler](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  
