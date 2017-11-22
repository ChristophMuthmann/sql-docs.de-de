---
title: MSmerge_conflicts_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- MSmerge_conflicts_info_TSQL
- MSmerge_conflicts_info
dev_langs: TSQL
helpviewer_keywords: MSmerge_conflicts_info system table
ms.assetid: 6b76ae96-737a-4000-a6b6-fcc8772c2af4
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85ce4ab68f0ae49425b72b1e0d7601a7d0ff5f60
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msmergeconflictsinfo-transact-sql"></a>MSmerge_conflicts_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_conflicts_info** -Tabelle verfolgt Konflikte, die beim Synchronisieren eines Abonnements für eine Mergeveröffentlichung auftreten. Die verlierenden Zeilendaten für Konflikte befindet sich in der [MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md) Tabelle für den Artikel, in dem der Konflikt aufgetreten ist. Diese Tabelle wird auf dem Verleger in der Veröffentlichungsdatenbank und auf dem Abonnenten in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|Der Spitzname der veröffentlichten Tabelle.|  
|**ROWGUID**|**uniqueidentifier**|Der Bezeichner für die Konfliktzeile.|  
|**origin_datasource**|**nvarchar(255)**|Der Name der Datenbank, aus der die konfliktverursachende Änderung stammt.|  
|**conflict_type**|**int**|Der Typ des Konflikts, der aufgetreten ist. Die folgenden Werte sind möglich.<br /><br /> **1** = Update-Konflikt: der Konflikt wird erkannt, auf der Zeilenebene.<br /><br /> **2** = Spalte Update-Konflikt: der Konflikt auf Spaltenebene erkannt.<br /><br /> **3** = Update-Delete gewinnt: der Löschvorgang gewinnt den Konflikt.<br /><br /> **4** = Update gewinnt Delete-Konflikt: die gelöschte Zeilen-GUID, die den Konflikt verliert, wird in dieser Tabelle aufgezeichnet.<br /><br /> **5** = Fehler beim Einfügen hochladen: der Einfügevorgang des Abonnenten konnte nicht auf dem Verleger angewendet werden.<br /><br /> **6** = Fehler beim Einfügen herunterladen: der Einfügevorgang des Verlegers konnte nicht auf dem Abonnenten angewendet werden.<br /><br /> **7** = Fehler beim Löschen hochladen: der Löschvorgang des Abonnenten konnte nicht an den Verleger hochgeladen werden.<br /><br /> **8** = Fehler beim Löschen herunterladen: der Löschvorgang des Verlegers konnte nicht auf den Abonnenten heruntergeladen werden.<br /><br /> **9** = Fehler beim Update hochladen: der Updatevorgang des Abonnenten konnte nicht auf dem Verleger angewendet werden.<br /><br /> **10** = Fehler beim Update herunterladen: der Updatevorgang des Verlegers konnte nicht auf den Abonnenten angewendet werden.<br /><br /> **11** = Lösung<br /><br /> **12** = logischer Datensatz Delete, Update gewinnt: der gelöschte logische Datensatz, der den Konflikt verliert, wird in dieser Tabelle aufgezeichnet.<br /><br /> **13** = logischer Datensatz Konflikt Insert/Update: Insert in einen logischen Datensatz steht in Konflikt mit einem Update.<br /><br /> **14** = logischer Datensatz löschen WINS-Update-Konflikt: der aktualisierte logische Datensatz, der den Konflikt verliert, wird in dieser Tabelle aufgezeichnet.|  
|**reason_code**|**int**|Der Fehlercode, der kontextbezogen sein kann. Im Fall von Update / Update und Update / Delete-Konflikte für diese Spalte verwendete Wert ist identisch mit der **Conflict_type**. Bei Konflikten, bei denen Fehler beim Ändern aufgetreten sind, wird als Ursachencode der bei der Änderung im Merge-Agent aufgetretene Fehler verwendet. Wenn der Merge-Agent aufgrund einer Verletzung eines Primärschlüssels eine Insert auf dem Abonnenten angewendet werden können, z. B. protokolliert eine **Conflict_type** 6 ("Download Insert Fehler") und ein **Reason_code** 2627, also die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interne Fehlermeldung für eine primärschlüsselverletzung: "Verletzung der %ls-Einschränkung ' %. * ls'. Doppelten Schlüssel kann nicht eingefügt werden, in Objekt ' %. \*ls'. "|  
|**reason_text**|**nvarchar(720)**|Die Fehlerbeschreibung, die kontextbezogen sein kann.|  
|**pubid**|**uniqueidentifier**|Der Bezeichner für die Veröffentlichung.|  
|**MSrepl_create_time**|**datetime**|Die Uhrzeit, zu der der Konflikt aufgetreten ist.|  
|**origin_datasource_id**|**uniqueidentifier**|Der Bezeichner der Datenbank, aus der die konfliktverursachende Änderung stammt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
