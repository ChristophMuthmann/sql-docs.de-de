---
title: Sysarticles (Transact-SQL) | Microsoft Docs
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
- sysarticles
- sysarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticles system table
ms.assetid: 9d9d5d51-6d8f-4e42-84a9-82e58eb0301e
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a89895f89e55daa70ca1357aabba73dc58dffd31
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysarticles-transact-sql"></a>sysarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden in der lokalen Datenbank definierten Artikel. Diese Tabelle wird in der veröffentlichten Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Die Identitätsspalte, die eine eindeutige ID für den Artikel bereitstellt.|  
|**creation_script**|**nvarchar(255)**|Das Schemaskript für den Artikel.|  
|**del_cmd**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Löschungen bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**description**|**nvarchar(255)**|Der Beschreibungseintrag für den Artikel.|  
|**dest_table**|**sysname**|Der Name der Zieltabelle|  
|**filter**|**int**|Die ID der gespeicherten Prozedur, die für horizontales Partitionieren verwendet wird.|  
|**filter_clause**|**ntext**|Die WHERE-Klausel des Artikels, die für horizontales Filtern verwendet wird.|  
|**ins_cmd**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Einfügungen bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**name**|**sysname**|Der mit dem Artikel verknüpfte Name, der innerhalb der Veröffentlichung eindeutig ist.|  
|**OBJID**|**int**|Die Objekt-ID der veröffentlichten Tabelle.|  
|**pubid**|**int**|Die ID der Veröffentlichung, zu der der Artikel gehört.|  
|**pre_creation_cmd**|**tinyint**|Der Voraberstellungsbefehl für DROP TABLE, DELETE TABLE oder TRUNCATE:<br /><br /> **0** = None.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCATE.|  
|**status**|**tinyint**|Die Bitmaske der Artikeloptionen und der Status, die das Ergebnis des bitweisen logischen OR von mindestens einem der folgenden Werte sein können:<br /><br /> **1** = Artikel ist aktiv.<br /><br /> **8** = Den Spaltennamen in INSERT-Anweisungen einschließen.<br /><br /> **16** = Parametrisierte Anweisungen verwenden.<br /><br /> **24** = Sowohl den Spaltennamen in INSERT-Anweisungen einschließen als auch parametrisierte Anweisungen verwenden.<br /><br /> **64** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Ein aktiver Artikel, der parametrisierte Anweisungen verwendet, würde in dieser Spalte beispielsweise den Wert **17** anzeigen. Der Wert **0** bedeutet, dass der Artikel inaktiv ist und keine zusätzlichen Eigenschaften definiert wurden.|  
|**sync_objid**|**int**|Die ID der Tabelle oder Sicht, die die Artikeldefinition darstellt.|  
|**type**|**tinyint**|Der Artikeltyp:<br /><br /> **1** = Protokollbasierter Artikel.<br /><br /> **3** = Protokollbasierter Artikel mit manuell erstelltem Filter.<br /><br /> **5** = Protokollbasierter Artikel mit manuell erstellter Sicht.<br /><br /> **7** = Protokollbasierter Artikel mit manuell erstelltem Filter und manuell erstellter Sicht.<br /><br /> **8** = Ausführung einer gespeicherten Prozedur.<br /><br /> **24** = Ausführung einer serialisierbaren gespeicherten Prozedur.<br /><br /> **32** = gespeicherte Prozedur (Schema only).<br /><br /> **64** = Sicht (Schema only).<br /><br /> **128** = Funktion (Schema only).|  
|**upd_cmd**|**nvarchar(255)**|Der Replikationsbefehlstyp, der zur Replikation von Updates bei Tabellenartikeln verwendet wird. Weitere Informationen finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**schema_option**|**binary(8)**|Die Bitmaske der Schemagenerierungsoptionen für den Artikel, die steuern, welche Teile des Artikelschemas zur Übermittlung an den Abonnenten ausgegeben werden. Weitere Informationen zu den Schemaoptionen finden Sie unter [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|Der Besitzer der Tabelle in der Zieldatenbank|  
|**ins_scripting_proc**|**int**|Die registrierte benutzerdefinierte gespeicherte Prozedur oder das Skript, die/das beim Replizieren einer INSERT-Anweisung ausgeführt wird.|  
|**del_scripting_proc**|**int**|Die registrierte benutzerdefinierte gespeicherte Prozedur oder das Skript, die/das beim Replizieren einer DELETE-Anweisung ausgeführt wird.|  
|**upd_scripting_proc**|**int**|Die registrierte benutzerdefinierte gespeicherte Prozedur oder das Skript, die/das beim Replizieren einer UPDATE-Anweisung ausgeführt wird.|  
|**custom_script**|**nvarchar(2048)**|Die registrierte benutzerdefinierte gespeicherte Prozedur oder das Skript, die/das am Ende des DDL-Triggers ausgeführt wird|  
|**fire_triggers_on_snapshot**|**bit**|Zeigt an, ob replizierte Trigger beim Anwenden der Momentaufnahme ausgeführt werden oder nicht. Es werden folgende Werte unterstützt:<br /><br /> **0** = Trigger werden nicht ausgeführt.<br /><br /> **1** = Trigger werden ausgeführt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [Sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)  
  
  
