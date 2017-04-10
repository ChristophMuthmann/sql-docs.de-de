---
title: "Ver&#246;ffentlichungsinformationen, Warnungen (Momentaufnahmever&#246;ffentlichung, SQL Server 2005 und h&#246;her) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.warningsandagents.snapshot.f1"
ms.assetid: 7aa2eb52-b6b7-4dd3-8483-8ef00d9f0435
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Ver&#246;ffentlichungsinformationen, Warnungen (Momentaufnahmever&#246;ffentlichung, SQL Server 2005 und h&#246;her)
  Die Registerkarte **Warnungen** ist für Verteiler verfügbar, auf denen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höhere Versionen ausgeführt werden. Auf der Registerkarte **Warnungen** können Sie folgende Tasks für die ausgewählte Veröffentlichung ausführen:  
  
-   Aktivieren von Warnungen.  
  
-   Angeben von Schwellenwerten, die den Warnungen zugeordnet werden.  
  
-   Festlegen von Hinweisen, die den Warnungen zugeordnet werden.  
  
## Warnungen, Schwellenwerte und Warnhinweise  
 Standardmäßig werden vom Replikationsmonitor Warnungen zu nicht initialisierten Abonnements angezeigt: auf den Seiten mit den Abonnementinformationen wird in der Spalte **Status** - der Status **Nicht initialisiertes Abonnement** als Warnung angezeigt. Für Momentaufnahmeveröffentlichungen können Sie auch angeben, dass ein bevorstehender Abonnementablauf zu einer Warnung führt. Legen Sie hierzu die Option **Warnung, wenn ein Abonnement innerhalb des Schwellenwerts abläuft**fest. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird der Abonnementstatus als angezeigt **läuft demnächst ab/abgelaufen** (es sei denn, ein Problem mit einer höheren Priorität angezeigt werden muss).  
  
 Neben der Warnung im Replikationsmonitor kann bei Erreichen eines Schwellenwerts auch ein Warnhinweis ausgelöst werden. Zum Definieren eines Warnhinweises klicken Sie auf **Warnungen konfigurieren** , und stellen Sie im Dialogfeld **Replikationswarnungen konfigurieren** die entsprechenden Informationen bereit.  
  
## Optionen  
 **Aktiviert**  
 Wählen Sie diese Option aus, um eine Warnung zu aktivieren und einen Schwellenwert anzugeben.  
  
 **Warnung**  
 Eine Beschreibung der Warnung, die einem Schwellenwert zugeordnet ist.  
  
 **Schwellenwert**  
 Geben Sie einen Wert für den Schwellenwert an.  
  
 **Warnungen konfigurieren**  
 Wählen Sie eine Zeile in der **Warnungen** Raster aus, und klicken Sie auf **Warnungen konfigurieren** zum Starten der **Replikationswarnungen konfigurieren** Dialogfeld. In dem Dialogfeld können Sie einen Warnhinweis definieren, der dem ausgewählten Schwellenwert und der Warnung zugeordnet wird.  
  
 **Änderungen verwerfen**  
 Klicken Sie hier, um die Änderungen an Warnungen und Schwellenwerten zu verwerfen.  
  
> [!NOTE]  
>  Auf **Änderungen verwerfen** wirkt sich nicht auf die Warnungen, die gemäß den **Replikationswarnungen konfigurieren** Dialogfeld.  
  
 **Änderungen speichern**  
 Klicken Sie hier, um die Änderungen an Warnungen und Schwellenwerten zu speichern.  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  