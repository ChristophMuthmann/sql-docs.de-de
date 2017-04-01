---
title: "Erstellen, Aufbauen und Abfragen von geometry-Instanzen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-spatial"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Planare räumliche Daten [SQL Server], Erste Schritte"
  - "geometry-Datentyp [SQL Server], Erste Schritte"
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Erstellen, Aufbauen und Abfragen von geometry-Instanzen
  Der planare räumliche Datentyp **geometry**, stellt Daten in einem euklidischen (flachen) Koordinatensystem dar. Dieser Datentyp wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als CLR-Datentyp (Common Language Runtime) implementiert.  
  
 Der **geometry** -Typ ist vordefiniert und in jeder Datenbank verfügbar. Sie können Tabellenspalten des **geometry** -Typs in der gleichen Weise erstellen und **geometry** -Daten in der gleichen Weise verwenden wie andere CLR-Typen.  
  
 Der (planare) **geometry**-Datentyp, der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wird, entspricht der Open Geospatial Consortium (OGC) Simple Features for SQL Specification Version 1.1.0.  
  
 Weitere Informationen zu den OGC-Spezifikationen finden Sie in den folgenden Themen:  
  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](http://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [OGC Specifications, Simple Feature Access Part 2 – SQL Options](http://go.microsoft.com/fwlink/?LinkId=93629)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt eine Teilmenge des bestehenden GML 3.1-Standards, der im folgenden Schema definiert ist: [http://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](http://go.microsoft.com/fwlink/?LinkId=230959).  
  
##  <a name="creating"></a> Erstellen oder Konstruieren einer neuen geometry-Instanz  
  
###  <a name="existing"></a> Erstellen einer neuen geometry-Instanz aus einer vorhandenen Instanz  
 Der **geometry**-Datentyp stellt viele integrierte Methoden zur Verfügung, mit denen neue **geometry**-Instanzen auf der Grundlage vorhandener Instanzen erstellt werden können.  
  
 **So erstellen Sie einen Puffer um eine Geometrie**  
 [STBuffer &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)  
  
 [BufferWithTolerance &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)  
  
 **So erstellen Sie eine vereinfachte Version einer Geometrie**  
 [Reduce &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/reduce-geometry-data-type.md)  
  
 **So erstellen Sie die konvexe Hülle einer Geometrie**  
 [STConvexHull &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stconvexhull-geometry-data-type.md)  
  
 **So erstellen Sie eine Geometrie aus der Schnittmenge zweier Geometrien**  
 [STIntersection &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stintersection-geometry-data-type.md)  
  
 **So erstellen Sie eine Geometrie aus der Vereinigung zweier Geometrien**  
 [STUnion &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stunion-geometry-data-type.md)  
  
 **So erstellen Sie eine Geometrie aus den Punkten, an denen eine Geometrie eine andere nicht überlappt**  
 [STDifference &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stdifference-geometry-data-type.md)  
  
 **So erstellen Sie eine Geometrie aus den Punkten, an denen zwei Geometrien nicht überlappen**  
 [STSymDifference &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stsymdifference-geometry-data-type.md)  
  
 **So erstellen Sie eine beliebige Punktinstanz, die auf einer vorhandenen Geometrie liegt**  
 [STPointOnSurface &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="wkt"></a> Erstellen einer geometry-Instanz anhand einer WKT-Eingabe (Well-Known Text)  
 Der **geometry**-Datentyp bietet mehrere integrierte Methoden zur Erstellung einer Geometrie anhand der WKT-Darstellung von Open Geospatial Consortium (OGC). Der WKT-Standard ist eine Textzeichenfolge, die den Austausch von Geometriedaten in Textform ermöglicht.  
  
 **So erstellen Sie eine beliebige geometry-Instanz anhand einer WKT-Eingabe**  
 [STGeomFromText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)  
  
 [Parse &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/parse-geometry-data-type.md)  
  
 **So erstellen Sie eine Point-geometry-Instanz anhand einer WKT-Eingabe**  
 [STPointFromText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stpointfromtext-geometry-data-type.md)  
  
 **So erstellen Sie eine MultiPoint-geometry-Instanz anhand einer WKT-Eingabe**  
 [STMPointFromText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stmpointfromtext-geometry-data-type.md)  
  
 **So erstellen Sie eine LineString-geometry-Instanz anhand einer WKT-Eingabe**  
 [STLineFromText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stlinefromtext-geometry-data-type.md)  
  
 **So erstellen Sie eine MultiLineString-geometry-Instanz anhand einer WKT-Eingabe**  
 [STMLineFromText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stmlinefromtext-geometry-data-type.md)  
  
 **So erstellen Sie eine Polygon-geometry-Instanz anhand einer WKT-Eingabe**  
 [STPolyFromText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stpolyfromtext-geometry-data-type.md)  
  
 **So erstellen Sie eine MultiPolygon-geometry-Instanz anhand einer WKT-Eingabe**  
 [STMPolyFromText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type.md)  
  
 **So erstellen Sie eine GeometryCollection-geometry-Instanz anhand einer WKT-Eingabe**  
 [STGeomCollFromText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="wkb"></a> Erstellen einer geometry-Instanz aus einer WKB-Eingabe (Well-Known Binary)  
 WKB ist ein vom Open Geospatial Consortium spezifiziertes Binärformat, das den Austausch von **geometry**-Daten zwischen einer Clientanwendung und einer SQL-Datenbank ermöglicht. Die folgenden Funktionen akzeptieren die WKB-Eingabe zum Zweck der Erstellung von Geometrien:  
  
 **So erstellen Sie einen beliebigen geometry-Instanztyp anhand einer WKB-Eingabe**  
 [STGeomFromWKB &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type.md)  
  
 **So erstellen Sie eine Point-geometry-Instanz anhand einer WKB-Eingabe**  
 [STPointFromWKB &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stpointfromwkb-geometry-data-type.md)  
  
 **So erstellen Sie eine MultiPoint-geometry-Instanz anhand einer WKB-Eingabe**  
 [STMPointFromWKB &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type.md)  
  
 **So erstellen Sie eine LineString-geometry-Instanz anhand einer WKB-Eingabe**  
 [STLineFromWKB &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stlinefromwkb-geometry-data-type.md)  
  
 **So erstellen Sie eine MultiLineString-geometry-Instanz anhand einer WKB-Eingabe**  
 [STMLineFromWKB &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type.md)  
  
 **So erstellen Sie eine Polygon-geometry-Instanz anhand einer WKB-Eingabe**  
 [STPolyFromWKB &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type.md)  
  
 **So erstellen Sie eine MultiPolygon-geometry-Instanz anhand einer WKB-Eingabe**  
 [STMPolyFromWKB &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type.md)  
  
 **So erstellen Sie eine GeometryCollection-geometry-Instanz anhand einer WKB-Eingabe**  
 [STGeomCollFromWKB &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="gml"></a> Erstellen einer geometry-Instanz anhand einer GML-Texteingabe  
 Der **geometry** -Datentyp bietet eine Methode, die eine **geometry** -Instanz aus GML generiert, einer XML-Darstellung geometrischer Objekte. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt eine Teilmenge von GML.  
  
 **So erstellen Sie einen beliebigen geometry-Instanztyp anhand einer GML-Eingabe**  
 [GeomFromGml &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/geomfromgml-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
##  <a name="returning"></a> Zurückgeben von WKT (Well-Known Text) oder WKB (Well-Known Binary) aus einer geometry-Instanz  
 Anhand der folgenden Methoden können Sie entweder das WKT- oder das WKB-Format einer **geometry** zurückgeben:  
  
 **So geben Sie eine WKT-Darstellung einer geometry-Instanz zurück**  
 [STAsText &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)  
  
 [ToString &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/tostring-geometry-data-type.md)  
  
 **So geben Sie eine WKT-Darstellung einer geometry-Instanz einschließlich Z- und M-Werten zurück**  
 [AsTextZM &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
 **So geben Sie eine WKB-Darstellung einer geometry-Instanz zurück**  
 [STAsBinary &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stasbinary-geometry-data-type.md)  
  
 **So geben Sie eine GML-Darstellung einer geometry-Instanz zurück**  
 [AsGml &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/asgml-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
##  <a name="querying"></a> Abfragen der Eigenschaften und Verhalten von geometry-Instanzen  
 Allee **geometry** -Instanzen verfügen über eine Reihe von Eigenschaften, die über durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellte Methoden abgerufen werden können. In den folgenden Themen werden die Eigenschaften und Verhalten von geometry-Typen und die Methoden zum Abrufen der einzelnen Eigenschaften und Verhalten beschrieben.  
  
###  <a name="valid"></a> Gültigkeit, Instanztyp und GeometryCollection-Informationen  
 Sobald eine **geometry**-Instanz erstellt wurde, können Sie anhand der folgenden Methoden ermitteln, ob sie wohlgeformt ist, den Instanztyp zurückgeben oder, wenn es sich um eine Collection-Instanz handelt, eine spezifische **geometry**-Instanz zurückgeben.  
  
 **So geben Sie den Instanztyp einer Geometrie zurück**  
 [STGeometryType &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
 **So bestimmen Sie, ob eine Geometrie einen gegebenen Instanztyp aufweist**  
 [InstanceOf &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/instanceof-geometry-data-type.md)  
  
 **So bestimmen Sie, ob eine geometry-Instanz für ihren Instanztyp wohlgeformt ist**  
 [STIsValid &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
 **So konvertieren Sie eine geometry-Instanz in eine wohlgeformte Geometrieinstanz mit einem Instanztyp**  
 [MakeValid &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)  
  
 **So geben Sie die Anzahl von Geometrien in einer geometry-Auflistungsinstanz zurück**  
 [STNumGeometries &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stnumgeometries-geometry-data-type.md)  
  
 So geben Sie eine bestimmte Geometrie in einer geometry-Auflistungsinstanz zurück  
 [STGeometryN &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stgeometryn-geometry-data-type.md)STGeometryN (geometry-Datentyp)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="number"></a> Anzahl von Punkten  
 Alle nicht leeren **geometry** -Instanzen bestehen aus *Punkten*. Diese Punkte stellen die x- und y-Koordinaten der Ebene dar, auf die die Geometrien gezeichnet werden. **geometry** stellt zahlreiche integrierte Methoden zum Abfragen der Punkte einer Instanz bereit.  
  
 **So geben Sie die Anzahl von Punkten zurück, aus denen eine Instanz besteht**  
 [STNumPoints &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)  
  
 **So geben Sie einen bestimmten Punkt einer Instanz zurück**  
 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)  
  
 **So geben Sie einen beliebigen Punkt zurück, der auf einer Instanz liegt**  
 [STPointOnSurface](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
 **So geben Sie den Ausgangspunkt einer Instanz zurück**  
 [STStartPoint](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)  
  
 **So geben Sie den Endpunkt einer Instanz zurück**  
 [STEndpoint](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)  
  
 **So geben Sie die X-Koordinate einer Point-Instanz zurück**  
 [STX &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)  
  
 **So geben Sie die Y-Koordinate einer Point-Instanz zurück**  
 [STY](../../t-sql/spatial-geometry/sty-geometry-data-type.md)  
  
 **So geben Sie den geometrischen Mittelpunkt einer Polygon-, CurvePolygon- oder MultiPolygon-Instanz zurück**  
 [STCentroid](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="dimension"></a> Dimension  
 Eine nicht leere **geometry**-Instanz kann null-, ein- oder zweidimensional sein. Nulldimensionale **Geometrien**, wie z.B. **Point** und **MultiPoint**, haben weder Länge noch Fläche. Eindimensionale Objekte, wie z.B. **LineString, CircularString, CompoundCurve** und **MultiLineString**, haben Länge. Zweidimensionale Instanzen, z.B. **Polygon**, **CurvePolygon** und **MultiPolygon**, haben Fläche und Länge. Für leere Instanzen wird als Dimension -1 ausgegeben, und für eine **GeometryCollection**-Auflistung wird eine Fläche ausgegeben, die vom Typ der darin enthaltenen Elemente abhängt.  
  
 **So geben Sie die Dimension einer Instanz zurück**  
 [STDimension](../../t-sql/spatial-geometry/stdimension-geometry-data-type.md)  
  
 **So geben Sie die Länge einer Instanz zurück**  
 [STLength](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)  
  
 **So geben Sie die Fläche einer Instanz zurück**  
 [STArea](../../t-sql/spatial-geometry/starea-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="empty"></a> Empty  
 Eine *empty***geometry** -Instanz besitzt keine Punkte. Die Länge von leeren **LineString, CircularString**-, **CompoundCurve**- und **MultiLineString** -Instanzen ist 0 (null). Die Fläche von leeren **Polygon**-, **CurvePolygon**- und **MultiPolygon** -Instanzen ist 0 (null).  
  
 **So bestimmen Sie, ob eine Instanz leer ist**  
 [STIsEmpty](../../t-sql/spatial-geometry/stisempty-geometry-data-type.md).  
  
 [In diesem Thema](#TOP)  
  
###  <a name="simple"></a> Einfach  
 Die Geometrie ( **geometry** ) einer Instanz ist *einfach*, wenn sie die beiden folgenden Anforderungen erfüllt:  
  
-   Keine Abbildung der Instanz darf sich selbst außer an den Endpunkten schneiden.  
  
-   Keine zwei Abbildungen einer Instanz dürfen sich an einem Punkt schneiden, der nicht auf den Umrisslinien dieser beiden Abbildungen liegt.  
  
> [!NOTE]  
>  Leere Geometrien sind stets einfach.  
  
 **So bestimmen Sie, ob eine Instanz einfach ist**  
 [STIsSimple](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md).  
  
 [In diesem Thema](#TOP)  
  
###  <a name="boundary"></a> Begrenzung, Innenbereich und Außenbereich  
 Unter dem *Innenbereich* einer **geometry** -Instanz wird der von der Instanz belegte Bereich und unter dem *Außenbereich* wird der nicht von der Instanz bedeckte Bereich verstanden.  
  
 Die*Begrenzung* wird vom OGC wie folgt definiert:  
  
-   **Point** - und **MultiPoint** -Instanzen haben keine Begrenzung.  
  
-   Die Begrenzung von**LineString** - und **MultiLineString** boundaries are formed by the start points - und end points, removing those that occur an even number of times.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 Die Begrenzung einer **Polygon** - oder **MultiPolygon** -Instanz besteht aus der Menge ihrer Ringe.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **So geben Sie die Begrenzung einer Instanz zurück**  
 [STBoundary](../../t-sql/spatial-geometry/stboundary-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="envelope"></a> Umschlag  
 Der *Umschlag* einer **geometry**-Instanz, auch *umgebendes Feld* genannt, ist das an den Achsen ausgerichtete Rechteck, das durch die minimalen und maximalen Koordinaten (X,Y) der Instanz gebildet wird.  
  
 **So geben Sie den Umschlag einer Instanz zurück**  
 [STEnvelope](../../t-sql/spatial-geometry/stenvelope-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="closure"></a> Abgeschlossenheit  
 Eine *geschlossene* **geometry**-Instanz ist eine Abbildung, deren Ausgangs- und Endpunkt identisch ist. Alle**Polygon** -Instanzen gelten als geschlossen. Alle**Point** -Instanzen gelten als nicht geschlossen.  
  
 Ein Ring ist eine einfache, geschlossene **LineString** -Instanz.  
  
 **So bestimmen Sie, ob eine Instanz abgeschlossen ist**  
 [STIsClosed](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)  
  
 **So bestimmen Sie, ob eine Instanz ein Ring ist**  
 [STIsRing](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)  
  
 **So geben Sie den äußeren Ring einer Polygoninstanz zurück**  
 [STExteriorRing](../../t-sql/spatial-geometry/stexteriorring-geometry-data-type.md)  
  
 **So geben Sie die Anzahl der inneren Ringen in einer Polygoninstanz zurück**  
 [STNumInteriorRing](../../t-sql/spatial-geometry/stnuminteriorring-geometry-data-type.md)  
  
 **So geben Sie einen gegebenen inneren Ring einer Polygoninstanz zurück**  
 [STInteriorRingN](../../t-sql/spatial-geometry/stinteriorringn-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
###  <a name="srid"></a> SRID (Spatial Reference ID)  
 Der SRID (Spatial Reference ID) ist ein Bezeichner, der das Koordinatensystem angibt, in dem die **geometry**-Instanz dargestellt wird. Zwei Instanzen mit unterschiedlichen SRIDs können nicht verglichen werden.  
  
 **So können Sie die SRID einer Instanz festlegen oder zurückgeben**  
 [STSrid](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)  
  
 Diese Eigenschaft kann geändert werden.  
  
 [In diesem Thema](#TOP)  
  
##  <a name="rel"></a> Bestimmen der Beziehungen zwischen geometry-Instanzen  
 Der **geometry**-Datentyp stellt viele integrierte Methoden zur Verfügung, mit denen die Beziehungen zwischen zwei **geometry**-Instanzen bestimmt werden können.  
  
 **So bestimmen Sie, ob zwei Instanzen die gleiche Punktmenge umfassen**  
 [STEquals](../../t-sql/spatial-geometry/stequals-geometry-data-type.md)  
  
 **So bestimmen Sie, ob zwei Instanzen disjunkt sind**  
 [STDisjoint](../../t-sql/spatial-geometry/stdisjoint-geometry-data-type.md)  
  
 **So bestimmen Sie, ob sich zwei Instanzen überschneiden**  
 [STIntersects](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
 **So bestimmen Sie, ob sich zwei Instanzen berühren**  
 [STTouches](../../t-sql/spatial-geometry/sttouches-geometry-data-type.md)  
  
 **So bestimmen Sie, ob sich zwei Instanzen überlappen**  
 [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
 **So bestimmen Sie, ob sich zwei Instanzen überkreuzen**  
 [STCrosses](../../t-sql/spatial-geometry/stcrosses-geometry-data-type.md)  
  
 **So bestimmen Sie, ob eine Instanz sich innerhalb einer anderen befindet**  
 [STWithin](../../t-sql/spatial-geometry/stwithin-geometry-data-type.md)  
  
 **So bestimmen Sie, ob eine Instanz eine andere enthält**  
 [STContains](../../t-sql/spatial-geometry/stcontains-geometry-data-type.md)  
  
 **So bestimmen Sie, ob eine Instanz eine andere überlappt**  
 [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
 **So bestimmen Sie, ob zwei Instanzen räumlich verbunden sind**  
 [STRelate](../../t-sql/spatial-geometry/strelate-geometry-data-type.md)  
  
 **So bestimmen Sie die kürzeste Entfernung zwischen Punkten in zwei Geometrien**  
 [STDistance](../../t-sql/spatial-geometry/stdistance-geometry-data-type.md)  
  
 [In diesem Thema](#TOP)  
  
##  <a name="defaultsrid"></a> geometry-Instanzen haben standardmäßig die SRID 0 (null)  
 Der Standard-SRID für **geometry** -Instanzen lautet in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 0. Bei räumlichen **geometry** -Daten ist zur Ausführung von Berechnungen des SRID der Räumlichkeitsinstanz nicht erforderlich. Daher können sich Instanzen in einer undefinierten ebenen Fläche befinden. Zur Angabe einer undefinierten ebenen Fläche in Berechnungen mit Methoden des **geometry** -Datentyps wird in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] der SRID 0 verwendet.  
  
##  <a name="examples"></a> Beispiele  
 Die folgenden zwei Beispiele zeigen, wie Geometriedaten hinzugefügt und abgefragt werden.  
  
-   Im ersten Beispiel wird eine Tabelle mit einer Identitätsspalte und der `geometry`-Spalte `GeomCol1` erstellt. Eine dritte Spalte rendert die `geometry`-Spalte als Darstellung im Open Geospatial Consortium (OGC) WKT-Format und verwendet die `STAsText()`-Methode. Dann werden zwei Zeilen eingefügt: Eine Zeile enthält eine `LineString`-Instanz des Typs `geometry` und die andere eine `Polygon`-Instanz.  
  
    ```  
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
  
-   Im zweiten Beispiel werden mithilfe der `STIntersection()` -Methode die Punkte zurückgegeben, an denen die beiden zuvor eingegebenen `geometry` -Instanzen sich schneiden.  
  
    ```  
    DECLARE @geom1 geometry;  
    DECLARE @geom2 geometry;  
    DECLARE @result geometry;  
  
    SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geom1.STIntersection(@geom2);  
    SELECT @result.STAsText();  
    ```  
  
 [In diesem Thema](#TOP)  
  
## Siehe auch  
 [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  