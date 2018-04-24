---
title: TRY_CONVERT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
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
- TRY_CONVERT_TSQL
- TRY_CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CONVERT function
ms.assetid: 3e6e7825-6482-4cb2-a8c2-9abc99e265a6
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2ef43a22ebbdd936ec6be0ef1fec1186e80caffc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
 *data_type [ ( length ) ]*  
 Der Datentyp, in den *expression*umgewandelt werden soll.  
  
 *expression*  
 Der umzuwandelnde Wert.  
  
 *style*  
 Ein optionaler ganzzahliger Ausdruck, der angibt, wie die **TRY_CONVERT**-Funktion *expression* übersetzen soll.  
  
 *style* akzeptiert die gleichen Werte wie der *style*-Parameter der **CONVERT**-Funktion. Weitere Informationen finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 Der Bereich zulässiger Werte wird durch den Wert von *data_type*bestimmt. Wenn *style* NULL ist, gibt **TRY_CONVERT** NULL zurück.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt einen in den angegebenen Datentyp umgewandelten Wert zurück, wenn die Umwandlung erfolgreich ist. Andernfalls wird NULL zurückgegeben.  
  
## <a name="remarks"></a>Remarks  
 **TRY_CONVERT** versucht, den übergebenen Wert in den angegebenen *data_type*zu konvertieren. Wenn die Umwandlung erfolgreich ist, gibt **TRY_CONVERT** den Wert als angegebenen *data_type* zurück. Bei einem Fehler wird NULL zurückgegeben. Wenn Sie jedoch eine Konvertierung anfordern, die explizit nicht zulässig ist, verursacht **TRY_CONVERT** einen Fehler.  
  
 **TRY_CONVERT** ist ein reserviertes Schlüsselwort in Kompatibilitätsgrad 110 und höher.  
  
 Diese Funktion kann remote auf Servern mit einer Version von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder höher ausgeführt werden. Eine Remoteausführung auf Servern mit einer Version vor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ist nicht möglich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-tryconvert-returns-null"></a>A. TRY_CONVERT gibt NULL zurück.  
 Im folgenden Beispiel wird veranschaulicht, dass TRY_CONVERT bei fehlerhafter Umwandlung NULL zurückgibt.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
