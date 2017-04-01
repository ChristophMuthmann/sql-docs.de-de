---
title: "Abonnement, Nicht verteilte Befehle (Transaktionsabonnement, SQL Server 2005 und h&#246;her) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.subscription.performance.f1"
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Abonnement, Nicht verteilte Befehle (Transaktionsabonnement, SQL Server 2005 und h&#246;her)
  Mithilfe der Registerkarte **Nicht verteilte Befehle** können Sie Informationen zur Anzahl der Befehle in der Verteilungsdatenbank anzeigen, die nicht an den ausgewählten Abonnenten übermittelt wurden, sowie die geschätzte Zeit zur Übermittlung dieser Befehle. Informationen zum Anzeigen der Befehle in der Verteilungsdatenbank finden Sie unter [Sp_replshowcmds & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md).  
  
## Optionen  
 **Anzahl von Befehlen in der Verteilungsdatenbank, die darauf warten, auf diesen Abonnenten angewendet zu werden**  
 Die Anzahl von Befehlen in der Verteilungsdatenbank, die nicht an den ausgewählten Abonnenten übermittelt wurden. Ein Befehl besteht aus einer Transact-SQL-DML-Anweisung (Data Manipulation Language, Datenbearbeitungssprache) oder einer DDL-Anweisung (Data Definition Language, Datendefinitionssprache).  
  
 **Geschätzte Zeit, um diese Befehle anzuwenden, basierend auf der früheren Leistung**  
 Die geschätzte Zeitdauer für die Übermittlung von Befehlen an den Abonnenten. Wenn dieser Wert größer ist, als die zum Generieren und Anwenden einer Momentaufnahme auf den Abonnenten erforderliche Zeit, sollten Sie eine erneute Initialisierung des Abonnenten in Betracht ziehen. Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Überwachen der Leistung mit dem Replikationsmonitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  