---
title: AT TIME ZONE (Transact-SQL) | Microsoft-Dokumentation
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: eab5b57e48c0eb1b11e09b228a29d78bfe45aa10
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="at-time-zone-transact-sql"></a>AT TIME ZONE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Konvertiert einen *inputdate*-Wert in den entsprechenden *datetimeoffset*-Wert in der Zielzeitzone. Wenn *inputdate* ohne Offsetinformationen bereitgestellt wird, wendet die Funktion den Zeitzonenoffset an und setzt dabei voraus, dass der *inputdate*-Wert in der Zielzeitzone bereitgestellt wird. Wenn *inputdate* als *datetimeoffset*-Wert bereitgestellt wird, rechnet die **AT TIME ZONE**-Klausel den Wert mithilfe der Umrechnungsregeln der Zielzeitzone in die Zielzeitzone um.  
  
 Die Implementierung von **AT TIME ZONE** hängt von einem Windows-Mechanismus zum Umrechnen von **datetime**-Werten in verschiedene Zeitzonen ab.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>Argumente  
 *inputdate*  
 Ein Ausdruck, der in einen der folgenden Werte aufgelöst werden kann: **smalldatetime**, **datetime**, **datetime2** oder **datetimeoffset**.  
  
 *timezone*  
 Name der Zielzeitzone. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] basiert auf in der Windows-Registrierung gespeicherten Zeitzonen. Alle auf dem Computer installierten Zeitzonen sind in der folgenden Registrierungsstruktur gespeichert: **KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones**. Eine Liste der installierten Zeitzonen wird auch über die [sys.time_zone_info &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md)-Sicht angezeigt.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Datentyp von **datetimeoffset** zurück.  
  
## <a name="return-value"></a>Rückgabewert  
 Der **datetimeoffset**-Wert in der Zielzeitzone.  
  
## <a name="remarks"></a>Remarks  
 **AT TIME ZONE** wendet bestimmte Regeln für die Umrechnung von Eingabewerten in die Datentypen **smalldatetime**, **datetime** und **datetime2** an, die in einem Intervall liegen, das durch den Wechsel zur Sommerzeit bestimmt wird:  
  
-   Wenn die Uhr vorgestellt wird, entsteht in der Ortszeit eine Lücke, deren Dauer von der Uhrzeitanpassung abhängt (in der Regel eine Stunde, kann jedoch je nach Zeitzone auch 30 oder 45 Minuten betragen). In diesem Fall werden Zeitpunkte innerhalb dieser Lücke mit dem Offset *nach* dem Wechsel zur Sommerzeit umgerechnet.  
  
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
  
- Wenn die Uhr wieder zurückgestellt wird, überschneiden sich zwei Stunden der Ortszeit um eine Stunde.  In diesem Fall werden Zeitpunkte im Überlappungsintervall mit dem Offset *vor* der Uhrzeitumstellung dargestellt:  
  
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

Da Informationen (wie Zeitzonenregeln) außerhalb von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] gespeichert und von Zeit zu Zeit geändert werden, wird die **AT TIME ZONE**-Funktion als nicht deterministisch klassifiziert. 
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. Hinzufügen des Zielzeitzonenoffsets zu datetime ohne Offsetinformationen  
 Verwenden Sie **AT TIME ZONE** zum Hinzufügen des Offsets basierend auf Zeitzonenregeln, wenn Sie wissen, dass die ursprünglichen **datetime**-Werte in derselben Zeitzone bereitgestellt werden:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>B. Umrechnen von Werten zwischen verschiedenen Zeitzonen  
 Im folgenden Beispiel werden Werte zwischen verschiedenen Zeitzonen umgerechnet:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>C. Abfragen von temporalen Tabellen mithilfe der lokalen Zeitzone  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datums- und Uhrzeittypen](../../t-sql/data-types/date-and-time-types.md)   
 [Date and Time Data Types and Functions &#40;Transact-SQL&#41; (Datums- und Uhrzeitdatentypen und zugehörige Funktionen (Transact-SQL))](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  
