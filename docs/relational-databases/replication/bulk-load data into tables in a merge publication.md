---
title: "Massenladen von Daten in Tabellen in einer Mergever&#246;ffentlichung (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
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
  - "Massenladen [SQL Server-Replikation]"
  - "Massenladen einer Mergereplikation [SQL Server-Replikation]"
  - "sp_addtabletocontents"
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Massenladen von Daten in Tabellen in einer Mergever&#246;ffentlichung (Replikationsprogrammierung mit Transact-SQL)
  Beim Laden von Daten in Tabellen mit der [Dienstprogramm Bcp](../../tools/bcp-utility.md) oder [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) Befehl standardmäßig die Mergereplikationstrigger, das Verwalten von Überwachungsdaten in die [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) -Systemtabelle werden nicht ausgelöst. Sie haben die Möglichkeit, das Auslösen der Mergereplikationstrigger beim Laden der Daten zu erzwingen, oder Sie können die generierten Replikationsmetadaten programmgesteuert nach dem Massenkopiervorgang mithilfe gespeicherter Replikationsprozeduren einfügen.  
  
### So können Sie mit dem Hilfsprogramm "bcp" Daten per Massenladevorgang in mithilfe der Mergereplikation veröffentlichte Tabellen laden  
  
1.  Führen Sie auf dem Verleger oder dem Abonnenten das Hilfsprogramm [bcp Utility](../../tools/bcp-utility.md) oder [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) aus, um Daten in eine mithilfe der Mergereplikation veröffentlichte Tabelle einzufügen.  
  
2.  Verwenden Sie eine der folgenden Methoden, um sicherzustellen, dass die Replikationsmetadaten für die eingefügten Daten generiert werden.  
  
    -   Führen Sie den Massenkopiervorgang mithilfe der FIRE_TRIGGERS-Option aus.  
  
    -   Führen Sie in der Datenbank, in die Daten eingefügt wurde, [Sp_addtabletocontents & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md). Geben Sie den Namen der Tabelle, in die die Daten, für eingefügt wurde **@table_name**.  
  
  