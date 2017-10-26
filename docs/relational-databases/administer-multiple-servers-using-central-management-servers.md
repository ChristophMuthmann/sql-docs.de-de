---
title: Verwalten mehrerer Server mithilfe von zentralen Verwaltungsservern | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbe8297c459d4513d1b8e45c7d64807e0d73b503
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Verwalten mehrerer Server mithilfe von zentralen Verwaltungsservern
  Sie können mehrere Server verwalten, indem Sie zentrale Verwaltungsserver festlegen und Servergruppen erstellen.  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>Erläuterung zum zentralen Verwaltungsserver und zu Servergruppen  
 Eine Instanz von SQL Server, die als zentraler Verwaltungsserver festgelegt wurde, verwaltet die Servergruppen, die die Verbindungsinformationen für Instanzen enthalten. Sie können [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen und Richtlinien der richtlinienbasierten Verwaltung gleichzeitig für Servergruppen ausführen. Sie können auch die Protokolldateien in Instanzen anzeigen, die von einem zentralen Verwaltungsserver verwaltet werden. 
 
 Im Grunde ist ein zentraler Verwaltungsserver ein zentrales Repository, das eine Liste Ihrer verwalteten Server enthält. Versionen, die älter sind als [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] , können nicht als zentraler Verwaltungsserver festgelegt werden.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen können auch für lokale Servergruppen in registrierten Servern ausgeführt werden.  
  
## <a name="create-central-management-server-and-server-groups"></a>Erstellen eines zentralen Verwaltungsservers und einer Servergruppe 
 Um einen zentralen Verwaltungsserver und Servergruppen zu erstellen, verwenden Sie das Fenster **Registrierte Server** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Beachten Sie, dass der zentrale Verwaltungsserver nicht Mitglied einer Gruppe sein kann, die er verwaltet. 
 
 Informationen zum Erstellen von zentralen Verwaltungsservern und Servergruppen finden Sie unter [Erstellen eines zentralen Verwaltungsservers und einer Servergruppe &#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  

