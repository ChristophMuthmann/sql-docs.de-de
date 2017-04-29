---
title: "Massenladen von Daten in Tabellen in einer Mergeveröffentlichung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cbcbfedbd5b2296da2cb266bf78ca3f7db9760ac
ms.lasthandoff: 04/11/2017

---
# <a name="bulk-load-data-into-tables-in-a-merge-publication"></a>Massenladen von Daten in Tabellen in einer Mergeveröffentlichung
  Beim Laden von Daten in Tabellen unter Berücksichtigung der Informationen in [bcp Utility](../../tools/bcp-utility.md) oder mithilfe des [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) -Befehls werden die Mergereplikationstrigger, die die internen Überwachungsdaten in der [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) -Systemtabelle verwalten, standardmäßig nicht ausgelöst. Sie haben die Möglichkeit, das Auslösen der Mergereplikationstrigger beim Laden der Daten zu erzwingen, oder Sie können die generierten Replikationsmetadaten programmgesteuert nach dem Massenkopiervorgang mithilfe gespeicherter Replikationsprozeduren einfügen.  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>So können Sie mit dem Hilfsprogramm "bcp" Daten per Massenladevorgang in mithilfe der Mergereplikation veröffentlichte Tabellen laden  
  
1.  Führen Sie auf dem Verleger oder dem Abonnenten das Hilfsprogramm [bcp Utility](../../tools/bcp-utility.md) oder [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) aus, um Daten in eine mithilfe der Mergereplikation veröffentlichte Tabelle einzufügen.  
  
2.  Verwenden Sie eine der folgenden Methoden, um sicherzustellen, dass die Replikationsmetadaten für die eingefügten Daten generiert werden.  
  
    -   Führen Sie den Massenkopiervorgang mithilfe der FIRE_TRIGGERS-Option aus.  
  
    -   Führen Sie in der Datenbank, in die Daten eingefügt wurden, [sp_addtabletocontents (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md) aus. Geben Sie den Namen der Tabelle an, in die die Daten für **@table_name**aus.  
  
  
