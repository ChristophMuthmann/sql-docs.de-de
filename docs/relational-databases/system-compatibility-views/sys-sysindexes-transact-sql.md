---
title: Sys.sysindexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysindexes
- sysindexes_TSQL
- sys.sysindexes
- sys.sysindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysindexes system table
- sys.sysindexes compatibility view
ms.assetid: f483d89c-35c4-4a08-8f8b-737fd80d13f5
caps.latest.revision: 57
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 541b0de942e5b67c4c4be26ed1a6e29578a178ab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Index und jede Tabelle in der aktuellen Datenbank. XML-Indizes werden in dieser Sicht nicht unterstützt. Partitionierte Tabellen und Indizes werden in dieser Sicht nicht vollständig unterstützt; Verwenden Sie die [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) stattdessen die Katalogsicht.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID der Tabelle, zu der der Index gehört.|  
|**status**|**int**|Systemstatusinformationen.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**erste**|**Binary(6)**|Zeiger auf die erste Seite oder Stammseite.<br /><br /> Nicht verwendet, wenn **indid** = 0.<br /><br /> NULL = Index ist partitioniert, wenn **Indid** > 1.<br /><br /> NULL = Tabelle ist partitioniert, wenn **indid** gleich 0 oder 1.|  
|**indid**|**smallint**|ID des Indexes:<br /><br /> 0 = Heap<br /><br /> 1 = Gruppierter Index<br /><br /> >1 = Nicht gruppierter Index|  
|**Stamm**|**Binary(6)**|Für **Indid** > = 1, **Root** ist der Zeiger auf die Stammseite.<br /><br /> Nicht verwendet, wenn **indid** = 0.<br /><br /> NULL = Index ist partitioniert, wenn **Indid** > 1.<br /><br /> NULL = Tabelle ist partitioniert, wenn **indid** gleich 0 oder 1.|  
|**minlen**|**smallint**|Mindestgröße einer Zeile.|  
|**keycnt**|**smallint**|Anzahl der Schlüssel.|  
|**groupid**|**smallint**|ID der Dateigruppe, für die das Objekt erstellt wurde.<br /><br /> NULL = Index ist partitioniert, wenn **Indid** > 1.<br /><br /> NULL = Tabelle ist partitioniert, wenn **indid** gleich 0 oder 1.|  
|**Dpages**|**int**|Für **indid** = 0 oder **indid** = 1 ist **dpages** die Anzahl der verwendeten Datenseiten.<br /><br /> Für **Indid** > 1, **Dpages** ist die Anzahl der verwendeten Indexseiten.<br /><br /> 0 = Index ist partitioniert, wenn **Indid** > 1.<br /><br /> 0 = Tabelle ist partitioniert, wenn **indid** gleich 0 oder 1.<br /><br /> Bei einem Zeilenüberlauf ist das Ergebnis ungenau.|  
|**Reserviert**|**int**|Für **indid** = 0 oder **indid** = 1 ist **reserved** die Anzahl der allen Indizes und Tabellendaten zugeordneten Seiten.<br /><br /> Für **Indid** > 1, **reservierte** ist die Anzahl der für den Index reservierten Seiten.<br /><br /> 0 = Index ist partitioniert, wenn **Indid** > 1.<br /><br /> 0 = Tabelle ist partitioniert, wenn **indid** gleich 0 oder 1.<br /><br /> Bei einem Zeilenüberlauf ist das Ergebnis ungenau.|  
|**verwendet**|**int**|Für **indid** = 0 oder **indid** = 1 ist **used** die Gesamtanzahl der für alle Indizes und Tabellendaten verwendeten Seiten.<br /><br /> Für **Indid** > 1, **verwendet** ist die Anzahl der Seiten, die für den Index verwendet.<br /><br /> 0 = Index ist partitioniert, wenn **Indid** > 1.<br /><br /> 0 = Tabelle ist partitioniert, wenn **indid** gleich 0 oder 1.<br /><br /> Bei einem Zeilenüberlauf ist das Ergebnis ungenau.|  
|**rowcnt**|**bigint**|Zeilenanzahl auf Datenebene, basierend auf **indid** = 0 und **indid** = 1.<br /><br /> 0 = Index ist partitioniert, wenn **Indid** > 1.<br /><br /> 0 = Tabelle ist partitioniert, wenn **indid** gleich 0 oder 1.|  
|**rowmodctr**|**int**|Zählt die Gesamtzahl der eingefügten, gelöschten oder aktualisierten Zeilen, seitdem die Statistiken für die Tabelle zuletzt aktualisiert wurden.<br /><br /> 0 = Index ist partitioniert, wenn **Indid** > 1.<br /><br /> 0 = Tabelle ist partitioniert, wenn **indid** gleich 0 oder 1.<br /><br /> In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höher, **Rowmodctr** ist nicht vollständig kompatibel mit früheren Versionen. Weitere Informationen finden Sie in den Hinweisen.|  
|**reserved3**|**int**|Gibt 0 zurück.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|Gibt 0 zurück.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**smallint**|Maximale Größe einer Zeile|  
|**maxirow**|**smallint**|Maximale Größe einer Indexzeile, die kein Blatt darstellt.<br /><br /> In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höher, **Maxirow** ist nicht vollständig kompatibel mit früheren Versionen.|  
|**OrigFillFactor**|**tinyint**|Ursprünglicher Füllfaktorwert, der beim Erstellen des Indexes verwendet wurde. Dieser Wert wird nicht aufrechterhalten, kann jedoch hilfreich sein, wenn Sie einen Index neu erstellen müssen und sich nicht an den verwendeten Füllfaktorwert erinnern.|  
|**StatVersion**|**tinyint**|Gibt 0 zurück.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved2**|**int**|Gibt 0 zurück.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**Binary(6)**|NULL = Index ist partitioniert.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**smallint**|Indeximplementierungsflag.<br /><br /> Gibt 0 zurück.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**lockflags**|**smallint**|Wird zur Einschränkung der berücksichtigten Granularitäten von Sperren für einen Index verwendet. Beispielsweise könnte zur Minimierung der Sperrkosten eine Nachschlagetabelle, die im Wesentlichen schreibgeschützt ist, so eingerichtet werden, dass die Sperrung nur auf Tabellenebene erfolgt.|  
|**pgmodctr**|**int**|Gibt 0 zurück.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**keys**|**varbinary(816)**|Liste der Spalten-IDs der Spalten, aus denen der Indexschlüssel besteht.<br /><br /> Gibt NULL zurück.<br /><br /> Verwenden Sie zum Anzeigen der Indexschlüsselspalten [sys.sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md).|  
|**name**|**sysname**|Name des Indexes oder der Statistik. Gibt NULL zurück, wenn **indid** = 0. Ändern Sie die Anwendung so, dass nach einem Heapnamen mit dem Wert NULL gesucht wird.|  
|**statblob**|**image**|Statistik-BLOB (Binary Large Object).<br /><br /> Gibt NULL zurück.|  
|**maxlen**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**rows**|**int**|Zeilenanzahl auf Datenebene auf Grundlage **Indid** = 0 und **Indid** = 1, und der Wert wird für wiederholt **Indid** > 1.|  
  
## <a name="remarks"></a>Hinweise  
 Als reserviert definierte Spalten sollten nicht verwendet werden.  
  
 Die Spalten **dpages**, **reserved**und **used** geben keine genauen Ergebnisse zurück, wenn die Tabelle bzw. der Index Daten in der ROW_OVERFLOW-Zuordnungseinheit enthält. Zudem werden die Seitenanzahlen aller Indizes separat nachverfolgt und nicht für die Basistabelle aggregiert. Verwenden Sie zum Anzeigen der seitenanzahlen die [allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) oder [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) Katalogsichten, oder die [dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) -verwaltungssicht.  
  
 In SQL Server 2000 und früheren Versionen wurden von [!INCLUDE[ssDE](../../includes/ssde-md.md)] Änderungszähler auf Zeilenebene verwaltet. Solche Zähler werden nun auf Spaltenebene verwaltet. Daher wird die **rowmodctr** -Spalte ähnlich wie in früheren Versionen berechnet und erzeugt ähnliche Ergebnisse. Diese sind jedoch nicht genau.  
  
 Wenn Sie mit dem Wert in **rowmodctr** den Zeitpunkt des Statistikupdates bestimmen möchten, können Sie folgende Lösungen in Betracht ziehen:  
  
-   Tun Sie nichts. Der neue **rowmodctr** -Wert hilft Ihnen häufig dabei, den Zeitpunkt für das Statistikupdate zu bestimmen, da das Verhalten weitgehend dem Ergebnis früherer Versionen gleicht.  
  
-   Verwenden Sie AUTO_UPDATE_STATISTICS. Weitere Informationen finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
-   Verwenden Sie ein Zeitlimit, um den Zeitpunkt für das Statistikupdate zu bestimmen. Beispielsweise jede Stunde, jeden Tag oder jede Woche.  
  
-   Verwenden Sie Informationen auf Anwendungsebene, um den Zeitpunkt für das Statistikupdate zu bestimmen. Beispielsweise jedes Mal, wenn sich der Maximalwert einer **identity** -Spalte um mehr als 10.000 ändert oder wenn ein Masseneinfügungsvorgang ausgeführt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Zuordnen von Systemtabellen zu Systemsichten &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
