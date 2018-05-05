---
title: Sp_help_fulltext_catalog_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalog_components_TSQL
- sp_help_fulltext_catalog_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalog_components
ms.assetid: fbd6a3d4-6a4c-42a2-bff8-2a5eb0745e47
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ccb6be6ad129fca1de84da014fb60cf3843bf15a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpfulltextcatalogcomponents-transact-sql"></a>sp_help_fulltext_catalog_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Liste aller Komponenten (Filter, Wörtertrennung und Protokollhandler) zurück, die für alle Volltextkataloge in der aktuellen Datenbank verwendet werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_fulltext_catalog_components  
```  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Volltext-Katalognamen**|**int**|Name des Volltextkatalogs.|  
|**Volltextkatalog-id**|**sysname**|ID des Volltextkatalogs.|  
|**componenttype**|**sysname**|Typ der Komponente. Einer der folgenden Typen:<br /><br /> Filter<br /><br /> Protokollhandler<br /><br /> Wörtertrennung|  
|**componentname**|**sysname**|Name der Komponente.|  
|**clsid**|**uniqueidentifier**|Klassenbezeichner der Komponente.|  
|**fullpath**|**nvarchar(256)**|Pfad zum Speicherort der Komponente.<br /><br /> NULL = Aufrufer ist kein Mitglied der festen Serverrolle **serveradmin** .|  
|**version**|**nvarchar(30)**|Version der Komponente.|  
|**Hersteller**|**sysname**|Name des Herstellers der Komponente.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [Volltextsuche und semantische Suche von gespeicherten Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [sys.fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [Sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)  
  
  
