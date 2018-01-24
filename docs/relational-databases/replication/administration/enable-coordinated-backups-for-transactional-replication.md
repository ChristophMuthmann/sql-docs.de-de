---
title: "Aktivieren koordinierter Sicherungen für die Transaktionsreplikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- transactional replication, backup and restore
- sp_replicationdboption
- sync with backup [SQL Server replication]
- coordinated backups [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
caps.latest.revision: "31"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85f528a2b114d3122f91a426224a1b0d7b3be2a8
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="enable-coordinated-backups-for-transactional-replication"></a>Aktivieren koordinierter Sicherungen für die Transaktionsreplikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Wenn Sie eine Datenbank für die Transaktionsreplikation aktivieren, können Sie angeben, dass alle Transaktionen gesichert werden müssen, bevor sie an die Verteilungsdatenbank übermittelt werden. Zudem können Sie auf der Verteilungsdatenbank die koordinierte Sicherung aktivieren, sodass das Transaktionsprotokoll der Veröffentlichungsdatenbank erst dann abgeschnitten wird, nachdem die an den Verteiler weitergegebenen Transaktionen gesichert wurden. Weitere Informationen finden Sie unter [Strategien zum Sichern und Wiederherstellen einer Momentaufnahme- und Transaktionsreplikation](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### <a name="to-enable-coordinated-backups-for-a-database-published-with-transactional-replication"></a>So aktivieren Sie koordinierte Sicherungen für eine mit der Transaktionsreplikation veröffentlichte Datenbank  
  
1.  Verwenden Sie auf dem Verleger die [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md)-Funktion, um die **IsSyncWithBackup**-Eigenschaft der Veröffentlichungsdatenbank zurückzugeben. Wenn die Funktion **1**zurückgibt, sind bereits koordinierte Sicherungen für die veröffentlichte Datenbank aktiviert.  
  
2.  Wenn die Funktion in Schritt 1 **0** zurückgibt, führen Sie [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank aus. Geben Sie einen Wert **sync with backup** für **@optname**und **true** für **@value**.  
  
    > [!NOTE]  
    >  Wenn Sie die Option **sync with backup** in **false**ändern, wird der Abschneidepunkt der Veröffentlichungsdatenbank nach Ausführen des Protokolllese-Agents aktualisiert oder, wenn der Protokolllese-Agent fortlaufend ausgeführt wird, nach einem bestimmten Zeitintervall. Das Maximalintervall wird vom **–MessageInterval** -Agentparameter gesteuert (standardmäßig 30 Sekunden).  
  
### <a name="to-enable-coordinated-backups-for-a-distribution-database"></a>So aktivieren Sie koordinierte Sicherungen für eine Verteilungsdatenbank  
  
1.  Verwenden Sie auf dem Verteiler die [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md)-Funktion, um die **IsSyncWithBackup**-Eigenschaft der Verteilungsdatenbank zurückzugeben. Wenn die Funktion **1**zurückgibt, sind bereits koordinierte Sicherungen für die Verteilungsdatenbank aktiviert.  
  
2.  Wenn die Funktion in Schritt 1 **0** zurückgibt, führen Sie [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank aus. Geben Sie einen Wert **sync with backup** für **@optname** und **true** für **@value**.  
  
### <a name="to-disable-coordinated-backups"></a>So deaktivieren Sie koordinierte Sicherungen  
  
1.  Führen Sie [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Verteiler für die Verteilungsdatenbank aus. Geben Sie einen Wert **sync with backup** für **@optname** und **false** für **@value**.  
  
  
