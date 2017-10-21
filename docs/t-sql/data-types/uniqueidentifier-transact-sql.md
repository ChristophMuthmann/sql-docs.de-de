---
title: "\"uniqueidentifier\" (Transact-SQL) | Microsoft Docs"
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
- uniqueidentifier
- uniqueidentifier_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- globally unique identifiers [SQL Server]
- GUIDs [SQL Server]
ms.assetid: b026035b-f3d2-4d70-989d-3884b4ca0233
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 1450aa86e3f47ef27be5acd5b5410fe40dd5983e
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

Ein 16-Byte-GUID.
  
## <a name="remarks"></a>Hinweise  
Es gibt die folgenden Möglichkeiten, um eine Spalte oder lokale Variable vom Datentyp **uniqueidentifier** zu initialisieren:
-   Mithilfe der NEWID-Funktion.  
-   Durch die Konvertierung einer Zeichenfolgenkonstanten der Form *xxxxxxxx*-*xxxx*-*xxxx*-*xxxx*-*xxxxxxxxxxxx*, in der jedes *x* für eine hexadezimale Ziffer zwischen 0 und 9 bzw. a und f steht. Beispielsweise ist 6F9619FF-8B86-D011-B42D-00C04FC964FF ein gültiger **uniqueidentifier** -Wert.  
  
Vergleichsoperatoren können mit **uniqueidentifier** -Werten verwendet werden. Allerdings erfolgt das Sortieren nicht durch Vergleichen der Bitmuster der beiden Werte. Die einzigen Operationen, die gegen erfolgen können eine **"uniqueidentifier"** Wert sind Vergleiche (= <>, \<, >, \<=, > =) und das Überprüfen auf NULL (IS NULL und IS NOT NULL). Es können keine weiteren arithmetischen Operatoren verwendet werden. Alle Spalteneinschränkungen und -eigenschaften, außer der IDENTITY-Eigenschaft, können mit dem **uniqueidentifier** -Datentyp verwendet werden.
  
Die Merge- und die Transaktionsreplikation mit Abonnements mit Update verwenden **uniqueidentifier** -Spalten. Dadurch wird sichergestellt, dass die Zeilen über mehrere Kopien der Tabelle hinweg eindeutig identifiziert werden.
  
## <a name="converting-uniqueidentifier-data"></a>Konvertieren von uniqueidentifier-Daten  
Der **uniqueidentifier** -Typ wird bei der Konvertierung von Zeichenausdrücken als Zeichentyp behandelt und unterliegt daher den Kürzungsregeln für die Konvertierung in einen Zeichentyp. Das heißt, wenn Zeichenausdrücke in einen Zeichendatentyp mit einer anderen Größe konvertiert werden, dann werden Werte, die für den neuen Datentyp zu lang sind, abgeschnitten. Siehe den Abschnitt "Beispiele".
  
## <a name="limitations-and-restrictions"></a>Einschränkungen

Diese Tools und Funktionen unterstützen nicht die `uniqueidentifier` -Datentyp:
- PolyBase
- [Dwloader laden Tool](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader) für Parallel Data Warehouse

## <a name="examples"></a>Beispiele  
Das folgende Beispiel konvertiert einen `uniqueidentifier` -Wert in einen `char` -Datentyp.
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
Im folgenden Beispiel wird das Abschneiden von Daten veranschaulicht, wenn der Wert zu lang für den Datentyp ist, in den er konvertiert wird. Da der **uniqueidentifier** -Typ auf 36 Zeichen beschränkt ist, werden die Zeichen, die diese Länge überschreiten, abgeschnitten.
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[NEWID &#40; Transact-SQL &#41;](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID &#40; Transact-SQL &#41; ](../../t-sql/functions/newsequentialid-transact-sql.md) 
 [Festgelegt @local_variable &#40; Transact-SQL &#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  

