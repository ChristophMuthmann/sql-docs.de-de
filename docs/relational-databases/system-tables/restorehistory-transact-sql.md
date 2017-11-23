---
title: Restorehistory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- restorehistory
- restorehistory_TSQL
dev_langs: TSQL
helpviewer_keywords: restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 070e18e19fb9653df051dde8b102992c99bf4dbe
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="restorehistory-transact-sql"></a>restorehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Wiederherstellungsvorgang. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Eine Nummer als eindeutiger Bezeichner, der jeden Wiederherstellungsvorgang angibt. Identität, Primärschlüssel.|  
|**restore_date**|**datetime**|Datum und Uhrzeit des Abschlusses des Wiederherstellungsvorgangs. Kann den Wert NULL haben.|  
|**destination_database_name**|**vom Datentyp nvarchar(128)**|Name der Zieldatenbank für den Wiederherstellungsvorgang. Kann den Wert NULL haben.|  
|**Benutzername**|**vom Datentyp nvarchar(128)**|Name des Benutzers, der den Wiederherstellungsvorgang ausgeführt hat. Kann den Wert NULL haben.|  
|**backup_set_id**|**int**|Eindeutige ID, die den wiederhergestellten Sicherungssatz bezeichnet. Verweise **backupset(backup_set_id)**.|  
|**restore_type**|**char(1)**|Typ des Wiederherstellungsvorgangs:<br /><br /> D = Datenbank<br /><br /> F = Datei<br /><br /> G = Dateigruppe<br /><br /> I = Differenziell<br /><br /> L = Protokoll<br /><br /> V = Nur überprüfen<br /><br /> Kann den Wert NULL haben.|  
|**Ersetzen Sie**|**bit**|Zeigt an, ob der Wiederherstellungsvorgang die Option REPLACE angegeben hat:<br /><br /> 1 = Angegeben<br /><br /> 0 = Nicht angegeben<br /><br /> Kann den Wert NULL haben.<br /><br /> Wenn eine Datenbank mit einer Datenbankmomentaufnahme wiederhergestellt wird, ist 0 die einzige mögliche Option.|  
|**recovery**|**bit**|Zeigt an, ob der Wiederherstellungsvorgang die Option RECOVERY oder NORECOVERY angegeben hat:<br /><br /> 1 = RECOVERY<br /><br /> Kann den Wert NULL haben.<br /><br /> Wenn eine Datenbank mit einer Datenbankmomentaufnahme wiederhergestellt wird, ist 1 die einzige Option.<br /><br /> 0 = NORECOVERY|  
|**neu starten**|**bit**|Zeigt an, ob der Wiederherstellungsvorgang die Option RESTART angegeben hat:<br /><br /> 1 = Angegeben<br /><br /> 0 = Nicht angegeben<br /><br /> Kann den Wert NULL haben.<br /><br /> Wenn eine Datenbank mit einer Datenbankmomentaufnahme wiederhergestellt wird, ist 0 die einzige mögliche Option.|  
|**stop_at**|**datetime**|Zeitpunkt, bis zu dem die Datenbank wiederhergestellt wurde. Kann den Wert NULL haben.|  
|**device_count**|**tinyint**|Anzahl der am Wiederherstellungsvorgang beteiligten Geräte. Diese Anzahl kann niedriger sein als die Anzahl der Medienfamilien für die Sicherung. Kann den Wert NULL haben.<br /><br /> Wenn eine Datenbank mit einer Datenbankmomentaufnahme wiederhergestellt wird, ist der Wert immer 1.|  
|**stop_at_mark_name**|**vom Datentyp nvarchar(128)**|Zeigt an, dass die Wiederherstellung bis zu der Transaktion erfolgt ist, die die benannte Markierung enthält. Kann den Wert NULL haben.<br /><br /> Wenn eine Datenbank mit einer Datenbankmomentaufnahme wiederhergestellt wird, ist dieser Wert NULL.|  
|**stop_before**|**bit**|Zeigt an, ob die Transaktion, die die benannte Markierung enthält, in den Wiederherstellungsvorgang eingeschlossen wurde:<br /><br /> 0 = Wiederherstellung hielt vor der markierten Transaktion an.<br /><br /> 1 = Wiederherstellung schloss die markierte Transaktion ein.<br /><br /> Kann den Wert NULL haben.<br /><br /> Wenn eine Datenbank mit einer Datenbankmomentaufnahme wiederhergestellt wird, ist dieser Wert NULL.|  
  
## <a name="remarks"></a>Hinweise  
 Um die Anzahl der Zeilen in dieser Tabelle und in anderen Tabellen sicherungs- und Verlaufstabellen zu verringern, führen Sie die [Sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) gespeicherte Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von Tabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [Restorefile &#40; Transact-SQL &#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [Restorefilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [Systemtabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
