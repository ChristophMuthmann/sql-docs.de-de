---
title: "Momentaufnahme-Agent | Microsoft Docs"
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
  - "sql13.rep.monitor.snapshotagent.f1"
helpviewer_keywords: 
  - "Momentaufnahme-Agent (Dialogfeld)"
ms.assetid: b715e621-2cd5-4a15-8f58-a341aa8ef5e4
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Momentaufnahme-Agent
  Im Dialogfeld **Momentaufnahme-Agent** werden detaillierte Informationen zum Momentaufnahme-Agent, wie Status, Verlauf, Informationsmeldungen und alle Fehlermeldungen, angezeigt.  
  
## Optionen  
 Wählen Sie im Menü **Sicht** aus, welche Sitzungen des Momentaufnahme-Agents angezeigt werden, und wählen Sie dann eine bestimmte Sitzung aus dem Raster mit der Bezeichnung **Sitzungen des Momentaufnahme-Agents**aus. Detaillierte Informationen zu dieser Sitzung werden im Raster mit der Bezeichnung **Aktionen in der ausgewählten Sitzung**angezeigt. Wenn die ausgewählte Sitzung mit einem Fehler beendet wurde, wird auch der Textbereich mit der Bezeichnung **Fehlerdetails oder Meldung der ausgewählten Sitzung** angezeigt.  
  
 **Sicht**  
 Wählen Sie aus, welche Sitzungen des Momentaufnahme-Agents angezeigt werden.  
  
 **Status**  
 Der Status des Momentaufnahme-Agents. In der folgenden Liste sind die möglichen Statuswerte aufgeführt:  
  
-   Fehler  
  
-   Fehlgeschlagener Befehl wird wiederholt  
  
-   Wird nicht ausgeführt  
  
-   Abgeschlossen  
  
 **Startzeit**  
 Startzeit der Sitzung.  
  
 **Beendigungszeit**  
 Beendigungszeit der Sitzung. Wenn der Agent noch nicht beendet wurde, ist dieses Feld leer.  
  
 **Dauer**  
 Die Zeitspanne, für die der Momentaufnahme-Agent in dieser Sitzung ausgeführt wurde. Dieser Wert stellt die bisher abgelaufene Zeit dar, wenn der Agent immer noch ausgeführt wird, und die Gesamtzeit, wenn die Agentsitzung beendet ist.  
  
 **Fehlermeldung**  
 Wenn eine Sitzung mit einem Fehler beendet wurde, wird in diesem Feld die Fehlermeldung angezeigt, die vom Momentaufnahme-Agent protokolliert wurde. Wurde die Sitzung nicht mit einem Fehler beendet, ist dieses Feld leer.  
  
 **Aktionsmeldung**  
 Alle Informationsmeldungen und Fehlermeldungen, die der Momentaufnahme-Agent während der ausgewählten Sitzung protokolliert hat.  
  
 **Aktionszeit**  
 Die Uhrzeit, an dem die Aktion, in beschrieben, der **Aktionsnachricht** ausgeführt wurde.  
  
 **Fehlerdetails oder Meldung der ausgewählten Sitzung**  
 Wird nur angezeigt, wenn die ausgewählte Sitzung Wert zeigt **Fehler** in den **Status** Spalte. Dieser Textbereich zeigt detaillierte Fehlerinformationen sowie den Befehl an, der zum Zeitpunkt des Fehlers auszuführen versucht wurde. Er enthält außerdem Links zu weiteren Informationen, die sich auf den Fehler beziehen.  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung & #40 zugeordneten Agents; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  