---
title: "Geben Sie an, dass Löschvorgänge für Mergeartikel nicht nachverfolgt werden sollen | Microsoft-Dokumentation"
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
dev_langs:
- TSQL
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4c6b6a295d40d9a1a5e161bf10d5a61648e49eb
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="specify-that-deletes-should-not-be-tracked-for-merge-articles"></a>Geben Sie an, dass Löschvorgänge für Mergeartikel nicht nachverfolgt werden sollen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Standardmäßig synchronisiert die Mergereplikation DELETE-Befehle zwischen dem Verleger und dem Abonnenten. Die Mergereplikation ermöglicht Ihnen, Zeilen in der Abonnementdatenbank auch dann beizubehalten, wenn sie aus der Veröffentlichung gelöscht wurden und umgekehrt. Sie können bei der Erstellung eines neuen Artikels programmgesteuert festlegen, dass der DELETE-Befehl ignoriert wird, oder Sie können diese Funktionalität zu einem späteren Zeitpunkt mithilfe von gespeicherten Replikationsprozeduren aktivieren.  
  
> [!IMPORTANT]  
>  Die Aktivierung dieser Funktionalität führt zu Nichtkonvergenz, was bedeutet, dass die dem Abonnenten verfügbaren Daten nicht genau den Daten des Verlegers entsprechen. Sie müssen einen eigenen Mechanismus implementieren, um die gelöschten Zeilen zu entfernen.  
  
### <a name="to-specify-that-deletes-be-ignored-for-a-new-merge-article"></a>So geben Sie an, dass Löschvorgänge für Mergeartikel ignoriert werden sollen  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)aus. Geben Sie den Wert **false** für **@delete_tracking**aus. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung veröffentlicht wurde, muss der Wert von **delete_tracking** für beide Artikel gleich sein.  
  
### <a name="to-specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>So geben Sie an, dass Löschvorgänge für einen vorhandenen Mergeartikel ignoriert werden sollen  
  
1.  Führen Sie [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) aus, um zu ermitteln, ob die Fehlerkompensierung für einen Artikel aktiviert ist, und achten Sie im Resultset auf den Wert von **delete_tracking**. Ist dieser Wert **0**, werden Löschvorgänge bereits ignoriert.  
  
2.  Ist der in Schritt 1 ermittelte Wert **1** ist, führen Sie [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie den Wert **delete_tracking** für **@property**und den Wert **false** für **@value**aus.  
  
    > [!NOTE]  
    >  Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung veröffentlicht wurde, muss der Wert von **delete_tracking** für beide Artikel gleich sein.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Optimieren der Mergereplikationsleistung durch bedingtes Nachverfolgen von Löschvorgängen](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
