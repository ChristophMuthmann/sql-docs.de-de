---
title: "Aktualisieren von Daten in Replikationsmonitor | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Aktualisieren von Daten"
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Aktualisieren von Daten in Replikationsmonitor
  Im Replikationsmonitor können das Hauptfenster und die Detailfenster (die Fenster, die vom Hauptfenster aus aufrufbar sind) sowohl automatisch als auch manuell aktualisiert werden. Zum manuellen Aktualisieren eines Fensters drücken Sie F5. Das Hauptfenster wird standardmäßig alle fünf Sekunden aktualisiert. Diese Zeiteinstellung kann aber für jeden Verleger individuell angepasst werden.  
  
 Im Replikationsmonitor angezeigten Daten werden aus dem Cache abgefragt. Informationen über die Beziehung zwischen dem Cache und Aktualisieren der Replikationsmonitor finden Sie unter [Zwischenspeichern, aktualisieren und Leistung des Replikationsmonitors](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md). Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### So legen Sie die Aktualisierungseinstellungen für den Replikationsmonitor fest  
  
1.  Mit der rechten Maustaste im linken Bereich des Replikationsmonitors Verleger, und klicken Sie dann auf **Verlegereinstellungen**.  
  
2.  Legen Sie im Dialogfeld **Verlegereinstellungen** für die Optionen **Automatisch aktualisieren** und **Aktualisierungsrate** eine Einstellung fest. Die Einstellung für **Automatisch aktualisieren** wirkt sich auf das Hauptfenster im Replikationsmonitor aus. Die **Aktualisierungsrate** Einstellung beeinflusst auch Detailfenster, für die automatische Aktualisierung festgelegt (Änderungen an der Einstellung wirken sich nur auf die Detailfenster, die nach der Änderung geöffnet).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### So geben Sie an, dass ein Detailfenster automatisch aktualisiert wird  
  
1.  Öffnen Sie das gewünschte Detailfenster im Replikationsmonitor. Zum Beispiel:  
  
    1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
    2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
    3.  Mit der rechten Maustaste ein Abonnement, und klicken Sie dann auf **Details zum**.  
  
2.  In der **Abonnement \< SubscriptionName>** Detailfenster, klicken Sie auf **Aktion**, und klicken Sie dann auf **automatisch aktualisieren**. Die Häufigkeit der Aktualisierung richtet sich nach der Einstellung **Aktualisierungsrate** im Dialogfeld **Verlegereinstellungen** .  
  
## Siehe auch  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  