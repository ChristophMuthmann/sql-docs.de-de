---
title: FORMATMESSAGE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMATMESSAGE
- FORMATMESSAGE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysmessages system table
- sys.messages catalog view
- FORMATMESSAGE function
- messages [SQL Server], formats
- errors [SQL Server], formats
ms.assetid: 83f18102-2035-4a87-acd0-8d96d03efad5
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f90213e9e70d07f3f9d2bb661a64ef10f96c5068
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine Nachricht aus einer vorhandenen Meldung in sys.messages oder aus einer angegebenen Zeichenfolge. Die Funktionalität von FORMATMESSAGE ähnelt der RAISERROR-Anweisung. RAISERROR gibt die Meldung jedoch direkt aus, während FORMATMESSAGE die bearbeitete Meldung zur weiteren Verarbeitung zurückgibt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *msg_number*  
 Ist die ID der Meldung in sys.messages gespeichert. Wenn *Msg_number* ist < = 13000 ist oder wenn die Meldung in sys.messages nicht vorhanden ist, wird NULL zurückgegeben.  
  
 *"msg_string"*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Eine Zeichenfolge in einfachen Anführungszeichen und enthaltenden Parameterwert Platzhalter eingeschlossen ist. Die Fehlermeldung kann maximal 2.047 Zeichen enthalten. Wenn die Meldung mehr als 2.048 Zeichen enthält, werden nur die ersten 2.044 angezeigt und Auslassungspunkte angefügt, die anzeigen, dass die Meldung abgeschnitten wurde. Aufgrund des internen Speicherverhaltens beanspruchen Ersetzungsparameter mehr Zeichen als in der Ausgabe angezeigt werden.  Informationen über die Struktur einer Meldungszeichenfolge und der Verwendung von Parametern in der Zeichenfolge, finden Sie unter der Beschreibung der *Msg_str* Argument in [RAISERROR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 *param_value*  
 Ein Parameterwert, der in der Meldung verwendet wird. Hierbei kann es sich um mehrere Parameterwerte handeln. Die Werte müssen in der Reihenfolge angegeben werden, in der die Platzhaltervariablen in der Meldung vorkommen. Es können maximal 20 Werte angegeben werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar**  
  
## <a name="remarks"></a>Hinweise  
 Wie bei der RAISERROR-Anweisung ersetzt FORMATMESSAGE die Platzhaltervariablen in der Meldung mit den angegebenen Parameterwerten. Weitere Informationen zu zulässigen Platzhaltern in Fehlermeldungen und zum Bearbeitungsprozess finden Sie unter [RAISERROR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 FORMATMESSAGE sucht die Meldung in der aktuellen Sprache des Benutzers. Wenn es keine lokalisierte Version der Meldung gibt, wird die Version für Englisch (USA) Englische Version verwendet wird.  
  
 Für lokalisierte Meldungen müssen die angegebenen Parameterwerte den Parameterplatzhaltern in der Version für Englisch (USA) entsprechen. Das heißt, Parameter 1 in der lokalisierten Version muss Parameter 1 in der Version für Englisch (USA) entsprechen, Parameter 2 in der lokalisierten Version muss Parameter 2 in der Version für Englisch (USA) entsprechen usw.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-example-with-a-message-number"></a>A. Beispiel mit einer Meldungsnummer  
 Im folgenden Beispiel wird eine replikationsmeldung `20009` in sys.messages als gespeichert, "im Artikel"%s"konnte nicht hinzugefügt werden für die Veröffentlichung"%s"." In der FORMATMESSAGE-Anweisung werden für die Parameterplatzhalter die Werte `First Variable` und `Second Variable` eingesetzt. Die Ergebniszeichenfolge "der Artikel konnte 'First Variable' nicht für die Veröffentlichung 'Second Variable' hinzugefügt werden.", wird in der lokalen Variable gespeichert `@var1`.  
  
```  
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>B. Beispiel mit einer Meldungszeichenfolge  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Im folgende Beispiel wird eine Zeichenfolge als Eingabe akzeptiert.  
  
```  
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 Gibt:`This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>C. Zusätzliche Meldung zeichenfolgenformatierung-Beispiele  
 Die folgenden Beispiele zeigen eine Vielzahl von Optionen für die Formatierung an.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [THROW &#40; Transact-SQL &#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Sp_addmessage &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [RAISERROR &#40; Transact-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
