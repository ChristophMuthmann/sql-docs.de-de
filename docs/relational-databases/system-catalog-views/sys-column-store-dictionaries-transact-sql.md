---
title: column_store_dictionaries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.column_store_dictionaries_TSQL
- column_store_dictionaries
- column_store_dictionaries_TSQL
- sys.column_store_dictionaries
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_dictionaries catalog view
ms.assetid: 56efd563-2f72-4caf-94e3-8a182385c173
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5c5c9d4ce8b3669404aa4a98118920d0a5a5a3d5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syscolumnstoredictionaries-transact-sql"></a>sys.column_store_dictionaries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jedes Wörterbuch, das in speicheroptimierten xVelocity-columnstore-Indizes verwendet wird. Wörterbücher werden zum Codieren bestimmter, aber nicht aller Datentypen verwendet. Daher verfügen nicht alle Spalten in einem columnstore-Index über Wörterbücher. Ein Wörterbuch kann als primäres Wörterbuch (für alle Segmente) und möglicherweise für weitere sekundäre Wörterbücher vorhanden sein, die für eine Teilmenge der Spaltensegmente verwendet werden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**hobt_id**|**bigint**|ID des Heaps oder B-Struktur-Indexes (hobt) für die Tabelle, die diesen columnstore-Index aufweist.|  
|**column_id**|**int**|ID des columnstore-Spalte, beginnend mit 1. Die erste Spalte hat ID = 1, die zweite Spalte hat ID = 2, usw.|  
|**dictionary_id**|**int**|Es können zwei Arten von Wörterbüchern, globalen und lokalen, ein Spaltensegment zugeordnet sein. Eine Dictionary_id 0 stellt das globale Wörterbuch, das über alle spaltensegmente (eine für jede Zeilengruppe ") für diese Spalte gemeinsam verwendet wird.|  
|**version**|**int**|Version des Wörterbuchformats.|  
|**type**|**int**|Wörterbuchtyp:<br /><br /> 1-Hash Wörterbuch mit **Int** Werte<br /><br /> 2 - Nicht verwendet<br /><br /> 3 – Hashwörterbuch, das Zeichenfolgenwerte enthält<br /><br /> 4 – hashwörterbuch Wörterbuch mit **"float"** Werte<br /><br /> Weitere Informationen zu Wörterbüchern finden Sie unter [Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md).|  
|**last_id**|**int**|Die letzte Daten-ID im Wörterbuch.|  
|**entry_count**|**bigint**|Die Anzahl von Einträgen im Wörterbuch.|  
|**on_disc_size**|**bigint**|Größe des Wörterbuchs in Byte.|  
|**partition_id**|**bigint**|Gibt die Partitions-ID an. Ist innerhalb einer Datenbank eindeutig.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Spalten erfordern mindestens die VIEW DEFINITION-Berechtigung für die Tabelle. Die folgenden Spalten geben null zurück, es sei denn, der Benutzer verfügt auch über **wählen** Berechtigung: Last_id, Entry_count, Data_ptr.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Beschreibung von Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [Beschreibung von Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

