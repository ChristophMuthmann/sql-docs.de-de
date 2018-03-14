---
title: "Ausführen von Skripts vor und nach dem Anwenden einer Momentaufnahme | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa164497bef683b80db7e386c2d8f782f85e613d
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="execute-scripts-before-and-after-a-snapshot-is-applied"></a>Ausführen von Skripts vor und nach dem Anwenden der Momentaufnahme
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Geben Sie auf der Seite **Momentaufnahme** des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** ein optionales Skript an, das vor oder nach dem Anwenden der Momentaufnahme ausgeführt wird. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Diese Optionen sind nicht verfügbar, wenn für **Momentaufnahmeformat** die Option **Zeichen**festgelegt ist.  
  
### <a name="to-execute-a-script-before-or-after-a-snapshot-is-applied"></a>So führen Sie ein Skript vor und nach dem Anwenden einer Momentaufnahme aus  
  
1.  Gehen Sie auf der Seite **Momentaufnahme** des Dialogfelds **Veröffentlichungseigenschaften - \<Veröffentlichung>** wie folgt vor:  
  
    -   Wenn Sie ein Skript angeben möchten, das vor dem Anwenden der Momentaufnahme ausgeführt werden soll, klicken Sie auf **Durchsuchen** , um zum entsprechenden Skript zu navigieren, oder geben Sie im Textfeld **Dieses Skript vor Anwenden der Momentaufnahme ausführen** den Pfad zum gewünschten Skript ein.  
  
        > [!NOTE]  
        >  Der Verteilungs-Agent bzw. Merge-Agent muss für das von Ihnen angegebene Verzeichnis Leseberechtigungen besitzen. Bei Verwendung von Pullabonnements müssen Sie ein freigegebenes Verzeichnis als UNC-Pfad angeben, wie z.B. \\\computername\scripts\myscript.sql.  
  
    -   Wenn Sie ein Skript angeben möchten, das nach dem Anwenden der Momentaufnahme ausgeführt werden soll, klicken Sie auf **Durchsuchen** , um zum entsprechenden Skript zu navigieren, oder geben Sie im Textfeld **Dieses Skript nach Anwenden der Momentaufnahme ausführen** den UNC-Pfad zum gewünschten Skript ein.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren von Momentaufnahmeeigenschaften &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Ausführen von Skripts vor und nach dem Anwenden der Momentaufnahme](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
