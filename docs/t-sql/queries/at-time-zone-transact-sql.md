---
title: ZUR ZEITZONE (Transact-SQL) | Microsoft Docs
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0983cbd76b1ec3a71985537f098f8faf002b93e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="at-time-zone-transact-sql"></a>ZUR ZEITZONE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Konvertiert eine *Inputdate* auf den entsprechenden *"DateTimeOffset"* Wert in der Zielzeitzone. Wenn *Inputdate* erfolgt ohne Offsetinformationen, die Funktion den Offset der Zeitzone, vorausgesetzt, dass gilt *Inputdate* Wert wird angegeben, in der Zielzeitzone. Wenn *Inputdate* dient als ein *"DateTimeOffset"* Wert als **AT TIME ZONE** Klausel konvertiert sie in der Zielzeitzone, die mithilfe von Konvertierungsregeln für die Zeitzone.  
  
 **ZUR ZEITZONE** Implementierung basiert auf einem Windows-Mechanismus zu konvertierende **"DateTime"** Werte zwischen Zeitzonen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>Argumente  
 *inputdate*  
 Ist ein Ausdruck, der in aufgelöst werden kann ein **Smalldatetime**, **"DateTime"**, **datetime2**, oder **"DateTimeOffset"** Wert.  
  
 *Zeitzone*  
 Name der Zielzeitzone. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]basiert auf Zeitzonen, die in der Windows-Registrierung gespeichert sind. Alle Zeitzonen, die auf dem Computer installiert werden in der folgenden Registrierungsstruktur gespeichert: **KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zonen**. Eine Liste der installierten Zeitzonen ist ebenfalls verfügbar gemacht, durch die [Sys. time_zone_info &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) anzeigen.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Datentyp des **"DateTimeOffset"**  
  
## <a name="return-value"></a>Rückgabewert  
 Die **"DateTimeOffset"** Wert in der Zielzeitzone.  
  
## <a name="remarks"></a>Hinweise  
 **ZUR ZEITZONE** gelten bestimmte Regeln zum Konvertieren der Eingabewerte in **Smalldatetime**, **"DateTime"** und **datetime2** -Datentypen, die in fallen ein Intervall, das betroffen ist von der Änderung DST:  
  
-   Wenn die Uhr im voraus festgelegt ist, besteht eine Lücke in Ortszeit, die die Dauer hängt von der Dauer der Anpassung Uhr (in der Regel 1 Stunde, aber es kann je nach Zeitzone 30 oder 45 Minuten). In diesem Fall werden Zeitpunkten, die diese Lücke gehören konvertiert, wobei der Offset *nach* DST ändern.  
  
    ```  
    /*  
        Moving to DST in "Central European Standard Time" zone: 
        offset changes from +01:00 -> +02:00   
        Change occurred on March 29th, 2015 at 02:00:00.   
        Adjusted local time became 2015-03-29 03:00:00.  
    */  
    
    --Time before DST change has standard time offset (+01:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T01:01:00', 126)     
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 01:01:00 +01:00   
  
    /*
      Adjusted time from the "gap interval" (between 02:00 and 03:00)
      is moved 1 hour ahead and presented with the summer time offset
      (after the DST change) 
    */
    SELECT CONVERT(datetime2(0), '2015-03-29T02:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00
      
    --Time after 03:00 is presented with the summer time offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00  
  
    ```  
  
- Wenn die Uhr wieder festgelegt ist, werden 2 Stunden nach der lokalen Zeit auf eine Stunde überlappt.  In diesem Fall werden Zeitpunkten, die das überlappte Intervall gehören dargestellt, mit dem Offset *vor* die Uhr ändern:  
  
    ```  
    /*  
        Moving back from DST to standard time in 
        "Central European Standard Time" zone: 
        offset changes from +02:00 -> +01:00.  
        Change occurred on October 25th, 2015 at 03:00:00.   
        Adjusted local time became 2015-10-25 02:00:00   
    */  
    
    --Time before the change has DST offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-10-25T01:01:00', 126)      
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 01:01:00 +02:00  
    
    /*
      Time from the "overlapped interval" is presented with standard time 
      offset (before the change)    
    */
    SELECT CONVERT(datetime2(0), '2015-10-25T02:00:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 02:00:00 +02:00  
    
    
    --Time after 03:00 is regularly presented with the standard time offset (+01:00)    
    SELECT CONVERT(datetime2(0), '2015-10-25T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 03:01:00 +01:00
  
    ```  

Da einige Informationen (z. B. Timezone-Regeln), außerhalb von verwaltet wird [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und gelegentlich gerechnet werden die **AT TIME ZONE** Funktion wird als nicht deterministisch klassifiziert. 
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. Hinzufügen von Ziel Zeitzonenoffset in "DateTime" ohne Offsetinformationen  
 Verwendung **AT TIME ZONE** hinzuzufügende Offset basierend auf der Zeitzonenregeln, wenn Sie wissen, dass die ursprüngliche **"DateTime"** Werte finden Sie in der gleichen Zeitzone:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>B. Konvertieren von Werten zwischen verschiedenen Zeitzonen  
 Das folgende Beispiel konvertiert die Werte zwischen verschiedenen Zeitzonen:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>C. Abfragen von Temporalen Tabellen mit der lokalen Zeitzone  
 Im folgenden Beispiel werden Daten aus einer temporalen Tabelle ausgewählt.  
  
```  
USE AdventureWorks2016;  
GO  
  
DECLARE @ASOF datetimeoffset;  
SET @ASOF = DATEADD (month, -1, GETDATE()) AT TIME ZONE 'UTC';  
  
-- Query state of the table a month ago projecting period   
-- columns as Pacific Standard Time  
SELECT BusinessEntityID, PersonType, NameStyle, Title,   
    FirstName, MiddleName,  
    ValidFrom AT TIME ZONE 'Pacific Standard Time' 
FROM  Person.Person_Temporal  
FOR SYSTEM_TIME AS OF @ASOF;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datums- und Uhrzeittypen](../../t-sql/data-types/date-and-time-types.md)   
 [Datums- und Zeitdaten Typen und-Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  

