---
title: Money und Smallmoney (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- money_TSQL
- money
- smallmoney
- smallmoney_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- money data type, about money data type
- money data type
- smallmoney data type
- values [SQL Server], monetary
- currency [SQL Server]
ms.assetid: 57861137-89ea-4b89-b361-390597d7bccc
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bd07ecd1cdacc686e0f831320fd5e939c0c174da
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="money-and-smallmoney-transact-sql"></a>money und smallmoney (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Datentypen zur Darstellung von Währungswerten.
  
## <a name="remarks"></a>Hinweise  
  
|Datentyp|Bereich|Speicherung|  
|---|---|---|
|**money**|-922.337.203.685.477,5808 zu 922.337.203.685.477,5807 (-922,337,203,685,477.58<br />Um 922,337,203,685,477.58 für Informatica –.  Informatica – unterstützt nur zwei Dezimalstellen, die nicht vier.)|8 Byte|  
|**smallmoney**|-214.748,3648 bis 214.748,3647|4 bytes|  
  
Die **Money** und **Smallmoney** Datentypen sind genau eine Zehntausendstels der dargestellten Währungseinheiten, die sie darstellen. Für Informatica – die **Money** und **Smallmoney** Datentypen sind auf eine Hundertstelsekunde der dargestellten Währungseinheiten, die sie darstellen.
  
Mit einem Punkt werden Währungsuntereinheiten, wie z. B. Cent, von ganzen Währungseinheiten getrennt. Die Zahl 2.15 gibt z. B. 2 Dollar und 15 Cent an.
  
Diese Datentypen können eines der folgenden Währungssymbole verwenden.
  
![Tabelle mit Währungssymbolen, hexadezimale Werte](../../t-sql/data-types/media/money01.gif "Tabelle mit Währungssymbolen, hexadezimale Werte")
  
Währungsdaten müssen nicht in einfache Anführungszeichen (') eingeschlossen werden. Sie sollten stets bedenken, dass Sie zwar Währungswerte angeben können, denen ein Währungssymbol vorangestellt ist, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jedoch keinerlei mit diesem Symbol verbundene Währungsinformationen speichert, sondern lediglich den nummerischen Wert.
  
## <a name="converting-money-data"></a>Konvertieren von Money-Daten
Beim Konvertieren in **Money** vom Integer-Datentypen, Einheiten wird angenommen, dass in Währungseinheiten. Beispielsweise wird der ganzzahlige Wert 4 in konvertiert die **Money** 4 Währungseinheiten entspricht.
  
Das folgende Beispiel konvertiert **Smallmoney** und **Money** Werte **Varchar** und **decimal** Datentypen.
  
```sql
DECLARE @mymoney_sm smallmoney = 3148.29,  
        @mymoney    money = 3148.29;  
SELECT  CAST(@mymoney_sm AS varchar) AS 'SM_MONEY varchar',  
        CAST(@mymoney AS decimal)    AS 'MONEY DECIMAL';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
SM_MONEY VARCHAR               MONEY DECIMAL  
------------------------------ ----------------------  
3148.29                        3148    
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) 
 [CAST und CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md) 
 [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md) 
 [Datentypen &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md) 
 [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
 [Festgelegt @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/set-local-variable-transact-sql.md) 
 [sys.types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

