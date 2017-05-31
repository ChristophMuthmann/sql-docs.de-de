---
title: Abonnements initialisieren | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.initializesubscriptions.f1
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1dd4015c8247802bb86973673f4942e2f9cb270a
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="initialize-subscriptions"></a>Abonnements initialisieren
  Bevor Abonnenten replizierte Daten empfangen können, müssen sie initialisiert werden. Zwar ist kein Anfangsdataset erforderlich, jedoch müssen für den Abonnenten mindestens das Schema für jedes replizierte Objekt sowie alle für die Replikation benötigten Metadatentabellen und -prozeduren vorhanden sein.  
  
## <a name="options"></a>Optionen  
 **Abonnementeigenschaften**  
 Aktivieren Sie dieses Kontrollkästchen in der **Initialisieren** -Spalte für jeden Abonnenten, für den ein Anfangsdataset erforderlich ist. Wenn das Kontrollkästchen deaktiviert ist, werden nur die Metadaten und Prozeduren für die Replikation initialisiert. Weitere Informationen über das Initialisieren eines Abonnements ohne Momentaufnahmen finden Sie unter [Initialisieren eines Transaktionsabonnements ohne Momentaufnahme](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Wählen Sie aus der Dropdownliste in der **Initialisierungszeitpunkt** -Spalte die Option **Sofort** aus, wenn die Momentaufnahmedateien vom Merge- oder Verteilungs-Agent unmittelbar nach dem Abschließen des Assistenten an den Abonnenten übertragen werden sollen. Wählen Sie **Bei der ersten Synchronisierung** aus, wenn die Dateien bei der nächsten laut Zeitplan festgelegten Ausführung der Momentaufnahme übertragen werden sollen. Die Option **Sofort** steht für Pullabonnements in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]nicht zur Verfügung. Da der Merge-Agent und der Verteilungs-Agent für Instanzen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]nicht ausgeführt werden können, muss das Abonnement durch eine andere Methode initialisiert werden.  
  
> [!NOTE]  
>  Der Assistent fordert möglicherweise zur Eingabe einer Verbindung mit dem Verteiler auf, um den entsprechenden Auftrag für den Verteilungs- oder Merge-Agent zu starten.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
