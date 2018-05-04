---
title: IHpublishertables (Transact-SQL) | Microsoft Docs
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
- IHpublishertables
- IHpublishertables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishertables system table
ms.assetid: 7d16ac39-633a-4fe2-8f22-1d9afc191ee9
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 18708bc7a8ef32f4a3f4de05a77c294aa5d4dd64
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ihpublishertables-transact-sql"></a>IHpublishertables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHpublishertables** -Systemtabelle stellt auf dem Verleger gespeicherte Metadaten dar. Diese Tabelle enthält eine Zeile für jede Quelltabelle, die von einer nicht - SQL Server-Verleger mithilfe des aktuellen Verteilers veröffentlicht. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|Identifiziert eine veröffentlichte Tabelle|  
|**publisher_id**|**smallint**|Identifiziert den nicht - SQL Server-Verleger aus dem die Tabelle veröffentlicht wird.|  
|**name**|**sysname**|Der Name der veröffentlichten Tabelle|  
|**Besitzer**|**sysname**|Der Tabellenbesitzer|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
