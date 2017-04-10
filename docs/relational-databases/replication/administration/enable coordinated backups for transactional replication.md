---
title: "Aktivieren koordinierter Sicherungen f&#252;r die Transaktionsreplikation (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
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
  - "Transaktionsreplikation, Sicherung und Wiederherstellung"
  - "sp_replicationdboption"
  - "sync with backup [SQL Server-Replikation]"
  - "Koordinierte Sicherungen [SQL Server-Replikation]"
  - "Sicherungen [SQL Server-Replikation], Transaktionsreplikation"
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Aktivieren koordinierter Sicherungen f&#252;r die Transaktionsreplikation (Replikationsprogrammierung mit Transact-SQL)
  Wenn Sie eine Datenbank für die Transaktionsreplikation aktivieren, können Sie angeben, dass alle Transaktionen gesichert werden müssen, bevor sie an die Verteilungsdatenbank übermittelt werden. Zudem können Sie auf der Verteilungsdatenbank die koordinierte Sicherung aktivieren, sodass das Transaktionsprotokoll der Veröffentlichungsdatenbank erst dann abgeschnitten wird, nachdem die an den Verteiler weitergegebenen Transaktionen gesichert wurden. Weitere Informationen finden Sie unter [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### So aktivieren Sie koordinierte Sicherungen für eine mit der Transaktionsreplikation veröffentlichte Datenbank  
  
1.  Verwenden Sie auf dem Verleger die [DATABASEPROPERTYEX & #40; Transact-SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) Funktion zum Zurückgeben der **IsSyncWithBackup** Eigenschaft der Veröffentlichungsdatenbank. Wenn die Funktion **1**zurückgibt, sind bereits koordinierte Sicherungen für die veröffentlichte Datenbank aktiviert.  
  
2.  Wenn die Funktion in Schritt 1 zurückgibt **0**, führen Sie [Sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie einen Wert **sync with backup** für **@optname**und **true** für **@value**an.  
  
    > [!NOTE]  
    >  Wenn Sie die Option **sync with backup** in **false**ändern, wird der Abschneidepunkt der Veröffentlichungsdatenbank nach Ausführen des Protokolllese-Agents aktualisiert oder, wenn der Protokolllese-Agent fortlaufend ausgeführt wird, nach einem bestimmten Zeitintervall. Das maximale Zeitintervall wird gesteuert, indem die **– MessageInterval** Agentparameter (mit einem Standardwert von 30 Sekunden).  
  
### So aktivieren Sie koordinierte Sicherungen für eine Verteilungsdatenbank  
  
1.  Auf dem Verteiler verwenden die [DATABASEPROPERTYEX & #40; Transact-SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) Funktion zum Zurückgeben der **IsSyncWithBackup** Eigenschaft der Verteilungsdatenbank. Wenn die Funktion **1**zurückgibt, sind bereits koordinierte Sicherungen für die Verteilungsdatenbank aktiviert.  
  
2.  Wenn die Funktion in Schritt 1 zurückgibt **0**, führen Sie [Sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) auf dem Verteiler für die Verteilungsdatenbank. Geben Sie einen Wert **sync with backup** für **@optname** und **true** für **@value**an.  
  
### So deaktivieren Sie koordinierte Sicherungen  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Verteiler für die Verteilungsdatenbank [Sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Geben Sie einen Wert **sync with backup** für **@optname** und **false** für **@value**an.  
  
  