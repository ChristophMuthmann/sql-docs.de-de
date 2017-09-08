---
title: SQL Server-Sortierungsname (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7265f4efe0d790ab61e4e522af83d6b91b710a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server-Sortierungsname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Eine einzelne Zeichenfolge, die den Sortierungsnamen für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierung angibt.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt Windows-Sortierungen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt darüber hinaus eine begrenzte Anzahl (<80) von Sortierungen, die als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierungen bezeichnet werden und entwickelt wurden, bevor Windows-Sortierungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wurden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierungen werden weiterhin aus Gründen der Abwärtskompatibilität unterstützt, sollten für neue Entwicklungen jedoch nicht verwendet werden. Weitere Informationen zu Windows-Sortierungen finden Sie unter [Windows-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
<SQL_collation_name> :: =   
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>  
  
<ComparisonStyle> ::=  
_CaseSensitivity_AccentSensitivity | _BIN  
```  
  
## <a name="arguments"></a>Argumente  
 *SortRules*  
 Eine Zeichenfolge, die das Alphabet oder die Sprache, dessen oder deren Sortierungsregeln beim Angeben der Wörterbuchsortierung angewendet werden, identifiziert. Beispiele sind Latin1_General oder Polish.  
  
 **Pref**  
 Gibt an, dass Großschreibung bevorzugt wird. Selbst wenn bei Vergleichen wird die Groß-/Kleinschreibung nicht beachtet wird, stehen Großbuchstaben in der Sortierreihenfolge vor ihren entsprechenden Kleinbuchstaben, wenn es davon abgesehen keine Unterschiede gibt.  
  
 *Codepage*  
 Gibt eine ein- bis vierstellige Zahl an, die die von der Sortierung verwendete Codepage identifiziert. **CP1** gibt Codepage 1252, für alle anderen Code die vollständige Codepagenummer Seiten angegeben ist. Beispielsweise **CP1251** gibt Codepage 1251 und **CP850** gibt Codepage 850 an.  
  
 *CaseSensitivity*  
 **CI** gibt Groß-/Kleinschreibung, **CS** gibt Groß-/Kleinschreibung beachtet.  
  
 *AccentSensitivity*  
 **AI** gibt Unterscheidung nach Akzent **AS** gibt an, nach Akzent unterschieden wird.  
  
 **"BIN"**  
 Gibt die zu verwendende binäre Sortierreihenfolge an.  
  
## <a name="remarks"></a>Hinweise  
 Führen Sie die folgende Abfrage aus, um die vom Server unterstützten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierungen aufzulisten.  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

>  [!NOTE]  
>  Verwenden Sie für Sortierreihenfolge Order ID 80 die Windows-Sortierungen mit der Codepage des 1250 und Binärreihenfolge. Beispiel: Albanian_BIN, Croatian_BIN, Czech_BIN, Romanian_BIN, Slovak_BIN, Slovenian_BIN.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Konstanten &#40; Transact-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Table &#40; Transact-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  

