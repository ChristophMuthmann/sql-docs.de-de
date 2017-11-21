---
title: float- und Real (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- float
- real_TSQL
- real
- float_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- numeric data type, floating point
- float data type
- floating point data [SQL Server]
- real data type
ms.assetid: 08ea66b7-624e-4d8b-86bc-750ff76cdfc5
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 0ce2e3272c30057f533796e0822256c6235de0c1
ms.contentlocale: de-de
ms.lasthandoff: 10/04/2017

---
# <a name="float-and-real-transact-sql"></a>float und real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Ungefähre Zahlendatentypen für numerische Gleitkommadaten. Gleitkommadaten sind Näherungswerte, deshalb können nicht alle Werte im Bereich des Datentyps exakt dargestellt werden. Das ISO-Synonym für **echte** ist **float(24)**.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
**"float"** [ **(***n***)** ], in dem  *n*  ist die Anzahl der Bits, die zum Speichern verwendet werden die Mantisse des der **"float"** Zahl in wissenschaftlicher Schreibweise und wie die Genauigkeit und Speichergröße. Wenn  *n*  angegeben wird, muss er einen Wert zwischen **1** und **53**. Der Standardwert von  *n*  ist **53**.
  
|*n*Wert|Genauigkeit|Speichergröße|  
|---|---|---|
|**1-24**|7 Dezimalstellen|4 bytes|  
|**25-53**|15 Stellen|8 Byte|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]behandelt  *n*  als einen von zwei möglichen Werten. Wenn **1**<=n<=**24**,  *n*  so behandelt, als **24**. Wenn **25**<=n<=**53**,  *n*  so behandelt, als **53**.  
  
Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"float"**[**(n)**]-Datentyp entspricht dem ISO-Standard für alle Werte des  *n*  aus **1** über **53**. Das Synonym für **doppelte Genauigkeit** ist **float(53)**.
  
## <a name="remarks"></a>Hinweise  
  
|Datentyp|Bereich|Speicherung|  
|---|---|---|
|**float**|- 1,79E+308 bis -2,23E-308, 0 und 2,23E-308 bis 1,79E+308|Hängt vom Wert von*n*|  
|**real**|- 3,40E + 38 bis -1,18E - 38, 0 und 1,18E - 38 bis 3,40E + 38|4 bytes|  
  
##  <a name="converting-float-and-real-data"></a>Konvertieren von float- und real-Daten  
Werte des **"float"** werden bei der Konvertierung in einen ganzzahligen Datentyp abgeschnitten.
  
Wenn Sie konvertieren möchten **"float"** oder **echte** in Zeichendaten mithilfe der STR-Zeichenfolgenfunktion wird in der Regel nützlicher, als CAST (). Der Grund hierfür ist, dass STR Ihnen bessere Steuerungsmöglichkeiten über die Formatierung bietet. Weitere Informationen finden Sie unter [STR &#40; Transact-SQL &#41; ](../../t-sql/functions/str-transact-sql.md) und [Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/functions.md).
  
Konvertierung von **"float"** Werte, die wissenschaftliche für Schreibweise **decimal** oder **numerischen** auf den Werten der Genauigkeit von 17 Stellen beschränkt. Jeder Wert < 5e-18 auf 0 abgerundet.
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

