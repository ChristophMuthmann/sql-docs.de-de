---
title: Sysextendedarticlesview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysextendedarticlesview_TSQL
- sysextendedarticlesview
dev_langs:
- TSQL
helpviewer_keywords:
- sysextendedarticlesview view
ms.assetid: 8bdd22f7-c268-49b6-820c-3fe603feb128
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7600ee20683846aa5a2defb676d10daea0038d7d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysextendedarticlesview-transact-sql"></a>sysextendedarticlesview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **Sysextendedarticlesview** Ansicht enthält Informationen zu veröffentlichten Artikeln. Diese Sicht wird in der distribution-Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Die Identitätsspalte, die eine eindeutige ID für den Artikel bereitstellt.|  
|**creation_script**|**nvarchar(255)**|Das Schemaerstellungsskript für den Artikel|  
|**del_cmd**|**nvarchar(255)**|Der bei einer DELETE-Anweisung auszuführende Befehl, wird sonst aus dem Protokoll konstruiert|  
|**description**|**nvarchar(255)**|Der Beschreibungseintrag für den Artikel.|  
|**dest_table**|**nvarchar(128)**|Der Name der Zieltabelle|  
|**filter**|**int**|Der Objektbezeichner der gespeicherten Prozedur, die für horizontale Partitionen verwendet wird|  
|**filter_clause**|**ntext**|Die WHERE-Klausel des Artikels, die für horizontales Filtern verwendet wird.|  
|**ins_cmd**|**nvarchar(255)**|Der bei einer INSERT-Anweisung auszuführende Befehl|  
|**name**|**nvarchar(128)**|Der mit dem Artikel verknüpfte Name, der innerhalb der Veröffentlichung eindeutig ist.|  
|**OBJID**|**int**|Die Objekt-ID der veröffentlichten Tabelle.|  
|**pubid**|**int**|Die ID der Veröffentlichung, zu der der Artikel gehört.|  
|**pre_creation_cmd**|**tinyint**|Der Voraberstellungsbefehl für DROP TABLE, DELETE TABLE oder TRUNCATE:<br /><br /> **0** = None.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCATE.|  
|**status**|**int**|Die Bitmaske der Artikeloptionen und der Status, die das Ergebnis des bitweisen logischen OR von mindestens einem der folgenden Werte sein können:<br /><br /> **1** = Artikel ist aktiv.<br /><br /> **8** = Den Spaltennamen in INSERT-Anweisungen einschließen.<br /><br /> **16** = Parametrisierte Anweisungen verwenden.<br /><br /> **24** = Sowohl den Spaltennamen in INSERT-Anweisungen einschließen als auch parametrisierte Anweisungen verwenden.<br /><br /> Ein aktiver Artikel, der parametrisierte Anweisungen verwendet, würde in dieser Spalte beispielsweise den Wert 17 anzeigen. Der Wert 0 gibt an, dass der Artikel inaktiv ist und keine zusätzlichen Eigenschaften definiert wurden.|  
|**sync_objid**|**int**|Die ID der Tabelle oder Sicht, die die Artikeldefinition darstellt.|  
|**type**|**tinyint**|Der Artikeltyp:<br /><br /> **1** = Protokollbasierter Artikel.<br /><br /> **3** = Protokollbasierter Artikel mit manuell erstelltem Filter.<br /><br /> **5** = Protokollbasierter Artikel mit manuell erstellter Sicht.<br /><br /> **7** = Protokollbasierter Artikel mit manuell erstelltem Filter und manuell erstellter Sicht.|  
|**upd_cmd**|**nvarchar(255)**|Der bei einer UPDATE-Anweisung auszuführende Befehl, wird sonst aus dem Protokoll konstruiert|  
|**schema_option**|**binary**|Gibt an, welche Eigenschaften des veröffentlichten Objekts in der Momentaufnahme ausgegeben wurden.  Eine Liste der unterstützten Schemaoptionen finden Sie [Sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**nvarchar(128)**|Der Besitzer der Tabelle in der Zieldatenbank|  
|**ins_scripting_proc**|**int**|Der Objektbezeichner der benutzerdefinierten gespeicherten Prozedur oder des Skripts, die bzw. das beim Replizieren einer INSERT-Anweisung ausgeführt wird|  
|**del_scripting_proc**|**int**|Der Objektbezeichner der benutzerdefinierten gespeicherten Prozedur oder des Skripts, die bzw. das beim Replizieren einer DELETE-Anweisung ausgeführt wird|  
|**upd_scripting_proc**|**int**|Der Objektbezeichner der benutzerdefinierten gespeicherten Prozedur oder des Skripts, die bzw. das beim Replizieren einer UPDATE-Anweisung ausgeführt wird|  
|**custom_script**|**int**|Der Objektbezeichner des benutzerdefinierten Skripts oder der Prozedur, die bzw. das nach Ausführung eines DDL-Triggers ausgeführt wird|  
|**fire_triggers_on_snapshot**|**int**|Gibt an, ob replizierte Trigger beim Anwenden der Momentaufnahme ausgeführt werden. Es werden folgende Werte unterstützt:<br /><br /> **0** = Trigger werden nicht ausgeführt.<br /><br /> **1** = Trigger werden ausgeführt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sysarticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
