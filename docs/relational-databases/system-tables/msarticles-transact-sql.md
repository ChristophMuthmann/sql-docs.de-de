---
title: MSarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- MSarticles
- MSarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7699eb0df6ddd0280daaf0bee6f501dbb1a2ee71
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSarticles** Tabelle enthält eine Zeile für jeden von einem Verleger replizierten Artikel. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Die ID des Verlegers|  
|**publisher_db**|**sysname**|Der Name der Verlegerdatenbank.|  
|**publication_id**|**int**|Die ID der Veröffentlichung.|  
|**article**|**sysname**|Der Name des Artikels.|  
|**article_id**|**int**|Die ID des Artikels.|  
|**destination_object**|**sysname**|Der Name der auf dem Abonnenten erstellten Tabelle.|  
|**source_owner**|**sysname**|Der Name des Schemas der Quelltabelle auf dem Verleger.|  
|**source_object**|**sysname**|Der Name des Quellobjekts, aus dem der Artikel hinzugefügt werden soll.|  
|**description**|**nvarchar(255)**|Die Beschreibung des Artikels.|  
|**destination_owner**|**sysname**|Der Name des Schemas der auf dem Abonnenten erstellten Tabelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
