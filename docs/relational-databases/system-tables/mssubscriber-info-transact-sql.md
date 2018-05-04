---
title: MSsubscriber_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsubscriber_info_TSQL
- MSsubscriber_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_info system table
ms.assetid: 5ca22f41-6020-4f72-8110-e69baf3447cb
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 33b09b942cea3fc8e2da711ef956e86e85119a5d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mssubscriberinfo-transact-sql"></a>MSsubscriber_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSsubscriber_info** Tabelle enthält eine Zeile für jedes Verleger/Abonnent-Paar, die Abonnements aus dem lokalen Verteiler wird per Push übertragen wird. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
 **Hinweis** diese Systemtabelle wurde als veraltet markiert und ist weiterhin für die Unterstützung von früheren Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Der Name des Verlegers.|  
|**subscriber**|**sysname**|Den Namen des Abonnenten.|  
|**type**|**tinyint**|Der Abonnententyp:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten.<br /><br /> **1** = ODBC-Datenquelle.|  
|**login**|**sysname**|Der Anmeldename für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. Wird verschlüsselt gespeichert, wenn der Abonnent mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierungsmodus hinzugefügt wird.|  
|**password**|**nvarchar(524)**|Das Kennwort für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung. Wird verschlüsselt gespeichert, wenn der Abonnent mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierungsmodus hinzugefügt wird.|  
|**description**|**nvarchar(255)**|Die Beschreibung des Abonnenten.|  
|**security_mode**|**int**|Der implementierte Sicherheitsmodus:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Authentifizierung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
