---
title: "Affinity64 Mask (Serverkonfigurationsoption) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Prozessoraffinität [SQL Server]"
  - "affinity64 mask (Option)"
  - "Binden von Prozessoren [SQL Server]"
ms.assetid: 75ed08c7-f85c-4e15-9ee1-e7bc545d3293
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Affinity64 Mask (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Durch Affinity64 Mask werden Prozessoren an bestimmte Threads gebunden, ähnlich wie bei der Option Affinity Mask. Verwenden Sie Affinity Mask, um die ersten 32 Prozessoren zu binden. Mit Affinity64 Mask binden Sie die restlichen Prozessoren auf dem Computer. Diese Option wird nur in der 64-Bit-Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angezeigt.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] Verwenden Sie stattdessen [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).  
  
## Siehe auch  
 [Affinitätsmaske (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  