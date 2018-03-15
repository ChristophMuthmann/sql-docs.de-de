---
title: -- (Kommentar) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2cae636f23fc166246b3cf6cb755fde570b3d19c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="---comment-transact-sql"></a>-- (Kommentar) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt vom Benutzer bereitgestellten Text an. Kommentare können in einer eigenen Zeile eingefügt werden, geschachtelt am Ende einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Befehlszeile oder innerhalb einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung. Der Kommentar wird vom Server nicht ausgewertet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>Argumente  
 *text_of_comment*  
 Die Zeichenfolge mit dem Kommentartext.  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie zwei Bindestriche (--) für einzeilige oder geschachtelte Kommentare. Kommentare, die mit -- eingefügt werden, werden mit dem Neue-Zeile-Zeichen begrenzt. Es gibt keine Maximallänge für Kommentare. In der folgenden Tabelle sind die Tastenkombinationen aufgeführt, die Sie verwenden können, um Text als Kommentar zu kennzeichnen oder auszukommentieren.  
  
|Aktion|Standard|  
|------------|--------------|  
|Umwandeln des markierten Texts in einen Kommentar|STRG+K, STRG+C|  
|Kommentierung des ausgewählten Texts entfernen|STRG+K, STRG+U|  
  
 Weitere Informationen zu diesen Tastenkombinationen finden Sie unter [Tastenkombinationen für SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
 Mehrzeilige Kommentare finden Sie unter [Slash Star &#40;Block Comment&#41; &#40;Transact-SQL&#41; (Schrägstrich – (Blockkommentar) (Transact-SQL))](../../t-sql/language-elements/slash-star-comment-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ablaufsteuerungssprache &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  
