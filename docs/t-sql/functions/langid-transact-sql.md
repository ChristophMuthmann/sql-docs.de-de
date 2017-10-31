---
title: '@@LANGID (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@LANGID'
- '@@LANGID_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- languages [SQL Server], current in use
- '@@LANGID function'
- current language in use
- ID for language in use
- local language IDs [SQL Server]
ms.assetid: 7a0fc089-2a48-4a81-9d78-2aaedb540d37
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 39d66c56a3cb0b21d8955dfe56dc5083472ec372
ms.contentlocale: de-de
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40langid-transact-sql"></a>& #x 40; & #x 40; LANGID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die lokale Sprachen-ID der zurzeit verwendeten Sprache zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@LANGID  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **smallint**  
  
## <a name="remarks"></a>Hinweise  
 Führen Sie zum Anzeigen von Informationen zu spracheinstellungen, einschließlich der Sprachen-ID-Nummern **Sp_helplanguage** ohne einen Parameter angegeben.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Sprache für die aktuelle Sitzung auf `Italian` festgelegt und dann `@@LANGID` zur Rückgabe der ID für Italienisch verwendet.  
  
```  
SET LANGUAGE 'Italian'  
SELECT @@LANGID AS 'Language ID'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Changed language setting to Italiano.  
Language ID  
-----------  
6            
```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LANGUAGE &#40; Transact-SQL &#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [Sp_helplanguage &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)  
  
  

