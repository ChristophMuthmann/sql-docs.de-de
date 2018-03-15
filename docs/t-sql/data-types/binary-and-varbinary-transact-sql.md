---
title: binary und varbinary (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 8/16/2017
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
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs:
- TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4ad5bce3cacc0f892f7087df785da8cedcb4e932
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="binary-and-varbinary-transact-sql"></a>binary und varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Binäre Datentypen mit fester Länge bzw. mit variabler Länge.
  
## <a name="arguments"></a>Argumente  
**binary** [ ( *n* ) ] Binärdaten mit einer festen Länge von *n* Bytes, wobei *n* einen Wert von 1 bis 8000 haben kann. Die Speichergröße beträgt *n* Byte.
  
**varbinary** [ ( *n* | **max**) ] Binärdaten variabler Länge. *n* kann ein Wert zwischen 1 und 8000 sein. **max** gibt an, dass die maximale Speichergröße 2^31-1 Byte beträgt. Die Speicherplatzgröße ist die tatsächliche Länge der eingegebenen Daten + 2 Byte. Die eingegebenen Daten können 0 Byte lang sein. Das ANSI SQL-Synonym für **varbinary** ist **binary varying**.
  
## <a name="remarks"></a>Remarks  
Wenn *n* in einer Datendefinitions- oder Variablendeklarationsanweisung nicht angegeben ist, beträgt die Standardlänge 1. Wenn *n* in der CAST-Funktion nicht angegeben ist, beträgt die Standardlänge 30.

| Datentyp | Verwenden Sie |
| --- | --- |
| **binary** | , wenn die Dateneinträge einer Spalte jeweils gleich lang sind.|
| **varbinary** | , wenn sich die Dateneinträge einer Spalte in ihrer Größe erheblich unterscheiden.|
| **varbinary(max)** | , wenn die Spaltendateneinträge 8000 Byte überschreiten.|


## <a name="converting-binary-and-varbinary-data"></a>Konvertieren von binary- und varbinary-Daten
Wenn Daten von einem Zeichenfolgendatentyp (**char**, **varchar**, **nchar**, **nvarchar**, **binary**, **varbinary**, **text**, **ntext** oder **image**) in einen **binary**- oder **varbinary**-Datentyp anderer Länge konvertiert werden, füllt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Daten nach rechts auf oder schneidet sie rechts ab. Bei der Konvertierung anderer Datentypen in **binary** oder **varbinary** werden die Daten nach links aufgefüllt oder links abgeschnitten. Für die Auffüllung werden hexadezimale Nullen verwendet.
  
Das Konvertieren von Daten in die Datentypen **binary** und **varbinary** ist hilfreich, wenn **binary**-Daten die einfachste Möglichkeit zum Verschieben von Daten darstellen. Beim Konvertieren aller Werte eines beliebigen Datentyps in einen ausreichend großen binären Wert und dem anschließenden Konvertieren in den ursprünglichen Datentyp ergibt sich stets derselbe Wert, wenn beide Konvertierungen mit der gleichen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt werden. Die binäre Darstellung eines Werts kann sich zwischen den Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ändern.
  
Sie können die Datentypen **int**, **smallint** und **tinyint** in die Datentypen **binary** oder **varbinary** konvertieren. Wenn Sie allerdings den **binary**-Wert wieder zurück in einen ganzzahligen Wert konvertieren, kann das Ergebnis von der ursprünglichen ganzen Zahl abweichen, falls der Wert abgeschnitten wurde. Die folgende SELECT-Anweisung zeigt beispielsweise, dass der ganzzahlige Wert `123456` in der Regel als binärer Wert `0x0001e240` gespeichert wird:
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
Diese `SELECT`-Anweisung zeigt, dass die vorangestellten Nullen automatisch abgeschnitten werden, wenn das **binary**-Ziel für die Aufnahme des gesamten Werts zu klein ist. Die gleiche Zahl wird daher als `0xe240` gespeichert:
  
```sql
SELECT CAST( 123456 AS BINARY(2) );  
```  
  
Der folgende Batch zeigt, dass sich das automatische Abschneiden des Werts auf arithmetische Operationen auswirken kann, ohne dass ein Fehler ausgelöst wird:
  
```sql
DECLARE @BinaryVariable2 BINARY(2);  
  
SET @BinaryVariable2 = 123456;  
SET @BinaryVariable2 = @BinaryVariable2 + 1;  
  
SELECT CAST( @BinaryVariable2 AS INT);  
GO  
```  
  
Das endgültige Ergebnis ist `57921` und nicht `123457`.
  
> [!NOTE]  
>  Konvertierungen zwischen einem beliebigen Datentyp und den **binary**-Datentypen sind bei unterschiedlichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Versionen nicht unbedingt identisch.  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypkonvertierung &#40;Datenbank-Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
