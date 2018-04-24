---
title: uniqueidentifier (Transact-SQL)| Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/1/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7371aba1657381e5f7b0222bed4b9b89480d2d15
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

Ein 16-Byte-GUID.
  
## <a name="remarks"></a>Remarks  
Es gibt die folgenden Möglichkeiten, um eine Spalte oder lokale Variable vom Datentyp **uniqueidentifier** zu initialisieren:
-   Durch die Verwendung der Funktionen [NEWID](../../t-sql/functions/newid-transact-sql.md) oder [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md).    
-   Durch die Konvertierung einer Zeichenfolgenkonstanten der Form *xxxxxxxx*-*xxxx*-*xxxx*-*xxxx*-*xxxxxxxxxxxx*, in der jedes *x* für eine hexadezimale Ziffer zwischen 0 und 9 bzw. a und f steht. Beispielsweise ist 6F9619FF-8B86-D011-B42D-00C04FC964FF ein gültiger **uniqueidentifier** -Wert.  
  
Vergleichsoperatoren können mit **uniqueidentifier** -Werten verwendet werden. Allerdings erfolgt das Sortieren nicht durch Vergleichen der Bitmuster der beiden Werte. Die einzigen Operationen, die für einen **uniqueidentifier**-Wert ausgeführt werden können, sind Vergleiche (=, <>, \<, >, \<=, >=) und die Überprüfung auf NULL (IS NULL und IS NOT NULL). Es können keine weiteren arithmetischen Operatoren verwendet werden. Alle Spalteneinschränkungen und -eigenschaften, außer der IDENTITY-Eigenschaft, können mit dem **uniqueidentifier** -Datentyp verwendet werden.
  
Die Merge- und die Transaktionsreplikation mit Abonnements mit Update verwenden **uniqueidentifier** -Spalten. Dadurch wird sichergestellt, dass die Zeilen über mehrere Kopien der Tabelle hinweg eindeutig identifiziert werden.
  
## <a name="converting-uniqueidentifier-data"></a>Konvertieren von uniqueidentifier-Daten  
Der **uniqueidentifier** -Typ wird bei der Konvertierung von Zeichenausdrücken als Zeichentyp behandelt und unterliegt daher den Kürzungsregeln für die Konvertierung in einen Zeichentyp. Das heißt, wenn Zeichenausdrücke in einen Zeichendatentyp mit einer anderen Größe konvertiert werden, dann werden Werte, die für den neuen Datentyp zu lang sind, abgeschnitten. Siehe den Abschnitt "Beispiele".
  
## <a name="limitations-and-restrictions"></a>Einschränkungen

Diese Tools und Features unterstützen den `uniqueidentifier`-Datentyp nicht:
- PolyBase
- [dwloader-Ladetool](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader) für Parallel Data Warehouse

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
[NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID &#40;Transact-SQL&#41;](../../t-sql/functions/newsequentialid-transact-sql.md)    
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  
