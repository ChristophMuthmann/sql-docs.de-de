---
title: SET-Sprache (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_LANGUAGE_TSQL
- SET LANGUAGE
dev_langs:
- TSQL
helpviewer_keywords:
- LANGUAGE option
- languages [SQL Server], setting language
- SET LANGUAGE statement
- options [SQL Server], date
- default languages
ms.assetid: 0ec0e5cf-e115-4be9-a0db-e65837d6fa45
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f334049b696685b366c36484857d1340853a4b15
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-language-transact-sql"></a>SET LANGUAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Gibt die Sprachumgebung für die Sitzung an. Die sitzungssprache bestimmt die **"DateTime"** Uhrzeitformate sowie systemmeldungen.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET LANGUAGE { [ N ] 'language' | @language_var }   
```  
  
## <a name="arguments"></a>Argumente  
 [**N**]**"***Sprache***"**  |   **@**   *language_var*  
 Der Name der Sprache ist, wie er in gespeichert [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md). Dieses Argument kann in Unicode oder in DBCS, das in Unicode konvertiert wurde, dargestellt sein. Verwenden Sie zum Angeben einer anderen Sprache in Unicode **N'***Sprache***"**. Wenn als Variable angegeben wird, muss die Variable **Sysname**.  
  
## <a name="remarks"></a>Hinweise  
 Die Einstellung von SET LANGUAGE wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 SET LANGUAGE legt implizit die Einstellung der [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Standardsprache auf `Italian` festgelegt, der Monatsname angezeigt, zurück zu `us_english` gewechselt und der Monatsname erneut angezeigt.  
  
```  
DECLARE @Today DATETIME;  
SET @Today = '12/5/2007';  
  
SET LANGUAGE Italian;  
SELECT DATENAME(month, @Today) AS 'Month Name';  
  
SET LANGUAGE us_english;  
SELECT DATENAME(month, @Today) AS 'Month Name' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 ["syslanguages"](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [Sp_helplanguage &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
