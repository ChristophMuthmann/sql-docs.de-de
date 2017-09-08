---
title: --(Kommentar) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a03aff79db25c07fc828145177e29196405a9264
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="---comment-transact-sql"></a>-- (Kommentar) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt vom Benutzer bereitgestellten Text an. Kommentare können in einer eigenen Zeile eingefügt werden, geschachtelt am Ende einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Befehlszeile oder innerhalb einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung. Der Kommentar wird vom Server nicht ausgewertet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>Argumente  
 *text_of_comment*  
 Die Zeichenfolge mit dem Kommentartext.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie zwei Bindestriche (--) für einzeilige oder geschachtelte Kommentare. Kommentare, die mit -- eingefügt werden, werden mit dem Neue-Zeile-Zeichen begrenzt. Es gibt keine Maximallänge für Kommentare. In der folgenden Tabelle sind die Tastenkombinationen aufgeführt, die Sie verwenden können, um Text als Kommentar zu kennzeichnen oder auszukommentieren.  
  
|Aktion|Standard|  
|------------|--------------|  
|Umwandeln des markierten Texts in einen Kommentar|STRG+K, STRG+C|  
|Kommentierung des ausgewählten Texts entfernen|STRG+K, STRG+U|  
  
 Weitere Informationen zu diesen Tastenkombinationen finden Sie unter [SQL Server Management Studio Keyboard Shortcuts](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
 Mehrzeilige Kommentare finden Sie unter [Schrägstrich Stern Kommentar &#40; Transact-SQL &#41; ](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Kommentarzeichen -- verwendet.  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Control-of-Flow-Sprache &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  

