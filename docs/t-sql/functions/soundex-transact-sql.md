---
title: SOUNDEX (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SOUNDEX
- SOUNDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SOUNDEX function
- comparing string data
- strings [SQL Server], similarity
- strings [SQL Server], comparing
- SOUNDEX values
ms.assetid: 8f1ed34e-8467-4512-a211-e0f43dee6584
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1499eda4d4e9f360256b52bf5baf6ddcaa67afcb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="soundex-transact-sql"></a>SOUNDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen aus vier Zeichen bestehenden (SOUNDEX) Code zur Bewertung der Ähnlichkeit von zwei Zeichenfolgen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SOUNDEX ( character_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein alphanumerischer [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der Zeichendaten. *character_expression* kann eine Konstante, Variable oder Spalte sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 SOUNDEX konvertiert eine alphanumerische Zeichenfolge in einen vierstelligen Code, der davon abhängig ist, wie sich eine Zeichenfolge anhört, wenn diese ausgesprochen wird. Beim ersten Zeichen des Codes handelt es sich um das erste Zeichen von *character_expression*, umgewandelt in Großbuchstaben. Das zweite bis vierte Zeichen des Codes sind Zahlen, die die Buchstaben im Ausdruck darstellen. Die Buchstaben A, E, I, O, U, STD, W und Y werden ignoriert, es sei denn, sie entsprechen dem ersten Buchstaben der Zeichenfolge. Nullen werden ggf. am Ende hinzugefügt, um einen vier Zeichen langen Code zu erzeugen. Weitere Informationen zum SOUNDEX-Code finden Sie unter [The Soundex Indexing System (Das Soundex-Indizierungssystem)](https://www.archives.gov/research/census/soundex.html).  
  
 SOUNDEX-Codes aus verschiedenen Zeichenfolgen können verglichen werden, um Ähnlichkeiten zwischen gesprochenen Zeichenfolgen festzustellen. Die DIFFERENCE-Funktion führt eine SOUNDEX-Funktion für zwei Zeichenfolgen aus und gibt eine ganze Zahl zurück, die die Ähnlichkeit der SOUNDEX-Codes für diese Zeichenfolgen darstellt.  
  
 SOUNDEX ist sortierungsabhängig. Zeichenfolgenfunktionen können geschachtelt werden.  
  
## <a name="soundex-compatibility"></a>SOUNDEX-Kompatibilität  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wurde von der SOUNDEX-Funktion eine Teilmenge der SOUNDEX-Regeln angewendet. Unter dem Datenbank-Kompatibilitätsgrad 110 oder höher wendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen vollständigeren Regelsatz an.  
  
 Möglicherweise sind die Indizes, Heaps oder CHECK-Einschränkungen, die die SOUNDEX-Funktion verwenden, nach dem Upgrade auf Kompatibilitätsgrad 110 oder höher erneut zu erstellen.  
  
-   Ein Heap, der eine persistierte berechnete Spalte enthält, die mit SOUNDEX definiert wurde, kann erst abgefragt werden, wenn der Heap durch Ausführen der `ALTER TABLE <table> REBUILD`-Anweisung neu erstellt wurde.  
  
-   Mit SOUNDEX definierte CHECK-Einschränkungen werden beim Upgrade deaktiviert. Führen Sie zum Aktivieren der Einschränkung die `ALTER TABLE <table> WITH CHECK CHECK CONSTRAINT ALL`-Anweisung aus.  
  
-   Indizes (einschließlich indizierter Sichten), die eine persistierte berechnete Spalte enthalten, die mit SOUNDEX definiert wurde, können erst abgefragt werden, wenn der Index durch Ausführen der `ALTER INDEX ALL ON <object> REBUILD`-Anweisung neu erstellt wurde.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die SOUNDEX-Funktion sowie die verwandte DIFFERENCE-Funktion. Im ersten Beispiel werden die standardmäßigen `SOUNDEX`-Werte für alle Konsonanten zurückgegeben. Die Rückgabe von `SOUNDEX` für `Smith` und `Smythe` ergibt das gleiche SOUNDEX-Ergebnis, da alle Vokale, der Buchstabe `y`, doppelt vorhandene Buchstaben und der Buchstabe `h` nicht einbezogen werden.  
  
```  
-- Using SOUNDEX  
SELECT SOUNDEX ('Smith'), SOUNDEX ('Smythe');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Gültig für eine Latin1_General-Sortierung.  
  
```  
  
----- -----   
S530  S530    
  
(1 row(s) affected)  
```  
  
 Die `DIFFERENCE`-Funktion vergleicht den Unterschied der Werte, die von der `SOUNDEX`-Funktion zurückgegeben werden. Das folgende Beispiel zeigt zwei Zeichenfolgen, die sich nur in den Vokalen unterscheiden. Der zurückgegebene Wert beträgt `4` (größtmögliche Übereinstimmung).  
  
```  
-- Using DIFFERENCE  
SELECT DIFFERENCE('Smithers', 'Smythers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Gültig für eine Latin1_General-Sortierung.  
  
```  
-----------   
4             
  
(1 row(s) affected)  
```  
  
 Im folgenden Beispiel weisen die Zeichenfolgen unterschiedliche Konsonanten auf; die Funktion gibt daher den Wert `2` (geringere Übereinstimmung) zurück.  
  
```  
SELECT DIFFERENCE('Anothers', 'Brothers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Gültig für eine Latin1_General-Sortierung.  
  
```  
-----------   
2             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DIFFERENCE &#40;Transact-SQL&#41;](../../t-sql/functions/difference-transact-sql.md)   
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)   
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

