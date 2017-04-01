---
title: "MSSQL_ENG020596 | Microsoft Docs"
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
  - "MSSQL_ENG020596 (Fehler)"
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020596
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20596|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Nur '%s' und Mitglieder der db_owner-Rolle können den anonymen Agent löschen.|  
  
## Erklärung  
 Sie besitzen nicht die erforderlichen Berechtigungen, um den Agent für das anonyme Abonnement zu löschen. Die verwendete Anmeldung beim Aufrufen von [Sp_dropanonymousagent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md) muss ein Mitglied der **Sysadmin** festen Serverrolle auf dem Verteiler oder **Db_owner** -Datenbankrolle in der Verteilungsdatenbank oder der Benutzer muss derjenige sein, der die erste Ausführung des Agents initiiert hat.  
  
## Benutzeraktion  
 Melden Sie sich mit den entsprechenden Anmeldeinformationen an, und führen Sie **Sp_dropanonymousagent**.  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  