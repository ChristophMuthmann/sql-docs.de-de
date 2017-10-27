---
title: "Verwenden von Warnungen für Replikations-Agentereignisse | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing alerts
- Queue Reader Agent, alerts
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
- Log Reader Agent, alerts
- Distribution Agent, alerts
- Merge Agent, alerts
- agents [SQL Server replication], alerts
- displaying alerts
- Snapshot Agent, alerts
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 915d79db6a2c8f55443c92cb568bac8a9cc2c7d4
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="use-alerts-for-replication-agent-events"></a>Verwenden von Warnungen für Replikations-Agentereignisse
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] und der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent ermöglichen anhand von Warnungen das Überwachen von Ereignissen, wie Ereignissen des Replikations-Agents. Der[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent überwacht das Windows-Anwendungsprotokoll auf Ereignisse, die Warnungen zugeordnet sind. Bei Auftreten eines solchen Ereignisses antwortet der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent automatisch, indem er eine Aufgabe ausführt, die Sie definiert haben, und/oder eine E-Mail- oder Pager-Nachricht an den angegebenen Operator sendet. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enthält einen Satz vordefinierter Warnungen für Replikations-Agents ein, die Sie konfigurieren können, um eine Task auszuführen und/oder einen Operator zu benachrichtigen. Weitere Informationen zum Definieren eines auszuführenden Tasks finden Sie im Abschnitt zum Automatisieren einer Antwort auf eine Warnung in diesem Thema.  
  
 Die folgenden Warnungen werden installiert, wenn ein Computer als Verteiler konfiguriert wird:  
  
|Meldungs-ID|Vordefinierte Warnung|Bedingung, die die Warnung auslöst|Zusätzlich eingegebene Informationen in msdb..sysreplicationalerts|  
|----------------|----------------------|-----------------------------------------|-----------------------------------------------------------------|  
|14150|**Replikation: Der Agent war erfolgreich.**|Agent wird erfolgreich heruntergefahren.|ja|  
|14151|**Replikation: Fehler beim Agent.**|Agent wird mit einem Fehler heruntergefahren.|ja|  
|14152|**Replikation: Wiederholung des Agents.**|Der Agent wird nach dem erfolglosen erneuten Versuch einer Operation beendet (der Agent stellt einen Fehler fest, wie z. B. einen nicht verfügbaren Server, einen Deadlock, einen Verbindungsfehler oder einen Timeoutfehler).|ja|  
|14157|**Replikation: Abgelaufenes Abonnement wurde gelöscht.**|Ein abgelaufenes Abonnement wurde gelöscht.|Nein|  
|20572|**Replikation: Das Abonnement wurde nach einem Überprüfungsfehler neu initialisiert.**|Antwortauftrag 'Abonnements bei Datenüberprüfungsfehler erneut initialisieren' initialisiert ein Abonnement erfolgreich erneut.|Nein|  
|20574|**Replikation: Fehler bei der Datenüberprüfung auf dem Abonnenten.**|Datenüberprüfung durch Verteilungs- oder Merge-Agent fehlgeschlagen.|ja|  
|20575|**Replikation: Der Abonnent hat die Datenüberprüfung erfolgreich durchlaufen.**|Verteilungs- oder Merge-Agent durchläuft eine Datenüberprüfung.|ja|  
|20578|**Replikation: Der Agent wurde benutzerdefiniert heruntergefahren.**|||  
|22815|**Peer-zu-Peer-Konflikterkennungswarnung**|Der Verteilungs-Agent hat bei dem Versuch, eine Änderung an einem Peer-zu-Peer-Knoten vorzunehmen, einen Konflikt erkannt.|ja|  
  
 Zusätzlich zu diesen Warnungen bietet der Replikationsmonitor eine Reihe von status- und leistungsbezogenen Warnungen. Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). Mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Infrastruktur für Warnungen können Sie außerdem auch Warnungen für andere Replikationsereignisse definieren. Weitere Informationen finden Sie unter [Erstellen eines benutzerdefinierten Ereignisses](http://msdn.microsoft.com/library/03d71a35-97fa-4bba-aa9a-23ac9c9cf879).  
  
 **So konfigurieren Sie vordefinierte Replikationswarnungen**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Konfigurieren von vordefinierten Replikationswarnungen &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## <a name="viewing-the-application-log-directly"></a>Direktes Anzeigen des Anwendungsprotokolls  
 Verwenden Sie zum Anzeigen des Anwendungsprotokolls von Windows die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Ereignisanzeige. Das Anwendungsprotokoll enthält sowohl [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Fehlermeldungen als auch Meldungen zu vielen anderen Aktivitäten auf dem Computer. Im Gegensatz zum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Fehlerprotokoll wird beim Neustart von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht jedes Mal ein neues Anwendungsprotokoll erstellt (in jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Sitzung werden neue Ereignisse in ein vorhandenes Anwendungsprotokoll geschrieben). Sie können allerdings angeben, wie lange die protokollierten Ereignisse beibehalten werden. Wenn Sie das Windows-Anwendungsprotokoll anzeigen, können Sie das Protokoll nach bestimmten Ereignissen filtern. Weitere Informationen finden Sie in der Windows-Dokumentation.  
  
## <a name="automating-a-response-to-an-alert"></a>Automatisieren einer Antwort auf eine Warnung  
 Die Replikation stellt einen Antwortauftrag für Abonnements bereit, deren Überprüfung fehlgeschlagen ist, und bietet außerdem ein Framework zum Erstellen weiterer automatischer Antworten auf Warnungen. Der Antwortauftrag lautet **Abonnements bei Datenüberprüfungsfehler erneut initialisieren** und ist in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] im Ordner **Aufträge** des [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]-Agents gespeichert. Weitere Informationen zum Aktivieren dieses Antwortauftrags finden Sie unter [Konfigurieren von vordefinierten Replikationswarnungen &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md). Wenn die Überprüfung bei Artikeln in einer Transaktionsveröffentlichung einen Fehler erzeugt, werden nur die fehlerhaften Artikel vom Antwortauftrag erneut initialisiert. Schlägt die Überprüfung in einer Mergeveröffentlichung fehl, werden alle Artikel vom Antwortauftrag erneut initialisiert.  
  
### <a name="framework-for-automating-responses"></a>Framework für automatische Antworten  
 Wenn eine Warnung auftritt, sind in der Regel die einzigen Informationen, mit deren Hilfe Sie verstehen können, was die Warnung auslöste und welche entsprechende Maßnahme ergriffen werden sollte, in der Warnmeldung enthalten. Eine Analyse dieser Informationen kann sich als fehleranfällig und zeitraubend erweisen. Die Replikation vereinfacht automatische Antworten, da in der **sysreplicationalerts** -Systemtabelle zusätzliche Informationen zur Warnung bereitgestellt werden. Diese Informationen sind bereits so analysiert, dass sie einfach in benutzerdefinierten Programmen verwendet werden können.  
  
 Wenn z. B. die Daten in der **Sales.SalesOrderHeader** -Tabelle auf dem Abonnenten A die Gültigkeitsüberprüfung nicht bestehen, löst [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Warnmeldung 20574 aus, in der Sie über dieses Fehlschlagen benachrichtigt werden. Sie empfangen die folgende Meldung: "Fehler bei der Datenüberprüfung für das Abonnement des Abonnenten 'A', für den 'SalesOrderHeader'-Artikel in der in der 'MyPublication'-Veröffentlichung."  
  
 Wenn Sie eine Antwort basierend auf dieser Meldung erstellen, müssen Sie den Namen des Abonnenten, den Artikelnamen, den Veröffentlichungsnamen und den Fehler aus der Meldung manuell analysieren. Da der Verteilungs-Agent und der Merge-Agent aber die gleichen Informationen in **sysreplicationalerts** schreiben, zusammen mit Details wie Agenttyp, Zeitpunkt der Warnung, Veröffentlichungsdatenbank und Veröffentlichungstyp, kann der Antwortauftrag die relevanten Informationen direkt aus der Tabelle abfragen. Obwohl die genaue Zeile nicht einer spezifischen Warnungsinstanz zugeordnet werden kann, kann die **status** -Spalte in der Tabelle zum Nachverfolgen der Diensteinträge verwendet werden. Die Einträge in dieser Tabelle werden während der Beibehaltungsdauer für den Verlauf beibehalten.  
  
 Wenn Sie z. B. einen Antwortauftrag in [!INCLUDE[tsql](../../../includes/tsql-md.md)] -SQL erstellen sollen, der Warnmeldung 20574 behandelt, können Sie die folgende Logik verwenden:  
  
```  
declare @publisher sysname, @publisher_db sysname, @publication sysname, @publication_type int, @article sysname, @subscriber sysname, @subscriber_db sysname, @alert_id int  
declare hc cursor local for select publisher, publisher_db, publication, publication_type, article, subscriber,   
  subscriber_db, alert_id from   
  msdb..sysreplicationalerts where  
  alert_error_code = 20574 and status = 0  
  for read only  
open hc  
fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
while (@@fetch_status <> -1)  
begin  
/* Do custom work  */  
/* Update status to 1, which means the alert has been serviced. This prevents subsequent runs of this job from doing this again */  
update msdb..sysreplicationalerts set status = 1 where alert_id = @alert_id  
 fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
end  
close hc  
deallocate hc  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Überwachen &#40;Replikation&#41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  

