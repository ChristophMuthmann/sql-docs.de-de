---
title: nchar und nvarchar (Transact-SQL) | Microsoft-Dokumentation
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
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4c3f2e9ad1d63992be8f4e4a4c65d821fae73389
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar und nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Zeichendatentypen, bei denen es sich um Unicode-Daten entweder fester Länge (**nchar**) oder variabler Länge (**nvarchar**) handelt und die den UNICODE UCS-2-Zeichensatz verwenden.
  
## <a name="arguments"></a>Argumente  
**nchar** [ ( n ) ]  
Unicode-Zeichenfolgendaten mit fester Länge. *n* definiert die Zeichenfolgenlänge und muss ein Wert von 1 bis 4.000 sein. Die Speichergröße beträgt zweimal *n* Byte. Auch wenn die Sortierungscodepage Doppelbytezeichen verwendet, ist die Speichergröße nach wie vor *n* Byte. Je nach Zeichenfolge kann die Speichergröße von *n* Byte weniger als der für *n* angegebene Wert betragen. Die ISO-Synonyme für **nchar** lauten **national char** und **national character**.
  
**nvarchar** [ ( n | **max** ) ]  
Unicode-Zeichenfolgendaten variabler Länge. *n* definiert die Zeichenfolgenlänge und kann ein Wert von 1 bis 4.000 sein. **max** gibt an, dass die maximale Speichergröße 2^31-1 Zeichen (2 GB) beträgt. Die Speichergröße in Bytes beträgt zweimal die tatsächliche Länge der eingegebenen Daten + 2 Byte. Die ISO-Synonyme für **nvarchar** lauten **national char varying** und **national character varying**.
  
## <a name="remarks"></a>Remarks  
Wenn *n* in einer Datendefinitions- oder Variablendeklarationsanweisung nicht angegeben ist, beträgt die Standardlänge 1. Wenn *n* in der CAST-Funktion nicht angegeben ist, beträgt die Standardlänge 30.
  
Verwenden Sie **nchar**, wenn die Größen der Spaltendateneinträge wahrscheinlich ähnlich sein werden.
  
Verwenden Sie **nvarchar**, wenn die Größen der Spaltendateneinträge wahrscheinlich stark variieren werden.
  
**sysname** ist ein vom System bereitgestellter benutzerdefinierter Datentyp, der funktional **nvarchar(128)** entspricht, außer dass er keine NULL-Werte zulässt. **sysname** wird zum Verweisen auf Datenbankobjektnamen verwendet.
  
Objekten, die **nchar** or **nvarchar** verwenden, wird die Standardsortierung der Datenbank zugewiesen, es sei denn, mithilfe der COLLATE-Klausel wird eine bestimmte Sortierung zugewiesen.
  
SET ANSI_PADDING hat für **nchar** und **nvarchar** immer den Wert ON. SET ANSI_PADDING OFF gilt nicht für die Datentypen **nchar** oder **nvarchar**.
  
Unicode-Zeichenfolgenkonstanten mit dem vorausgehenden Buchstaben „N“. Ohne dieses wird die Zeichenfolge in die Standardcodepage der Datenbank konvertiert. Diese Standardcodepage erkennt möglicherweise bestimmte Zeichen nicht.
 
> [!NOTE]  
>  Wenn einer Zeichenfolgenkonstante der Buchstabe „N“ vorausgeht, gibt die implizite Konvertierung eine Unicode-Zeichenfolge zurück, wenn die Konstante, die konvertiert werden soll, die maximale Länge für einen Datentyp für Unicode-Zeichenfolgen (4.000) nicht überschreitet. Andernfalls hat die implizite Konvertierung Unicode mit höheren Werten (max) zur Folge.
  
> [!WARNING]  
>  Jede **varchar(max)**- oder **nvarchar(max)**-Spalte, die ungleich NULL ist, erfordert 24 Byte an zusätzlicher fester Verteilung, die während eines Sortiervorgangs hinsichtlich des Zeilenlimits von 8.060 Byte gelten. Dies kann zur Erstellung einer impliziten Beschränkung der Anzahl der **varchar(max)**- oder **nvarchar(max)**-Spalten führen, die ungleich NULL sind und in einer Tabelle erstellt werden können. Beim Erstellen der Tabelle (außerhalb der üblichen Warnung darüber, dass die maximale Zeilengröße das zulässige Maximum von 8.060 Bytes überschreitet) oder zum Zeitpunkt der Dateneinfügung wird kein spezieller Fehler ausgegeben. Diese große Zeilengröße kann während einiger normaler Vorgänge Fehler (z. B. Fehler 512) verursachen. Dazu gehören z. B. die Aktualisierung des gruppierten Indexschlüssels oder Teile des vollständigen Spaltensatzes. Bis zum Ausführen eines Vorgangs können Benutzer diese Fehler nicht vorhersehen.  
  
## <a name="converting-character-data"></a>Konvertieren von Zeichendaten  
Informationen zum Konvertieren von Zeichendaten finden Sie unter [char und varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
## <a name="examples"></a>Beispiele  
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyNCharColumn nchar(15)  
,MyNVarCharColumn nvarchar(20)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (N'Test data', N'More test data');  
GO  
SELECT MyNCharColumn, MyNVarCharColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyNCharColumn   MyNVarCharColumn  
--------------- --------------------  
Test data       More test data  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)
  
  
