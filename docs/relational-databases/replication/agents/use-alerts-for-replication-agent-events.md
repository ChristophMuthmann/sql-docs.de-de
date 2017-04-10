---
title: "Verwenden von Warnungen f&#252;r Replikations-Agentereignisse | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anzeige von Warnungen"
  - "Warteschlangenlese-Agent, Warnungen"
  - "Warnungen [SQL Server-Replikation]"
  - "Vordefinierte Replikationswarnungen [SQL Server-Replikation]"
  - "Protokolllese-Agent, Warnungen"
  - "Verteilungs-Agent, Warnungen"
  - "Merge-Agent, Warnungen"
  - "Agents [SQL Server-Replikation], Warnungen"
  - "Anzeigen von Warnungen"
  - "Momentaufnahme-Agent, Warnungen"
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Verwenden von Warnungen f&#252;r Replikations-Agentereignisse
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] und der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent ermöglichen anhand von Warnungen das Überwachen von Ereignissen, wie Ereignissen des Replikations-Agents. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent überwacht das Windows-Anwendungsprotokoll auf Ereignisse, die Warnungen zugeordnet sind. Bei Auftreten eines solchen Ereignisses antwortet der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Agent automatisch, indem er eine Aufgabe ausführt, die Sie definiert haben, und/oder eine E-Mail- oder Pager-Nachricht an den angegebenen Operator sendet. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enthält einen Satz vordefinierter Warnungen für Replikations-Agents, die Sie zum Ausführen eines Tasks und/oder Benachrichtigung eines Operators konfigurieren können. Weitere Informationen zum Definieren eines auszuführenden Tasks finden Sie im Abschnitt zum Automatisieren einer Antwort auf eine Warnung in diesem Thema.  
  
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
|22815|**Peer-zu-Peer-Konflikterkennungswarnung**|Der Verteilungs-Agent hat bei dem Versuch, eine Änderung an einem Peer-zu-Peer-Knoten vorzunehmen, einen Konflikt erkannt.|Ja|  
  
 Zusätzlich zu diesen Warnungen bietet der Replikationsmonitor eine Reihe von status- und leistungsbezogenen Warnungen. Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). Mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Infrastruktur für Warnungen können Sie außerdem auch Warnungen für andere Replikationsereignisse definieren. Weitere Informationen finden Sie unter [Erstellen eines benutzerdefinierten Ereignisses](../../../ssms/agent/create-a-user-defined-event.md).  
  
 **So konfigurieren Sie vordefinierte Replikationswarnungen**  
  
-   [! INCLUDE [SsManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [Configure Predefined Replication Alerts &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## Direktes Anzeigen des Anwendungsprotokolls  
 Verwenden Sie zum Anzeigen des Anwendungsprotokolls von Windows die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Ereignisanzeige. Das Anwendungsprotokoll enthält sowohl [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Fehlermeldungen als auch Meldungen zu vielen anderen Aktivitäten auf dem Computer. Im Gegensatz zum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Fehlerprotokoll wird beim Neustart von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht jedes Mal ein neues Anwendungsprotokoll erstellt (in jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sitzung werden neue Ereignisse in ein vorhandenes Anwendungsprotokoll geschrieben). Sie können allerdings angeben, wie lange die protokollierten Ereignisse beibehalten werden. Wenn Sie das Windows-Anwendungsprotokoll anzeigen, können Sie das Protokoll nach bestimmten Ereignissen filtern. Weitere Informationen finden Sie in der Windows-Dokumentation.  
  
## Automatisieren einer Antwort auf eine Warnung  
 Die Replikation stellt einen Antwortauftrag für Abonnements bereit, deren Überprüfung fehlgeschlagen ist, und bietet außerdem ein Framework zum Erstellen weiterer automatischer Antworten auf Warnungen. Der Antwortauftrag lautet **Abonnements bei Datenüberprüfungsfehler erneut initialisieren** und ist in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] im Ordner **Aufträge** des [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]-Agents gespeichert. Informationen zum Aktivieren dieses antwortauftrags finden Sie unter [vordefinierte Replikationswarnungen konfigurieren & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md). Wenn die Überprüfung bei Artikeln in einer Transaktionsveröffentlichung einen Fehler erzeugt, werden nur die fehlerhaften Artikel vom Antwortauftrag erneut initialisiert. Schlägt die Überprüfung in einer Mergeveröffentlichung fehl, werden alle Artikel vom Antwortauftrag erneut initialisiert.  
  
### Framework für automatische Antworten  
 Wenn eine Warnung auftritt, sind in der Regel die einzigen Informationen, mit deren Hilfe Sie verstehen können, was die Warnung auslöste und welche entsprechende Maßnahme ergriffen werden sollte, in der Warnmeldung enthalten. Eine Analyse dieser Informationen kann sich als fehleranfällig und zeitraubend erweisen. Die Replikation vereinfacht automatische Antworten, da in der **sysreplicationalerts** -Systemtabelle zusätzliche Informationen zur Warnung bereitgestellt werden. Diese Informationen sind bereits so analysiert, dass sie einfach in benutzerdefinierten Programmen verwendet werden können.  
  
 Wenn z. B. die Daten in der **Sales.SalesOrderHeader** -Tabelle auf dem Abonnenten A die Gültigkeitsüberprüfung nicht bestehen, löst [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Warnmeldung 20574 aus, in der Sie über dieses Fehlschlagen benachrichtigt werden. Sie empfangen die folgende Meldung: "Fehler bei der Datenüberprüfung für das Abonnement des Abonnenten 'A', für den 'SalesOrderHeader'-Artikel in der in der 'MyPublication'-Veröffentlichung."  
  
 Wenn Sie eine Antwort basierend auf dieser Meldung erstellen, müssen Sie den Namen des Abonnenten, den Artikelnamen, den Veröffentlichungsnamen und den Fehler aus der Meldung manuell analysieren. Aber da die Snapshot-Agent und der Merge-Agent die gleiche Informationen in schreiben **Sysreplicationalerts** (zusammen mit Details wie Agenttyp, Zeitpunkt der Warnung, Veröffentlichungsdatenbank, Abonnentendatenbank und Typ der Veröffentlichung) kann der Antwortauftrag die relevante Informationen aus der Tabelle direkt Abfragen. Obwohl die genaue Zeile nicht einer spezifischen Warnungsinstanz zugeordnet werden kann, kann die **status** -Spalte in der Tabelle zum Nachverfolgen der Diensteinträge verwendet werden. Die Einträge in dieser Tabelle werden während der Beibehaltungsdauer für den Verlauf beibehalten.  
  
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
  
## Siehe auch  
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Bewährte Methoden für die Replikationsverwaltung](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Überwachung & #40; Replikation & #41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  