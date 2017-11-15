---
title: "Veröffentlichungsinformationen, Agents (Mergeveröffentlichung) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.publicationinfo.downlevelagents.merge.f1
ms.assetid: 73ff590a-20da-4f10-b592-c60b7226d22b
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30bce9036adcb03ad202fbb6568f3bf74cb014cf
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="publication-information-agents-merge-publication"></a>Veröffentlichungsinformationen, Agents (Mergeveröffentlichung)
  Auf der Registerkarte **Agents** werden Zusammenfassungsinformationen zum Momentaufnahme-Agent für die ausgewählte Veröffentlichung angezeigt.  
  
## <a name="options"></a>Optionen  
 Ausführliche Informationen und die Aufträge für den Momentaufnahme-Agent können Sie anzeigen, indem Sie mit der rechten Maustaste in die Zeile des jeweiligen Agents klicken und eine Option im Kontextmenü auswählen. Wenn Sie die Anzeige der Daten im Raster ändern möchten, klicken Sie mit der rechten Maustaste auf das Raster, und klicken Sie anschließend auf eine der folgenden Optionen:  
  
-   **Sortieren**: Sortieren Sie nach einer oder mehreren Spalten im Dialogfeld **Spalten sortieren** .  
  
-   **Anzuzeigende Spalten auswählen**: Wählen Sie die anzuzeigenden Spalten sowie die Reihenfolge aus, in der diese im Dialogfeld **Spalten auswählen** angezeigt werden sollen.  
  
-   **Filtern**: Filtern Sie Zeilen im Raster auf Grundlage der Spaltenwerte im Dialogfeld **Filtereinstellungen** .  
  
-   **Filter löschen**: Löschen Sie alle Filtereinstellungen für das Raster.  
  
 Filtereinstellungen sind rasterspezifisch. Die Spaltenauswahl und -sortierung wird auf alle Raster desselben Typs angewendet, z. B. das Veröffentlichungsraster für jeden Verleger.  
  
 **Status**  
 Der Status des Momentaufnahme-Agents. In der folgenden Liste sind die möglichen Statuswerte aufgeführt:  
  
-   Fehler  
  
-   Fehlgeschlagener Befehl wird wiederholt  
  
-   Wird nicht ausgeführt  
  
-   Abgeschlossen  
  
 **Agent**  
 Der Momentaufnahme-Agent. Das ist der einzige Agent, der einer Mergeveröffentlichung zugeordnet ist. Der Merge-Agent ist den Abonnements dieser Veröffentlichung zugeordnet. Weitere Information finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agents &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
 **Letzte Startzeit**  
 Zeitpunkt, zu dem der Agent zuletzt gestartet wurde.  
  
 **Dauer**  
 Zeitdauer, für die der Agent ausgeführt wurde. Dieser Wert gibt entweder die verstrichene Zeit eines zurzeit ausgeführten Agents oder die Gesamtzeit des zuvor ausgeführten Agents an.  
  
 **Letzte Aktion**  
 Die letzte Aktion, die bei der letzten Ausführung des Agents ausgeführt wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für die einer Veröffentlichung zugeordneten Agents &#40;Replikationsmonitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
