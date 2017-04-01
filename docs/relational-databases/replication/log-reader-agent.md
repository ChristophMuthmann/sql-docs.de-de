---
title: "Protokolllese-Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.logreaderagent.f1"
helpviewer_keywords: 
  - "Protokolllese-Agent (Dialogfeld)"
ms.assetid: 300a3c46-0e48-4334-99c0-9ee690d2ef4f
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Protokolllese-Agent
  Im Dialogfeld **Protokolllese-Agent** werden detaillierte Informationen zum Protokolllese-Agent wie Status, Verlauf, Informationsmeldungen und alle Fehlermeldungen angezeigt.  
  
## Optionen  
 Wählen Sie im Menü **Sicht** aus, welche Sitzungen des Protokolllese-Agents angezeigt werden, und wählen Sie dann eine bestimmte Sitzung aus dem Raster mit der Bezeichnung **Sitzungen des Protokolllese-Agents**aus. Detaillierte Informationen zu dieser Sitzung werden im Raster mit der Bezeichnung **Aktionen in der ausgewählten Sitzung**angezeigt. Wenn die ausgewählte Sitzung mit einem Fehler beendet wurde, wird auch der Textbereich mit der Bezeichnung **Fehlerdetails oder Meldung der ausgewählten Sitzung** angezeigt.  
  
 **Sicht**  
 Wählen Sie aus, welche Sitzungen des Protokolllese-Agents angezeigt werden. Da der Protokolllese-Agent in der Regel kontinuierlich ausgeführt wird, kann möglicherweise nur eine Sitzung angezeigt werden.  
  
 **Status**  
 Status des Protokolllese-Agents. In der folgenden Liste sind die möglichen Statuswerte aufgeführt:  
  
-   Fehler  
  
-   Fehlgeschlagener Befehl wird wiederholt  
  
-   Wird nicht ausgeführt  
  
-   Wird ausgeführt  
  
 **Startzeit**  
 Startzeit der Sitzung.  
  
 **Beendigungszeit**  
 Beendigungszeit der Sitzung. Wenn der Agent noch nicht beendet wurde, ist dieses Feld leer.  
  
 **Dauer**  
 Zeitspanne, für die der Protokolllese-Agent in dieser Sitzung ausgeführt wurde. Dieser Wert stellt die bisher abgelaufene Zeit dar, wenn der Agent immer noch ausgeführt wird, und die Gesamtzeit, wenn die Agentsitzung beendet ist.  
  
 **Fehlermeldung**  
 Wenn eine Sitzung mit einem Fehler beendet wurde, wird in diesem Feld die Fehlermeldung angezeigt, die vom Protokolllese-Agent protokolliert wurde. Wurde die Sitzung nicht mit einem Fehler beendet, ist dieses Feld leer.  
  
 **Aktionsmeldung**  
 Alle Informationsmeldungen und Fehlermeldungen, die der Protokolllese-Agent während der ausgewählten Sitzung protokolliert hat.  
  
 **Aktionszeit**  
 Die Uhrzeit, an dem die Aktion, in beschrieben, der **Aktionsnachricht** ausgeführt wurde.  
  
 **Fehlerdetails oder Meldung der ausgewählten Sitzung**  
 Nur angezeigt, wenn die ausgewählte Sitzung Wert zeigt **Fehler** in den **Status** Spalte. Dieser Textbereich zeigt detaillierte Fehlerinformationen sowie den Befehl an, der zum Zeitpunkt des Fehlers auszuführen versucht wurde. Er enthält außerdem Links zu weiteren Informationen, die sich auf den Fehler beziehen.  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung & #40 zugeordneten Agents; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  