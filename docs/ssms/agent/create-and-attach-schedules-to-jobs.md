---
title: Anlegen und Zuweisen von Zeitplänen zu Aufträgen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server]
- scheduling jobs [SQL Server]
- jobs [SQL Server], scheduling
- CPU [SQL Server], idle conditions
- automatic job processing
- SQL Server Agent jobs, scheduling
- idle time [SQL Server]
ms.assetid: 079c2984-0052-4a37-a2b8-4ece56e6b6b5
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d46a10ac4701e45bbec0684d0141062b1ebd9709
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-and-attach-schedules-to-jobs"></a>Anlegen und Zuweisen von Zeitplänen zu Aufträgen
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Zeitpläne für Aufträge des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents zu erstellen bedeutet, die Bedingung(en) zu definieren, durch die die Ausführung des Auftrags ohne Benutzerinteraktion gestartet wird. Sie können einen Auftrag so planen, dass er automatisch ausgeführt wird, indem Sie einen neuen Zeitplan für den Auftrag erstellen oder indem Sie dem Auftrag einen vorhandenen Zeitplan zuweisen.  
  
Es gibt zwei Möglichkeiten, einen Zeitplan zu erstellen:  
  
-   Erstellen Sie den Zeitplan, während Sie einen Auftrag erstellen.  
  
-   Erstellen Sie den Zeitplan im Objekt-Explorer.  
  
Nach dem Erstellen eines Zeitplans können Sie ihn mehreren Aufträgen zuweisen, auch wenn der Zeitplan für einen bestimmten Auftrag erstellt wurde. Sie können auch Zeitpläne von Aufträgen trennen.  
  
Ein Zeitplan kann zeit- oder ereignisbasiert sein. Zum Beispiel können Sie einen Auftrag so planen, dass er zu den folgenden Zeitpunkten ausgeführt wird:  
  
-   Ausführung sobald der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent startet.  
  
-   Ausführung, wenn sich die CPU-Auslastung des Computers in einem Bereich befindet, den Sie als Leerlauf definiert haben.  
  
-   Einmalige Ausführung zu einem bestimmten Zeitpunkt.  
  
-   Regelmäßige Ausführung.  
  
Als Alternative zu Auftragszeitplänen können Sie auch eine Warnung erstellen, durch die in Reaktion auf ein Ereignis ein bestimmter Auftrag ausgeführt wird.  
  
> [!NOTE]  
> Es kann nur jeweils eine einzige Instanz eines Auftrags ausgeführt werden. Wenn Sie versuchen, einen Auftrag manuell auszuführen, der bereits im Rahmen eines Zeitplans ausgeführt wird, lehnt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die Anforderung ab.  
  
Um zu verhindern, dass ein geplanter Auftrag ausgeführt wird, müssen Sie eine der folgendem Aktionen ausführen:  
  
-   Den Zeitplan deaktivieren.  
  
-   Den Auftrag deaktivieren.  
  
-   Den Zeitplan von dem Auftrag trennen.  
  
-   Den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst beenden.  
  
-   Den Zeitplan löschen.  
  
Wenn der Zeitplan nicht aktiviert ist, kann der Auftrag dennoch als Reaktion auf eine Warnung oder durch einen Benutzer manuell ausgeführt werden. Wenn der Auftragszeitplan nicht aktiviert ist, ist der Zeitplan auch für keinen der anderen Aufträge aktiviert, die ihn verwenden.  
  
Ein deaktivierter Zeitplan muss explizit erneut aktiviert werden. Beim Bearbeiten eines Zeitplans wird dieser nicht automatisch erneut aktiviert.  
  
## <a name="scheduling-start-dates"></a>Planen von Startdaten  
Das Startdatum eines Zeitplans muss größer als oder gleich 19900101 sein.  
  
Wenn Sie einem Auftrag einen Zeitplan zuweisen, überprüfen Sie das Startdatum, das der Zeitplan für das erstmalige Ausführen des Auftrags verwendet. Das Startdatum hängt von dem Tag und der Uhrzeit ab, zu denen Sie den Zeitplan dem Auftrag zuweisen. Sie erstellen z. B. einen Zeitplan, der an jedem zweiten Montag um 8:00 Uhr ausgeführt wird. Wenn Sie einen Auftrag am Montag, 3. März 2008, um 10:00 Uhr erstellen, ist das Startdatum Montag, 17. März 2008. Wenn Sie einen weiteren Auftrag am Dienstag, dem 4. März 2008 erstellen, ist das Startdatum Montag, der 10. März 2008.  
  
Sie können das Startdatum des Zeitplans ändern, nachdem Sie den Zeitplan einem Auftrag zugewiesen haben.  
  
## <a name="cpu-idle-schedules"></a>CPU-Leerlauf-Zeitpläne  
Zur maximalen Nutzung der CPU-Ressourcen können Sie eine CPU-Leerlaufbedingung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent definieren. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent verwendet die CPU-Leerlaufbedingung, um den optimalen Zeitpunkt für die Ausführung von Aufträgen festzustellen. So können Sie beispielsweise einen Zeitplan für einen Auftrag zur Neuerstellung von Indizes erstellen, der während der CPU-Leerlaufzeit und zu Zeiten mit geringer Produktion eintritt.  
  
Bevor Sie Aufträge definieren, die während der CPU-Leerlaufzeit ausgeführt werden sollen, müssen Sie die CPU-Auslastung während der normalen Verarbeitung ermitteln. Dazu können Sie mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler_md.md)] oder mit dem Systemmonitor den Serververkehr überwachen und Statistiken erfassen. Anschließend können Sie die zusammengestellten Informationen zum Festlegen des Prozentwertes und der Dauer der CPU-Leerlaufzeit verwenden.  
  
Definieren Sie die CPU-Leerlaufbedingung als Prozentwert, unter den die CPU-Nutzung für eine bestimmte Dauer absinken muss. Legen Sie dann die Zeitdauer fest. Wenn die CPU-Nutzung für die angegebene Zeitdauer unter den angegebenen Prozentwert abfällt, startet der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent alle Aufträge mit CPU-Leerlaufzeitplänen. Weitere Informationen zur Verwendung von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler_md.md)] oder des Systemmonitors zur Überwachung der CPU-Nutzung finden Sie unter [Überwachen der CPU-Auslastung](http://msdn.microsoft.com/en-us/2a02a3b6-07b2-4ad0-8a24-670414d19812).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Beschreibung**|**Thema**|  
|Beschreibt, wie ein Zeitplan für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftrag erstellt wird.|[Create a Schedule](../../ssms/agent/create-a-schedule.md)|  
|Beschreibt, wie ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftrag geplant wird.|[Planen eines Auftrags](../../ssms/agent/schedule-a-job.md)|  
|Erläutert, wie die CPU-Leerlaufbedingung für den Server definiert wird.|[Festlegen der Leerlaufzeit und Leerlaufdauer der CPU &#40;SQL Server Management Studio&#41;](../../ssms/agent/set-cpu-idle-time-and-duration-sql-server-management-studio.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[sp_help_jobschedule](http://msdn.microsoft.com/en-us/2cded902-9272-4667-ac4b-a4f95a9f008e)  
[sysjobschedules](http://msdn.microsoft.com/en-us/ccdafec7-2a9b-4356-bffb-1caa3a12db59)  
  
