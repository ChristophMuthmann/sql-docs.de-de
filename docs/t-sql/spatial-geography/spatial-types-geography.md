---
title: geography (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- geography
dev_langs:
- TSQL
helpviewer_keywords:
- geography data type [SQL Server], Transact-SQL
- spatial data types [SQL Server]
ms.assetid: d9e4952a-1841-4465-a64b-11e9288dba1d
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b21ec5aa3f46d665691bde7d026eedc934040164
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spatial-types---geography"></a>Räumliche Typen - geography
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Der Räumlichkeitsdatentyp **geography** wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als .NET-CLR-Datentyp (Common Language Runtime) implementiert. Dieser Typ stellt Daten in einem Erdkugel-Koordinatensystem dar. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** data type stores ellipsoidal (round-earth) data, such as GPS latitude and longitude coordinates.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt einen Satz von Methoden für den räumlichen **geography**-Datentyp. Dazu gehören Methoden für **geography**, die im OGC-Standard (Open Geospatial Consortium) sowie in einer Gruppe von [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Erweiterungen dieses Standards definiert sind.  
 
 Die Fehlertoleranz für die **geography**-Methoden kann bis zu 1,0e-7 * Erweiterungen groß sein. Die Erweiterungen verweisen auf den ungefähren maximalen Abstand zwischen Punkten des **geography**-Objekts.
  

## <a name="registering-the-geography-type"></a>Registrieren des geography-Datentyps  
 Der **geography** -Typ ist vordefiniert und in jeder Datenbank verfügbar. Sie können Tabellenspalten des **geography** -Typs in der gleichen Weise erstellen und **geography** -Daten in der gleichen Weise verwenden wie andere vom System bereitgestellte Typen. Kann in persistierten und nicht persistierten berechneten Spalten verwendet werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-showing-how-to-add-and-query-geography-data"></a>A. Darstellung des Hinzufügens und Abfragens von Geografiedaten  
 Die folgenden Beispiele zeigen, wie Geografiedaten hinzugefügt und abgefragt werden. Im ersten Beispiel wird eine Tabelle mit einer Identitätsspalte und der `geography`-Spalte `GeogCol1` erstellt. Eine dritte Spalte rendert die `geography` -Spalte als Darstellung im Open Geospatial Consortium (OGC) WKT-Format und verwendet die `STAsText()` -Methode. Dann werden zwei Zeilen eingefügt: Eine Zeile enthält eine `LineString` -Instanz des Typs `geography`und die andere eine `Polygon` -Instanz.  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeogCol1 geography,   
    GeogCol2 AS GeogCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326));  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653 , -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geography-instances"></a>B. Zurückgeben der Schnittmenge von zwei geography-Instanzen  
 Im folgenden Beispiel werden mithilfe der `STIntersection()`-Methode die Punkte zurückgegeben, an denen die beiden zuvor eingegebenen `geography`-Instanzen sich schneiden.  
  
```  
DECLARE @geog1 geography;  
DECLARE @geog2 geography;  
DECLARE @result geography;  
  
SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geog1.STIntersection(@geog2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geography-in-a-computed-column"></a>C. Verwenden des geography-Typs in einer berechneten Spalte  
 Im folgenden Beispiel wird eine Tabelle mit einer persistierten berechneten Spalte mit einem **geography**-Typ erstellt.  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geography,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   

  
  
