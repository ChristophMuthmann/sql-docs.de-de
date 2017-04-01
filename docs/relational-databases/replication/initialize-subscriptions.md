---
title: "Abonnements initialisieren | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.initializesubscriptions.f1"
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Abonnements initialisieren
  Bevor Abonnenten replizierte Daten empfangen können, müssen sie initialisiert werden. Zwar ist kein Anfangsdataset erforderlich, jedoch müssen für den Abonnenten mindestens das Schema für jedes replizierte Objekt sowie alle für die Replikation benötigten Metadatentabellen und -prozeduren vorhanden sein.  
  
## Optionen  
 **Abonnementeigenschaften**  
 Aktivieren Sie das Kontrollkästchen in der **initialisieren** -Spalte für jeden Abonnenten, die einen anfänglichen Satz von Daten erforderlich sind. Wenn das Kontrollkästchen deaktiviert ist, werden nur die Metadaten und Prozeduren für die Replikation initialisiert. Weitere Informationen zum Initialisieren eines Abonnements ohne Momentaufnahme finden Sie unter [eine Transaktionsabonnements ohne Momentaufnahme initialisieren](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Wählen Sie **sofort** aus dem Dropdown-Listenfeld in der **bei** Spalte der Merge-Agent oder Merge-Agents übertragen lassen snapshot-Dateien auf den Abonnenten nach dem Abschließen des Assistenten. Wählen Sie **Bei der ersten Synchronisierung** aus, wenn die Dateien bei der nächsten laut Zeitplan festgelegten Ausführung der Momentaufnahme übertragen werden sollen. Die Option **Sofort** steht für Pullabonnements in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]nicht zur Verfügung. Da der Merge-Agent und der Verteilungs-Agent für Instanzen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]nicht ausgeführt werden können, muss das Abonnement durch eine andere Methode initialisiert werden.  
  
> [!NOTE]  
>  Der Assistent fordert möglicherweise zur Eingabe einer Verbindung mit dem Verteiler auf, um den entsprechenden Auftrag für den Verteilungs- oder Merge-Agent zu starten.  
  
## Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)   
 [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  