---
title: MSsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d7fbb80963679858339cc1df9206f101968f4f8e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSsnapshotdeliveryprogress** Tabelle wird verwendet, um Dateien zu verfolgen, die erfolgreich an den Abonnenten übermittelt wurden, wenn eine Momentaufnahme angewendet wird. Die Daten werden zum Fortsetzen der Dateiübermittlung verwendet, falls es dem Merge-Agent nicht gelingt, alle Dateien während einer Sitzung zu übermitteln. Dadurch wird erreicht, dass beim nächsten Ausführen des Merge-Agents nicht dieselben Dateien noch einmal übermittelt werden. Diese Tabelle wird auf dem Abonnenten in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|Identifiziert den Pfad zum Momentaufnahmeordner, von dem aus die Datei erfolgreich übermittelt wurde. Für Veröffentlichungen mit parametrisierten Filtern wird die Zeichenfolge **Dynsnap** auf den Wert angefügt.|  
|**progress_token_hash**|**int**|Ein Hashwert generiert basierend auf den Wert der *Progress_token* , der verwendet wird Effizienz Suche für eine bestimmte *Progress_token* Wert.|  
|**progress_token**|**nvarchar(500)**|Identifiziert eine Datei, die erfolgreich übermittelt wurde, wobei der Wert sich aus einer Kombination des Dateinamens und des Pfads ergibt.|  
|**progress_timestamp**|**datetime**|Die **"DateTime"** Wert, der angibt, wann eine Momentaufnahmedatei erfolgreich übermittelt wurde.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
