---
title: IHarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 53542af40c2d5c477b9fbd2ff21467ffd6af69e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="iharticles-transact-sql"></a>IHarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHarticles** -Systemtabelle enthält eine Zeile für jeden Artikel, die von einer nicht - SQL Server-Verleger mithilfe des aktuellen Verteilers repliziert wird. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Die Identitätsspalte, die eine eindeutige ID für den Artikel bereitstellt.|  
|**name**|**sysname**|Der mit dem Artikel verknüpfte Name, der innerhalb der Veröffentlichung eindeutig ist.|  
|**publication_id**|**smallint**|Die ID der Veröffentlichung, zu der der Artikel gehört.|  
|**table_id**|**int**|Die ID der Tabelle, die von veröffentlicht [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md).|  
|**publisher_id**|**smallint**|Die ID der nicht-SQL Server-Verleger.|  
|**creation_script**|**nvarchar(255)**|Das Schemaskript für den Artikel.|  
|**del_cmd**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Löschungen bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**filter**|**int**|Diese Spalte wird nicht verwendet und ist enthalten, nur um stellen die [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) -Ansicht der **IHarticles** Tabelle, die kompatibel mit der [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) Sicht, die für SQL Server-Artikel ( [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**filter_clause**|**ntext**|Die WHERE-Klausel des Artikels, die zum horizontalen Filtern verwendet wird und in einem standardmäßigen Transact-SQL-Code geschrieben ist, der von anderen als SQL Server-Verlegern interpretiert werden kann.|  
|**ins_cmd**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Einfügungen bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**pre_creation_cmd**|**tinyint**|Der Befehl, der vor dem Anwenden der Anfangsmomentaufnahme ausgeführt wird, wenn auf dem Abonnenten bereits ein Objekt mit dem gleichen Namen vorhanden ist.<br /><br /> **0** = none - ein Befehl nicht ausgeführt wird.<br /><br /> **1** = DROP - die Zieltabelle löschen.<br /><br /> **2** = löschen: Löschen von Daten aus der Zieltabelle.<br /><br /> **3** = TRUNCATE - die Zieltabelle abgeschnitten.|  
|**status**|**tinyint**|Die Bitmaske der Artikeloptionen und der Status, die das Ergebnis des bitweisen logischen OR von mindestens einem der folgenden Werte sein können:<br /><br /> **0** = keine zusätzlichen Eigenschaften.<br /><br /> **1** = aktiv.<br /><br /> **8** = Den Spaltennamen in INSERT-Anweisungen einschließen.<br /><br /> **16** = Parametrisierte Anweisungen verwenden.<br /><br /> Ein aktiver Artikel, der parametrisierte Anweisungen verwendet, würde in dieser Spalte beispielsweise den Wert 17 anzeigen. Der Wert 0 gibt an, dass der Artikel inaktiv ist und keine zusätzlichen Eigenschaften definiert wurden.|  
|**type**|**tinyint**|Der Artikeltyp:<br /><br /> **1** = Protokollbasierter Artikel.|  
|**upd_cmd**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Updates bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**schema_option**|**binary(8)**|Das Bitmuster der Schemagenerierungsoption für den angegebenen Artikel, die das Ergebnis des bitweisen logischen OR von mindestens einem der folgenden Werte sein kann:<br /><br /> **0 x 00** = deaktiviert die Skripterstellung durch den Momentaufnahme-Agent und verwendet das bereitgestellte Skript CreationScript.<br /><br /> **0 x 01** = generiert die objekterstellung (CREATE TABLE, CREATE PROCEDURE usw.).<br /><br /> **0 x 10** = generiert einen entsprechenden gruppierten Index.<br /><br /> **0 x 40** = generiert entsprechende nicht gruppierte Indizes.<br /><br /> **0 x 80** = enthält die deklarierte referenziellen Integrität für die Primärschlüssel.<br /><br /> **0 x 1000** = repliziert auf Spaltenebene Sortierung. Hinweis: Diese Option ist standardmäßig für Oracle-Verleger, damit Groß-/Kleinschreibung bei Vergleichen werden festgelegt.<br /><br /> **0 x 4000** = repliziert eindeutige Schlüssel, wenn auf einem Tabellenartikel definiert.<br /><br /> **0 x 8000** = repliziert einen Primärschlüssel und eindeutige Schlüssel eines Tabellenartikels als Einschränkungen, die mithilfe von ALTER TABLE-Anweisungen.|  
|**dest_owner**|**sysname**|Der Besitzer der Tabelle in der Zieldatenbank|  
|**dest_table**|**sysname**|Der Name der Zieltabelle|  
|**tablespace_name**|**nvarchar(255)**|Identifiziert den von der Protokollierungstabelle für den Artikel verwendeten Tabellenbereich.|  
|**OBJID**|**int**|Diese Spalte wird nicht verwendet und ist enthalten, nur um stellen die [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) -Ansicht der **IHarticles** Tabelle, die kompatibel mit der [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) Sicht, die für SQL Server-Artikel ( [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**sync_objid**|**int**|Diese Spalte wird nicht verwendet und ist enthalten, nur um stellen die [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) -Ansicht der **IHarticles** Tabelle, die kompatibel mit der [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) Sicht, die für SQL Server-Artikel ( [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**description**|**nvarchar(255)**|Der Beschreibungseintrag für den Artikel.|  
|**publisher_status**|**int**|Wird verwendet, um anzugeben, ob die Sicht, die den veröffentlichten Artikel definiert durch den Aufruf definiert wurde [Sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md).<br /><br /> **0** = [Sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) aufgerufen wurde.<br /><br /> **1** = [Sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) nicht aufgerufen wurde.|  
|**article_view_owner**|**nvarchar(255)**|Der Besitzer des Synchronisierungsobjekts auf dem Verleger, das vom Protokolllese-Agent verwendet wird.|  
|**article_view**|**nvarchar(255)**|Das Synchronisierungsobjekts auf dem Verleger, das vom Protokolllese-Agent verwendet wird.|  
|**ins_scripting_proc**|**int**|Diese Spalte wird nicht verwendet und ist enthalten, nur um stellen die [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) -Ansicht der **IHarticles** Tabelle, die kompatibel mit der [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) Sicht, die für SQL Server-Artikel ( [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**del_scripting_proc**|**int**|Diese Spalte wird nicht verwendet und ist enthalten, nur um stellen die [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) -Ansicht der **IHarticles** Tabelle, die kompatibel mit der [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) Sicht, die für SQL Server-Artikel ( [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**upd_scripting_proc**|**int**|Diese Spalte wird nicht verwendet und ist enthalten, nur um stellen die [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) -Ansicht der **IHarticles** Tabelle, die kompatibel mit der [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) Sicht, die für SQL Server-Artikel ( [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**custom_script**|**int**|Diese Spalte wird nicht verwendet und ist enthalten, nur um stellen die [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) -Ansicht der **IHarticles** Tabelle, die kompatibel mit der [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) Sicht, die für SQL Server-Artikel ( [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**fire_triggers_on_snapshot**|**bit**|Diese Spalte wird nicht verwendet und ist enthalten, nur um stellen die [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) -Ansicht der **IHarticles** Tabelle, die kompatibel mit der [Sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) Sicht, die für SQL Server-Artikel ( [Sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**instance_id**|**int**|Identifiziert die aktuelle Instanz des Artikelprotokolls für die veröffentlichte Tabelle.|  
|**use_default_datatypes**|**bit**|Gibt an, ob der Artikel standardmäßige datentypzuordnungen verwendet. der Wert **1** gibt an, dass die standardmäßigen datentypzuordnungen verwendet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [Sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
