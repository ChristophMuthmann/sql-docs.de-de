---
title: TEXTPTR (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TEXTPTR_TSQL
- TEXTPTR
dev_langs:
- TSQL
helpviewer_keywords:
- TEXTPTR function
- viewing text pointer values
- text-pointer values
- displaying text pointer values
ms.assetid: 2672b8cb-f747-46f3-9358-9b49b3583b8e
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 137f5200829916c69c2cf8fcae4c8490e48b2b6e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="text-and-image-functions---textptr-transact-sql"></a>Text- und Bildfunktionen: TEXTPTR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Textzeigerwert zurück, der einer **text**-, **ntext**- oder **image**-Spalte im Format **varbinary** entspricht. Der abgerufene Textzeigerwert kann in READTEXT-, WRITETEXT- und UPDATE-Anweisungen verwendet werden.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Es steht keine alternative Funktionalität zur Verfügung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TEXTPTR ( column )  
```  
  
## <a name="arguments"></a>Argumente  
 *column*  
 Entspricht der **text**-, **ntext**- oder **image**-Spalte, die verwendet wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary**  
  
## <a name="remarks"></a>Remarks  
 TEXTPTR gibt für Tabellen mit Text in Zeilen ein Handle für den zu verarbeitenden Text zurück. Sie können selbst dann einen gültigen Textzeiger erhalten, wenn der Textwert gleich NULL ist.  
  
 Sie können die Funktion TEXTPTR nicht für Spalten von Sichten verwenden. Sie können sie nur für Spalten von Tabellen verwenden. Wenn Sie die Funktion TEXTPTR für eine Spalte einer Sicht verwenden möchten, müssen Sie den Kompatibilitätsgrad mithilfe von [ALTER DATABASE Compatibility Level](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) auf 80 setzen. Wenn eine Tabelle keinen Text in Zeilen hat und wenn eine **text**-, **ntext**- oder **image**-Spalte nicht mit einer UPDATETEXT-Anweisung initialisiert wurde, gibt TEXTPTR einen NULL-Zeiger zurück.  
  
 Verwenden Sie TEXTVALID, um zu testen, ob ein Textzeiger vorhanden ist. Sie können UPDATETEXT, WRITETEXT oder READTEXT nicht ohne einen gültigen Textzeiger verwenden.  
  
 Diese Funktionen und Anweisungen sind auch bei Daten vom Typ **text**, **ntext** oder **image** hilfreich.  
  
|Funktion oder Anweisung|Description|  
|---------------------------|-----------------|  
|PATINDEX **('***%pattern%***' ,** *expression***)**|Gibt die Zeichenposition einer angegebenen Zeichenfolge in Spalten von Typ **text** oder **ntext** zurück.|  
|DATALENGTH **(***expression***)**|Gibt die Länge der Daten in den **text**-, **ntext**- und **image**-Spalten zurück.|  
|SET TEXTSIZE|Gibt das Limit der **text**-, **ntext**- oder **image**-Daten, die von einer SELECT-Anweisung zurückgegeben werden sollen, in Byte zurück.|  
|SUBSTRING**(***text_column*, *start*, *length***)**|Gibt eine **varchar**-Zeichenfolge zurück, die durch den Offset *start* und *length* angegeben wird. Die Länge sollte kleiner als 8 KB sein.|  
  
## <a name="examples"></a>Beispiele  
  
> [!NOTE]  
>  Sie müssen die **pubs**-Datenbank installieren, um die folgenden Beispiele auszuführen.  
  
### <a name="a-using-textptr"></a>A. Verwenden von TEXTPTR  
 Im folgenden Beispiel wird die Funktion `TEXTPTR` verwendet, um die **image**-Spalte `logo`, die mit `New Moon Books` verknüpft ist, in der `pub_info`-Tabelle der `pubs`-Datenbank zu suchen. Der Textzeiger wird in der lokalen Variablen `@ptrval.` abgelegt.  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(logo)  
FROM pub_info pr, publishers p  
WHERE p.pub_id = pr.pub_id   
   AND p.pub_name = 'New Moon Books';  
GO  
```  
  
### <a name="b-using-textptr-with-in-row-text"></a>B. Verwenden von TEXTPTR mit Text in Zeilen  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss der Textzeiger in Zeilen innerhalb einer Transaktion verwendet werden, wie im folgenden Beispiel gezeigt.  
  
```  
CREATE TABLE t1 (c1 int, c2 text);  
EXEC sp_tableoption 't1', 'text in row', 'on';  
INSERT t1 VALUES ('1', 'This is text.');  
GO  
BEGIN TRAN;  
   DECLARE @ptrval VARBINARY(16);  
   SELECT @ptrval = TEXTPTR(c2)  
   FROM t1  
   WHERE c1 = 1;  
   READTEXT t1.c2 @ptrval 0 1;  
COMMIT;  
```  
  
### <a name="c-returning-text-data"></a>C. Zurückgeben von Textdaten  
 Im folgenden Beispiel wird die Spalte `pub_id` und der 16 Byte lange Textzeiger der Spalte `pr_info` aus der Tabelle `pub_info` ausgewählt.  
  
```  
USE pubs;  
GO  
SELECT pub_id, TEXTPTR(pr_info)  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id                                      
------ ----------------------------------   
0736   0x6c0000000000feffb801000001000100   
0877   0x6d0000000000feffb801000001000300   
1389   0x6e0000000000feffb801000001000500   
1622   0x700000000000feffb801000001000900   
1756   0x710000000000feffb801000001000b00   
9901   0x720000000000feffb801000001000d00   
9952   0x6f0000000000feffb801000001000700   
9999   0x730000000000feffb801000001000f00   
  
(8 row(s) affected)  
```  
  
 Das folgende Beispiel zeigt, wie die ersten `8000` Byte Text ohne Verwendung von TEXTPTR zurückgegeben werden.  
  
```  
USE pubs;  
GO  
SET TEXTSIZE 8000;  
SELECT pub_id, pr_info  
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id pr_info                                                                                                                                                                                                                                                           
------ -----------------------------------------------------------------  
0736   New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!                                                                                                             
0877   This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washington, D.C.  
  
This is sample text data for Binnet & Hardley, publisher 0877 in the pubs database. Binnet & Hardley is located in Washi   
1389   This is sample text data for Algodata Infosystems, publisher 1389 in the pubs database. Algodata Infosystems is located in Berkeley, California.  
  
9999   This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in Paris, France.  
  
This is sample text data for Lucerne Publishing, publisher 9999 in the pubs database. Lucerne publishing is located in   
  
(8 row(s) affected)  
```  
  
### <a name="d-returning-specific-text-data"></a>D. Zurückgeben von bestimmten Textdaten  
 Im folgenden Beispiel wird die Spalte `text` (`pr_info`), die mit `pub_id``0736` verknüpft ist, in der Tabelle `pub_info` der `pubs`-Datenbank gesucht. Es wird zunächst die lokale Variable `@val` deklariert. Der Textzeiger (eine lange Binärzeichenfolge) wird dann in der Variablen `@val` abgelegt und als Parameter der `READTEXT`-Anweisung übergeben. Diese Anweisung gibt beginnend beim fünften Byte (Offset 4) 10 Byte zurück.  
  
```  
USE pubs;  
GO  
DECLARE @val varbinary(16);  
SELECT @val = TEXTPTR(pr_info)   
FROM pub_info  
WHERE pub_id = '0736';  
READTEXT pub_info.pr_info @val 4 10;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pr_info                                                                                                                                                                                                                                                           
-----------------------------------------------------------------------  
 is sample  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Text- und Bildfunktionen &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [UPDATETEXT (Transact-SQL)](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)  
  
  
