---
title: IHsyscolumns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 416b4256f162ee76c10f56aa06a3f952b77e872b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHsyscolumns** -Sicht macht Spalteninformationen für die von einer nicht - SQL Server-Verleger veröffentlichten Artikeln verfügbar. Diese Sicht ist in der Distributiondatabase gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name der Spalte oder des Prozedurparameters.|  
|**id**|**int**|Die Objekt-ID der Tabelle, zu der diese Spalte gehört, oder die ID der gespeicherten Prozedur, der dieser Parameter zugeordnet ist.|  
|**xtype**|**tinyint**|Der Typ des physischen Speichers aus [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|Die ID des erweiterten benutzerdefinierten Datentyps.|  
|**length**|**bigint**|Die maximale physische Speicherlänge aus [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|Die Spalten- oder Parameter-ID.|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|Die ID des Standards für diese Spalte.|  
|**domain**|**int**|Die ID der Regel oder der CHECK-Einschränkung für diese Spalte.|  
|**number**|**int**|Die Nummer der Unterprozedur, wenn die Prozedur gruppiert ist (**0** für Einträge).|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**int**|Der Offset in die Zeile, in der diese Spalte angezeigt wird.|  
|**collationid**|**int**|Die ID der Spaltensortierung. Ist für nicht zeichenbasierte Spalten NULL.|  
|**language**|**int**|Die Sprachen-ID für die Spalte.|  
|**status**|**int**|Das Bitmuster, das zum Beschreiben einer Eigenschaft der Spalte oder des Parameters verwendet wird:<br /><br /> **0 x 08** = Spalte null-Werte zulässt.<br /><br /> **0 x 10** = ANSI-Auffüllung war aktiviert **Varchar** oder **Varbinary** wurden Spalten hinzugefügt. Nachfolgende Leerzeichen werden bei **varchar** -Spalten beibehalten, nachfolgende Nullen werden bei **varbinary** -Spalten beibehalten.<br /><br /> **0 x 40** = Parameter ist ein OUTPUT-Parameter.<br /><br /> **0 x 80** = Spalte ist eine Identitätsspalte.|  
|**type**|**int**|Der Typ des physischen Speichers aus [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**usertype**|**tinyint**|Die ID des benutzerdefinierten Datentyps aus [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|Der Genauigkeitsgrad für diese Spalte.|  
|**scale**|**int**|Die Dezimalstellen in dieser Spalte.|  
|**iscomputed**|**int**|Das Flag, das anzeigt, ob die Spalte berechnet ist:<br /><br /> **0** = nicht berechnet.<br /><br /> **1** = berechnet.|  
|**isoutparam**|**int**|Gibt an, ob der Prozedurparameter ein Ausgabeparameter ist.<br /><br /> **1** = "true".<br /><br /> **0** = "false".|  
|**isnullable**|**int**|Gibt an, ob die Spalte NULL-Werte zulässt.<br /><br /> **1** = "true".<br /><br /> **0** = "false".|  
|**collation**|**int**|Der Name der Sortierung der Spalte. Ist für nicht zeichenbasierte Spalten NULL.|  
|**tdscollation**|**int**|Der Name der Sortierung der Spalte, wenn diese in einem Tabular Data Stream (TDS) zurückgegeben wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
