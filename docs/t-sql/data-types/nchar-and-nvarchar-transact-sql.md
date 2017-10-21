---
title: Nchar und Nvarchar (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc7de3b64519f3d0fd1f2e9557ccf7196e3f07a8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar und nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Zeichendatentypen, die entweder fester Länge sind **Nchar**, oder variabler Länge, **Nvarchar**, Unicode-Daten und verwenden den UNICODE UCS-2-Zeichensatz.
  
## <a name="arguments"></a>Argumente  
**NCHAR** [(n)]  
Unicode-Zeichenfolgendaten mit fester Länge. *n*definiert die Zeichenfolgenlänge und muss ein Wert zwischen 1 und 4.000 sein. Die Speichergröße beträgt zweimal  *n*  Bytes. Wenn die Codeseite der zielsortierung Doppelbytezeichen verwendet, ist immer noch die Speichergröße  *n*  Bytes. Je nach der Zeichenfolge, die Speichergröße der  *n*  Bytes können kleiner sein als der angegebene Wert für  *n* . Die ISO-Synonyme für **Nchar** sind **national Char** und **nationaler Zeichensätze**...
  
**Nvarchar** [(n | **Max** )]  
Unicode-Zeichenfolgendaten variabler Länge. *n*definiert die Zeichenfolgenlänge und kann ein Wert zwischen 1 und 4.000 sein. **Max.** gibt an, dass die maximale Speichergröße 2 ^ 31-1 Bytes (2 GB). Die Speichergröße in Bytes beträgt zweimal die tatsächliche Länge der eingegebenen Daten + 2 Byte. Die ISO-Synonyme für **Nvarchar** sind **national Char varying** und **nationaler Zeichensätze varying**.
  
## <a name="remarks"></a>Hinweise  
Wenn  *n*  ist nicht angegeben in einer Datendefinitions- oder variablendeklarationsanweisung, die Standardlänge 1. Wenn  *n*  ist nicht angegeben mit der CAST-Funktion, die Standardlänge ist 30.
  
Verwendung **Nchar** Wenn die Größen der spaltendateneinträge spaltendateneinträge wahrscheinlich ähnlich sein.
  
Verwendung **Nvarchar** Wenn die Größen der spaltendateneinträge spaltendateneinträge wahrscheinlich stark variieren.
  
**Sysname** ist ein vom System bereitgestellten benutzerdefinierten Datentyp, der funktional **vom Datentyp nvarchar(128)**, außer dass es keine NULL-Werte zulässt. **Sysname** wird verwendet, um die Namen von Datenbankobjekten zu verweisen.
  
Objekten, **Nchar** oder **Nvarchar** werden die standardsortierung der Datenbank zugewiesen, es sei denn, eine bestimmte Sortierung zugewiesen ist, mithilfe der COLLATE-Klausel.
  
SET ANSI_PADDING ist immer auf für **Nchar** und **Nvarchar**. SET ANSI_PADDING OFF gilt nicht für die **Nchar** oder **Nvarchar** Datentypen.
  
Unicode-Zeichenfolgenkonstanten mit den Buchstaben n-Präfix Ohne das Präfix N ist die Zeichenfolge in die Standardcodepage der Datenbank konvertiert. Diese Standardcodepage erkennt möglicherweise bestimmte Zeichen nicht.
 
> [!NOTE]  
>  Wenn eine Zeichenfolgenkonstante, die mit dem Buchstaben N vorangestellt, kommen die implizite Konvertierung in eine Unicode-Zeichenfolge die Konstante konvertiert die maximale Länge für eine Unicode-Zeichenfolgen-Datentyp (4000) nicht überschreitet. Andernfalls wird die implizite Konvertierung in einen Unicode-umfangreichen Werten (Max) zurückgegeben.
  
> [!WARNING]  
>  Jeder Wert ungleich Null **varchar(max)** oder **nvarchar(max)** Spalte erfordert eine zusätzliche feste Verteilung, das für das Zeilenlimit von 8.060 Byte während eines Sortiervorgangs zählt 24 Bytes. Dies kann zur Erstellung einer impliziten Beschränkung der Anzahl der nicht-Null **varchar(max)** oder **nvarchar(max)** Spalten, die in einer Tabelle erstellt werden können. Beim Erstellen der Tabelle (außerhalb der üblichen Warnung darüber, dass die maximale Zeilengröße das zulässige Maximum von 8.060 Bytes überschreitet) oder zum Zeitpunkt der Dateneinfügung wird kein spezieller Fehler ausgegeben. Diese große Zeilengröße kann während einiger normaler Vorgänge Fehler (z. B. Fehler 512) verursachen. Dazu gehören z. B. die Aktualisierung des gruppierten Indexschlüssels oder Teile des vollständigen Spaltensatzes. Bis zum Ausführen eines Vorgangs können Benutzer diese Fehler nicht vorhersehen.  
  
## <a name="converting-character-data"></a>Konvertieren von Zeichendaten  
Informationen zum Konvertieren von Zeichendaten finden Sie unter [Char und Varchar &#40; Transact-SQL &#41; ](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
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
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[WIE &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)
  
  

