---
title: "Ver&#246;ffentlichungstypen der Transaktionsreplikation | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Transaktionsreplikation, Veröffentlichungen"
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# Ver&#246;ffentlichungstypen der Transaktionsreplikation
  Die Transaktionsreplikation stellt drei Veröffentlichungstypen bereit:  
  
|Veröffentlichungstyp|Beschreibung|  
|----------------------|-----------------|  
|Standardmäßige Transaktionsveröffentlichung|Geeignet für Topologien, in denen alle Daten auf dem Abonnenten schreibgeschützt sind (von der Transaktionsreplikation wird dies auf dem Abonnenten nicht erzwungen).<br /><br /> Diese Transaktionsveröffentlichungen werden standardmäßig bei der Verwendung von Transact-SQL oder Replikationsverwaltungsobjekten (RMO) erstellt. Im Assistenten für neue Veröffentlichung werden sie erstellt, wenn auf der Seite **Veröffentlichungstyp** die Option **Transaktionsveröffentlichung** ausgewählt wird.<br /><br /> Weitere Informationen zum Erstellen von Veröffentlichungen finden Sie unter [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).|  
|Transaktionsveröffentlichung in einer Peer-zu-Peer-Topologie|Dieser Veröffentlichungstyp weist die folgenden Merkmale auf:<br /><br /> – Jeder Server verfügt über identische Daten und fungiert gleichzeitig als Verleger und Abonnent.<br /><br /> – Dieselbe Zeile kann nur jeweils an einer Stelle geändert werden.<br /><br /> – Diese Topologie eignet sich für Serverumgebungen am besten, die eine hohe Verfügbarkeit und Leseskalierbarkeit erfordern.<br /><br /> <br /><br /> Weitere Informationen finden Sie unter [Peer-zu-Peer-Transaktionsreplikation](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
## Siehe auch  
 [Transaktionsreplikation](../../../relational-databases/replication/transactional/transactional-replication.md)  
  
  