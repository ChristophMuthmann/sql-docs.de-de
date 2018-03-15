---
title: PARSE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSE
- PARSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PARSE function
ms.assetid: 6a2dbf10-f692-471b-9458-24d246963049
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3e172a7d68edc212ce4803103dc1f975e4bf89db
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="parse-transact-sql"></a>PARSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt das Ergebnis eines Ausdrucks zurück, der in den angeforderten Datentyp in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] umgewandelt wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *string_value*  
 **nvarchar**(4000)-Wert, der den formatierten Wert darstellt, der als angegebener Datentyp analysiert werden soll.  
  
 *string_value* muss eine gültige Darstellung des angeforderten Datentyps sein. Andernfalls löst PARSE einen Fehler aus.  
  
 *data_type*  
 Literalwert, der den für das Ergebnis angeforderten Datentyp darstellt.  
  
 *culture*  
 Optionale Zeichenfolge, die die Kultur angibt, in der *string_value* formatiert wird.  
  
 Wenn das *culture*-Argument nicht angegeben wurde, wird die Sprache der aktuellen Sitzung verwendet. Diese Sprache ist entweder implizit definiert oder wird explizit mit der Anweisung SET LANGUAGE festgelegt. *culture* lässt alle von .NET Framework unterstützten Kulturen zu und ist auf die explizit durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützten Sprachen beschränkt. Wenn das *culture*-Argument nicht gültig ist, löst PARSE einen Fehler aus.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt das Ergebnis des Ausdrucks zurück, das in den angeforderten Datentyp umgewandelt wurde.  
  
## <a name="remarks"></a>Remarks  
 NULL-Werte, die als Argumente an PARSE übergeben wurden, werden auf die zwei Arten verarbeitet:  
  
1.  Wenn eine NULL-Konstante übergeben wird, wird ein Fehler ausgelöst. Ein NULL-Wert kann nicht unter Berücksichtigung der Kultur in einen anderen Datentyp analysiert werden.  
  
2.  Wenn ein Parameter mit einem NULL-Wert zur Laufzeit übergeben wird, wird NULL zurückgegeben. So wird verhindert, dass der gesamte Batch abgebrochen wird.  
  
 Verwenden Sie PARSE nur, um eine Zeichenfolge in ein Datum und eine Uhrzeit oder in eine Zahl zu konvertieren. Für die allgemeine Typkonvertierungen sollten Sie auch weiterhin CAST oder CONVERT verwenden. Bedenken Sie, dass die Analyse des Zeichenfolgenwerts mit gewissen Leistungseinbußen verbunden ist.  
  
 Für PARSE muss die .NET Framework-Common Language Runtime (CLR) vorhanden sein.  
  
 Diese Funktion wird nicht remote ausgeführt, da sie die Existenz der CLR voraussetzt. Die Remoteausführung einer Funktion, die die CLR erfordert, würde einen Fehler auf dem Remoteserver auslösen.  
  
 **Weitere Informationen zum data_type-Parameter**  
  
 Die Werte für den *data_type*-Parameter sind auf die in der folgenden Tabelle dargestellten Typen sowie die zugehörigen Formate beschränkt. Die Formatinformationen werden bereitgestellt, um die Ermittlung der zulässigen Mustertypen zu unterstützen. Weitere Informationen zu Formaten finden Sie in der .NET Framework-Dokumentation für die Enumerationen **System.Globalization.NumberStyles** und **DateTimeStyles**.  
  
|Kategorie|Typ|.NET Framework-Typ|Verwendete Formate|  
|--------------|----------|-------------------------|-----------------|  
|Numerisch|bigint|Int64|NumberStyles.Number|  
|Numerisch|ssNoversion|Int32|NumberStyles.Number|  
|Numerisch|SMALLINT|Int16|NumberStyles.Number|  
|Numerisch|TINYINT|Byte|NumberStyles.Number|  
|Numerisch|Decimal|Decimal|NumberStyles.Number|  
|Numerisch|NUMERIC|Decimal|NumberStyles.Number|  
|Numerisch|FLOAT|Double|NumberStyles.Float|  
|Numerisch|REAL|Single|NumberStyles.Float|  
|Numerisch|smallmoney|Decimal|NumberStyles.Currency|  
|Numerisch|money|Decimal|NumberStyles.Currency|  
|Datum und Uhrzeit|date|datetime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Datum und Uhrzeit|Uhrzeit|TimeSpan|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Datum und Uhrzeit|DateTime|datetime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Datum und Uhrzeit|smalldatetime|datetime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Datum und Uhrzeit|datetime2|datetime|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
|Datum und Uhrzeit|datetimeoffset|DateTimeOffset|DateTimeStyles.AllowWhiteSpaces &#124; DateTimeStyles.AssumeUniversal|  
  
 **Weitere Informationen zum culture-Parameter**  
  
 In der folgenden Tabelle werden die Zuordnungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sprachen zu .NET Framework-Kulturen angezeigt.  
  
|Vollständiger Name|Alias|LCID|Bestimmte Kultur|  
|---------------|-----------|----------|----------------------|  
|us_english|Englisch|1033|de-DE|  
|Deutsch|Deutsch|1031|de-DE|  
|Français|Französisch|1036|fr-FR|  
|日本語|Japanisch|1041|ja-JP|  
|Dansk|Dänisch|1030|da-DK|  
|Español|Spanisch|3082|es-ES|  
|Italiano|Italienisch|1040|it-IT|  
|Nederlands|Niederländisch|1043|nl-NL|  
|Norsk|Norwegisch|2068|nn-NO|  
|Português|Portugiesisch|2070|pt-PT|  
|Suomi|Finnisch|1035|fi|  
|Svenska|Schwedisch|1053|sv-SE|  
|čeština|Tschechisch|1029|Cs-CZ|  
|magyar|Ungarisch|1038|Hu-HU|  
|polski|Polnisch|1045|Pl-PL|  
|română|Rumänisch|1048|Ro-RO|  
|hrvatski|Kroatisch|1050|hr-HR|  
|slovenčina|Slowakisch|1051|Sk-SK|  
|slovenski|Slowenisch|1060|Sl-SI|  
|ελληνικά|Griechisch|1032|El-GR|  
|български|Bulgarisch|1026|bg-BG|  
|русский|Russisch|1049|Ru-RU|  
|Türkçe|Türkisch|1055|Tr-TR|  
|British|Englisch (britisch)|2057|en-GB|  
|eesti|Estnisch|1061|Et-EE|  
|latviešu|Lettisch|1062|lv-LV|  
|lietuvių|Litauisch|1063|lt-LT|  
|Português (Brasil)|Brasilianisch|1046|pt-BR|  
|繁體中文|Chinesisch (traditionell)|1028|zh-TW|  
|한국어|Koreanisch|1042|Ko-KR|  
|简体中文|Chinesisch (vereinfacht)|2052|zh-CN|  
|Arabisch|Arabisch|1025|ar-SA|  
|ไทย|Thai|1054|Th-TH|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-parse-into-datetime2"></a>A. PARSE in datetime2  
  
```  
SELECT PARSE('Monday, 13 December 2010' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-13 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-parse-with-currency-symbol"></a>B. PARSE mit Währungssymbol  
  
```  
SELECT PARSE('€345,98' AS money USING 'de-DE') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
345.98  
  
(1 row(s) affected)  
```  
  
### <a name="c-parse-with-implicit-setting-of-language"></a>C. PARSE mit impliziter Einstellung der Sprache  
  
```  
-- The English language is mapped to en-US specific culture  
SET LANGUAGE 'English';  
SELECT PARSE('12/16/2010' AS datetime2) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-16 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
  
