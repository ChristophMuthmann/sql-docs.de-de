---
title: "Überwachen der Auftragsaktivität | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, monitoring
- jobs [SQL Server Agent], monitoring
- monitoring [SQL Server], jobs
- activity monitoring [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- SQL Server Agent Job Activity Monitor
- SQL Server Agent jobs, monitoring
- performance [SQL Server], jobs
- current activity
ms.assetid: 71cb432b-631d-4b8b-9965-e731b3d8266d
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 762fd21319860bfe98fcbeeec5b777b62f54c533
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="monitor-job-activity"></a>Überwachen der Auftragsaktivität
Sie können die aktuellen Aktivitäten aller definierten Aufträge auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] überwachen, indem Sie den Auftragsaktivitätsmonitor des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agents verwenden.  
  
## <a name="sql-server-agent-sessions"></a>Sitzungen des SQL Server-Agents  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent erstellt jedes Mal, wenn der Dienst gestartet wird, eine neue Sitzung. Beim Erstellen einer neuen Sitzung wird die **sysjobactivity** -Tabelle in der **msdb** -Datenbank mit allen vorhandenen definierten Aufträgen aufgefüllt. Beim Neustart des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents bleibt die letzte Auftragsaktivität in dieser Tabelle erhalten. Jede Sitzung zeichnet die normale Auftragsaktivität des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents vom Anfang bis zum Ende des Auftrags auf. Informationen zu diesen Sitzungen werden in der **syssessions** -Tabelle der **msdb** -Datenbank gespeichert.  
  
## <a name="job-activity-monitor"></a>Auftragsaktivitätsmonitor  
Mit dem Auftragsaktivitätsmonitor können Sie die **sysjobactivity** -Tabelle mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]anzeigen. Sie können alle Aufträge auf dem Server anzeigen oder Filter definieren, um die Anzahl der angezeigten Aufträge zu beschränken. Sie können die Auftragsinformationen auch sortieren, indem Sie auf eine Spaltenüberschrift im Raster **Agentauftragsaktivität** klicken. Wenn Sie beispielsweise die Spaltenüberschrift **Letzte Ausführung** auswählen, können Sie die Aufträge in der Reihenfolge anzeigen, in der sie zuletzt ausgeführt wurden. Wenn Sie erneut auf die Spaltenüberschrift klicken, werden die Aufträge je nach ihrem letzten Ausführungsdatum so umgeschaltet, dass sie in auf- bzw. absteigender Reihenfolge angezeigt werden.  
  
Mit dem Auftragsaktivitätsmonitor können Sie folgende Aufgaben ausführen:  
  
-   Starten und Beenden von Aufträgen  
  
-   Anzeigen von Auftragseigenschaften  
  
-   Anzeigen des Verlaufsprotokolls für einen bestimmten Auftrag  
  
-   Manuelles Aktualisieren der Informationen im Raster **Agentauftragsaktivität** oder Festlegen eines automatischen Aktualisierungsintervalls durch Klicken auf **Aktualisierungseinstellungen anzeigen**.  
  
Verwenden Sie den Auftragsaktivitätsmonitor, um zu ermitteln, für welche Aufträge eine Ausführung geplant ist, oder um festzustellen, welche Aufträge derzeit ausgeführt werden bzw. im Leerlauf sind. Sie können mit dem Auftragsaktivitätsmonitor auch das Ergebnis von Aufträgen anzeigen, die während der aktuellen Sitzung ausgeführt wurden. Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst unerwartet einen Fehler erzeugt, können Sie ermitteln, welche Aufträge zum Zeitpunkt des Fehlers ausgeführt wurden, indem Sie im Auftragsaktivitätsmonitor die vorherige Sitzung anzeigen.  
  
Erweitern Sie im Objekt-Explorer von **die Option** SQL Server-Agent [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] , um den Auftragsaktivitätsmonitor zu öffnen. Klicken Sie mit der rechten Maustaste auf **Auftragsaktivitätsmonitor**, und klicken Sie dann auf **Auftragsaktivitäten anzeigen**.  
  
Sie können Auftragsaktivitäten für die aktuelle Sitzung auch mithilfe der gespeicherten Prozedur **sp_help_jobactivity**anzeigen.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|**Description**|**Thema**|  
|Beschreibt, wie der Laufzeitstatus von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträgen angezeigt wird.|[Auftragsaktivitäten anzeigen](../../ssms/agent/view-job-activity.md)|  
  
## <a name="see-also"></a>Siehe auch  
[Auftragsaktivitäten anzeigen](../../ssms/agent/view-job-activity.md)  
[sysjobactivity (Transact-SQL)](http://msdn.microsoft.com/en-us/fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e)  
[syssessions (Transact-SQL)](http://msdn.microsoft.com/en-us/187819b6-c7f4-4a26-b74c-0a89e96695cf)  
[sp_help_jobactivity (Transact-SQL)](http://msdn.microsoft.com/en-us/d344864f-b4d3-46b1-8933-b81dec71f511)  
  

