---
title: MSmerge_tombstone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ab72c613b23d6f8edefdd318aa47dbf2f188cd7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msmergetombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_tombstone** Tabelle enthält Informationen zu gelöschten Zeilen und lässt die Löschvorgängen an andere Abonnenten weitergegeben werden. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|Der Zeilenbezeichner.|  
|**tablenick**|**int**|Spitzname der Tabelle|  
|**type**|**tinyint**|Der Typ des Löschvorgangs:<br /><br /> 1 = Löschvorgang durch Benutzer.<br /><br /> 5 = Zeile gehört nicht mehr zur gefilterten Partition.<br /><br /> 6 = Löschvorgang durch System.|  
|**Datenherkunft**|**varbinary(249)**|Zeigt die Version des Datensatzes an, der gelöscht wurde, und die Updates, die bekannt waren, als der Datensatz gelöscht wurde. Ermöglicht Regeln für eine konsistente Auflösung eines Konflikts, wenn ein Abonnent eine Zeile aktualisiert, während diese auf einem anderen Abonnenten gelöscht wird.|  
|**generation**|**int**|Wird zugewiesen, wenn eine Zeile gelöscht wird. Wenn ein Abonnent die Generierung N anfordert, werden nur Tombstones mit Generierung >= N gesendet.|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|Identifiziert den logischen Datensatz, zu dem eine gelöschte Zeile gehört hat.|  
|**logical_record_lineage**|**varbinary(501)**|Paare aus Spitzname des Abonnenten und Versionsnummer, die zur Verwaltung eines Verlaufs der Löschungen für den logischen Datensatz, zu dem diese Zeile gehört, verwendet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
