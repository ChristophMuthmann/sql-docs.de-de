---
title: "MSSQL_ENG018456 | Microsoft Docs"
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
  - "MSSQL_ENG018456 (Fehler)"
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018456
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|18456|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Fehler bei der Anmeldung für Benutzer ' %. * ls'.%.\*ls|  
  
## Erklärung  
 Der Fehler MSSQL_ENG018456 wird ausgelöst, wenn ein Anmeldeversuch einen Fehler erzeugt. Wenn die Fehlermeldung das Konto enthält **Distributor_admin** (Fehler bei der Anmeldung für den Benutzer 'Distributor_admin'.), liegt ein Problem mit einem Konto, das von der Replikation verwendet. Die Replikation erstellt einen Remoteserver **Repl_distributor**, wodurch die Kommunikation zwischen dem Verteiler und Verleger. Die Anmeldung **Distributor_admin** wird diesem Remoteserver zugeordnet und muss ein gültiges Kennwort besitzen.  
  
## Benutzeraktion  
 Stellen Sie sicher, dass Sie ein Kennwort für dieses Konto angegeben haben. Weitere Informationen finden Sie unter [Schützen des Verteilers](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  