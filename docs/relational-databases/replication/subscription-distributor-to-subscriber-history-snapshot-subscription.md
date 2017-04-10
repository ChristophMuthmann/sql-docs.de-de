---
title: "Abonnement, Verlauf Verteiler zu Abonnent (Momentaufnahmeabonnement) | Microsoft Docs"
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
  - "sql13.rep.monitor.subscription.pubtodist.snapshot.f1"
ms.assetid: d3575964-f287-4bcf-8d2e-f81a33141b25
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Abonnement, Verlauf Verteiler zu Abonnent (Momentaufnahmeabonnement)
  Die Registerkarte **Verlauf Verteiler zu Abonnent** zeigt detaillierte Informationen zum Verteilungs-Agent an, u. a. Status, Verlauf, Informationsmeldungen und alle Fehlermeldungen.  
  
## Optionen  
 Wählen Sie im Menü **Sicht** aus, welche Sitzungen des Verteilungs-Agents angezeigt werden, und wählen Sie dann eine bestimmte Sitzung aus dem Raster mit der Bezeichnung **Sitzungen des Verteilungs-Agents**aus. Detaillierte Informationen zu dieser Sitzung werden im Raster mit der Bezeichnung **Aktionen in der ausgewählten Sitzung**angezeigt. Wenn die ausgewählte Sitzung mit einem Fehler beendet wurde, wird auch der Textbereich mit der Bezeichnung **Fehlerdetails oder Meldung der ausgewählten Sitzung** angezeigt.  
  
 **Sicht**  
 Wählen Sie aus, welche Sitzungen des Verteilungs-Agents angezeigt werden.  
  
 **Status**  
 Der Status des Verteilungs-Agents. In der folgenden Liste sind die möglichen Statuswerte aufgeführt:  
  
-   Fehler  
  
-   Abgeschlossen  
  
-   Wird wiederholt  
  
-   Wird ausgeführt  
  
 **Startzeit**  
 Startzeit der Sitzung.  
  
 **Beendigungszeit**  
 Beendigungszeit der Sitzung. Wenn der Agent noch nicht beendet wurde, ist dieses Feld leer.  
  
 **Dauer**  
 Zeitspanne, für die der Verteilungs-Agent in dieser Sitzung ausgeführt wurde. Die Zeit stellt die bisher abgelaufene Zeit dar, wenn der Agent immer noch ausgeführt wird, und die Gesamtzeit, wenn die Agentsitzung beendet ist.  
  
 **Fehlermeldung**  
 Wenn eine Sitzung mit einem Fehler beendet wurde, wird in diesem Feld die Fehlermeldung angezeigt, die vom Verteilungs-Agent protokolliert wurde. Wurde die Sitzung nicht mit einem Fehler beendet, ist dieses Feld leer.  
  
 **Aktionsmeldung**  
 Alle Informationsmeldungen und Fehlermeldungen, die der Verteilungs-Agent während der ausgewählten Sitzung protokolliert hat.  
  
 **Aktionszeit**  
 Die Uhrzeit, an dem die Aktion, in beschrieben, der **Aktionsnachricht** ausgeführt wurde.  
  
 **Fehlerdetails oder Meldung der ausgewählten Sitzung**  
 Nur angezeigt, wenn die ausgewählte Sitzung Wert zeigt **Fehler** in den **Status** Spalte. Dieser Textbereich zeigt detaillierte Fehlerinformationen sowie den Befehl an, der zum Zeitpunkt des Fehlers auszuführen versucht wurde. Er enthält außerdem Links zu weiteren Informationen, die sich auf den Fehler beziehen.  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40 zugeordneten Agents; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  