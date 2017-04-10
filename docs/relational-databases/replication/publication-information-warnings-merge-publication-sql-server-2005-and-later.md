---
title: "Ver&#246;ffentlichungsinformationen, Warnungen (Mergever&#246;ffentlichung, SQL Server 2005 und h&#246;her) | Microsoft Docs"
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
  - "sql13.rep.monitor.publicationinfo.warningsandagents.merge.f1"
ms.assetid: 9bef3565-5f13-42ac-8723-ebe55b0c11e6
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# Ver&#246;ffentlichungsinformationen, Warnungen (Mergever&#246;ffentlichung, SQL Server 2005 und h&#246;her)
  Die Registerkarte **Warnungen** ist für Verteiler verfügbar, auf denen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höhere Versionen ausgeführt werden. Auf der Registerkarte **Warnungen** können Sie folgende Tasks für die ausgewählte Veröffentlichung ausführen:  
  
-   Aktivieren von Warnungen.  
  
-   Angeben von Schwellenwerten, die den Warnungen zugeordnet werden.  
  
-   Festlegen von Hinweisen, die den Warnungen zugeordnet werden.  
  
## Warnungen, Schwellenwerte und Warnhinweise  
 Standardmäßig werden vom Replikationsmonitor Warnungen zu nicht initialisierten Abonnements angezeigt: auf den Seiten mit den Abonnementinformationen wird in der Spalte **Status** - der Status **Nicht initialisiertes Abonnement** als Warnung angezeigt. Sie können angeben, ob durch folgende weitere Bedingungen bei Mergeveröffentlichungen eine Warnung ausgelöst wird:  
  
-   Bevorstehender Abonnementablauf.  
  
     Diese Bedingung entspricht der Option **Warnung, wenn ein Abonnement innerhalb des Schwellenwerts abläuft**. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird der Abonnementstatus als angezeigt **läuft demnächst ab/abgelaufen** (es sei denn, ein Problem mit einer höheren Priorität angezeigt werden muss).  
  
-   Die angegebene Synchronisierungszeit wird überschritten.  
  
     Diese Bedingung entspricht den Optionen **Warnung, wenn eine Zusammenführungslänge für DFÜ-Verbindungen den Schwellenwert überschreitet** und **Warnung, wenn eine Zusammenführungslänge für LAN-Verbindungen den Schwellenwert überschreitet**. Beide Schwellenwerte können festgelegt werden, aber nur ein Wert wird während einer Synchronisierung verwendet. Der Merge-Agent wendet auf der Grundlage des Verbindungstyps den entsprechenden Schwellenwert an.  
  
     Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird der Abonnementstatus als angezeigt **langer Mergevorgang** (es sei denn, ein Problem mit einer höheren Priorität angezeigt werden muss).  
  
-   Die angegebene Zahl von Zeilen konnte nicht innerhalb der festgelegten Zeit verarbeitet werden.  
  
     Diese Bedingung entspricht den Optionen **Warnung, wenn der Wert für zusammengeführte Zeilen pro Sekunde für DFÜ-Verbindungen kleiner als der Schwellenwert ist** und **Warnung, wenn eine Zusammenführungslänge für LAN-Verbindungen den Schwellenwert überschreitet**. Beide Schwellenwerte können festgelegt werden, aber nur ein Wert wird während einer Synchronisierung verwendet. Der Merge-Agent wendet auf der Grundlage des Verbindungstyps den entsprechenden Schwellenwert an.  
  
     Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird der Abonnementstatus als angezeigt **Leistung ist kritisch** (es sei denn, ein Problem mit einer höheren Priorität angezeigt werden muss).  
  
 Wenn Sie eine Warnung aktivieren, müssen Sie auch einen Schwellenwert festlegen. Wenn Sie z. B. die Warnung **Warnung, wenn eine Zusammenführungslänge für LAN-Verbindungen den Schwellenwert überschreitet**aktivieren, legen Sie die maximal zulässige Zeit für eine Mergesynchronisierung fest.  
  
 Neben der Warnung im Replikationsmonitor kann bei Erreichen eines Schwellenwerts auch ein Warnhinweis ausgelöst werden. Zum Definieren eines Warnhinweises klicken Sie auf **Warnungen konfigurieren** , und stellen Sie im Dialogfeld **Replikationswarnungen konfigurieren** die entsprechenden Informationen bereit.  
  
## Optionen  
 **Aktiviert**  
 Wählen Sie diese Option aus, um eine Warnung zu aktivieren und einen Schwellenwert anzugeben.  
  
 **Warnung**  
 Wählen Sie diese Option aus, um die Warnungseinstellung für eine angegebene Replikationswarnung zu aktivieren.  
  
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
 [Überwachen der Leistung mit dem Replikationsmonitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  