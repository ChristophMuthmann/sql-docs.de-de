---
title: Decimal und Numeric (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- decimal
- decimal_TSQL
- numeric
- numeric_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decimal data type
- decimal data type, about decimal data type
- numeric data type
- numeric data type, about numeric data type
ms.assetid: 9d862a90-e6b7-4692-8605-92358dccccdf
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6c8ec4ea2255e8496b6e5ed464fbff220d270e7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="decimal-and-numeric-transact-sql"></a>decimal und numeric (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Numerische Datentypen mit fester Genauigkeit und fester Anzahl von Dezimalstellen. Decimal und Numeric sind Synonyme und austauschbar.
  
## <a name="arguments"></a>Argumente  
**Decimal**[ **(***p*[ **,***s*] **)**] und **numerische** [ **(***p*[ **,***s*] **)**]  
Zahlen mit fester Genauigkeit und mit fester Anzahl von Dezimalstellen. Wenn maximale Genauigkeit verwendet wird, liegen gültige Werte zwischen - 10^38 +1 und 10^38 - 1. Die ISO-Synonyme für **decimal** sind **Dec** und **Dec (***p*, *s***)**. **numerische** ist funktionell gleichwertig mit **decimal**.
  
p (Precision = Genauigkeit)  
Die maximale Gesamtanzahl von Dezimalstellen, sowohl links als auch rechts vom Dezimalkomma, die gespeichert wird. Die Genauigkeit muss ein Wert zwischen 1 und der maximalen Genauigkeit von 38 sein. Die Standardgenauigkeit beträgt 18.
  
> [!NOTE]  
>  Informatica – unterstützt nur 16 signifikanten Ziffern, unabhängig von der Genauigkeit und Dezimalstellenanzahl angegeben.  
  
*s* (skalieren)  
Die Anzahl von Dezimalstellen rechts vom Dezimalkomma, die gespeichert wird. Diese Zahl subtrahiert *p* bestimmt die maximale Anzahl von Ziffern links vom Dezimaltrennzeichen an. Die maximal speicherbare Zahl an Dezimalstellen rechts vom Dezimalkomma. Skalierung muss einen Wert zwischen 0 und *p*. Der Dezimalstellenwert kann nur angegeben werden, wenn eine Genauigkeit angegeben ist. Der Standardwert ist 0; aus diesem Grund 0 < = *s* \< =  *p*. Die maximalen Speichergrößen variieren abhängig von der Genauigkeit.
  
|Genauigkeit|Speicherplatz in Bytes|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica – (über den SQL Server PDW Informatica-Connector verbunden) unterstützt nur 16 signifikanten Ziffern, unabhängig von der Genauigkeit und Dezimalstellenanzahl angegeben.  
  
## <a name="converting-decimal-and-numeric-data"></a>Konvertieren von decimal- und numeric-Daten
Für die **decimal** und **numerischen** Datentypen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jede auftretende Kombination aus Genauigkeit und Dezimalstellenanzahl als einen anderen Datentyp betrachtet. Beispielsweise **decimal(5,5)** und **decimal(5,0)** gelten als unterschiedliche Datentypen.
  
In [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen die, eine Konstante mit einem Dezimaltrennzeichen automatisch in konvertiert eine **numerischen** Daten Wert, mit die minimale Genauigkeit und Skalierung erforderlich. Die Konstante 12.345 wird z. B. in konvertiert eine **numerischen** Wert mit einer Genauigkeit von 5 und 3 Dezimalstellen.
  
Konvertieren von **decimal** oder **numerischen** auf **"float"** oder **echte** kann Genauigkeitsverlust führen. Konvertieren von **Int**, **"smallint"**, **"tinyint"**, **"float"**, **echte**, **Money** , oder **Smallmoney** entweder **decimal** oder **numerischen** einen Überlauf verursachen.
  
Standardmäßig [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerundet wird beim Konvertieren einer Zahl in einem **decimal** oder **numerischen** Wert mit einer geringeren Genauigkeit und Dezimalstellen. Wenn allerdings die Option SET ARITHABORT auf ON festgelegt ist, löst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei Auftreten eines Überlaufs einen Fehler aus. Eine Verringerung der Genauigkeit und der Anzahl der Dezimalstellen reicht zum Auslösen eines Fehlers nicht aus.
  
Beim Konvertieren von float- oder real-Werten in decimal oder numeric umfasst der decimal-Wert nie mehr als 17 Dezimalstellen. float-Werte < 5E-18 werden immer in 0 konvertiert.
  
## <a name="examples"></a>Beispiele  
Im folgende Beispiel wird eine Tabelle mit den **decimal** und **numerischen** Datentypen.  Werte werden in jede Spalte eingefügt, und die Ergebnisse werden mithilfe einer SELECT-Anweisung zurückgegeben.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn decimal(5,2)  
,MyNumericColumn numeric(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sys.Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

