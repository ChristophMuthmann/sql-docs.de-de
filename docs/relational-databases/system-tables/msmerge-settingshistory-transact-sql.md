---
title: MSmerge_settingshistory (Transact-SQL) | Microsoft Docs
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
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 08fa1c93123cb29492913fccc1e3f7c1db7f9d59
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msmergesettingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_settingshistory** Tabelle wird verwendet, um die Verwaltung eines Verlaufs der Änderungen an Artikel- und Veröffentlichungseigenschaften bei der Mergereplikation mit einer Zeile für jede Änderung an einer mergereplikationstopologie. In dieser Tabelle werden auch Informationen zu dem Zeitpunkt gespeichert, zu dem die ursprünglichen Eigenschaftseinstellungen vorgenommen wurden. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**EventTime**|**datetime**|Die Uhrzeit, zu der das Ereignis aufgetreten ist|  
|**pubid**|**uniqueidentifier**|Die eindeutige ID für eine bestimmte Veröffentlichung|  
|**artid**|**uniqueidentifier**|Die eindeutige ID des angegebenen Artikels.|  
|**EventType**|**tinyint**|Gibt den Ereignistyp an, der aufgezeichnet wird. Es kann einer der folgenden Typen sein:<br /><br /> **1** – ursprüngliche veröffentlichungsebenen-eigenschaftseinstellung.<br /><br /> **2** -veröffentlichungseigenschaft ändern.<br /><br /> **101** -ursprüngliche.<br /><br /> **102** -Artikeleigenschaft ändern.|  
|**propertyname**|**sysname**|Der Name der festgelegten oder geänderten Eigenschaft|  
|**previousvalue**|**sysname**|Der vorhergehende Eigenschaftswert, falls eine Eigenschaft geändert wurde|  
|**newValue**|**sysname**|Der Wert, zu dem die Eigenschaft geändert oder mit dem die Eigenschaft erstellt wurde|  
|**eventText**|**Datentyp nvarchar(2000)**|Die Zeichenfolge, die das Ereignis beschreibt|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
