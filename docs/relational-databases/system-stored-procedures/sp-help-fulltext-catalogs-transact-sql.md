---
title: Sp_help_fulltext_catalogs (Transact-SQL) | Microsoft Docs
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
- sp_help_fulltext_catalogs_TSQL
- sp_help_fulltext_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs
ms.assetid: 1b94f280-e095-423f-88bc-988c9349d44c
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 59d944a2b33f11f2e6f543364d6e9c870c0c5b6f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpfulltextcatalogs-transact-sql"></a>sp_help_fulltext_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die ID, den Namen, das Stammverzeichnis, den Status und die Anzahl von volltextindizierten Tabellen für den angegebenen Volltextkatalog zurück.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden der [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) stattdessen die Katalogsicht.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_fulltext_catalogs [ @fulltext_catalog_name = ] 'fulltext_catalog_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@fulltext_catalog_name=**] **"***Fulltext_catalog_name***"**  
 Der Name des Volltextkatalogs. *Fulltext_catalog_name* ist **Sysname**. Wenn dieser Parameter ausgelassen wird oder den Wert NULL aufweist, werden Informationen zu allen Volltextkatalogen zurückgegeben, die der aktuellen Datenbank zugeordnet sind.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 In der folgenden Tabelle ist das Resultset dargestellt, das nach **ftcatid**sortiert ist.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|Bezeichner des Volltextkatalogs.|  
|**NAME**|**sysname**|Name des Volltextkatalogs.|  
|**PATH**|**nvarchar(260)**|Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hat diese Klausel keine Auswirkungen.|  
|**STATUS**|**int**|Status der Volltextindexauffüllung des Katalogs:<br /><br /> 0 = Im Leerlauf.<br /><br /> 1 = Vollständiges Auffüllen wird ausgeführt<br /><br /> 2 = Angehalten<br /><br /> 3 = Gedrosselt<br /><br /> 4 = Wird wiederhergestellt<br /><br /> 5 = Herunterfahren<br /><br /> 6 = Inkrementelles Auffüllen wird ausgeführt<br /><br /> 7 = Index wird erstellt<br /><br /> 8 = Datenträger voll Angehalten<br /><br /> 9 = Änderungsprotokollierung<br /><br /> NULL = Benutzer verfügt nicht über VIEW-Berechtigung für den Volltextkatalog, oder Datenbank ist nicht volltextfähig, oder Volltextkomponente ist nicht installiert.|  
|**NUMBER_FULLTEXT_TABLES**|**int**|Anzahl von volltextindizierten Tabellen, die dem Katalog zugeordnet sind.|  
  
## <a name="permissions"></a>Berechtigungen  
 Die Ausführungsberechtigungen werden standardmäßig der **public** -Rolle erteilt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zum `Cat_Desc`-Volltextkatalog zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_catalogs 'Cat_Desc' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [FULLTEXTCATALOGPROPERTY & #40; Transact-SQL & #41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [Sp_help_fulltext_catalogs_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
