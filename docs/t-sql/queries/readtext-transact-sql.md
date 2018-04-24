---
title: READTEXT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- READTEXT_TSQL
- READTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- column reading [SQL Server]
- READTEXT statement
- reading columns
ms.assetid: 91b69853-1381-4306-8343-afdb73105738
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1cfbec25af14a46c36989428102c2243a22baaa2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Liest **text**-, **ntext**- oder **image**-Werte aus einer **text**-, **ntext**- oder **image**-Spalte, wobei bei einem angegebenen Offset begonnen und die angegebene Anzahl von Bytes gelesen wird.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen die Funktion [SUBSTRING](../../t-sql/functions/substring-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>Argumente  
 *table* **.** *column*  
 Dies ist der Name einer Tabelle und Spalte, aus der gelesen wird. Tabellen- und Spaltennamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Die Angabe der Tabellen- und Spaltennamen ist erforderlich, wohingegen die Angabe des Datenbank- und Besitzernamens optional ist.  
  
 *text_ptr*  
 Ein gültiger Textzeiger. *text_ptr* muss vom Datentyp **binary(16)** sein.  
  
 *offset*  
 Die Anzahl von Bytes (beim Verwenden der Datentypen **text** oder **image**) oder Zeichen (beim Verwenden des Datentyps **ntext**), die ausgelassen werden sollen, bevor mit dem Lesen der **text**-, **image**- oder **ntext**-Daten begonnen wird.  
  
 *size*  
 Die Anzahl von Bytes (beim Verwenden der Datentypen **text** oder **image**) oder Zeichen (beim Verwenden des Datentyps **ntext**) der zu lesenden Daten. Wenn *size* = 0 ist, werden 4 KB Daten gelesen.  
  
 HOLDLOCK  
 Bewirkt, dass der Textwert bis zum Ende der Transaktion gesperrt wird und nur gelesen werden kann. Andere Benutzer können den Wert dann lesen, aber nicht ändern.  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie die [TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)-Funktion, um einen gültigen *text_ptr*-Wert abzurufen. TEXTPTR gibt einen Zeiger auf die **text**-, **ntext**- oder **image**-Spalte in der angegebenen Zeile oder auf die **text**-, **ntext**- oder **image**-Spalte der letzten Zeile zurück, die von der Abfrage zurückgegeben wird, wenn mehrere Zeilen zurückgegeben werden. Da TEXTPTR eine 16 Bytes große binäre Zeichenfolge zurückgibt, ist es empfehlenswert, eine lokale Variable für den Textzeiger zu deklarieren und dann die Variable mit READTEXT einzusetzen. Weitere Informationen zum Deklarieren einer lokalen Variablen finden Sie unter [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt es möglicherweise Textzeiger in Zeilen, die jedoch ungültig sind. Weitere Informationen zur Option **text in row** finden Sie unter [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Weitere Informationen dazu, wie Textzeiger ungültig gemacht werden können, finden Sie unter [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 Der Wert der @@TEXTSIZE-Funktion setzt die für READTEXT angegebene Größe außer Kraft, wenn diese geringer als die für READTEXT angegebene Größe ist. Die @@TEXTSIZE-Funktion gibt die Beschränkung der Anzahl zurückzugebender Bytes an, die von der SET TEXTSIZE-Anweisung festgelegt wurde. Weitere Informationen zum Festlegen der Sitzungseinstellung für TEXTSIZE finden Sie unter [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 READTEXT-Berechtigungen werden standardmäßig an Benutzer mit SELECT-Berechtigungen für die angegebene Tabelle vergeben. Die Berechtigungen sind übertragbar, wenn SELECT-Berechtigungen übertragen werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Zeichen 2 bis 26 der `pr_info`-Spalte in der `pub_info`-Tabelle gelesen.  
  
> [!NOTE]  
>  Um dieses Beispiel auszuführen, müssen Sie die **pubs**-Beispieldatenbank installieren.  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr INNER JOIN publishers p  
      ON pr.pub_id = p.pub_id   
      AND p.pub_name = 'New Moon Books'  
READTEXT pub_info.pr_info @ptrval 1 25;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [UPDATETEXT (Transact-SQL)](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)  
  
  
