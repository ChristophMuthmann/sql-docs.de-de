---
title: Sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c342ad591c790e4c0d8167ab78f73436e81610b0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>Sys.dm_pdw_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu allen Anforderungen zurzeit oder zuletzt in Aktiv [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Eine Zeile pro Anforderung bzw. die Abfrage aufgeführt.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Der Schlüssel für diese Ansicht. Eindeutige numerische Id der Anforderung zugeordnet ist.|Für alle Anforderungen im System eindeutig.|  
|session_id|**nvarchar(32)**|Eindeutige numerische Id der Sitzung, in der diese Abfrage ausgeführt wurde, zugeordnet. Finden Sie unter [sys.dm_pdw_exec_sessions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Aktueller Status der Anforderung.|"Wird ausgeführt", "Angehalten", "Abgeschlossen", "Abgebrochen", "Fehlgeschlagen".|  
|submit_time|**datetime**|Der Zeitpunkt an dem die Anforderung übermittelt wurde für die Ausführung.|Gültige **"DateTime"** kleiner oder gleich der aktuellen Uhrzeit und Start_time.|  
|start_time|**datetime**|Zeitpunkt, an dem die anforderungsausführung gestartet wurde.|NULL für Anforderungen in der Warteschlange. andernfalls, gültige **"DateTime"** kleiner oder gleich der aktuellen Zeit.|  
|end_compile_time|**datetime**|Zeitpunkt, an dem das Modul abgeschlossen Kompilieren die Anforderung.|NULL für Anforderungen, die noch nicht kompiliert. andernfalls ein gültiger **"DateTime"** kleiner Start_time und kleiner oder gleich der aktuellen Zeit.|
|end_time|**datetime**|Zeitpunkt, an dem die anforderungsausführung abgeschlossen wird, ist fehlgeschlagen, oder wurde abgebrochen.|NULL für in der Warteschlange "oder" aktiv Anforderungen. andernfalls ein gültiger **"DateTime"** kleiner oder gleich der aktuellen Zeit.|  
|total_elapsed_time|**int**|Bei der Ausführung verstrichene Zeit seit dem Start die Anforderung, in Millisekunden.|Zwischen 0 und der Unterschied zwischen Start_time und end_time des Intervalls.<br /><br /> Wenn Total_elapsed_time den maximalen Wert für eine ganze Zahl überschreitet, weiterhin Total_elapsed_time der maximale Wert sein. Diese Bedingung generiert die Warnung "der maximale Wert überschritten wurde."<br /><br /> Der maximale Wert in Millisekunden entspricht 24.8 Tage.|  
|Bezeichnung|**nvarchar(255)**|Optionale Bezeichnung-Zeichenfolge, die einige Anweisungen SELECT-Abfrage zugeordnet.|Eine beliebige Zeichenfolge mit "a-Z", "A-Z", "0-9', '_'.|  
|error_id|**nvarchar(36)**|Eindeutige Id des Fehlers mit der Anforderung verknüpft sind, sofern vorhanden.|Finden Sie unter [sys.dm_pdw_errors &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); auf NULL festgelegt werden, wenn kein Fehler aufgetreten ist.|  
|database_id|**int**|ID der Datenbank, die durch explizite Kontext (z. B. Verwendung DB_X) verwendet.|Finden Sie unter-Id in [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|Befehl|**nvarchar(4000)**|Enthält den vollständigen Text der Anforderung als vom Benutzer übermittelt.|Jeder gültige Abfrage oder einen Anforderung-Text. Abfragen, die länger als 4.000 Byte sind, werden abgeschnitten.|  
|resource_class|**nvarchar(20)**|Die Ressourcenklasse für diese Anforderung. Weitere Informationen finden Sie im Zusammenhang **Concurrency_slots_used** in [sys.dm_pdw_resource_waits &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie unter "Minimale und Maximalwerte" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung.  
  
## <a name="security"></a>Sicherheit  
 Sys.dm_pdw_exec_requests filtert keine Abfrageergebnisse entsprechend datenbankspezifischen Berechtigungen. Anmeldungen mit VIEW SERVER STATE-Berechtigung können die Ergebnisse für alle Datenbanken Abfrageergebnisse erhalten  
  
> [!WARNING]  
>  Angreifer können sys.dm_pdw_exec_requests für das Abrufen von Informationen über bestimmte Datenbankobjekte, indem Sie einfach durch die VIEW SERVER STATE-Berechtigung und ohne eine datenbankspezifische-Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
