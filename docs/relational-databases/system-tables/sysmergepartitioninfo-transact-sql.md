---
title: Sysmergepartitioninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sysmergepartitioninfo_TSQL
- sysmergepartitioninfo
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfo system table
ms.assetid: 7429ad2c-dd33-4f7d-89cc-700e083af518
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bcf556a371dc391b41e08778434b25131bfcf09e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmergepartitioninfo-transact-sql"></a>sysmergepartitioninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt Informationen zu Partitionen für jeden Artikel bereit. Enthält eine Zeile für jeden in der lokalen Datenbank definierten Mergeartikel. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**uniqueidentifier**|Die eindeutige ID des angegebenen Artikels.|  
|**pubid**|**uniqueidentifier**|Die eindeutige ID für diese Veröffentlichung. Sie wird generiert, wenn die Veröffentlichung hinzugefügt wird.|  
|**partition_view_id**|**int**|Die ID der Partitionssicht für diese Tabelle. In dieser Sicht wird eine Zuordnung jeder Zeile im Artikel zu den verschiedenen zugehörigen Partitions-IDs angezeigt.|  
|**repl_view_id**|**int**|Muss hinzugefügt werden.|  
|**partition_deleted_view_rule**|**nvarchar(4000)**|Die SQL-Anweisung, mit der in einem Mergereplikationstrigger die Partitions-ID für jede gelöschte oder aktualisierte Zeile basierend auf den alten Spaltenwerten abgerufen wird.|  
|**partition_inserted_view_rule**|**nvarchar(4000)**|Die SQL-Anweisung, mit der in einem Mergereplikationstrigger die Partitions-ID für jede eingefügte oder aktualisierte Zeile basierend auf den neuen Spaltenwerten abgerufen wird.|  
|**membership_eval_proc_name**|**sysname**|Der Name der Prozedur, die die aktuellen Partitions-IDs von Zeilen in ergibt **MSmerge_contents**.|  
|**column_list**|**nvarchar(4000)**|Die durch Trennzeichen getrennte Liste mit in einem Artikel replizierten Spalten.|  
|**column_list_blob**|**nvarchar(4000)**|Die durch Trennzeichen getrennte Liste mit in einem Artikel replizierten Spalten, einschließlich BLOB-Spalten (Binary Large Object).|  
|**expand_proc**|**sysname**|Der Name der Prozedur, mit der Partitions-IDs für alle untergeordneten Zeilen einer neu eingefügten übergeordneten Zeile sowie für übergeordnete Zeilen, die einer Partitionsänderung unterzogen oder gelöscht wurden, neu ausgewertet werden.|  
|**logical_record_parent_nickname**|**int**|Der Spitzname des übergeordneten Elements der obersten Ebene eines Artikels in einem logischen Datensatz.|  
|**logical_record_view**|**int**|Eine Sicht, die den rowguid-Wert des übergeordneten Artikels der obersten Ebene ausgibt, der jedem untergeordneten rowguid-Wert entspricht.|  
|**logical_record_deleted_view_rule**|**nvarchar(4000)**|Ähnlich wie **Logical_record_view**, außer dass damit untergeordnete Zeilen in der "gelöschten" Tabelle in Update- und delete-Trigger.|  
|**logical_record_level_conflict_detection**|**bit**|Gibt an, ob Konflikte auf der logischen Datensatzebene oder auf der Zeilen- oder Spaltenebene erkannt werden sollen.<br /><br /> **0** = konflikterkennung verwendet wird, mit Zeilen- oder Spaltenebene.<br /><br /> **1** = logischer Datensatz konflikterkennung verwendet wird, wenn eine Änderung in einer Zeile auf dem Verleger und die Änderung in einer separaten Zeile desselben logischen Datensatzes auf dem Abonnenten als Konflikt behandelt.<br /><br /> Wenn dieser Wert ist **1**, nur Auflösung des Konflikts Ebene zwischen logischen Datensatz verwendet werden kann.|  
|**logical_record_level_conflict_resolution**|**bit**|Gibt an, ob Konflikte auf der logischen Datensatzebene oder auf der Zeilen- oder Spaltenebene aufgelöst werden sollen.<br /><br /> **0** = Auflösung verwendet mit Zeilen- oder Spaltenebene.<br /><br /> **1** = bei einem Konflikt der gesamte logische Datensatz des Gewinners den gesamten logischen Datensatz des verlierers überschreibt.<br /><br /> Der Wert **1** kann mit beiden Erkennung der logischen Datensatzebene und für die Zeilen- oder Spaltenebene Erkennung verwendet werden.|  
|**partition_options**|**tinyint**|Definiert die Art und Weise, wie Daten im Artikel partitioniert werden. Dies ermöglicht Leistungsoptimierungen, wenn alle Zeilen nur zu einer einzigen Partition oder zu einem einzigen Abonnement gehören. *Partition_options* kann einen der folgenden Werte sein.<br /><br /> **0** = das Filtern für den Artikel ist entweder statisch oder keine eindeutige Teilmenge von Daten für jede Partition, d. h. eine "überlappende" Partition ergibt.<br /><br /> **1** = die Partitionen überlappen, und auf dem Abonnenten vorgenommene DML-Updates können nicht ändern, die Partition, zu der eine Zeile gehört.<br /><br /> **2** = das Filtern für den Artikel nicht überlappende Partitionen ergibt, aber mehrere Abonnenten können die gleiche Partition erhalten.<br /><br /> **3** = das Filtern für den Artikel nicht überlappende Partitionen ergibt, die für jedes Abonnement eindeutig sind.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
