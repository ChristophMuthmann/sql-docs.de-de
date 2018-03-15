---
title: TRY_PARSE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
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
- TRY_PARSE_TSQL
- TRY_PARSE
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_PARSE function
ms.assetid: 292bac1d-edd8-468c-8ff1-8c7de625bc55
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0b26f46431909dd4fbfaa820db8c3869333f555d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="tryparse-transact-sql"></a>TRY_PARSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt das Ergebnis eines Ausdrucks zurück, das in den angeforderten Datentyp übersetzt wurde. Schlägt die Umwandlung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fehl, wird NULL zurückgegeben. Verwenden Sie TRY_PARSE nur, um eine Zeichenfolge in ein Datum und eine Uhrzeit oder in eine Zahl zu konvertieren.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TRY_PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *string_value*  
 **nvarchar**(4000)-Wert, der den formatierten Wert darstellt, der als angegebener Datentyp analysiert werden soll.  
  
 *string_value* muss eine gültige Darstellung des angeforderten Datentyps sein. Andernfalls gibt TRY_PARSE NULL zurück.  
  
 *data_type*  
 Literal, das den für das Ergebnis angeforderten Datentyp darstellt.  
  
 *culture*  
 Optionale Zeichenfolge, die die Kultur angibt, in der *string_value* formatiert wird.  
  
 Wenn das *culture* -Argument nicht angegeben wurde, wird die Sprache der aktuellen Sitzung verwendet. Diese Sprache ist entweder implizit definiert oder wird explizit mit der Anweisung SET LANGUAGE festgelegt. *culture* lässt alle von .NET Framework unterstützten Kulturen zu und ist auf die explizit durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützten Sprachen beschränkt. Wenn das *culture*-Argument nicht gültig ist, löst PARSE einen Fehler aus.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt das Ergebnis des Ausdrucks zurück, das in den angeforderten Datentyp übersetzt wurde. Schlägt die Umwandlung fehl, wird NULL zurückgegeben.  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie TRY_PARSE nur, um eine Zeichenfolge in ein Datum und eine Uhrzeit oder in eine Zahl zu konvertieren. Für die allgemeine Typkonvertierungen sollten Sie auch weiterhin CAST oder CONVERT verwenden. Bedenken Sie, dass die Analyse des Zeichenfolgenwerts mit gewissen Leistungseinbußen verbunden ist.  
  
 Für TRY_PARSE muss .NET Framework Common Language Runtime (CLR) vorhanden sein.  
  
 Diese Funktion wird nicht remote ausgeführt, da sie die Existenz der CLR voraussetzt. Die Remoteausführung einer Funktion, die die CLR erfordert, würde einen Fehler auf dem Remoteserver auslösen.  
  
 **Weitere Informationen zum data_type-Parameter**  
  
 Die Werte für den *data_type*-Parameter sind auf die in der folgenden Tabelle dargestellten Typen sowie die zugehörigen Formate beschränkt. Die Formatinformationen werden bereitgestellt, um die Ermittlung der zulässigen Mustertypen zu unterstützen. Weitere Informationen zu Formaten finden Sie in der .NET Framework-Dokumentation für die Enumerationen **System.Globalization.NumberStyles** und **DateTimeStyles**.  
  
|Kategorie|Typ|.NET-Typ|Verwendete Formate|  
|--------------|----------|---------------|-----------------|  
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
  
### <a name="a-simple-example-of-tryparse"></a>A. Einfaches Beispiel für TRY_PARSE  
  
```  
SELECT TRY_PARSE('Jabberwokkie' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-detecting-nulls-with-tryparse"></a>B. Erkennen von NULL-Werten mit TRY_PARSE  
  
```  
SELECT  
    CASE WHEN TRY_PARSE('Aragorn' AS decimal USING 'sr-Latn-CS') IS NULL  
        THEN 'True'  
        ELSE 'False'  
END  
AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
True  
  
(1 row(s) affected)  
```  
  
### <a name="c-using-iif-with-tryparse-and-implicit-culture-setting"></a>C. Verwenden von IIF mit TRY_PARSE und impliziter Kultureinstellung  
  
```  
SET LANGUAGE English;  
SELECT IIF(TRY_PARSE('01/01/2011' AS datetime2) IS NULL, 'True', 'False') AS Result;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
False  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [PARSE &#40;Transact-SQL&#41;](../../t-sql/functions/parse-transact-sql.md)   
 [Konvertierungsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/conversion-functions-transact-sql.md)   
 [TRY_CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
