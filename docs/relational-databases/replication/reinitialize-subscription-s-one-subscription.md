---
title: "Abonnements erneut initialisieren – Ein Abonnement | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.reinit.single.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: 9b0cf0be-d1f1-4163-a0ca-d6f095aa707e
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8661d832e511c5e905ac71a65b17c2b5095d8a8
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="reinitialize-subscriptions---one-subscription"></a>Abonnements erneut initialisieren - Ein Abonnement
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Im Dialogfeld **Abonnements erneut initialisieren** können Sie Abonnements für eine Neuinitialisierung kennzeichnen. Im Zuge der Neuinitialisierung wird eine Momentaufnahme auf den Abonnenten angewendet. Die Momentaufnahmeanwendung wird für Abonnements von Transaktionsveröffentlichungen durch den Verteilungs-Agent und für Abonnements von Mergeveröffentlichungen durch den Merge-Agent vorgenommen.  
  
## <a name="options"></a>Tastatur  
 **Aktuelle Momentaufnahme verwenden**  
 Wählen Sie diese Option aus, wenn die aktuelle Momentaufnahme beim nächsten Ausführen des Verteilungs- oder Merge-Agents auf den Abonnenten angewendet werden soll. Wenn keine gültige Momentaufnahme verfügbar ist, kann diese Option nicht ausgewählt werden.  
  
 **Neue Momentaufnahme verwenden**  
 Wählen Sie diese Option aus, wenn das Abonnement mithilfe einer neuen Momentaufnahme erneut initialisiert werden soll. Die Momentaufnahme kann erst auf den Abonnenten angewendet werden, nachdem sie vom Momentaufnahme-Agent generiert wurde. Wenn für die Ausführung des Momentaufnahme-Agents ein Zeitplan festgelegt ist, wird das Abonnement erst bei der nächsten Ausführung des Momentaufnahme-Agents erneut initialisiert.  
  
 Wählen Sie die Option **Neue Momentaufnahme jetzt generieren** , um den Momentaufnahme-Agent sofort zu starten.  
  
 **Unsynchronisierte Änderungen am Abonnenten vor der erneuten Initialisierung hochladen**  
 Nur für Mergereplikationen zulässig. Wählen Sie diese Option aus, um alle ausstehenden Änderungen aus der Abonnementdatenbank herunterzuladen, bevor die Daten des Abonnenten durch eine Momentaufnahme überschrieben werden.  
  
 Wenn Sie einen parametrisierten Filter hinzufügen, löschen oder ändern, können ausstehende Änderungen auf dem Abonnenten während der erneuten Initialisierung nicht auf den Verleger hochgeladen werden. Wenn Sie ausstehende Änderungen hochladen möchten, sollten Sie vor dem Ändern des Filters alle Abonnements synchronisieren.  
  
 **Für erneute Initialisierung kennzeichnen**  
 Klicken Sie auf diese Option, um das Abonnement für die Neuinitialisierung zu kennzeichnen. Sofern eine gültige Momentaufnahme verfügbar ist, wird er beim nächsten Start des Verteilungs- oder Merge-Agents für das Abonnement auf den Abonnenten angewendet.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erneutes Initialisieren von Abonnements](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  
