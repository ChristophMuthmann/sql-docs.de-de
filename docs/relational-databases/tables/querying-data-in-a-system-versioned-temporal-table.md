---
title: Abfragen von Daten in einer temporalen Tabelle mit Systemversionsverwaltung | Microsoft-Dokumentation
ms.custom: SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d358c2e-ebd8-4eb3-9bff-cfa598a39125
caps.latest.revision: "7"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9b9e126587a2c3a6beb34b74f234375de5a4469b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="querying-data-in-a-system-versioned-temporal-table"></a>Abfragen von Daten in einer temporalen Tabelle mit Systemversionsverwaltung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Wenn Sie den letzten (aktuellsten) Zustand der Daten in einer temporalen Tabelle abrufen möchten, können Sie die Abfrage wie gewohnt durchführen, so wie auch bei nicht temporalen Tabellen. Wenn die PERIOD-Spalten nicht ausgeblendet sind, erscheinen ihre Werte in einer SELECT \* -Abfrage. Wenn Sie die **PERIOD** -Spalten als ausgeblendet angegeben haben, erscheinen ihre Werte nicht in einer SELECT \* -Abfrage. Wenn die **PERIOD** -Spalten ausgeblendet wurden, verweisen Sie in der SELECT-Klausel explizit auf die **PERIOD** -Spalten, um die Werte für diese Spalten zurückzugeben.  
  
 Verwenden Sie die neue  **FOR SYSTEM_TIME** -Klausel mit vier temporal-spezifischen Unterklauseln zum Abfragen von Daten über die aktuellen Tabellen und Verlaufstabellen, um eine zeitbasierte Analyse jedweder Art auszuführen. Weitere Informationen zu diesen Klauseln finden Sie unter [Temporal Tables](../../relational-databases/tables/temporal-tables.md) (Temporäre Tabellen) und [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
-   AS OF <Datum>  
  
-   FROM <Startdatum_Uhrzeit> TO <Enddatum_Uhrzeit>  
  
-   BETWEEN <Startdatum_Uhrzeit> AND <Enddatum_Uhrzeit>  
  
-   CONTAINED IN (<Startdatum_Uhrzeit>, <Enddatum_Uhrzeit>)  
  
-   ALL  
  
 **FOR SYSTEM_TIME** kann unabhängig für jede Tabelle in einer Abfrage angegeben werden. Es kann in allgemeinen Tabellenausdrücken, Tabellenwertfunktionen und gespeicherten Prozeduren verwendet werden.  
  
## <a name="query-for-a-specific-time-using-the-as-of-sub-clause"></a>Abfrage für einen bestimmten Zeitpunkt mithilfe der AS OF-Unterklausel  
 Verwenden Sie die**AS OF** -Unterklausel, wenn Sie den Zustand der Daten wiederherstellen möchten, wie er zu einem bestimmten Zeitpunkt in der Vergangenheit war.  Sie können die Daten mit der Genauigkeit vom datetime2-Typ rekonstruieren, der in den Spaltendefinitionen von **PERIOD** angegeben war.    
Die Klausel der**AS OF** -Unterklausel kann mit konstanten Literalen oder mit Variablen verwendet werden, womit Sie eine Zeitbedingung dynamisch angeben können. Die bereitgestellten Werte werden als UTC-Zeit interpretiert.  
  
 Dieses erste Beispiel gibt den Status der Tabelle dbo.Department ab (AS OF) einem bestimmen Zeitpunkt in der Vergangenheit zurück.  
  
```  
/*State of entire table AS OF specific date in the past*/   
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]   
FROM [dbo].[Department]   
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;  
  
```  
  
 Dieses zweite Beispiel vergleicht die Werte zwischen zwei Zeitpunkten für eine Teilmenge von Zeilen.  
  
```  
DECLARE @ADayAgo datetime2   
SET @ADayAgo = DATEADD (day, -1, sysutcdatetime())   
/*Comparison between two points in time for subset of rows*/   
SELECT D_1_Ago.[DeptID], D.[DeptID],   
D_1_Ago.[DeptName], D.[DeptName],   
D_1_Ago.[SysStartTime], D.[SysStartTime],   
D_1_Ago.[SysEndTime], D.[SysEndTime]   
FROM [dbo].[Department] FOR SYSTEM_TIME AS OF @ADayAgo AS D_1_Ago   
JOIN [Department] AS D ON  D_1_Ago.[DeptID] = [D].[DeptID]    
AND D_1_Ago.[DeptID] BETWEEN 1 and 5 ;  
```  
  
### <a name="using-views-with-as-of-sub-clause-in-temporal-queries"></a>Verwenden von Sichten mit der AS-OF-Unterklausel in temporalen Abfragen  
 Das Verwenden von Ansichten ist sehr nützlich in Szenarien, in denen komplexe Point-in-Time-Analysen erforderlich sind.   
Ein gängiges Beispiel ist die Generierung eines Geschäftsberichts zum aktuellen Zeitpunkt mit den Werten des letzten Monats.   
In der Regel besitzen Kunden ein normalisiertes Datenbankmodell, das viele Tabellen mit Fremdschlüsselbeziehungen enthält. Es kann sich schwierig gestalten, herauszufinden, wie Daten aus einem normalisierten Modell zu einem Zeitpunkt in der Vergangenheit ausgesehen haben, da alle Tabellen sich unabhängig voneinander und in ihrem eigenen Rhythmus ändern.   
In diesem Fall ist die beste Option, eine Ansicht zu erstellen und die **AS OF** -Unterklausel auf die komplette Ansicht anzuwenden. Mit dieser Vorgehensweise können Sie die Modellierung der Datenzugriffsebene von der Point-in-Time-Analyse entkoppeln, da SQL Server die **AS OF** -Klausel transparent auf alle temporalen Tabellen angewendet, die an der Ansichtsdefinition beteiligt sind. Darüber hinaus können Sie temporäre Tabellen in derselben Ansicht mit nicht-temporären Tabellen kombinieren und **AS OF** wird nur auf die temporalen angewendet. Wenn die Ansicht nicht mindestens auf eine temporale Tabelle verweist, schlägt die Anwendung von temporalen Abfrageklausel auf diese fehl.  
  
```  
/* Create view that joins three temporal tables: Department, CompanyLocation, LocationDepartments */   
CREATE VIEW [dbo].[vw_GetOrgChart]   
AS   
SELECT   
     [CompanyLocation].LocID  
   , [CompanyLocation].LocName  
   , [CompanyLocation].City  
   , [Department].DeptID  
   , [Department].DeptName    
FROM [dbo].[CompanyLocation]   
LEFT JOIN [dbo].[LocationDepartments]    
   ON [CompanyLocation].LocID = LocationDepartments.LocID   
LEFT JOIN [dbo].[Department]    
   ON LocationDepartments.DeptID = [Department].DeptID ;  
GO   
/* Querying view AS OF */   
SELECT * FROM [vw_GetOrgChart]   
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;  
  
```  
  
## <a name="query-for-changes-to-specific-rows-over-time"></a>Abfragen von Änderungen an bestimmten Zeilen über einen Zeitraum  
 Die temporalen Unterklauseln **FROM...TO**, **BETWEEN...AND** und **CONTAINED IN** sind nützlich, wenn Sie eine Datenüberwachung durchführen möchten, d.h., wenn Sie alle Verlaufsänderungen für eine bestimmte Zeile in der aktuellen Tabelle abrufen müssen.   
Die ersten beiden Unterklauseln geben Zeilenversionen zurück, die sich mit einem bestimmten Zeitraum überschneiden (d.h. die Zeilenversionen, die vor dem angegebene Zeitraum begannen und danach beendeten), CONTAINED IN gibt dagegen nur die Zeilenversionen zurück, die innerhalb bestimmter Zeitraumgrenzen vorhanden waren.  
  
> [!IMPORTANT]  
>  Wenn Sie nur nach nicht-aktuellen Zeilenversionen suchen, sollten Sie **CONTAINED IN** verwenden, da es nur mit der Verlaufstabelle funktioniert und die beste Abfrageleistung erzielt. Verwenden Sie **ALL** , wenn Sie aktuelle Daten und Verlaufsdaten ohne Einschränkungen abfragen müssen.  
  
```  
/* Query using BETWEEN...AND sub-clause*/  
SELECT   
     [DeptID]  
   , [DeptName]  
   , [SysStartTime]  
   , [SysEndTime]  
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual   
FROM [dbo].[Department]   
FOR SYSTEM_TIME BETWEEN  '2015-01-01' AND '2015-12-31'   
WHERE DeptId = 1   
ORDER BY SysStartTime DESC;   
  
/*  Query using CONTAINED IN sub-clause */  
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]   
FROM [dbo].[Department]   
FOR SYSTEM_TIME CONTAINED IN ('2015-04-01', '2015-09-25')   
WHERE DeptId = 1   
ORDER BY SysStartTime DESC ;  
  
/*  Query using ALL sub-clause */   
SELECT    
     [DeptID]   
   , [DeptName]   
   , [SysStartTime]   
   , [SysEndTime]   
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual    
FROM [dbo].[Department] FOR SYSTEM_TIME ALL   
ORDER BY [DeptID], [SysStartTime] Desc  
  
```  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Queryinging%20a%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>Siehe auch  
 [Temporal Tables](../../relational-databases/tables/temporal-tables.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Erstellen einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Ändern von Daten in einer temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Ändern vom Schema einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Beenden der Versionsverwaltung auf einer versionsverwalteten temporalen Tabelle](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  
