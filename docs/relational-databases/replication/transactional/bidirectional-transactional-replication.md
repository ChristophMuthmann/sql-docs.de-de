---
title: "Bidirektionale Transaktionsreplikation | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Bidirektionale Replikation"
  - "Transaktionsreplikation, bidirektionale Replikation"
  - "Bidirektionale Transaktionsreplikation"
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# Bidirektionale Transaktionsreplikation
  Die bidirektionale Transaktionsreplikation stellt eine spezielle Transaktionsreplikationstopologie dar, über die zwei Server Änderungen austauschen können: Jeder Server veröffentlicht Daten und abonniert dann eine Veröffentlichung mit denselben Daten vom anderen Server. Die **@loopback_detection** Parameter [Sp_addsubscription & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) ist auf TRUE festgelegt, um sicherzustellen, dass Änderungen nur an den Abonnenten gesendet werden und nicht in die Änderung an den Verleger gesendet werden.  
  
 In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und höheren Versionen dieser Topologie wird auch von der Peer-to-Peer-Transaktionsreplikation unterstützt, aber bidirektionale Replikation bietet verbesserte Leistung.  
  
## Siehe auch  
 [Peer-zu-Peer-Transaktionsreplikation](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  