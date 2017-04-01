---
title: "Anzeigen des Ver&#246;ffentlichungs- und Abonnementstatus im Replikationsmonitor | Microsoft Docs"
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
  - "Protokolllese-Agent, Überwachung"
  - "Merge-Agent, Überwachung"
  - "Warteschlangenlese-Agent, Überwachung"
  - "Veröffentlichungen [SQL Server-Replikation], Anzeigen von Informationen"
  - "Momentaufnahme-Agent, Überwachung"
  - "Verteilungs-Agent, Überwachung"
  - "Überwachen der Leistung [SQL Server-Replikation], Veröffentlichungsstatus"
  - "Überwachen der Leistung [SQL Server-Replikation], Abonnementstatus"
  - "Abonnements [SQL Server-Replikation], Anzeigen des Status"
  - "Replikationsmonitor, Veröffentlichungs- und Abonnementstatus"
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Anzeigen des Ver&#246;ffentlichungs- und Abonnementstatus im Replikationsmonitor
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] werden Statusinformationen für Veröffentlichungen und Abonnements angezeigt:  
  
-   Der Status einer Veröffentlichung wird durch den Status mit höchster Priorität der zugehörigen Abonnements bestimmt. Wenn beispielsweise ein Abonnement einer Veröffentlichung einen Fehler aufweist und bei einem anderen Abonnement ein leistungsbezogenes Problem vorliegt, wird für die Veröffentlichung ein Statusfehler gemeldet.  
  
-   Der Status eines Abonnements wird durch den Status der Agents bestimmt, die das Abonnement bedienen. Bei einer Mergereplikation handelt es sich hierbei um den Merge-Agent. Bei einer Transaktionsreplikation handelt es sich um den Protokolllese-Agent oder den Verteilungs-Agent (der Status mit höchster Priorität wird angezeigt; der Status kann auch durch den Warteschlangenlese-Agent ermittelt werden, wenn Abonnements mit verzögertem Update über eine Warteschlange verwendet werden). Bei einer Momentaufnahmereplikation handelt es sich hierbei um den Momentaufnahme-Agent oder den Verteilungs-Agent (der Status mit höchster Priorität wird angezeigt).  
  
 In den Tabellen in den nachfolgenden Abschnitten werden mögliche Statuswerte für Veröffentlichungen und Abonnements aufgeführt. Drei der Statuswerte werden nur angezeigt, wenn ein Schwellenwert erreicht oder überschritten wird.  
  
-   Läuft demnächst ab  
  
     Dieser Statuswert gilt für alle Arten der Replikation. Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Leistung ist kritisch  
  
     Dieser Statuswert gilt für die Transaktionsreplikation und die Mergereplikation. Weitere Informationen finden Sie unter [Überwachen der Leistung mit dem Replikationsmonitor](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
-   Langer Mergevorgang  
  
     Dieser Statuswert gilt für die Mergereplikation. Weitere Informationen finden Sie unter [Überwachen der Leistung mit dem Replikationsmonitor](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 Zusätzlich zum Veröffentlichungs- und Abonnementstatus stellt die Mergereplikation Statistiken auf Artikelebene bereit, wodurch Sie z. B. wesentlich ausführlichere Informationen zu folgenden wichtigen Fragen erhalten: Wie lange dauert es bis zum Abschluss einer Mergephase? Wie viel Zeit wurde für die Verarbeitung eines bestimmten Artikels aufgewendet? Welchen Verbindungstyp verwendet ein Abonnent? Die Statistiken werden im Replikationsmonitor im Fenster des Merge-Agents angezeigt. Bei der Momentaufnahme- und Transaktionsreplikation werden ausführliche Informationen zur Verteilungs-Agent-Verarbeitung bereitgestellt.  
  
 **So zeigen Sie den Veröffentlichungs- und Abonnementstatus an**  
  
-   Replikationsmonitor: [Informationen anzeigen und Ausführen von Aufgaben für eine Veröffentlichung & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md) und [Informationen anzeigen und Ausführen von Aufgaben für ein Abonnement & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
  
 **So zeigen Sie ausführliche Informationen zu Agents an:**  
  
-   Replikationsmonitor: [Informationen anzeigen und Ausführen von Aufgaben für eine Veröffentlichung & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md) und [Informationen anzeigen und Ausführen von Aufgaben für ein Abonnement & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Veröffentlichungsstatuswerte  
 In der nachfolgenden Tabelle werden Veröffentlichungsstatuswerte und ihre entsprechenden Symbole nach Priorität geordnet aufgeführt.  
  
|Status|Symbol|  
|------------|----------|  
|Fehler|![UI-Symbol: Fehler](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "UI-Symbol: Fehler")|  
|Leistung ist kritisch|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|fehlerhafter Befehl wird wiederholt|![UI-Symbol: Wiederholungsversuch des Replikations-Agents](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "UI-Symbol: Wiederholungsversuch des Replikations-Agents")|  
|OK|none|  
  
## Abonnementstatuswerte  
 In den nachfolgenden Tabellen werden Abonnementstatuswerte und ihre entsprechenden Symbole nach Priorität geordnet aufgeführt. Es ist möglich, dass ein Abonnement kann zwei Statusangaben gleichzeitig, z. B. **läuft demnächst ab/abgelaufen** und **fehlerhafter Befehl**; Prioritätsstatus mit der höchste wird angezeigt.  
  
 Die Statuswerte **Leistung ist kritisch**, **läuft demnächst ab/abgelaufen**, und **nicht initialisiert** Warnungen. Wenn eine Warnung eingeblendet wird, geht aus dem Replikationsmonitor ebenfalls hervor, ob derzeit ein Agent ausgeführt wird. Der Status kann also beispielsweise **Wird ausgeführt, Leistungskritisch**sein.  
  
### Transaktionsabonnements  
  
|Status|Symbol|  
|------------|----------|  
|Fehler|![UI-Symbol: Fehler](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "UI-Symbol: Fehler")|  
|Leistung ist kritisch|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|Läuft demnächst ab/Abgelaufen|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|Nicht initialisiertes Abonnement|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|fehlerhafter Befehl wird wiederholt|![UI-Symbol: Wiederholungsversuch des Replikations-Agents](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "UI-Symbol: Wiederholungsversuch des Replikations-Agents")|  
|Wird nicht ausgeführt|![UI-Symbol: Replikations-Agent wird beendet](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "UI-Symbol: Replikations-Agent wird beendet")|  
|Wird ausgeführt|![UI-Symbol: Replikations-Agent wird ausgeführt](../../../relational-databases/replication/monitor/media/repl-icon-running.png "UI-Symbol: Replikations-Agent wird ausgeführt")|  
  
### Mergeabonnements  
  
|Status|Symbol|  
|------------|----------|  
|Fehler|![UI-Symbol: Fehler](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "UI-Symbol: Fehler")|  
|Leistung ist kritisch|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|Langer Mergevorgang|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|Läuft demnächst ab/Abgelaufen|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|Nicht initialisiertes Abonnement|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|fehlerhafter Befehl wird wiederholt|![UI-Symbol: Wiederholungsversuch des Replikations-Agents](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "UI-Symbol: Wiederholungsversuch des Replikations-Agents")|  
|Wird synchronisiert|![UI-Symbol: Replikations-Agent wird ausgeführt](../../../relational-databases/replication/monitor/media/repl-icon-running.png "UI-Symbol: Replikations-Agent wird ausgeführt")|  
|Synchronisierung wird nicht ausgeführt|![UI-Symbol: Replikations-Agent wird beendet](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "UI-Symbol: Replikations-Agent wird beendet")|  
  
### Momentaufnahmeabonnements  
  
|Status|Symbol|  
|------------|----------|  
|Fehler|![UI-Symbol: Fehler](../../../database-engine/availability-groups/windows/media/repl-icon-error.png "UI-Symbol: Fehler")|  
|Läuft demnächst ab/Abgelaufen|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|Nicht initialisiertes Abonnement|![UI-Symbol: warning](../../../database-engine/availability-groups/windows/media/repl-icon-warn.png "UI-Symbol: warning")|  
|fehlerhafter Befehl wird wiederholt|![UI-Symbol: Wiederholungsversuch des Replikations-Agents](../../../relational-databases/replication/monitor/media/repl-icon-retry.png "UI-Symbol: Wiederholungsversuch des Replikations-Agents")|  
|Wird synchronisiert|![UI-Symbol: Replikations-Agent wird ausgeführt](../../../relational-databases/replication/monitor/media/repl-icon-running.png "UI-Symbol: Replikations-Agent wird ausgeführt")|  
|Synchronisierung wird nicht ausgeführt|![UI-Symbol: Replikations-Agent wird beendet](../../../relational-databases/replication/monitor/media/repl-icon-stopped.png "UI-Symbol: Replikations-Agent wird beendet")|  
  
## Siehe auch  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  