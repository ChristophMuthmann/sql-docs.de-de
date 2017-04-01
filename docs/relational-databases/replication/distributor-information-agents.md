---
title: "Verteilerinformationen, Agents | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.Distributor.commonjobs..f1"
ms.assetid: 5d601a64-6af0-42f9-81b1-cf0087f1c50d
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Verteilerinformationen, Agents
  Auf der Registerkarte **Agents** werden Informationen zu den Agents und Wartungsaufträgen angezeigt, die dem Verleger und dem Abonnenten zugeordnet sind:  
  
 Die Agents, die auf der Registerkarte **Agents** in der Verteileransicht für einen Verteiler verfügbar sind, umfassen alle Agents, die auf der Registerkarte **Agents** für einen Verleger verfügbar sind. Die Registerkarte **Agents** für einen Verteiler in der Verteileransicht enthält jedoch auch einen Verteiler-Agent und einen Merge-Agent.  
  
 Weitere Informationen zu Momentaufnahme-, Protokollleser- und Warteschlangenlese-Agents sowie Wartungsaufträgen finden Sie unter [Publisher Information, Agents](../../relational-databases/replication/publisher-information-agents.md). Beachten Sie, dass beim Anzeigen von Agent-Informationen für einen Verteiler auf der Registerkarte **Agents** Verlegerinformationen für den Momentaufnahme- und den Protokollleser-Agent vorhanden sind. Auf der Registerkarte **Agents** für einen Verteiler in der Verteileransicht können Sie auch jedoch **Verteiler-Agent** und **Merge-Agent**auswählen.  
  
## Optionen  
 In den folgenden Abschnitten werden die Daten beschrieben, die auf dieser Registerkarte für den Verteiler-Agent und den Merge-Agent angezeigt werden.  
  
### Verteiler-Agent  
 **Status**  
 Der Status des Agents. In der folgenden Liste sind die möglichen Statuswerte aufgeführt:  
  
-   Fehler  
  
-   Wiederholen  
  
-   Wird ausgeführt  
  
-   Wird nicht ausgeführt  
  
-   Nie gestartet  
  
 **Verleger**  
 Der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz des Verlegers.  
  
 **Veröffentlichung**  
 Der Name der Veröffentlichung, der der Agent zugeordnet ist.  
  
 **Abonnement**  
 Der Name des Abonnements, in der Form: [*SubscriberName*]. [*Datenbank*].  
  
 **Typ**  
 Der Typ der Replikation: push, pull oder anonymous.  
  
 **Letzte Startzeit**  
 Zeitpunkt, zu dem der Agent beim letzten Mal gestartet wurde.  
  
 **Dauer**  
 Die Zeitdauer, für die der Agent ausgeführt wurde. Dieser Wert gibt entweder die verstrichene Zeit eines zurzeit ausgeführten Agents oder die Gesamtzeit des zuvor ausgeführten Agents an.  
  
 **Letzte Aktion**  
 Die letzte Aktion, die bei der letzten Ausführung des Agents ausgeführt wurde.  
  
 **Übermittlungsrate**  
 Die Rate (in Befehlen pro Sekunde), mit der bei der letzten Ausführung des Agents für Initialisierungsbefehle ein Commit in der Verteilungsdatenbank ausgeführt wurde.  
  
 **Latenzzeit**  
 Die verstrichene Zeit in Sekunden zwischen dem Commit der letzten Änderung in der Veröffentlichungsdatenbank und dem Commit des zugehörigen Befehls in der Verteilungsdatenbank.  
  
 **#Trans**  
 Die Anzahl von Transaktionen, für die bei der letzten Ausführung des Agents ein Commit in der Verteilungsdatenbank ausgeführt wurde.  
  
 **#Befehle**  
 Die Anzahl von Befehlen, für die bei der letzten Ausführung des Agents ein Commit in der Verteilungsdatenbank ausgeführt wurde. Ein Befehl entspricht einer Datenänderung, z. B. einem Update.  
  
 **Durchschn. #Befehle**  
 Die durchschnittliche Anzahl von Befehlen pro Transaktion bei der letzten Ausführung des Agents.  
  
### Merge-Agent  
 **Status**  
 Der Status des Agents. In der folgenden Liste sind die möglichen Statuswerte aufgeführt:  
  
-   Fehler  
  
-   Wiederholen  
  
-   Wird ausgeführt  
  
-   Wird nicht ausgeführt  
  
-   Nie gestartet  
  
 **Verleger**  
 Der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz des Verlegers.  
  
 **Veröffentlichung**  
 Der Name der Veröffentlichung, der der Agent zugeordnet ist.  
  
 **Abonnement**  
 Der Name des Abonnements, in der Form: [*SubscriberName*]. [*Datenbank*].  
  
 **Typ**  
 Der Typ der Replikation: push, pull oder anonymous.  
  
 **Letzte Startzeit**  
 Zeitpunkt, zu dem der Agent beim letzten Mal gestartet wurde.  
  
 **Dauer**  
 Die Zeitdauer, für die der Agent ausgeführt wurde. Dieser Wert gibt entweder die verstrichene Zeit eines zurzeit ausgeführten Agents oder die Gesamtzeit des zuvor ausgeführten Agents an.  
  
 **Letzte Aktion**  
 Die letzte Aktion, die bei der letzten Ausführung des Agents ausgeführt wurde.  
  
 **Übermittlungsrate**  
 Die Rate (in Befehlen pro Sekunde), mit der für Änderungen ein Commit in der Verteilungsdatenbank ausgeführt wird.  
  
 **Verlegereinfügungen**  
 Die Anzahl der auf dem Verleger angewendeten INSERT-Befehle.  
  
 **Verlegerupdates**  
 Die Anzahl der auf dem Verleger angewendeten UPDATE-Befehle.  
  
 **Verlegerlöschungen**  
 Die Anzahl der auf dem Verleger angewendeten DELETE-Befehle.  
  
 **Verlegerkonflikte**  
 Die Anzahl der Konflikte beim Verleger, die im Rahmen des Mergevorgangs aufgetreten sind.  
  
 **Abonnenteneinfügungen**  
 Die Anzahl der auf dem Abonnenten angewendeten INSERT-Befehle.  
  
 **Abonnentenupdates**  
 Die Anzahl der auf dem Abonnenten angewendeten UPDATE-Befehle.  
  
 **Abonnentenlöschungen**  
 Die Anzahl der auf dem Abonnenten angewendeten DELETE-Befehle.  
  
 **Abonnentenkonflikte**  
 Die Anzahl der Konflikte beim Abonnenten, die im Rahmen des Mergevorgangs aufgetreten sind.  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung & #40 zugeordneten Agents; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  