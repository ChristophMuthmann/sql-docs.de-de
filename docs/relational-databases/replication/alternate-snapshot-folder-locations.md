---
title: "Alternative Speicherorte f&#252;r Momentaufnahmeordner | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Momentaufnahmen [SQL Server-Replikation], alternative Ordner"
  - "Momentaufnahmereplikation [SQL Server], alternative Ordner"
  - "Alternative Momentaufnahmeordner [SQL Server-Replikation]"
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Alternative Speicherorte f&#252;r Momentaufnahmeordner
  Alternative Momentaufnahmespeicherorte ermöglichen Ihnen das Speichern von Momentaufnahmedateien an einem anderen Speicherort oder zusätzlich zum Standardspeicherort, der sich normalerweise auf dem Verteiler befindet. Alternative Speicherorte können sich auf einem anderen Server, in einem Netzlaufwerk oder auf Wechselmedien befinden, z. B. CD-ROMs oder Wechseldatenträgern.  
  
 Alternative Momentaufnahmespeicherorte werden als Eigenschaft der Veröffentlichung gespeichert. Da der alternative Momentaufnahmespeicherort eine Veröffentlichungseigenschaft ist, sind der Verteilungs-Agent und der Merge-Agent in der Lage, die ordnungsgemäße Momentaufnahme als Teil des Synchronisierungsprozesses zu finden.  
  
 Wenn Sie einen alternativen Speicherort für Momentaufnahmeordner angeben oder Momentaufnahmedateien komprimieren möchten, erstellen Sie die Veröffentlichung, ohne die AnfangsMomentaufnahme sofort zu erstellen, legen Sie die Veröffentlichungseigenschaften für den Momentaufnahmespeicherort fest, und führen Sie dann den Momentaufnahme-Agent für diese Veröffentlichung aus. Wenn Sie den alternativen Speicherort nach der Erstellung der Anfangsmomentaufnahme ändern, wird keiner der für die Veröffentlichung generierten Momentaufnahmen an den alternativen Speicherort verschoben. In diesem Fall ist der Merge-Agent bzw. Verteilungs-Agent möglicherweise nicht in der Lage, die Momentaufnahmedateien an dem neuen alternativen Speicherort ausfindig zu machen.  
  
> [!NOTE]  
>  Geben Sie einen alternativen Speicherort (mit dem **Veröffentlichungseigenschaften** Dialogfeld oder [Sp_changepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)) Das ist der Standardspeicherort für momentaufnahmeordner identisch.  
  
> [!CAUTION]  
>  Verwenden Sie WebSync und alternative Ordnerspeicherorte für Momentaufnahmen nicht gleichzeitig.  
  
 **So geben Sie alternative Momentaufnahmespeicherorte an**  
  
-   [! INCLUDE [SsManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [Specify an Alternate Snapshot Folder Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   Replikation [!INCLUDE[tsql](../../includes/tsql-md.md)] programming: [Snapshot-Eigenschaften konfigurieren & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## Siehe auch  
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Momentaufnahmeoptionen](../../relational-databases/replication/snapshot-options.md)  
  
  