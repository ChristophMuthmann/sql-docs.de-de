---
title: Datentypkonvertierung (Datenbank-Engine) | Microsoft-Dokumentation
ms.custom: 
ms.date: 7/23/2017
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
- CAST function
- converting data types [SQL Server]
- CONVERT function
- data types [SQL Server], converting
- implicit data type conversions
- explicit data type conversions [SQL Server]
- converting data types [SQL Server], about converting data types
ms.assetid: ffacf45e-a488-48d0-9bb0-dcc7fd365299
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 811eacd3dc0cbbd622fc6eac6ad91a6e740554f4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="data-type-conversion-database-engine"></a>Datentypkonvertierung (Datenbank-Engine)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Datentypen können in den folgenden Szenarien konvertiert werden:
-   Wenn Daten aus einem Objekt zu einem anderen Objekt verschoben oder mit diesem verglichen oder kombiniert werden, müssen die Daten möglicherweise vom Datentyp des einen Objekts in den Datentyp des anderen Objekts konvertiert werden.  
-   Wenn Daten aus einer Ergebnisspalte, einem Rückgabecode oder einem Ausgabeparameter von [!INCLUDE[tsql](../../includes/tsql-md.md)] in eine Programmvariable verschoben werden, müssen die Daten vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp in den Datentyp der Variablen konvertiert werden.  
  
Bei der Konvertierung zwischen einer Anwendungsvariablen und einer Resultsetspalte, einem Rückgabecode, einem Parameter oder Parametermarker von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die unterstützten Datentypkonvertierungen von der Datenbank-API (Application Programming Interface, Anwendungsprogrammierschnittstelle) definiert.
  
## <a name="implicit-and-explicit-conversion"></a>Implizite und explizite Konvertierung
Datentypen können entweder implizit oder explizit konvertiert werden.
  
Implizite Konvertierungen sind für den Benutzer nicht sichtbar. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] konvertiert die Daten automatisch von einem Datentyp in einen anderen. Beispielsweise wird beim Vergleich eines **smallint**-Datentyps mit einem **int**-Datentyp der **smallint**-Datentyp implizit in **int** konvertiert, bevor der Vergleich fortgesetzt wird.
  
**GETDATE()** konvertiert das Datumsformat implizit in 0. **SYSDATETIME()** konvertiert das Datumsformat implizit in 21.
  
Explizite Konvertierungen verwenden die Funktionen CAST oder CONVERT.
  
Die Funktionen [CAST und CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) konvertieren einen Wert (eine lokale Variable, eine Spalte oder einen anderen Ausdruck) von einem Datentyp in einen anderen. Die folgende `CAST`-Funktion konvertiert z. B. den numerischen Wert `$157.27` in die Zeichenfolge `'157.27'`:
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
Verwenden Sie CAST anstelle von CONVERT, wenn der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Programmcode dem ISO-Standard entsprechen soll. Verwenden Sie hingegen CONVERT anstelle von CAST, wenn Sie die Vorteile der Formatfunktionen in CONVERT nutzen möchten.
  
In der folgenden Abbildung werden alle expliziten und impliziten Datentypkonvertierungen aufgeführt, die für die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-System bereitgestellten Datentypen zulässig sind. Dazu gehören **xml**, **bigint** und **sql_variant**. Es gibt keine implizite Konvertierung bei der Zuweisung vom **sql_variant**-Datentyp, eine implizite Konvertierung zum **sql_variant**-Datentyp findet jedoch statt.
  
![Konvertierungstabelle für Datentypen](../../t-sql/data-types/media/lrdatahd.png "Data type conversion table")
  
## <a name="data-type-conversion-behaviors"></a>Verhalten bei der Datentypkonvertierung
Einige implizite und explizite Datentypkonvertierungen werden nicht unterstützt, wenn Sie den Datentyp eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekts in einen anderen konvertieren. Ein **nchar**-Wert kann nicht in einen **image**-Wert konvertiert werden. **nchar** kann nur mit der expliziten Konvertierung in **binary** konvertiert werden; eine implizite Konvertierung in **binary** wird nicht unterstützt. **nchar** kann jedoch explizit oder implizit in **nvarchar** konvertiert werden.
  
In den folgenden Themen wird das Konvertierungsverhalten der entsprechenden Datentypen beschrieben:
  
 - [binary und varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money und smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40;Transact-SQL&#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char und varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal und numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float und real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint und tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;Transact-SQL&#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>Konvertieren von Datentypen mithilfe von gespeicherten Prozeduren der OLE-Automatisierung  
Da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]-Datentypen und die OLE-Automatisierung [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Datentypen verwendet, müssen die gespeicherten Prozeduren der OLE-Automatisierung übergebene Daten konvertieren.
  
In der folgenden Tabelle werden die Konvertierungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Datentypen dargestellt.
  
|SQL Server-Datentyp|Visual Basic-Datentyp|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **text**, **nvarchar**, **ntext**|**String**|  
|**decimal**, **numeric**|**String**|  
|**bit**|**Boolean**|  
|**binary**, **varbinary**, **image**|Eindimensionales **Byte()**-Array|  
|**int**|**Long**|  
|**smallint**|**Integer**|  
|**tinyint**|**Byte**|  
|**float**|**Double**|  
|**real**|**Single**|  
|**money**, **smallmoney**|**Währung**|  
|**datetime**, **smalldatetime**|**Datum**|  
|Beliebige auf NULL festgelegte Typen|**Variant** wurde auf NULL festgelegt.|  
  
Alle einzelnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Werte mit Ausnahme der **binary**-, **varbinary**- und **image**-Werte werden in einen einzelnen [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Wert konvertiert. Diese Werte werden in ein eindimensionales **Byte()**-Array in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] konvertiert. Dieses Array weist einen Bereich von **Byte(**0 to *length*1**)** auf, wobei *length* der Anzahl von Bytes in den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Werten **binary**, **varbinary** oder **image** entspricht.
  
Im Folgenden sehen Sie die Konvertierungen von [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Datentypen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen.
  
|Visual Basic-Datentyp|SQL Server-Datentyp|  
|----------------------------|--------------------------|  
|**Long**, **Integer**, **Byte**, **Boolean**, **Object**|**int**|  
|**Double**, **Single**|**float**|  
|**Währung**|**money**|  
|**Datum**|**datetime**|  
|**String** mit maximal 4000 Zeichen|**varchar**/**nvarchar**|  
|**String** mit mehr als 4000 Zeichen|**text**/**ntext**|  
|Eindimensionales **Byte()**-Array mit maximal 8000 Byte|**varbinary**|  
|Eindimensionales **Byte()**-Array mit mehr als 8000 Byte|**image**|  
  
## <a name="see-also"></a>Siehe auch
[Gespeicherte OLE-Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
