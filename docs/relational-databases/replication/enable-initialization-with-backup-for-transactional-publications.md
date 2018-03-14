---
title: "Aktivieren der Initialisierung mit Sicherung für Transaktionsveröffentlichungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
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
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b674b6debc307a6f87c5244a376174990631a1f0
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="enable-initialization-with-backup-for-transactional-publications"></a>Aktivieren der Initialisierung mit Sicherung für Transaktionsveröffentlichungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Wenn Sie ein Abonnement für eine Transaktionsveröffentlichung von einer Sicherung initialisieren möchten, aktivieren Sie die Veröffentlichung, um das Initialisieren von einer Sicherung zuzulassen. Geben Sie dann beim Erstellen des Abonnements die Sicherungsinformationen ein:  
  
-   Aktivieren Sie die Veröffentlichung im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** auf der Seite **Abonnementoptionen**. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Geben Sie mit der gespeicherten Prozedur [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) Sicherungsinformationen an. Weitere Informationen zu den für **sp_addsubscription** erforderlichen Parametern finden Sie unter [Initialisieren eines Transaktionsabonnements von einer Sicherung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md).  
  
### <a name="to-enable-initialization-with-a-backup"></a>So aktivieren Sie die Initialisierung mit einer Sicherung  
  
1.  Wählen Sie im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** auf der Seite **Abonnementoptionen** für die Option **Initialisierung aus Sicherungsdateien zulassen** den Wert **TRUE** aus.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Initialisieren eines Transaktionsabonnements ohne Momentaufnahme](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
