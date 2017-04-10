---
title: "Ver&#246;ffentlichungsinformationen: Alle Abonnements (Transaktionsver&#246;ffentlichung) | Microsoft Docs"
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
  - "sql13.rep.monitor.publicationinfo.allsubscriptions.tran.f1"
ms.assetid: 7073350c-f667-4f70-88e9-152c9a1b08dd
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Ver&#246;ffentlichungsinformationen: Alle Abonnements (Transaktionsver&#246;ffentlichung)
  Auf der Registerkarte **Alle Abonnements** werden Informationen zu allen Abonnements der ausgewählten Transaktionsveröffentlichung angezeigt.  
  
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
 Der Status des jeweiligen Abonnements, der vom Status des Verteilungs-Agents bzw. Protokolllese-Agents bestimmt wird. (Es wird der Status mit der höheren Priorität angezeigt. Der Status kann auch durch den Warteschlangenlese-Agent bestimmt werden, wenn Abonnements mit verzögertem Update über eine Warteschlange verwendet werden.)  
  
 Standardmäßig wird das Raster mit den Abonnementinformationen nach sortiert die **Status** Spalte (und dann nach der **Leistung** bei Abonnements mit dem gleichen Status). In der folgenden Liste werden die möglichen Statuswerte und ihre Sortierreihenfolge aufgeführt (Fehler werden z. B. immer oben im Raster angezeigt).  
  
-   Fehler  
  
-   Leistung ist kritisch (nur in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen)  
  
-   Läuft demnächst ab/Abgelaufen (nur in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen)  
  
-   Nicht initialisiertes Abonnement (nur in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen)  
  
-   fehlerhafter Befehl wird wiederholt  
  
-   Wird nicht ausgeführt  
  
-   Wird ausgeführt  
  
 Die Sortierreihenfolge bestimmt auch, welcher Wert angezeigt wird, wenn ein Abonnement mehr als einen Statuswert aufweist. Wenn ein Abonnement z. B. einen Fehler aufweist und bald abläuft, dann wird in der **Status** -Spalte der Eintrag **Fehler**angezeigt.  
  
 Die Statuswerte **Leistung ist kritisch**, **läuft demnächst ab/abgelaufen**, und **nicht initialisiertes Abonnement** Warnungen. Wenn eine Warnung angezeigt wird, wird unter **Status** auch angezeigt, ob ein Agent ausgeführt wird. Der Status kann also beispielsweise **Wird ausgeführt, Leistungskritisch**sein.  
  
 Die Statuswerte **Leistung ist kritisch** und **läuft demnächst ab/abgelaufen** werden nur angezeigt, wenn Schwellenwerte festgelegt sind. Informationen zu leistungsmessungen und Festlegen von Schwellenwerten finden Sie unter [Überwachen der Leistung mit dem Replikationsmonitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) und [Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Abonnement**  
 Der Name des jeweiligen Abonnements in der Form: *SubscriberName: SubscriptionDatabaseName*.  
  
 **Leistung**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Die Leistungsbewertung für jedes Abonnement basiert auf den neuesten Messungen, die vom Replikationsmonitor vorgenommen wurden, und reflektiert keinen Leistungsverlauf. Die Leistung wird für Abonnements von Veröffentlichungen gemessen, für die Leistungsschwellenwerte festgelegt sind. Wenn keine Leistungsschwellenwerte für eine Veröffentlichung festgelegt sind, wird in dieser Spalte **Nicht aktiviert**angezeigt. Die folgenden Werte sind für die Leistungsbewertung möglich:  
  
-   Hervorragend  
  
-   Gut  
  
-   Durchschnittlich  
  
-   Schlecht  
  
-   Kritisch  
  
 Wenn die Leistung kritisch ist, wird **Leistungskritisch** in der **Status** -Spalte angezeigt. Weitere Informationen für die Definition von leistungsbewertungen und zum Festlegen von Leistungsschwellenwerten finden Sie unter [Überwachen der Leistung mit dem Replikationsmonitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Latenzzeit**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Die durchschnittliche Zeit zwischen dem Ausführen eines Commits für eine Transaktion beim Verleger und der entsprechenden Ausführung des Commits für die Transaktion beim Abonnenten. Die angezeigte Latenzzeit basiert auf den neuesten Messungen des Replikationsmonitors. Weitere Informationen zur Messung von Latenzzeiten finden Sie unter [Measure Latenzzeit und überprüfen Verbindungen bei Transaktionsreplikationen](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40 zugeordneten Agents; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  