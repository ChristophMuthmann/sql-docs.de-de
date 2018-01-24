---
title: "Veröffentlichungstypen der Transaktionsreplikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: "32"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 018a2f804b25211b92dec8bcab89407dcd71022d
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="publication-types-for-transactional-replication"></a>Veröffentlichungstypen der Transaktionsreplikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die Transaktionsreplikation stellt drei Veröffentlichungstypen bereit:  
  
|Veröffentlichungstyp|Description|  
|----------------------|-----------------|  
|Standardmäßige Transaktionsveröffentlichung|Geeignet für Topologien, in denen alle Daten auf dem Abonnenten schreibgeschützt sind (von der Transaktionsreplikation wird dies auf dem Abonnenten nicht erzwungen).<br /><br /> Diese Transaktionsveröffentlichungen werden standardmäßig bei der Verwendung von Transact-SQL oder Replikationsverwaltungsobjekten (RMO) erstellt. Im Assistenten für neue Veröffentlichung werden sie erstellt, wenn auf der Seite **Veröffentlichungstyp** die Option **Transaktionsveröffentlichung** ausgewählt wird.<br /><br /> Weitere Informationen zum Erstellen von Veröffentlichungen finden Sie unter [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).|  
|Transaktionsveröffentlichung in einer Peer-zu-Peer-Topologie|Dieser Veröffentlichungstyp weist die folgenden Merkmale auf:<br /><br /> – Jeder Server verfügt über identische Daten und fungiert gleichzeitig als Verleger und Abonnent.<br /><br /> – Dieselbe Zeile kann nur jeweils an einer Stelle geändert werden.<br /><br /> – Diese Topologie eignet sich für Serverumgebungen am besten, die Hochverfügbarkeit und Leseskalierbarkeit erfordern.<br /><br /> <br /><br /> Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Transaktionsreplikation](../../../relational-databases/replication/transactional/transactional-replication.md)  
  
  
