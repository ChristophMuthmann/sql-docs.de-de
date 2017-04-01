---
title: "Nicht-SQL Server-Abonnenten hinzuf&#252;gen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.addnonsqlsubscriber.f1"
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# Nicht-SQL Server-Abonnenten hinzuf&#252;gen
  Die Replikation unterstützt das Erstellen von Pushabonnements für Momentaufnahme- und Transaktionsveröffentlichungen für Oracle und IBM DB2-Abonnenten.  
  
## Optionen  
 **Typ des hinzuzufügenden Abonnenten**  
 Wählen Sie einen Oracle-Abonnenten oder einen IBM DB2-Abonnenten aus. Weitere Informationen zur Unterstützung für diese Abonnenten finden Sie unter [nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 **Datenquellenname**  
 Der Name, der verwendet wird, um die Datenbank in einem Netzwerk zu suchen. Die Replikation erzeugt eine Verbindungszeichenfolge für die Datenbank mithilfe des Datenquellennamens, der mit dem Anmeldenamen, dem Kennwort und den Verbindungsoptionen kombiniert wird, die Sie auf der Seite **Sicherheit für den Verteilungs-Agent** in diesem Assistenten angegeben haben.  
  
> [!NOTE]  
>  Zeichenfolge der Datenquelle und die Verbindungszeichenfolge werden nicht überprüft werden, indem [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bis möchte, dass der Verteilungs-Agent das Abonnement zu initialisieren.  
  
## Siehe auch  
 [Erstellen eines Abonnements für einen Nicht-SQL Server-Abonnenten](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  