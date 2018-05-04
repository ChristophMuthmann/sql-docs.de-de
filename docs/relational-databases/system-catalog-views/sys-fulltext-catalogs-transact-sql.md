---
title: Sys. fulltext_catalogs (Transact-SQL) | Microsoft Docs
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
- sys.fulltext_catalogs_TSQL
- sys.fulltext_catalogs
- fulltext_catalogs
- fulltext_catalogs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_catalogs catalog view
ms.assetid: cf1489ff-4819-41fa-a62a-4ed797a16207
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 314fa09550ae3d9f5588dc2f382d6e5eba08e169
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysfulltextcatalogs-transact-sql"></a>sys.fulltext_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Volltextkatalog.  
  
> [!NOTE]  
>  Die folgenden Spalten werden in einer zukünftigen Version von entfernt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **Data_space_id**, **File_id**, und **Pfad**. Verwenden Sie diese Spalten nicht für Neuentwicklungen, und planen Sie so bald wie möglich die Änderung von Anwendungen, in denen diese Spalten derzeit verwendet werden.  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**int**|ID des Volltextkatalogs. Diese ID ist innerhalb aller Volltextkataloge in der Datenbank eindeutig.|  
|name|**sysname**|Name des Katalogs. Ist in der Datenbank eindeutig.|  
|path|**nvarchar(260)**|Name des Katalogverzeichnisses im Dateisystem.|  
|is_default|**bit**|Der Standard-Volltextkatalog.<br /><br /> True = Wird als Standard verwendet.<br /><br /> False = Wird nicht als Standard verwendet.|  
|is_accent_sensitivity_on|**bit**|Einstellung des Katalogs für die Unterscheidung nach Akzent.<br /><br /> True = Unterscheidung nach Akzent ist aktiviert.<br /><br /> False = Unterscheidung nach Akzent ist nicht aktiviert.|  
|data_space_id|**int**|Dateigruppe, in der dieser Katalog erstellt wurde.|  
|file_id|**int**|Datei-ID der mit dem Katalog verbundenen Volltextdatei.|  
|principal_id|**int**|ID des Datenbankprinzipals, der den Volltextkatalog besitzt.|  
|is_importing|**bit**|Gibt an, ob der Volltextkatalog importiert wird:<br /><br /> 1 = Der Katalog wird importiert.<br /><br /> 2 = Der Katalog wird nicht importiert.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Erstellen Sie FULLTEXT CATALOG & #40; Transact-SQL & #41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  
