---
title: MSmerge_contents (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- MSmerge_contents
- MSmerge_contents_TSQL
dev_langs: TSQL
helpviewer_keywords: MSmerge_contents system table
ms.assetid: 8d68a61a-683f-4b20-92f9-c0a8d9ba0ad1
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 14f004eea5240962740a544756301de6895a8bf8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msmergecontents-transact-sql"></a>MSmerge_contents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_contents** -Tabelle enthält eine Zeile für jede Zeile in der aktuellen Datenbank geändert, seit diese veröffentlicht wurde. Diese Tabelle wird vom Mergeprozess verwendet, um die geänderten Zeilen zu ermitteln. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|Der Spitzname der veröffentlichten Tabelle.|  
|**ROWGUID**|**uniqueidentifier**|Der Zeilenbezeichner für die angegebene Zeile.|  
|**Generation**|**bigint**|Die Generierung der identifizierten Zeile die **Tablenick** und **Rowguid**.|  
|**partchangegen**|**bigint**|Die Generierung, die der letzten Datenänderung zugeordnet ist, bei der die Zugehörigkeit der Zeile zu einer gefilterten Veröffentlichung geändert worden sein könnte|  
|**Datenherkunft**|**varbinary(501)**|Die Paare aus Spitzname des Abonnenten und Versionsnummer, die zur Verwaltung eines Verlaufs der Änderungen an dieser Zeile verwendet werden.|  
|**colvl**|**varbinary(7489)**|Die Versionsinformationen für die Spalte.|  
|**Marker**|**uniqueidentifier**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|Identifiziert die übergeordnete Zeile in **MSmerge_contents** (durch **Rowguid**) für jede entsprechende untergeordnete Zeile in einem logischen Datensatz.|  
|**logical_record_lineage**|**varbinary(501)**|Die Paare aus Spitzname des Abonnenten und Versionsnummer, die zur Verwaltung eines Verlaufs der Änderungen an der übergeordneten Zeile der obersten Ebene in einem logischen Datensatz verwendet werden. Für alle untergeordneten Zeilen in einem logischen Datensatz lautet dieser Wert NULL.|  
|**logical_relation_change_gen**|**bigint**|Der Generierungswert, der mit der letzten Änderung verbunden ist, die zur Neuausrichtung des logischen Datensatzes führte. Die Neuausrichtung wurde erforderlich, da eine vorhandene Zeile in den logischen Datensatz hinein oder aus diesem heraus verschoben wurde.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
