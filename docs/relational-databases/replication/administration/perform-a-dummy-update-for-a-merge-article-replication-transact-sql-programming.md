---
title: "Ausf&#252;hren eines Pseudoupdates f&#252;r einen Mergeartikel (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
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
  - "sp_mergedummyupdate"
  - "Pseudoupdates [SQL Server-Replikation]"
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Ausf&#252;hren eines Pseudoupdates f&#252;r einen Mergeartikel (Replikationsprogrammierung mit Transact-SQL)
  Bei der Mergereplikation kommen im Rahmen des Replikationsvorgangs Trigger zum Einsatz: Beim Aktualisieren einer veröffentlichten Tabelle wird ein Update-Trigger ausgelöst. In manchen Fällen können Daten aktualisiert werden, ohne dass der Trigger ausgelöst wird, z. B. bei WRITETEXT- und UPDATETEXT-Vorgängen. In diesen Fällen müssen Sie explizit eine UPDATE-Pseudoanweisung hinzufügen, um die Änderung zu replizieren. Sie können eine UPDATE-Pseudoanweisung mithilfe gespeicherter Replikationsprozeduren hinzufügen.  
  
### So fügen Sie eine UPDATE-Pseudoanweisung hinzu  
  
1.  Führen Sie den Vorgang (z. B. UPDATETEXT) für eine Zeile in einer veröffentlichten Tabelle für einen Mergevorgang aus, für die ein Pseudoupdate erforderlich ist.  
  
2.  Führen Sie auf dem Server (Verleger oder Abonnent) auf die Datenbank, in dem die Änderung vorgenommen wurde, [Sp_mergedummyupdate & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md). Geben Sie die Tabelle, auf dem die Änderung, für vorgenommen wurde **@source_object**, und der eindeutige Bezeichner der geänderten Zeile für **@rowguid**.  
  
3.  Synchronisieren Sie das Abonnement, um die geänderte Zeile zu replizieren.  
  
  