---
title: MSmerge_genhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bee379b36d0af531ee6a5d3d3b6b129199cec46c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msmergegenhistory-transact-sql"></a>MSmerge_genhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_genhistory** -Tabelle enthält eine Zeile für jede Generierung, die ein Abonnenten (innerhalb der Beibehaltungsdauer) bekannt. Sie wird verwendet, um zu verhindern, dass allgemeine Generierungsvorgänge bei Austauschvorgängen gesendet werden, und um aus Sicherungen wiederhergestellte Abonnenten erneut zu synchronisieren. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|Der globale Bezeichner der durch Generierung auf dem Abonnenten identifizierten Änderungen.|  
|**pubid**|**uniqueidentifier**|Der Bezeichner der Veröffentlichung.|  
|**generation**|**bigint**|Der Generierungswert.|  
|**art_nick**|**int**|Der Spitzname für den Artikel.|  
|**Spitznamen**|**varbinary(1001)**|Eine Liste der Spitznamen anderer Abonnenten, die bekanntermaßen bereits diese Generierung aufweisen. Die Liste wird verwendet, um das Senden einer Generierung an einen Abonnenten zu verhindern, der über diese Änderungen bereits informiert ist. Spitznamen in der Spitznamenliste werden in sortierter Reihenfolge verwaltet, damit Suchvorgänge effizienter ausgeführt werden können. Falls mehr Spitznamen vorhanden sind, als in dieses Feld passen, bietet diese Optimierung für sie keine Vorteile.|  
|**colDate**|**datetime**|Datum, an dem der Tabelle die aktuelle Generierung hinzugefügt wird.|  
|**genstatus**|**tinyint**|Der Status der Generierung:<br /><br /> **0** = geöffnet.<br /><br /> **1** = geschlossen.<br /><br /> **2** = geschlossen und stammt von einem anderen Abonnenten.|  
|**"changecount"**|**int**|Die Anzahl von Änderungen, die in einer bestimmten Generierung widergespiegelt sind.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
