---
title: "Ver&#246;ffentlichungsinformationen, Alle Abonnements (Momentaufnahmever&#246;ffentlichung) | Microsoft Docs"
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
  - "sql13.rep.monitor.publicationinfo.allsubscriptions.snapshot.f1"
ms.assetid: 7ce656c2-6e60-4625-8955-1daff641070c
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Ver&#246;ffentlichungsinformationen, Alle Abonnements (Momentaufnahmever&#246;ffentlichung)
  Auf der Registerkarte **Alle Abonnements** werden Informationen zu allen Abonnements der ausgewählten Momentaufnahmeveröffentlichung angezeigt.  
  
## Optionen  
 Ausführliche Informationen und eine Liste der Aufträge für ein Abonnement können Sie anzeigen, indem Sie mit der rechten Maustaste in die Zeile des jeweiligen Abonnements klicken und eine Option im Kontextmenü auswählen. Wenn Sie die Anzeige der Daten im Raster ändern möchten, klicken Sie mit der rechten Maustaste auf das Raster, und klicken Sie anschließend auf eine der folgenden Optionen:  
  
-   **Sortieren**: Sortieren Sie nach einer oder mehreren Spalten im Dialogfeld **Spalten sortieren** .  
  
-   **Anzuzeigende Spalten auswählen**: Wählen Sie die anzuzeigenden Spalten sowie die Reihenfolge aus, in der diese im Dialogfeld **Spalten auswählen** angezeigt werden sollen.  
  
-   **Filtern**: Filtern Sie Zeilen im Raster auf Grundlage der Spaltenwerte im Dialogfeld **Filtereinstellungen** .  
  
-   **Filter löschen**: Löschen Sie alle Filtereinstellungen für das Raster.  
  
 Filtereinstellungen sind rasterspezifisch. Die Spaltenauswahl und -sortierung wird auf alle Raster desselben Typs angewendet, z. B. das Veröffentlichungsraster für jeden Verleger.  
  
 **Anzeigen**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Wählen Sie die Abonnementstatus aus, die für Abonnements des ausgewählten Typs angezeigt werden sollen. Sie können z. B. auswählen, dass nur die Abonnements angezeigt werden, die einen Fehler aufweisen.  
  
 **Status**  
 Der Status jedes Abonnements, der vom Status des Momentaufnahme-Agents oder des Verteilungs-Agents bestimmt wird (der Status mit der höheren Priorität wird angezeigt).  
  
 Standardmäßig wird das Raster mit den Abonnementinformationen nach der **Status** -Spalte sortiert. In der folgenden Liste werden die möglichen Statuswerte und ihre Sortierreihenfolge aufgeführt (Fehler werden z. B. immer oben im Raster angezeigt).  
  
-   Fehler  
  
-   Läuft demnächst ab/Abgelaufen (nur in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen)  
  
-   Nicht initialisiertes Abonnement (nur in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen)  
  
-   fehlerhafter Befehl wird wiederholt  
  
-   Wird synchronisiert  
  
-   Synchronisierung wird nicht ausgeführt  
  
 Die Sortierreihenfolge bestimmt auch, welcher Wert angezeigt wird, wenn ein Abonnement mehr als einen Statuswert aufweist. Wenn ein Abonnement z. B. einen Fehler aufweist und bald abläuft, dann wird in der **Status** -Spalte der Eintrag **Fehler**angezeigt.  
  
 Die Statuswerte **läuft demnächst ab/abgelaufen** und **nicht initialisiertes Abonnement** Warnungen. Wenn eine Warnung angezeigt wird, wird unter **Status** auch angezeigt, ob ein Agent ausgeführt wird. Beispielsweise ist möglicherweise der Status **ausgeführt wird, läuft demnächst ab/abgelaufen**.  
  
 Der Statuswert **läuft demnächst ab/abgelaufen** wird nur angezeigt, wenn ein Schwellenwert festgelegt wird. Weitere Informationen zum Festlegen von Schwellenwerten, finden Sie unter [Legen Sie Schwellenwerte und Warnungen im Replikationsmonitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Abonnement**  
 Der Name des jeweiligen Abonnements in der Form: *SubscriberName: SubscriptionDatabaseName*.  
  
 **Letzte Synchronisierung**  
 Der Zeitpunkt der letzten Ausführung des Verteilungs-Agents. Wenn eine Synchronisierung ausgeführt wird, wird **Vorgang wird ausgeführt** angezeigt.  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40 zugeordneten Agents; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  