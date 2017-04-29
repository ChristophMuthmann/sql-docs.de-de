---
title: Bidirektionale Transaktionsreplikation | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5357fa35dcc99b260049788238a446dbaac38808
ms.lasthandoff: 04/11/2017

---
# <a name="bidirectional-transactional-replication"></a>Bidirektionale Transaktionsreplikation
  Die bidirektionale Transaktionsreplikation stellt eine spezielle Transaktionsreplikationstopologie dar, über die zwei Server Änderungen austauschen können: Jeder Server veröffentlicht Daten und abonniert dann eine Veröffentlichung mit denselben Daten vom anderen Server. Der **@loopback_detection**-Parameter von [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) ist auf TRUE festgelegt, um sicherzustellen, dass Änderungen nur an den Abonnenten gesendet werden und um zu verhindern, dass die Änderung wieder zurück auf den Verleger gelangt.  
  
 In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und höheren Versionen wird diese Topologie auch von der Peer-zu-Peer-Transaktionsreplikation unterstützt, doch kann die bidirektionale Replikation zu einer höheren Leistung führen.  
  
## <a name="see-also"></a>Siehe auch  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
