---
title: float und real (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 87b6b785af338745f3c02cb1d6d0b77efb01240c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="float-and-real-transact-sql"></a>float und real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Ungefähre Zahlendatentypen für numerische Gleitkommadaten. Gleitkommadaten sind Näherungswerte, deshalb können nicht alle Werte im Bereich des Datentyps exakt dargestellt werden. Das ISO-Synonym für **real** ist **float(24)**.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
**float** [ **(***n***)** ]. Hierbei entspricht *n* der Anzahl von Bits, die zum Speichern der Mantisse der **Gleitkommazahl** in der wissenschaftlichen Schreibweise verwendet werden. Dadurch werden die Genauigkeit und die Speichergröße festlegt. Wenn *n* angegeben wird, muss es sich um einen Wert zwischen **1** und **53** handeln. Der Standardwert von *n* lautet **53**.
  
|*n*-Wert|Genauigkeit|Speichergröße|  
|---|---|---|
|**1-24**|7 Stellen|4 Byte|  
|**25-53**|15 Stellen|8 Byte|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verarbeitet *n* als einen von zwei möglichen Werten. Wenn **1**<=n<=**24** gegeben ist, wird *n* als **24** behandelt. Wenn **25**<=n<=**53** gegeben ist, wird *n* als **53** behandelt.  
  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float**[**(n)**]-Datentyp entspricht dem ISO-Standard für alle Werte von *n* zwischen **1** und **53**. Das Synonym für **double precision** lautet **float(53)**.
  
## <a name="remarks"></a>Remarks  
  
|Datentyp|Bereich|Speicherung|  
|---|---|---|
|**float**|- 1,79E+308 bis -2,23E-308, 0 und 2,23E-308 bis 1,79E+308|Hängt vom Wert für *n* ab.|  
|**real**|- 3,40E + 38 bis -1,18E - 38, 0 und 1,18E - 38 bis 3,40E + 38|4 Byte|  
  
##  <a name="converting-float-and-real-data"></a>Konvertieren von float- und real-Daten  
Werte des Typs **float** werden bei der Konvertierung in einen Integertyp abgeschnitten.
  
Für das Konvertieren von **float**- oder **real**-Daten in Zeichendaten eignet sich die STR-Zeichenfolgenfunktion normalerweise besser als CAST( ). Der Grund hierfür ist, dass STR Ihnen bessere Steuerungsmöglichkeiten über die Formatierung bietet. Weitere Informationen finden Sie unter [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md) und [Aggregatfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md).
  
Die Konvertierung der **float**-Werte, die eine wissenschaftliche Schreibweise für **decimal** oder **numeric** verwenden, ist auf Werte mit einer Genauigkeit von 17 Stellen beschränkt. Jeder Wert < 5E-18 wird auf 0 (null) abgerundet.
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Datentypkonvertierung &#40;Datenbank-Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
