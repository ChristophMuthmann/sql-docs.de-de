---
title: MSmerge_conflict_&lt;Veröffentlichung&gt;_&lt;Artikel&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e82334105648183a9a5ad4d695f278949e51c07
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="msmergeconflictltpublicationgtltarticlegt-transact-sql"></a>MSmerge_conflict_&lt;Veröffentlichung&gt;_&lt;Artikel&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_conflict_*Veröffentlichung*_ * Artikel***-Tabelle enthält Informationen zu Zeilen mit Konflikten oder für zeilenänderungen, die rückgängig gemacht wurden, um Datenkonvergenz zu erreichen. Eine Konflikttabelle besteht für jede replizierte Tabelle in einer Veröffentlichung, wobei der Name der Konflikttabelle mit der Veröffentlichung und dem Artikelnamen angefügt wird. Diese artikelspezifischen Konflikttabellen sind in der für die Konfliktprotokollierung verwendeten Datenbank gespeichert. Dies ist in der Regel die Verlegerdatenbank, kann aber auch die Abonnementdatenbank sein, wenn die Konfliktprotokollierung dezentralisiert erfolgt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|***article_column_name***|**variable**|Stellt eine Spalte in einer replizierten Tabelle dar. Diese Systemtabelle enthält eine Spalte für jede Spalte im Tabellenartikel.|  
|**rowguid**|**uniqueidentifier**|Der Zeilenbezeichner für die Konfliktzeile.|  
|**ModifiedDate**|**datetime**|Der Zeitpunkt, zu dem der Konflikt aufgetreten ist.|  
|**origin_datasource_id**|**uniqueidentifier**|Das Abonnement, für das die Zeilenänderung rückgängig gemacht wurde oder das den Konflikt verloren hat.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
