---
title: "Verlegereinstellungen | Microsoft Docs"
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
  - "sql13.rep.monitor.publishersettings.f1"
helpviewer_keywords: 
  - "Verlegereinstellungen (Dialogfeld)"
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Verlegereinstellungen
  Im Dialogfeld **Verlegereinstellungen** können Sie die Einstellungen für Verleger ändern, die dem linken Bereich des Replikationsmonitors hinzugefügt wurden.  
  
## Optionen  
 **Verlegerverbindung**  
 Klicken Sie zum Starten der **Verbindung mit Server herstellen** dieses Dialogfeld können Sie anzeigen und Ändern der Verbindungseigenschaften und Anmeldeinformationen Replikationsmonitor für die Verbindung zu einem Verleger verwendet.  
  
 **Verteilerverbindung**  
 Wird nur angezeigt, wenn vom Verleger ein Remoteverteiler verwendet wird. Klicken Sie auf diese Option, um das Dialogfeld **Verbindung mit dem Server herstellen** zu starten. In diesem Dialogfeld können Sie die Verbindungseigenschaften und Anmeldeinformationen anzeigen und ändern, die vom Replikationsmonitor für die Verbindung mit dem Remoteverteiler verwendet werden.  
  
 **Beim Starten des Replikationsmonitors automatisch Verbindung herstellen**  
 Wählen Sie diese Option aus, damit der Replikationsmonitor automatisch eine Verbindung mit dem Verteiler herstellt und Statusinformationen für den Verleger abruft, der im Raster im oberen Bereich des Dialogfelds ausgewählt ist. Wenn dieses Kontrollkästchen deaktiviert ist, Sie müssen nach dem Starten des Replikationsmonitors manuell zu verbinden: auf dem Verleger im linken Bereich des Replikationsmonitors, und auf **Verbinden**.  
  
 **Status dieses Verlegers und seiner Veröffentlichungen automatisch aktualisieren**  
 Wählen Sie diese Option aus, damit der Replikationsmonitor automatisch den Status für den Verleger aktualisiert, der im Raster im oberen Bereich des Dialogfelds ausgewählt ist. Wenn diese Option ausgewählt ist, ruft der Replikationsmonitor die Statusinformationen für den Verleger und seine Veröffentlichungen über den Verteiler ab. Das Abrufintervall wird durch die Option **Aktualisierungsrate** festgelegt. Weitere Informationen zum Aktualisieren im Replikationsmonitor finden Sie unter [Zwischenspeichern, aktualisieren und Leistung des Replikationsmonitors](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Aktualisierungsrate**  
 Geben Sie einen Wert (in Sekunden) ein, um anzugeben, wie oft der Replikationsmonitor Statusinformationen über den Verteiler abrufen soll. Geringere Werte führen zu einem häufigeren Abruf, was die Leistung des Verteilers beeinträchtigen kann, wenn eine große Anzahl von Verlegern überwacht wird. Es wird empfohlen, das eigene System zu testen, um einen angemessenen Wert zu bestimmen. Die Einstellung **Aktualisierungsrate** wird ebenfalls verwendet, wenn Sie in einem der Detailfenster des Replikationsmonitors die Option **Automatisch aktualisieren** ausgewählt haben.  
  
 **Diese(n) Verleger in der folgenden Gruppe anzeigen**  
 Wählen Sie eine Verlegergruppe aus der Liste aus. Der Verleger wird unter dieser Gruppe im linken Bereich angezeigt. Gruppen stellen eine Möglichkeit zum Organisieren von Verlegern dar und haben keinen Einfluss auf die Funktion der Replikation.  
  
 **Neue Gruppe**  
 Klicken Sie auf diese Option, um eine neue Verlegergruppe zu erstellen. Eine Verlegergruppe stellt eine einfache Möglichkeit dar, um die Verleger innerhalb des Replikationsmonitors zu organisieren. Gruppen haben keinen Einfluss auf die Replikation der Daten oder die Beziehungen zwischen den Servern in der Replikationstopologie.  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  