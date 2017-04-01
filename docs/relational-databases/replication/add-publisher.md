---
title: "Verleger hinzuf&#252;gen | Microsoft Docs"
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
  - "sql13.rep.monitor.addpublisher.f1"
helpviewer_keywords: 
  - "Verleger hinzufügen (Dialogfeld)"
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Verleger hinzuf&#252;gen
  Mithilfe des Dialogfelds **Verleger hinzufügen** können Sie dem linken Bereich des Replikationsmonitors einen oder mehrere Verleger hinzufügen. Nach dem Hinzufügen eines Verlegers werden durch das Auswählen des Verlegers im linken Bereich Informationen zu diesem Verleger im rechten Bereich anzeigt.  
  
## Optionen  
 **Hinzufügen**  
 Klicken Sie, um den Typ des hinzuzufügenden Verlegers auszuwählen startet die **Verbindung mit Server herstellen** im Dialogfeld. Folgende Optionen sind verfügbar:  
  
-   **SQL Server-Verleger hinzufügen...**  
  
     Stellen Sie mithilfe des Dialogfelds **Verbindung mit Server herstellen** eine Verbindung mit dem Verleger her.  
  
-   **Oracle-Verleger hinzufügen...**  
  
     Stellen Sie mithilfe des Dialogfelds [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Verbindung mit dem **Verbindung mit Server herstellen** gestartet.  
  
-   **Geben Sie einen Verteiler an, und fügen Sie seine Verleger hinzu…**  
  
     Stellt mithilfe des Dialogfelds [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verbindung mit Server herstellen **eine Verbindung mit dem** -Verteiler her, der einem oder mehreren Verlegern zugeordnet ist.  
  
 Nach einer erfolgreichen Verbindungsherstellung mit dem Verleger oder Verteiler werden die Namen aller Verleger und ihrer Verteiler in dem Raster im oberen Bereich des Dialogfelds angezeigt.  
  
> [!NOTE]  
>  Verteiler und Verleger werden oft auf derselben Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt, aber der Verteiler kann auch auf einer anderen Instanz ausgeführt werden (diese Konfiguration wird als Remoteverteiler bezeichnet).  
  
 **Entfernen**  
 Wählen Sie einen Verleger in das Raster im oberen Bereich des Dialogfelds, und klicken Sie auf **Entfernen** auf den Verleger aus der Liste der hinzuzufügenden Verleger zu entfernen.  
  
> [!NOTE]  
>  Diese Schaltfläche kann nicht verwendet werden, um einen Verleger zu entfernen, der bereits im Replikationsmonitor angezeigt wird. So entfernen Sie ein Verleger, der bereits angezeigt wird mit der rechten Maustaste des Verlegers im linken Bereich des Replikationsmonitors, und klicken Sie auf **Entfernen**.  
  
 **Beim Starten des Replikationsmonitors automatisch Verbindung herstellen**  
 Wählen Sie diese Option aus, damit der Replikationsmonitor automatisch eine Verbindung mit dem Verteiler herstellt und Statusinformationen für den Verleger abruft, der im Raster im oberen Bereich des Dialogfelds ausgewählt ist. Wenn dieses Kontrollkästchen deaktiviert ist, Sie müssen nach dem Starten des Replikationsmonitors manuell zu verbinden: auf dem Verleger im linken Bereich des Replikationsmonitors, und auf **Verbinden**.  
  
 **Status dieses Verlegers und seiner Veröffentlichungen automatisch aktualisieren**  
 Wählen Sie diese Option aus, damit der Replikationsmonitor automatisch den Status für den Verleger aktualisiert, der im Raster im oberen Bereich des Dialogfelds ausgewählt ist. Wenn diese Option ausgewählt ist, ruft der Replikationsmonitor die Statusinformationen für den Verleger und seine Veröffentlichungen über den Verteiler ab. Das Abrufintervall wird durch die Option **Aktualisierungsrate** festgelegt. Weitere Informationen zum Aktualisieren im Replikationsmonitor finden Sie unter [Zwischenspeichern, aktualisieren und Leistung des Replikationsmonitors](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Aktualisierungsrate**  
 Geben Sie einen Wert (in Sekunden) ein, um anzugeben, wie oft der Replikationsmonitor Statusinformationen über den Verteiler abrufen soll. Geringere Werte führen zu einem häufigeren Abruf, was die Leistung des Verteilers beeinträchtigen kann, wenn eine große Anzahl von Verlegern überwacht wird. Es wird empfohlen, das eigene System zu testen, um einen angemessenen Wert zu bestimmen. Die Einstellung **Aktualisierungsrate** wird ebenfalls verwendet, wenn Sie in einem der Detailfenster des Replikationsmonitors die Option **Automatisch aktualisieren** ausgewählt haben.  
  
 **Diese(n) Verleger in der folgenden Gruppe anzeigen**  
 Wählen Sie eine Verlegergruppe aus der Liste aus. Der Verleger wird unter dieser Gruppe im linken Bereich angezeigt. Gruppen stellen eine Möglichkeit zum Organisieren von Verlegern dar und haben keinen Einfluss auf die Funktion der Replikation. Wenn keine Gruppen definiert wurden oder Sie eine neue Gruppe erstellen möchten, dann klicken Sie auf **Neue Gruppe**.  
  
 **Neue Gruppe**  
 Klicken Sie auf diese Option, um eine neue Verlegergruppe zu erstellen. Eine Verlegergruppe stellt eine einfache Möglichkeit dar, um die Verleger innerhalb des Replikationsmonitors zu organisieren. Gruppen haben keinen Einfluss auf die Replikation der Daten oder die Beziehungen zwischen den Servern in der Replikationstopologie.  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  