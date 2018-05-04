---
title: Sp_help_fulltext_catalogs_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_cursor
- sp_help_fulltext_catalogs_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs_cursor
ms.assetid: d44478d1-0cc4-415e-9d1a-6dccb64674fa
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 99b95392687ef711c0dc3cf6021fba5ef4d71273
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpfulltextcatalogscursor-transact-sql"></a>sp_help_fulltext_catalogs_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verwendet einen Cursor, um die ID, den Namen, das Stammverzeichnis, den Status und die Anzahl der volltextindizierten Tabellen für den angegebenen Volltextkatalog zurückzugeben.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden der [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) stattdessen die Katalogsicht.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_fulltext_catalogs_cursor [ @cursor_return= ] @cursor_variable OUTPUT ,   
     [ @fulltext_catalog_name = ] 'fulltext_catalog_name'   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@cursor_return=**] *@cursor_variable* **AUSGABE**  
 Bezeichnet die Ausgabevariable vom Typ **cursor**. Bei dem Cursor handelt es sich um einen schreibgeschützten, bildlauffähigen, dynamischen Cursor.  
  
 [  **@fulltext_catalog_name=**] **"***Fulltext_catalog_name***"**  
 Der Name des Volltextkatalogs. *Fulltext_catalog_name* ist **Sysname**. Wenn dieser Parameter ausgelassen wird oder den Wert NULL aufweist, werden Informationen zu allen Volltextkatalogen zurückgegeben, die der aktuellen Datenbank zugeordnet sind.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|Bezeichner des Volltextkatalogs.|  
|**NAME**|**sysname**|Name des Volltextkatalogs.|  
|**PATH**|**nvarchar(260)**|Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hat diese Klausel keine Auswirkungen.|  
|**STATUS**|**int**|Status der Volltextindexauffüllung des Katalogs:<br /><br /> 0 = Im Leerlauf.<br /><br /> 1 = Vollständiges Auffüllen wird ausgeführt<br /><br /> 2 = Angehalten<br /><br /> 3 = Gedrosselt<br /><br /> 4 = Wird wiederhergestellt<br /><br /> 5 = Herunterfahren<br /><br /> 6 = Inkrementelles Auffüllen wird ausgeführt<br /><br /> 7 = Index wird erstellt<br /><br /> 8 = Datenträger voll Angehalten<br /><br /> 9 = Änderungsprotokollierung|  
|**NUMBER_FULLTEXT_TABLES**|**int**|Anzahl von volltextindizierten Tabellen, die dem Katalog zugeordnet sind.|  
  
## <a name="permissions"></a>Berechtigungen  
 Die Ausführungsberechtigungen erhält standardmäßig die **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zum `Cat_Desc`-Volltextkatalog zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_catalogs_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>Siehe auch  
 [FULLTEXTCATALOGPROPERTY & #40; Transact-SQL & #41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
