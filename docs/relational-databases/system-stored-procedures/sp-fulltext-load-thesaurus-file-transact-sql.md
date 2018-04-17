---
title: Sp_fulltext_load_thesaurus_file (Transact-SQL) | Microsoft Docs
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
- sp_fulltext_load_thesaurus_file
- sp_fulltext_load_thesaurus_file_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_load_thesaurus_file
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], editing
ms.assetid: 73a309c3-6d22-42dc-a6fe-8a63747aa2e4
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6001b06b6caef3819b6243b7029a082f19257228
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spfulltextloadthesaurusfile-transact-sql"></a>sp_fulltext_load_thesaurus_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Veranlasst die Serverinstanz, die Daten aus der Thesaurusdatei zu analysieren und zu laden, die der Sprache des angegebenen Gebietsschemabezeichners (Locale Identifier, LCID) entspricht. Diese gespeicherte Prozedur bietet sich zur Anwendung nach dem Update einer Thesaurusdatei an. Ausführen von **Sp_fulltext_load_thesaurus_file** wird Neukompilierung der Volltextabfragen, die den Thesaurus mit der angegebenen LCID verwenden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_fulltext_load_thesaurus_file lcid [ , @loadOnlyIfNotLoaded  = action ]   
```  
  
## <a name="arguments"></a>Argumente  
 *lcid*  
 Eine ganze Zahl, mit der der Gebietsschemabezeichner (LCID) der Sprache zugeordnet wird, für die Sie die Thesaurus-XML-Definition laden möchten. Verwenden Sie zum Abrufen der LCIDs von Sprachen, die auf einer Serverinstanz verfügbar sind die [Sys. fulltext_languages &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) -Katalogsicht angezeigt.  
  
 **@loadOnlyIfNotLoaded** = *Aktion*  
 Gibt an, ob die Thesaurusdatei in die internen Thesaurustabellen geladen wird, auch wenn sie bereits geladen wurde. *Aktion* ist einer von:  
  
|Wert|Definition|  
|-----------|----------------|  
|**0**|Die Thesaurusdatei wird geladen, auch wenn sie bereits geladen wurde. Dies ist das Standardverhalten des **Sp_fulltext_load_thesaurus_file**.|  
|1|Die Thesaurusdatei wird nur geladen, wenn Sie noch nicht geladen wurde.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Thesaurusdateien werden automatisch von Volltextabfragen geladen, die den Thesaurus verwenden. Um diese erstmaligen Leistungseinbußen auf Volltextabfragen zu vermeiden, sollten Sie ausführen **Sp_fulltext_load_thesaurus_file**.  
  
 Verwendung [Sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)"**Update_languages**" die Liste der mit der Volltextsuche registrierte Sprachenliste zu aktualisieren.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder der Systemadministrator kann führen Sie die **Sp_fulltext_load_thesaurus_file** gespeicherte Prozedur.  
  
 Nur Systemadministratoren können Thesaurusdateien aktualisieren, ändern und löschen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-load-a-thesaurus-file-even-if-it-is-already-loaded"></a>A. Laden einer Thesaurusdatei, auch wenn sie bereits geladen wurde  
 Im folgenden Beispiel wird die Thesaurusdatei für die englische Sprache analysiert und geladen.  
  
```  
EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
GO  
```  
  
### <a name="b-load-a-thesaurus-file-only-if-it-is-not-yet-loaded"></a>B. Laden einer Thesaurusdatei nur dann, wenn Sie noch nicht geladen wurde  
 Im folgenden Beispiel wird die Thesaurusdatei für die arabische Sprache nur dann analysiert und geladen, wenn sie noch nicht geladen wurde.  
  
```  
EXEC sys.sp_fulltext_load_thesaurus_file 1025, @loadOnlyIfNotLoaded = 1;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
  
