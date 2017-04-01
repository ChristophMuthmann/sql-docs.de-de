---
title: "Eigenschaften der Verteilungsdatenbank | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configdistwizard.distdbproperties.f1"
helpviewer_keywords: 
  - "Eigenschaften der Verteilungsdatenbank (Dialogfeld)"
ms.assetid: 0f404ab9-1237-4936-8df5-888baab6a245
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Eigenschaften der Verteilungsdatenbank
  Mithilfe des Dialogfelds **Eigenschaften der Verteilungsdatenbank** können Sie eine Reihe von Eigenschaften anzeigen und die Transaktionsbeibehaltungsdauer und die Aufbewahrungsdauer für den Verlauf für die Datenbank festlegen.  
  
## Optionen  
 **Name**  
 Der Name der Verteilungsdatenbank. Der Standardwert ist 'distribution' (schreibgeschützt).  
  
 **Dateipfade**  
 Der Speicherort der Datenbankdatei und der Protokolldatei (schreibgeschützt).  
  
 **Transaktionsbeibehaltungsdauer**  
 Wird auch als Beibehaltungsdauer für die Verteilung bezeichnet. Der Zeitraum, für den Transaktionen für die Transaktionsreplikation gespeichert werden. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Aufbewahrungsdauer für Verlauf**  
 Der Zeitraum, für den die Metadaten des Verlaufs für jede Art von Replikation gespeichert werden.  
  
 **Sicherheit für den Warteschlangenlese-Agent**  
 Der Warteschlangenlese-Agent wird von Transaktionsreplikationen verwendet, die Abonnements mit verzögertem Update über eine Warteschlange zulassen. Ein Warteschlangenlese-Agent wird automatisch erstellt, wenn Sie die Option **Transaktionsveröffentlichung mit Updateabonnements** auf der Seite **Veröffentlichungstyp** des Assistenten für neue Veröffentlichung auswählen. Klicken Sie auf **Sicherheitseinstellungen…** , um das Konto zu ändern, unter dem der Agent ausgeführt wird und Verbindungen mit dem Verteiler herstellt.  
  
 Ein Warteschlangenlese-Agent kann auch erstellt werden, indem auswählen **Warteschlangenlese-Agent erstellen** auf dieser Seite (diese Option ist deaktiviert, wenn der Agent bereits erstellt wurde).  
  
 Für den Warteschlangenlese-Agent werden zusätzliche Verbindungsinformationen an zwei Stellen angegeben:  
  
-   Die Verbindung mit dem Verleger stellt der Agent mithilfe der Anmeldeinformationen her, die im Dialogfeld **Verlegereigenschaften** angegeben sind. Es ist auf der Seite **Verleger** des Dialogfelds **Verteilereigenschaften** verfügbar.  
  
-   Die Verbindung mit dem Abonnenten stellt der Agent mithilfe der Anmeldeinformationen her, die für den Verteilungs-Agent im Assistenten für neue Abonnements angegeben sind.  
  
 Weitere Informationen finden Sie unter  \\[Sicherheitsmodell des Replikations-Agent](../Topic/Replication%20Agent%20Security%20Model.md).  
  
## Siehe auch  
 [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)   
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  