---
title: "Angeben des Momentaufnahmeformats (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Momentaufnahmen [SQL Server-Replikation], Formate"
  - "Momentaufnahmereplikation [SQL Server], Formate"
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Angeben des Momentaufnahmeformats (SQL Server Management Studio)
  Angeben des momentaufnahmeformats auf die **Snapshot** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### So geben Sie das Momentaufnahmeformat an  
  
1.  Auf der **Snapshot** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Wählen Sie im Dialogfeld **systemeigenen SQLServer - alle Abonnenten müssen Server mit SQL Server sein** oder **Zeichen - erforderlich, wenn ein Verleger oder Abonnenten SQL Server nicht ausgeführt wird**.  
  
    > [!NOTE]  
    >  Sie sollten das systemeigene Format auswählen, sofern diese Veröffentlichung keine Abonnements für eine [!INCLUDE[ssEW](../../../includes/ssew-md.md)]-Datenbank und keine Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbank unterstützen muss.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Konfigurieren Sie Momentaufnahmeeigenschaften & #40. Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  