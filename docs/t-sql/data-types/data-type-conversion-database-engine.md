---
title: Datentypkonvertierung (Datenbankmodul) | Microsoft Docs
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
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0ed7f8e0e681de9f962e3eb963c0af315a0c25c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-conversion-database-engine"></a>Datentypkonvertierung (Datenbankmodul)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Datentypen können in den folgenden Szenarien konvertiert werden:
-   Wenn Daten aus einem Objekt zu einem anderen Objekt verschoben oder mit diesem verglichen oder kombiniert werden, müssen die Daten möglicherweise vom Datentyp des einen Objekts in den Datentyp des anderen Objekts konvertiert werden.  
-   Wenn Daten aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Ergebnisspalte, Rückgabecode und Ausgabeparameter eine Programmvariable verschoben wird, müssen die Daten konvertiert werden, aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemdatentyp in den Datentyp der Variablen.  
  
Bei der Konvertierung zwischen einer Anwendungsvariablen und einer Resultsetspalte, einem Rückgabecode, einem Parameter oder Parametermarker von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die unterstützten Datentypkonvertierungen von der Datenbank-API (Application Programming Interface, Anwendungsprogrammierschnittstelle) definiert.
  
## <a name="implicit-and-explicit-conversion"></a>Implizite und explizite Konvertierung
Datentypen können entweder implizit oder explizit konvertiert werden.
  
Implizite Konvertierungen sind für den Benutzer nicht sichtbar. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] konvertiert die Daten automatisch von einem Datentyp in einen anderen. Beispielsweise, wenn eine **"smallint"** im Vergleich zu einer **Int**, die **"smallint"** wird implizit in konvertiert **Int** vor dem Vergleich wird fortgesetzt.
  
**GETDATE()** implizit das Datumsformat 0 konvertiert. **SYSDATETIME()** implizit konvertiert das Datumsformat 21.
  
Explizite Konvertierungen verwenden die Funktionen CAST oder CONVERT.
  
Die [CAST und CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) Funktionen einen Wert (eine lokale Variable, eine Spalte oder einen anderen Ausdruck) von einem Datentyp in einen anderen zu konvertieren. Die folgende `CAST`-Funktion konvertiert z. B. den numerischen Wert `$157.27` in die Zeichenfolge `'157.27'`:
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
Verwenden Sie CAST anstelle von CONVERT, wenn der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Programmcode dem ISO-Standard entsprechen soll. Verwenden Sie hingegen CONVERT anstelle von CAST, wenn Sie die Vorteile der Formatfunktionen in CONVERT nutzen möchten.
  
In der folgenden Abbildung werden alle expliziten und impliziten Datentypkonvertierungen aufgeführt, die für die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-System bereitgestellten Datentypen zulässig sind. Dazu gehören **Xml**, **"bigint"**, und **Sql_variant**. Es gibt keine implizite Konvertierung bei der Zuweisung vom der **Sql_variant** -Datentyp, aber es die implizite Konvertierung in ist **Sql_variant**.
  
![Datentyp-Konvertierungstabelle](../../t-sql/data-types/media/lrdatahd.png "Datentyp-Konvertierungstabelle")
  
## <a name="data-type-conversion-behaviors"></a>Verhalten bei der datentypkonvertierung
Einige implizite und explizite Datentypkonvertierungen werden nicht unterstützt, wenn Sie den Datentyp eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekts in einen anderen konvertieren. Angenommen, ein **Nchar** Wert kann nicht konvertiert werden, um eine **Image** Wert. Ein **Nchar** können nur auf umgestellt werden **binäre** mithilfe der expliziten Konvertierung, eine implizite Konvertierung in **binäre** wird nicht unterstützt. Allerdings ein **Nchar** explizit oder implizit konvertiert werden können **Nvarchar**.
  
In den folgenden Themen wird das Konvertierungsverhalten der entsprechenden Datentypen beschrieben:
  
 - [binary und varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [Money und Smallmoney &#40; Transact-SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [Bit- &#40; Transact-SQL &#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [Smalldatetime &#40; Transact-SQL &#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char und varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [Decimal und Numeric &#40; Transact-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [Float und Real &#40; Transact-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [Zeit &#40; Transact-SQL &#41;](../../t-sql/data-types/time-transact-sql.md)  
 - ["DateTime" &#40; Transact-SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [Int, Bigint, Smallint und Tinyint &#40; Transact-SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - ["uniqueidentifier" &#40; Transact-SQL &#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>Konvertieren von Datentypen mithilfe von gespeicherten Prozeduren der OLE-Automatisierung  
Da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]-Datentypen und die OLE-Automatisierung [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Datentypen verwendet, müssen die gespeicherten Prozeduren der OLE-Automatisierung übergebene Daten konvertieren.
  
In der folgenden Tabelle werden die Konvertierungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Datentypen dargestellt.
  
|SQL Server-Datentyp|Visual Basic-Datentyp|  
|--------------------------|----------------------------|  
|**Char**, **Varchar**, **Text**, **Nvarchar**, **Ntext**|**String**|  
|**Decimal**, **numerischen**|**String**|  
|**bit**|**Boolean**|  
|**binäre**, **Varbinary**, **Bild**|Eindimensionale **Zeichen** Array|  
|**int**|**Long**|  
|**smallint**|**Integer**|  
|**tinyint**|**Byte**|  
|**float**|**Double**|  
|**real**|**Single**|  
|**money**, **smallmoney**|**Währung**|  
|**"DateTime"**, **Smalldatetime**|**Datum**|  
|Beliebige auf NULL festgelegte Typen|**Variant** auf Null gesetzt|  
  
Alle einzelnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Werte in einer einzelnen konvertiert [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] Wert mit Ausnahme von **binäre**, **Varbinary**, und **Image** Werte. Diese Werte werden in ein eindimensionales konvertiert **Zeichen** array [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Dieses Array weist einen Bereich von **Byte (**0 bis *Länge*1**)** , in denen *Länge* ist die Anzahl der Bytes in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  **binäre**, **Varbinary**, oder **Image** Werte.
  
Im Folgenden sehen Sie die Konvertierungen von [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Datentypen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen.
  
|Visual Basic-Datentyp|SQL Server-Datentyp|  
|----------------------------|--------------------------|  
|**Lange**, **Ganzzahl**, **Byte**, **booleschen**, **Objekt**|**int**|  
|**Doppelte**, **einzelne**|**float**|  
|**Währung**|**money**|  
|**Datum**|**datetime**|  
|**Zeichenfolge** mit 4000 Zeichen oder weniger|**Varchar**/**Nvarchar**|  
|**Zeichenfolge** mit mehr als 4000 Zeichen|**Text**/**Ntext**|  
|Eindimensionale **Zeichen** Array mit 8000 Bytes oder weniger|**varbinary**|  
|Eindimensionale **Zeichen** Array mit mehr als 8000 Bytes|**image**|  
  
## <a name="see-also"></a>Siehe auch
[Gespeicherte OLE-Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  

