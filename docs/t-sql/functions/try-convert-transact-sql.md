---
title: TRY_CONVERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- TRY_CONVERT_TSQL
- TRY_CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CONVERT function
ms.assetid: 3e6e7825-6482-4cb2-a8c2-9abc99e265a6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5fedc9777146d24cb04fb7652344f244babc8246
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="tryconvert-transact-sql"></a>TRY_CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt einen in den angegebenen Datentyp umgewandelten Wert zurück, wenn die Umwandlung erfolgreich ist. Andernfalls wird NULL zurückgegeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TRY_CONVERT ( data_type [ ( length ) ], expression [, style ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Data_type [(Länge)]*  
 Der Datentyp, in den *expression*umgewandelt werden soll.  
  
 *expression*  
 Der umzuwandelnde Wert.  
  
 *Stil*  
 Optionaler ganzzahliger Ausdruck, der angibt, wie die **TRY_CONVERT** Funktion besteht darin, übersetzen *Ausdruck*.  
  
 *Stil* akzeptiert die gleichen Werte wie die *Stil* Parameter von der **konvertieren** Funktion. Weitere Informationen finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 Der Bereich zulässiger Werte wird durch den Wert von *data_type*bestimmt. Wenn *Stil* null ist, **TRY_CONVERT** gibt null zurück.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt einen in den angegebenen Datentyp umgewandelten Wert zurück, wenn die Umwandlung erfolgreich ist. Andernfalls wird NULL zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 **TRY_CONVERT** nimmt den Wert übergeben wird, und versucht, es in den angegebenen konvertieren *Data_type*. Wenn die Umwandlung erfolgreich ist, **TRY_CONVERT** gibt den Wert als den angegebenen *Data_type*; Wenn ein Fehler auftritt, wird Null zurückgegeben. Jedoch wenn Sie eine Konvertierung anfordern, die explizit nicht zulässig ist **TRY_CONVERT** verursacht einen Fehler.  
  
 **TRY_CONVERT** ist ein reserviertes Schlüsselwort in Kompatibilitätsgrad 110 und höher.  
  
 Diese Funktion kann Remote auf Servern mit einer Version von ist [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höher. Sie werden nicht in der Remoteausführung auf Servern, auf denen eine Version unter [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-tryconvert-returns-null"></a>A. TRY_CONVERT gibt NULL zurück.  
 Im folgenden Beispiel wird veranschaulicht, dass TRY_CONVERT "0" zurückgibt, wenn die Umwandlung fehlerhaft ist.  
  
```sql  
SELECT   
    CASE WHEN TRY_CONVERT(float, 'test') IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 Im folgenden Beispiel wird veranschaulicht, dass der Ausdruck das erwartete Format aufweisen muss.  
  
```sql  
SET DATEFORMAT dmy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-tryconvert-fails-with-an-error"></a>B. Bei TRY_CONVERT tritt ein Fehler auf.  
 Im folgenden Beispiel wird veranschaulicht, dass TRY_CONVERT einen Fehler zurückgibt, wenn die Umwandlung explizit nicht zulässig ist.  
  
```sql  
SELECT TRY_CONVERT(xml, 4) AS Result;  
GO  
```  
  
 Das Ergebnis dieser Anweisung ist ein Fehler, da eine ganze Zahl nicht in einen XML-Datentyp umgewandelt werden kann.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-tryconvert-succeeds"></a>C. TRY_CONVERT ist erfolgreich.  
 In diesem Beispiel wird veranschaulicht, dass der Ausdruck das erwartete Format aufweisen muss.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
