---
title: "affinity64 I/O mask (Serverkonfigurationsoption) | Microsoft Docs"
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
  - "Binden von Prozessoren [SQL Server]"
  - "affinity64 I/O mask (Option)"
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# affinity64 I/O mask (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die Option **affinity64 I/O mask** bindet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenträger-E/A an eine bestimmte Teilmenge der CPUs. Diese Option verhält sich ähnlich wie die Option **affinity I/O mask**. Verwenden Sie **affinity I/O mask**, um die ersten 32 Prozessoren zu binden, und mit **affinity64 I/O mask** binden Sie die restlichen Prozessoren auf dem Computer. Wenn Sie **affinity64 I/O mask** neu konfigurieren, müssen Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu starten. Diese Option wird nur in der 64-Bit-Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angezeigt.  
  
## Siehe auch  
 [Affinity I/O Mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  