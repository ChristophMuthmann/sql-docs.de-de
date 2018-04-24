---
title: FORMATMESSAGE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FORMATMESSAGE
- FORMATMESSAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.messages catalog view
- FORMATMESSAGE function
- messages [SQL Server], formats
- errors [SQL Server], formats
ms.assetid: 83f18102-2035-4a87-acd0-8d96d03efad5
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 40ebf07e5da8286923cf9b49e0f528f3751c4746
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine Meldung aus einer vorhandenen Meldung in sys.messages oder über eine bereitgestellte Zeichenfolge. Die Funktionalität von FORMATMESSAGE ähnelt der RAISERROR-Anweisung. RAISERROR gibt die Meldung jedoch direkt aus, während FORMATMESSAGE die bearbeitete Meldung zur weiteren Verarbeitung zurückgibt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *msg_number*  
 Die ID der in sys.messages gespeicherten Meldung. Falls *msg_number* <= 13000 ist oder die Meldung in sys.messages nicht vorhanden ist, wird NULL zurückgegeben.  
  
 *msg_string*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Eine Zeichenfolge in einfachen Anführungszeichen mit den Platzhaltern für die Parameterwerte. Die Fehlermeldung kann maximal 2.047 Zeichen enthalten. Wenn die Meldung mehr als 2.048 Zeichen enthält, werden nur die ersten 2.044 angezeigt und Auslassungspunkte angefügt, die anzeigen, dass die Meldung abgeschnitten wurde. Aufgrund des internen Speicherverhaltens beanspruchen Ersetzungsparameter mehr Zeichen als in der Ausgabe angezeigt werden.  Weitere Informationen zur Struktur einer Nachrichtenzeichenfolge und der Verwendung von Parametern in einer Zeichenfolge finden Sie in der Beschreibung des *msg_str*-Arguments und unter [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 *param_value*  
 Ein Parameterwert, der in der Meldung verwendet wird. Hierbei kann es sich um mehrere Parameterwerte handeln. Die Werte müssen in der Reihenfolge angegeben werden, in der die Platzhaltervariablen in der Meldung vorkommen. Es können maximal 20 Werte angegeben werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 Wie bei der RAISERROR-Anweisung ersetzt FORMATMESSAGE die Platzhaltervariablen in der Meldung mit den angegebenen Parameterwerten. Weitere Informationen zu zulässigen Platzhaltern in Fehlermeldungen und zum Bearbeitungsprozess finden Sie unter [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 FORMATMESSAGE sucht die Meldung in der aktuellen Sprache des Benutzers. Wenn es keine lokalisierte Version der Meldung gibt, wird die Version für Englisch (USA) verwendet.  
  
 Für lokalisierte Meldungen müssen die angegebenen Parameterwerte den Parameterplatzhaltern in der Version für Englisch (USA) entsprechen. Das heißt, Parameter 1 in der lokalisierten Version muss Parameter 1 in der Version für Englisch (USA) entsprechen, Parameter 2 in der lokalisierten Version muss Parameter 2 in der Version für Englisch (USA) entsprechen usw.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-example-with-a-message-number"></a>A. Beispiel mit einer Meldungsnummer  
 Im folgenden Beispiel wird eine Replikationsmeldung mit dem Code `20009` verwendet, die mit folgendem Wortlaut in sys.messages gespeichert ist: "The article '%s' could not be added to the publication '%s'" (Der %s-Artikel konnte nicht zur %s-Veröffentlichung hinzugefügt werden.). In der FORMATMESSAGE-Anweisung werden für die Parameterplatzhalter die Werte `First Variable` und `Second Variable` eingesetzt. Die Ergebniszeichenfolge „The article 'First Variable' could not be added to the publication 'Second Variable'.“ („Der First Variable-Artikel konnte nicht zur Second Variable-Veröffentlichung hinzugefügt werden.“) wird in der lokalen Variablen `@var1` gespeichert.  
  
```  
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>B. Beispiel mit einer Meldungszeichenfolge  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Im folgenden Beispiel wird eine Zeichenfolge als Eingabe akzeptiert.  
  
```  
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 Rückgabewert: `This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>C. Zusätzliche Beispiele zur Formatierung von Meldungszeichenfolgen  
 Die folgenden Beispiele zeigen verschiedene Formatierungsoptionen.  
  
```  
SELECT FORMATMESSAGE('Signed int %i, %d %i, %d, %+i, %+d, %+i, %+d', 5, -5, 50, -50, -11, -11, 11, 11);  
SELECT FORMATMESSAGE('Signed int with leading zero %020i', 5);  
SELECT FORMATMESSAGE('Signed int with leading zero 0 %020i', -55);  
SELECT FORMATMESSAGE('Unsigned int %u, %u', 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal %o, %o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal %x, %X, %X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal with prefix: %#o, %#o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal with prefix: %#x, %#X, %#X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Hello %s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %-20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
  
  
