---
title: Zuordnen von CLR-Parameterdaten | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ffefa60797d41fc6660e82c208265153eacbd603
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="mapping-clr-parameter-data"></a>Zuordnen von CLR-Parameterdaten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Die folgende Tabelle enthält [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen, ihre Entsprechungen in die common Language Runtime (CLR) für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der **System.Data.SqlTypes** -Namespace und ihre systemeigenen CLR-Entsprechungen in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
||||  
|-|-|-|  
|**SQL Server-Datentyp**|Typ (in System.Data.SqlTypes oder Microsoft.SqlServer.Types)|**CLR-Datentyp ((.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, Nullable\<Int64>**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**Boolean "," NULL-Werte zulassen\<booleschen >**|  
|**char**|Keine|Keine|  
|**Cursor**|Keine|Keine|  
|**Datum**|**SqlDateTime**|**DateTime, Nullable\<DateTime>**|  
|**datetime**|**SqlDateTime**|**DateTime, Nullable\<DateTime>**|  
|**datetime2**|Keine|**DateTime, Nullable\<DateTime>**|  
|**DATETIMEOFFSET**|**InclusionThresholdSetting**|**"DateTimeOffset", NULL-Werte zulassen\<"DateTimeOffset" >**|  
|**decimal**|**SqlDecimal**|**Decimal, Nullable\<Decimal>**|  
|**float**|**SqlDouble**|**Double, Nullable\<Double>**|  
|**geography**|**SqlGeography**<br /><br /> **"Sqlgeography"** ist definiert in Microsoft.SqlServer.Types.dll wird mit SQL Server installiert und kann von heruntergeladen werden die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [-feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|Keine|  
|**Geometrie**|**SqlGeometry**<br /><br /> **"Sqlgeometry"** ist definiert in Microsoft.SqlServer.Types.dll wird mit SQL Server installiert und kann von heruntergeladen werden die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [-feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|Keine|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **Fehler bei SqlHierarchyId** ist definiert in Microsoft.SqlServer.Types.dll wird mit SQL Server installiert und kann von heruntergeladen werden die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [-feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|Keine|  
|**image**|Keine|Keine|  
|**int**|**SqlInt32**|**Int32, Nullable\<Int32>**|  
|**money**|**SqlMoney**|**Decimal, Nullable\<Decimal>**|  
|**nchar**|**SqlChars, SqlString**|**String, Char[]**|  
|**ntext**|Keine|Keine|  
|**numeric**|**SqlDecimal**|**Decimal, Nullable\<Decimal>**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** ist eine bessere Übereinstimmung für Datenübertragungen und Datenzugriff, und **SQLString** ist eine bessere Übereinstimmung für Vorgänge der Zeichenfolge.|**String, Char[]**|  
|**nvarchar(1), nchar(1)**|**SqlChars, SqlString**|**Char, String, Char[], Nullable\<char>**|  
|**real**|**SqlSingle** (des Bereichs von **SqlSingle**, ist jedoch größer als **real**)|**Einzelne, NULL-Werte zulassen\<einzelne >**|  
|**rowversion**|Keine|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16, NULL-Werte zulassen\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**Decimal, Nullable\<Decimal>**|  
|**sql_variant**|Keine|**Objekt**|  
|**table**|Keine|Keine|  
|**text**|Keine|Keine|  
|**Uhrzeit**|Keine|**TimeSpan, Nullable\<TimeSpan>**|  
|**timestamp**|Keine|Keine|  
|**tinyint**|**SqlByte**|**Byte, Nullable\<Byte>**|  
|**uniqueidentifier**|**SqlGuid**|**GUID, die NULL-Werte zulassen\<Guid >**|  
|**Benutzerdefinierte type(UDT)**|Keine|Dieselbe Klasse, die in derselben Assembly oder einer abhängigen Assembly an den benutzerdefinierten Typ gebunden ist.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**byte, Byte[], Nullable\<byte>**|  
|**varchar**|Keine|Keine|  
|**xml**|**SqlXml**|Keine|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Automatische Datentypkonvertierung mit Out-Parametern  
 Eine CLR-Methode kann Informationen an den aufrufenden Code oder Anwendung zurückgeben, markieren Sie zunächst einen Eingabeparameter mit dem **out** Modifizierer (Microsoft Visual c#) oder  **\<Out() > ByRef** (Microsoft Visual Basic) Wenn der Eingabeparameter ein CLR-Datentyp in ist die **System.Data.SqlTypes** Namespace und dem aufrufenden Programm gibt an, dessen Entsprechung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp als Eingabeparameter, erfolgt automatisch, eine Konvertierung vom Typ Wenn die CLR-Methode den Datentyp zurückgegeben.  
  
 Beispielsweise weist die folgenden CLR-gespeicherte Prozedur Eingabeparameter des **SqlInt32** CLR-Datentyp, der mit gekennzeichnet ist **out** (c#) oder  **\<Out() > ByRef** () Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ … }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
…  
End Sub  
```  
  
 Nachdem die Assembly erstellt und in der Datenbank erstellt wird, wird die gespeicherte Prozedur erstellt, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit dem folgenden Transact-SQL, gibt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentyp des **Int** als OUTPUT-Parameter:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Bei der CLR-gespeicherte Prozedur aufgerufen wird, die **SqlInt32** -Datentyp wird automatisch konvertiert, um eine **Int** -Datentyp, und an das aufrufende Programm zurückgegeben.  
  
 Allerdings können nicht alle CLR-Datentypen automatisch durch einen Out-Parameter in ihre entsprechenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen konvertiert werden. In der folgenden Tabelle werden diese Ausnahmen aufgeführt.  
  
|||  
|-|-|  
|**CLR-Datentyp (SQL Server)**|**SQL Server-Datentyp**|  
|**Decimal**|smallmoney|  
|**SqlMoney**|smallmoney|  
|**Decimal**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Hinzugefügt **"sqlgeography"**, **"sqlgeometry"**, und **SqlHierarchyId** Typen, um der Zuordnungstabelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Datentypen in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
