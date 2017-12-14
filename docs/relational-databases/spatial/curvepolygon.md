---
title: CurvePolygon | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: spatial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e000a1d8-a049-4542-bfeb-943fd6ab3969
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c87bfe2f5342cc9edceb6a472cba8579c09c220
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="curvepolygon"></a>CurvePolygon
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Ein **CurvePolygon** ist eine von einem äußeren Begrenzungsring und null (0) oder mehr inneren Ringen definierte topologisch geschlossene Fläche.  
  
> [!IMPORTANT]  
>  Laden Sie das Whitepaper [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Neue räumliche Funktionen in SQL Server 2012 **herunter, um eine ausführliche Beschreibung und Beispiele für die in** eingeführten räumlichen Funktionen (z.B. [CurvePolygon](http://go.microsoft.com/fwlink/?LinkId=226407)-Untertyp) zu erhalten.  
  
 Die Attribute einer **CurvePolygon** -Instanz werden durch folgende Kriterien definiert:  
  
-   Die Begrenzung der **CurvePolygon** -Instanz wird durch den äußeren Ring und alle inneren Ringe definiert.  
  
-   Das Innere der **CurvePolygon** -Instanz ist die Fläche zwischen dem äußeren Ring und allen inneren Ringen.  
  
 Eine **CurvePolygon** -Instanz unterscheidet sich von einer **Polygon** -Instanz darin, dass eine **CurvePolygon** -Instanz die folgenden Kreisbogensegmente enthalten kann: **CircularString** und **CompoundCurve**.  
  
## <a name="compoundcurve-instances"></a>CompoundCurve-Instanzen  
 In der unten stehenden Abbildung werden gültige **CurvePolygon** -Instanzen dargestellt:  
  
### <a name="accepted-instances"></a>Akzeptierte Instanzen  
 Damit eine **CurvePolygon** -Instanz akzeptiert wird, muss sie entweder leer sein oder ausschließlich akzeptierte Kreisbogenringe enthalten. Ein akzeptierter Kreisbogenring erfüllt die folgenden Anforderungen.  
  
1.  Er stellt eine akzeptierte **LineString**-, **CircularString**- oder **CompoundCurve** -Instanz dar. Weitere Informationen zu akzeptierten Instanzen finden Sie unter [LineString](../../relational-databases/spatial/linestring.md), [CircularString](../../relational-databases/spatial/circularstring.md)und [CompoundCurve](../../relational-databases/spatial/compoundcurve.md).  
  
2.  Er enthält mindestens vier Punkte.  
  
3.  Die X- und Y-Koordinaten für den Ausgangspunkt und den Endpunkt sind identisch.  
  
    > [!NOTE]  
    >  Z- und M-Werte werden ignoriert.  
  
 Im folgenden Beispiel werden akzeptierte **CurvePolygon** -Instanzen veranschaulicht.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0, 0 0))';  
DECLARE @g3 geometry = 'CURVEPOLYGON((0 0 1, 0 0 2, 0 0 3, 0 0 3))'  
DECLARE @g4 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
DECLARE @g5 geography = 'CURVEPOLYGON((-122.3 47, 122.3 -47, 125.7 -49, 121 -38, -122.3 47))';  
```  
  
 `@g3` wird akzeptiert, obwohl sich die Z-Werte des Ausgangspunkts und des Endpunkts voneinander unterscheiden, da Z-Werte ignoriert werden. `@g5` wird akzeptiert, obwohl die **geography** -Typinstanz ungültig ist.  
  
 In den folgenden Beispielen wird `System.FormatException`ausgelöst.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON((0 5, 0 0, 0 0, 0 0))';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0))';  
```  
  
 `@g1` wird nicht akzeptiert, da der Ausgangspunkt und der Endpunkt nicht denselben Y-Wert aufweisen. `@g2` wird nicht akzeptiert, da der Ring nicht über eine ausreichende Anzahl von Punkten verfügt.  
  
### <a name="valid-instances"></a>Gültige Instanzen  
 Eine **CurvePolygon** -Instanz ist gültig, wenn sowohl der äußere Ring als auch die inneren Ringe die folgenden Kriterien erfüllen:  
  
1.  Sie können sich nur an jeweils einem Tangentenpunkt berühren.  
  
2.  Sie können einander nicht schneiden.  
  
3.  Jeder Ring muss mindestens vier Punkte enthalten.  
  
4.  Jeder Ring muss ein akzeptabler Kurventyp sein.  
  
 Auch**CurvePolygon** -Instanzen müssen bestimmte Kriterien erfüllen, je nachdem, ob es sich dabei um einen **geometry** -Datentyp oder einen **geography** -Datentyp handelt.  
  
#### <a name="geometry-data-type"></a>geometry-Datentyp  
 Eine gültige **geometryCurvePolygon** -Instanz muss über die folgenden Attribute verfügen:  
  
1.  Alle inneren Ringe müssen im äußeren Ring enthalten sein.  
  
2.  Mehrere innere Ringe können vorhanden sein, ein innerer Ring darf jedoch keinen anderen inneren Ring enthalten.  
  
3.  Ringe dürfen weder sich selbst noch einen anderen Ring schneiden.  
  
4.  Ringe dürfen sich nur an einzelnen Tangentenpunkten berühren (wobei die Anzahl der Punkte, an denen Ringe einander berühren, endlich sein muss).  
  
5.  Der Innere des Polygons muss verbunden sein.  
  
 Im folgenden Beispiel werden gültige **geometryCurvePolygon** -Instanzen veranschaulicht.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
 Für CurvePolygon-Instanzen gelten dieselben Gültigkeitsregeln wie für Polygon-Instanzen. CurvePolygon-Instanzen können jedoch die neuen Kreisbogensegment-Typen akzeptieren. Weitere Beispiele für gültige oder nicht gültige Instanzen finden Sie unter [Polygon](../../relational-databases/spatial/polygon.md).  
  
#### <a name="geography-data-type"></a>geography-Datentyp  
 Eine gültige **geographyCurvePolygon** -Instanz muss über die folgenden Attribute verfügen:  
  
1.  Der Innere des Polygons ist mit der linken Regel verbunden.  
  
2.  Ringe dürfen weder sich selbst noch einen anderen Ring schneiden.  
  
3.  Ringe dürfen sich nur an einzelnen Tangentenpunkten berühren (wobei die Anzahl der Punkte, an denen Ringe einander berühren, endlich sein muss).  
  
4.  Der Innere des Polygons muss verbunden sein.  
  
 Im folgenden Beispiel wird eine gültige CurvePolygon-geography-Instanz veranschaulicht.  
  
```  
DECLARE @g geography = 'CURVEPOLYGON((-122.3 47, 122.3 47, 125.7 49, 121 38, -122.3 47))';  
SELECT @g.STIsValid();  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-curvepolygon"></a>A. Instanziieren einer geometry-Instanz mit einem leeren CurvePolygon  
 In diesem Beispiel wird veranschaulicht, wie eine leere **CurvePolygon** -Instanz erstellt wird:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-with-a-curvepolygon-in-the-same-statement"></a>B. Deklarieren und Instanziieren einer geometry-Instanz mit einem CurvePolygon in derselben Anweisung  
 In diesem Codeausschnitt wird veranschaulicht, wie eine geometry-Instanz und ein **CurvePolygon** in derselben Anweisung deklariert und initialisiert werden:  
  
```tsql  
DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))'  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-curvepolygon"></a>C. Instanziieren einer geography-Instanz mit einem CurvePolygon  
 In diesem Codeausschnitt wird veranschaulicht, wie eine **geography** -Instanz mit einem **CurvePolygon**deklariert und initialisiert wird:  
  
```tsql  
DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-curvepolygon-with-only-an-exterior-bounding-ring"></a>D. Speichern eines CurvePolygon mit nur einem äußeren Begrenzungsring  
 In diesem Beispiel wird veranschaulicht, wie ein einfacher Kreis in einer **CurvePolygon** -Instanz gespeichert wird (wobei der Kreis lediglich durch einen äußeren Begrenzungsring definiert wird):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
### <a name="e-storing-a-curvepolygon-containing-interior-rings"></a>E. Speichern eines CurvePolygon mit inneren Ringen  
 In diesem Beispiel wird ein Rad in einer **CurvePolygon** -Instanz erstellt (das Rad wird durch einen äußeren Begrenzungsring und einen inneren Ring definiert):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
 In diesem Beispiel werden eine gültige **CurvePolygon** -Instanz und eine ungültige Instanz für die Verwendung von inneren Ringen veranschaulicht:  
  
```tsql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (-2 2, 2 2, 2 -2, -2 -2, -2 2))');  
IF @g1.STIsValid() = 1  
  BEGIN  
     SELECT @g1.STArea();  
  END  
SET @g2 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (0 5, 5 0, 0 -5, -5 0, 0 5))');  
IF @g2.STIsValid() = 1  
  BEGIN  
     SELECT @g2.STArea();  
  END  
SELECT @g1.STIsValid() AS G1, @g2.STIsValid() AS G2;  
```  
  
 Sowohl @g1 als auch @g2 verwenden denselben äußeren Begrenzungsring (einen Kreis mit dem Radius 5), und für beide wird ein Quadrat als innerer Ring verwendet.  Die Instanz @g1 ist jedoch gültig, während die Instanz @g2 ungültig ist.  Der Grund für die Ungültigkeit von @g2 ist, dass der innere Ring die vom äußeren Ring begrenzte Fläche in vier separate Bereiche teilt.  Dies wird in der folgenden Zeichnung verdeutlicht:  
  
## <a name="see-also"></a>Siehe auch  
 [Polygon](../../relational-databases/spatial/polygon.md)   
 [CircularString](../../relational-databases/spatial/circularstring.md)   
 [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)   
 [geometry-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)   
 [geography-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)   
 [Übersicht über räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
