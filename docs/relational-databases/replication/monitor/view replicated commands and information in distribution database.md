---
title: "Anzeigen replizierter Befehle und anderer Informationen in der Verteilungsdatenbank (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_browsereplcmds"
  - "Transaktionsreplikation, Überwachung"
  - "Verteilungsdatenbanken [SQL Server-Replikation], Anzeigen replizierter Befehle"
  - "Anzeigen replizierter Befehle"
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Anzeigen replizierter Befehle und anderer Informationen in der Verteilungsdatenbank (Replikationsprogrammierung mit Transact-SQL)
  Bei Verwendung der Transaktionsreplikation werden Transaktionsbefehle in der Verteilungsdatenbank gespeichert, bis sie vom Verteilungs-Agent an alle Abonnenten weitergegeben oder bis die Änderungen von einem Verteilungs-Agent abgerufen werden. Diese ausstehenden Befehle in der Verteilungsdatenbank können programmgesteuert mit gespeicherten Replikationsprozeduren angezeigt werden. Weitere Informationen finden Sie unter [gespeicherten Replikationsprozeduren & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).  
  
### So zeigen Sie replizierte Befehle für alle Transaktionsveröffentlichungen in der Verteilungsdatenbank an  
  
1.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md).  
  
### So zeigen Sie replizierte Befehle in der Verteilungsdatenbank für einen bestimmten Artikel oder für eine bestimmte Datenbank an, der bzw. die mithilfe der Transaktionsreplikation veröffentlicht wurde  
  
1.  (Optional) Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Geben Sie **@publication** und **@article**an. Beachten Sie den Wert von **article id** im Resultset.  
  
2.  Führen Sie auf dem Verteiler für die Verteilungsdatenbank [Sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md). (Optional) Geben Sie die Artikel-ID aus Schritt 2 für **@article_id**. (Optional) Gibt die ID der Veröffentlichungsdatenbank für **@publisher_database_id**, aus abgerufen werden kann der **Database_id** -Spalte in der [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) Katalogsicht.  
  
## Siehe auch  
 [Programmgesteuertes Überwachen der Replikation](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  