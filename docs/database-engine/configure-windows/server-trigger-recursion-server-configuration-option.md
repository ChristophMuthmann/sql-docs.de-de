---
title: "Servertrigger-Rekursion (Serverkonfigurationsoption) | Microsoft Docs"
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
  - "Rekursive Trigger [SQL Server]"
  - "Trigger [SQL Server], rekursive"
  - "server trigger recursion (Option)"
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Servertrigger-Rekursion (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mithilfe der Option **server trigger recursion** geben Sie an, ob Trigger auf Serverebene rekursiv ausgelöst werden können. Wenn diese Option auf 1 (ON) festgelegt ist, können Trigger auf Serverebene rekursiv ausgelöst werden. Wenn sie auf 0 (OFF) festgelegt ist, können Trigger auf Serverebene nicht rekursiv ausgelöst werden. Nur die direkte Rekursion wird verhindert, wenn die Option server trigger recursion auf 0 (OFF) festgelegt ist. (Um die indirekte Rekursion zu deaktivieren, legen Sie die Option **nested triggers** auf 0 fest). Der Standardwert für diese Option ist 1 (ON). Die Einstellung ist ohne Neustart des Servers sofort wirksam.  
  
 Weitere Informationen finden Sie unter [Erstellen von geschachtelten Triggern](../../relational-databases/triggers/create-nested-triggers.md).  
  
## Siehe auch  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  