---
title: READTEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2c501fe8ea8146b4b2ec6e138f72fc2604b4b374
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Liest **Text**, **Ntext**, oder **Image** Werte aus einer **Text**, **Ntext**, oder **Bild**  -Spalte, beginnend bei einem angegebenen Offset und die angegebene Anzahl von Bytes zu lesen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwenden der [TEILZEICHENFOLGE](../../t-sql/functions/substring-transact-sql.md) stattdessen-Funktion.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Tabelle* **.** *Spalte*  
 Dies ist der Name einer Tabelle und Spalte, aus der gelesen wird. Tabellen- und Spaltennamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Die Angabe der Tabellen- und Spaltennamen ist erforderlich, wohingegen die Angabe des Datenbank- und Besitzernamens optional ist.  
  
 *text_ptr*  
 Ein gültiger Textzeiger. *Text_ptr* muss **binary(16)**.  
  
 *Offset*  
 Ist die Anzahl der Bytes (bei der **Text** oder **Image** Datentypen verwendet werden) oder Zeichen (bei der **Ntext** -Datentyp verwendet wird,) überspringen vor Beginn der Lesen**Text**, **Image**, oder **Ntext** Daten.  
  
 *Größe*  
 Ist die Anzahl der Bytes (bei der **Text** oder **Image** Datentypen verwendet werden) oder Zeichen (bei der **Ntext** -Datentyp verwendet wird) der zu lesenden Daten. Wenn *Größe* ist 0, 4 KB Daten gelesen wird.  
  
 HOLDLOCK  
 Bewirkt, dass der Textwert bis zum Ende der Transaktion gesperrt wird und nur gelesen werden kann. Andere Benutzer können den Wert dann lesen, aber nicht ändern.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der [TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md) Funktion zum Abrufen gültiger *Text_ptr* Wert. TEXTPTR gibt einen Zeiger auf die **Text**, **Ntext**, oder **Image** Spalte in der angegebenen Zeile oder auf die **Text**, **Ntext** , oder **Image** Spalte in der letzten Zeile, die von der Abfrage zurückgegeben werden, wenn mehr als eine Zeile zurückgegeben wird. Da TEXTPTR eine 16 Bytes große binäre Zeichenfolge zurückgibt, ist es empfehlenswert, eine lokale Variable für den Textzeiger zu deklarieren und dann die Variable mit READTEXT einzusetzen. Weitere Informationen zum Deklarieren einer lokalen Variablen finden Sie unter [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt es möglicherweise Textzeiger in Zeilen, die jedoch ungültig sind. Weitere Informationen zu den **Text in Zeile** finden Sie unter [Sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Weitere Informationen zu den Textzeiger, finden Sie unter [Sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 Der Wert für den @@TEXTSIZE Funktion ersetzt die Größe, die für READTEXT angegebene, wenn er kleiner als die für READTEXT angegebene Größe ist. Der @@TEXTSIZE Funktion gibt den Grenzwert für die Anzahl der Datenbytes, die von der SET TEXTSIZE-Anweisung zurückgegeben werden. Weitere Informationen zum Festlegen der sitzungseinstellung für TEXTSIZE finden Sie unter [SET TEXTSIZE &#40; Transact-SQL &#41; ](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 READTEXT-Berechtigungen werden standardmäßig an Benutzer mit SELECT-Berechtigungen für die angegebene Tabelle vergeben. Die Berechtigungen sind übertragbar, wenn SELECT-Berechtigungen übertragen werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Zeichen 2 bis 26 der `pr_info`-Spalte in der `pub_info`-Tabelle gelesen.  
  
> [!NOTE]  
>  Um dieses Beispiel auszuführen, müssen Sie installieren die **Pubs** -Beispieldatenbank.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [UPDATETEXT (Transact-SQL)](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)  
  
  
