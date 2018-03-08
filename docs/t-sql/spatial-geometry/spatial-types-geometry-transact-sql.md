---
title: die Geometrie (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- geometry
dev_langs:
- TSQL
helpviewer_keywords:
- spatial data types [SQL Server]
- geometry data type [SQL Server], Transact-SQL
ms.assetid: 3fefdf7b-f931-404c-821c-82c0375eaf51
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 734a57249ce3b65a3add16a604cc4e2ed2f4180f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="spatial-types---geometry-transact-sql"></a>Räumliche Typen - Geometrie (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Der planare räumliche Datentyp **Geometrie**, wird als common Language Runtime (CLR)-Datentyp in implementiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dieser Typ stellt Daten in einem euklidischen (flachen) Koordinatensystem dar.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt einen Satz von Methoden für die **Geometrie** räumlichen Datentyp. Dazu gehören Methoden für **Geometrie** durch den Standard Open Geospatial Consortium (OGC) und einen Satz von definiert sind, [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Erweiterungen dieses Standards.  
 
 Die Fehlertoleranz für den Geometry-Methoden kann so groß wie 1. 0e-7 * Blöcke. Die Wertebereiche finden Sie in die ungefähre maximale Entfernung zwischen Punkten von der **Geometrie**Objekt.
  
## <a name="registering-the-geometry-type"></a>Registrieren des geometry-Datentyps  
 Der **geometry** -Typ ist vordefiniert und in jeder Datenbank verfügbar. Sie können Tabellenspalten des **geometry** -Typs in der gleichen Weise erstellen und **geometry** -Daten in der gleichen Weise verwenden wie andere CLR-Typen. Kann in persistierten und nicht persistierten berechneten Spalten verwendet werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-showing-how-to-add-and-query-geometry-data"></a>A. Darstellung des Hinzufügens und Abfragens von Geometriedaten  
 Die folgenden zwei Beispiele zeigen, wie Geometriedaten hinzugefügt und abgefragt werden. Im erste Beispiel erstellt eine Tabelle mit einer Identity-Spalte und eine `geometry` Spalte `GeomCol1`. Eine dritte Spalte rendert die `geometry` -Spalte als Darstellung im Open Geospatial Consortium (OGC) WKT-Format und verwendet die `STAsText()` -Methode. Dann werden zwei Zeilen eingefügt: Eine Zeile enthält eine `LineString` -Instanz des Typs `geometry`und die andere eine `Polygon` -Instanz.  
  
```sql 
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeomCol1 geometry,   
    GeomCol2 AS GeomCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geometry-instances"></a>B. Zurückgeben der Schnittmenge von zwei geometry-Instanzen  
 Im zweiten Beispiel werden mithilfe der `STIntersection()` -Methode die Punkte zurückgegeben, an denen die beiden zuvor eingegebenen `geometry` -Instanzen sich schneiden.  
  
```sql  
DECLARE @geom1 geometry;  
DECLARE @geom2 geometry;  
DECLARE @result geometry;  
  
SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geom1.STIntersection(@geom2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geometry-in-a-computed-column"></a>C. Verwenden des geometry-Typs in einer berechneten Spalte  
 Das folgende Beispiel erstellt eine Tabelle mit einer permanenten berechneten Spalte mit einem **Geometrie** Typ.  
  
```sql  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geometry,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>Siehe auch  
  [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
