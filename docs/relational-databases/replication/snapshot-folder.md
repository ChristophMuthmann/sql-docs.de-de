---
title: Momentaufnahmeordner | Microsoft-Dokumentation
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
- sql13.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e34a0846efe8ad97e3767c40476416c31793033
ms.lasthandoff: 04/11/2017

---
# <a name="snapshot-folder"></a>Momentaufnahmeordner
  Die Seite **Momentaufnahmeordner** wird im Verteilungskonfigurations-Assistenten und im Assistenten für neue Veröffentlichung angezeigt. Der von Ihnen für den Momentaufnahmeordner angegebene Speicherort wird als Standardvorgabe für alle in diesem Assistenten aktivierten Verleger verwendet (der standardmäßige Momentaufnahmeordner gilt nicht für Verleger, die später mithilfe des Dialogfelds **Verteilereigenschaften** aktiviert werden). Sie können diese Standardeinstellung für jeden Verleger auf der Seite **Verleger** des Verteilungskonfigurations-Assistenten oder im Dialogfeld **Verteilereigenschaften** überschreiben.  
  
 Der Momentaufnahmeordner ist lediglich ein von Ihnen freigegebenes Verzeichnis. Agents, die aus diesem Ordner lesen bzw. in den Ordner schreiben, benötigen ausreichende Zugriffsberechtigungen. Weitere Informationen zum Sichern des Ordners finden Sie unter [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md). Testen Sie vor der Implementierung der Replikation, ob die Replikations-Agents eine Verbindung mit dem Momentaufnahmeordner herstellen können. Melden Sie sich unter dem von dem jeweiligen Agenten verwendeten Konto an, und versuchen Sie, auf den Momentaufnahmeordner zuzugreifen.  
  
## <a name="options"></a>Optionen  
 **Snapshot folder**  
 Geben Sie den Pfad für den Ordner an, in dem Momentaufnahmedateien gespeichert werden sollen.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt die Verwendung einer Netzwerkfreigabe als Speicherort des Momentaufnahmeordners. Auf lokale Pfade (beginnend mit einem Laufwerksbuchstaben, z.B. C:\\) können Agents und andere Computer nicht zugreifen.  
  
## <a name="see-also"></a>Siehe auch  
 [Alternative Speicherorte für Momentaufnahmeordner](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Verteilung konfigurieren](../../relational-databases/replication/configure-distribution.md)   
 [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
