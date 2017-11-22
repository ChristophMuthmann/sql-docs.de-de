---
title: MSpublication_access (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSpublication_access_TSQL
- MSpublication_access
dev_langs: TSQL
helpviewer_keywords: MSpublication_access system table
ms.assetid: 7bebe47e-3153-4579-8092-5723667a24c6
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e05d41df9d4f23a75a54205fa7515e6786dedab3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mspublicationaccess-transact-sql"></a>MSpublication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSpublication_access** Tabelle enthält eine Zeile für jede [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung, die Zugriff auf die spezifische Veröffentlichung oder Verleger verfügt. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|Die ID der Veröffentlichung.|  
|**Anmeldung**|**sysname**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konten, die sowohl auf der Verleger- als auch auf der Verteilerseite vorhanden sind|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
