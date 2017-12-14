---
title: "Alternative Speicherorte für Momentaufnahmeordner | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18a909ac5ed94e68df8c981d722e7f7a26f01530
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="alternate-snapshot-folder-locations"></a>Alternative Speicherorte für Momentaufnahmeordner
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Alternative Momentaufnahmespeicherorte ermöglichen Ihnen das Speichern von Momentaufnahmedateien an einem anderen Speicherort oder zusätzlich zum Standardspeicherort, der sich normalerweise auf dem Verteiler befindet. Alternative Speicherorte können sich auf einem anderen Server, in einem Netzlaufwerk oder auf Wechselmedien befinden, z. B. CD-ROMs oder Wechseldatenträgern.  
  
 Alternative Momentaufnahmespeicherorte werden als Eigenschaft der Veröffentlichung gespeichert. Da der alternative Momentaufnahmespeicherort eine Veröffentlichungseigenschaft ist, sind der Verteilungs-Agent und der Merge-Agent in der Lage, die ordnungsgemäße Momentaufnahme als Teil des Synchronisierungsprozesses zu finden.  
  
 Wenn Sie einen alternativen Speicherort für Momentaufnahmeordner angeben oder Momentaufnahmedateien komprimieren möchten, erstellen Sie die Veröffentlichung, ohne die AnfangsMomentaufnahme sofort zu erstellen, legen Sie die Veröffentlichungseigenschaften für den Momentaufnahmespeicherort fest, und führen Sie dann den Momentaufnahme-Agent für diese Veröffentlichung aus. Wenn Sie den alternativen Speicherort nach der Erstellung der Anfangsmomentaufnahme ändern, wird keiner der für die Veröffentlichung generierten Momentaufnahmen an den alternativen Speicherort verschoben. In diesem Fall ist der Merge-Agent bzw. Verteilungs-Agent möglicherweise nicht in der Lage, die Momentaufnahmedateien an dem neuen alternativen Speicherort ausfindig zu machen.  
  
> [!NOTE]  
>  Geben Sie keinen alternativen Speicherort (mithilfe des Dialogfelds **Veröffentlichungseigenschaften** oder [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)) an, der der gleiche ist wie der Standardspeicherort für Momentaufnahmen.  
  
> [!CAUTION]  
>  Verwenden Sie WebSync und alternative Ordnerspeicherorte für Momentaufnahmen nicht gleichzeitig.  
  
 **So geben Sie alternative Momentaufnahmespeicherorte an**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Angeben eines alternativen Speicherortes für den Momentaufnahmeordner &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]-Replikationsprogrammierung: [Konfigurieren von Momentaufnahmeeigenschaften &#40;Transact-SQL für Replikationsprogrammierung&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Momentaufnahmeoptionen](../../relational-databases/replication/snapshot-options.md)  
  
  
