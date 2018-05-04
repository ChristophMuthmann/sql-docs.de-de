---
title: IHextendedArticleView (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2e0bcc294189f4902fd8d39de230166e6956dd53
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHextendedArticleView** -Sicht macht Informationen zu Artikeln in einer Nicht-SQL Server-Veröffentlichung verfügbar. Diese Sicht wird in der **distribution** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Der eindeutige Bezeichner des Verlegers.|  
|**publication_id**|**int**|Der eindeutige Bezeichner der Veröffentlichung.|  
|**article**|**sysname**|Der Name des Artikels.|  
|**destination_object**|**sysname**|Der Name des veröffentlichten Objekts auf dem Abonnenten.|  
|**source_owner**|**sysname**|Der Besitzer des veröffentlichten Objekts auf dem Verleger.|  
|**source_object**|**sysname**|Der Name des veröffentlichten Objekts auf dem Verleger.|  
|**description**|**nvarchar(255)**|Die Beschreibung des Artikels.|  
|**creation_script**|**nvarchar(255)**|Das Schemaerstellungsskript für den Artikel|  
|**del_cmd**|**nvarchar(255)**|Der für eine DELETE-Anweisung ausgeführte Befehl.|  
|**filter**|**int**|Der Bezeichner für die gespeicherte Prozedur, die die horizontale Partition definiert.|  
|**filter_clause**|**ntext**|Die zum horizontalen Filtern des Artikels verwendete WHERE-Klausel.|  
|**ins_cmd**|**nvarchar(255)**|Der für eine INSERT-Anweisung ausgeführte Befehl.|  
|**pre_creation_cmd**|**tinyint**|Der Vorabbefehl für DROP TABLE, DELETE TABLE oder TRUNCATE:<br /><br /> **0** = None.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCATE.|  
|**status**|**tinyint**|Die Bitmaske der Artikeloptionen und der Status, die das Ergebnis des bitweisen logischen OR von mindestens einem der folgenden Werte sein können:<br /><br /> **1** = Artikel ist aktiv.<br /><br /> **8** = Den Spaltennamen in INSERT-Anweisungen einschließen.<br /><br /> **16** = Parametrisierte Anweisungen verwenden.<br /><br /> **24** = Sowohl den Spaltennamen in INSERT-Anweisungen einschließen als auch parametrisierte Anweisungen verwenden.<br /><br /> Ein aktiver Artikel, der parametrisierte Anweisungen verwendet, würde in dieser Spalte beispielsweise den Wert **17** anzeigen. Der Wert **0** bedeutet, dass der Artikel inaktiv ist und keine zusätzlichen Eigenschaften definiert wurden.|  
|**type**|**tinyint**|Artikeltyp:<br /><br /> **1** = Protokollbasierter Artikel.<br /><br /> **3** = Protokollbasierter Artikel mit manuell erstelltem Filter.<br /><br /> **5** = Protokollbasierter Artikel mit manuell erstellter Sicht.<br /><br /> **7** = Protokollbasierter Artikel mit manuell erstelltem Filter und manuell erstellter Sicht.|  
|**upd_cmd**|**nvarchar(255)**|Der für eine UPDATE-Anweisung ausgeführte Befehl.|  
|**schema_option**|**binary**|Zeigt an, was ausgegeben werden soll. Finden Sie unter [Sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) eine Liste der unterstützten Schemaoptionen.|  
|**dest_owner**|**sysname**|Der Besitzer des veröffentlichten Objekts in der Zieldatenbank.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
