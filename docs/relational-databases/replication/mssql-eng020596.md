---
title: MSSQL_ENG020596 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a10303fdf35a216ea0528962cb22e0818d03bc3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqleng020596"></a>MSSQL_ENG020596
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20596|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Nur '%s' und Mitglieder der db_owner-Rolle können den anonymen Agent löschen.|  
  
## <a name="explanation"></a>Erklärung  
 Sie besitzen nicht die erforderlichen Berechtigungen, um den Agent für das anonyme Abonnement zu löschen. Der Anmeldename, der zum Aufrufen von [sp_dropanonymousagent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md) verwendet wird, muss Mitglied der festen **sysadmin**-Serverrolle auf dem Verteiler bzw. Mitglied der festen **db_owner**-Datenbankrolle in der Verteilungsdatenbank sein, oder der Benutzer muss derjenige sein, der die erstmalige Ausführung des Agents initialisiert hat.  
  
## <a name="user-action"></a>Benutzeraktion  
 Melden Sie sich mit den entsprechenden Anmeldeinformationen an, und führen Sie **sp_dropanonymousagent**aus.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
